
>**"Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks"**
>[Patrick Lewis](https://arxiv.org/search/cs?searchtype=author&query=Lewis,+P), [Ethan Perez](https://arxiv.org/search/cs?searchtype=author&query=Perez,+E), [Aleksandra Piktus](https://arxiv.org/search/cs?searchtype=author&query=Piktus,+A), [Fabio Petroni](https://arxiv.org/search/cs?searchtype=author&query=Petroni,+F), [Vladimir Karpukhin](https://arxiv.org/search/cs?searchtype=author&query=Karpukhin,+V), [Naman Goyal](https://arxiv.org/search/cs?searchtype=author&query=Goyal,+N), [Heinrich Küttler](https://arxiv.org/search/cs?searchtype=author&query=K%C3%BCttler,+H), [Mike Lewis](https://arxiv.org/search/cs?searchtype=author&query=Lewis,+M), [Wen-tau Yih](https://arxiv.org/search/cs?searchtype=author&query=Yih,+W), [Tim Rocktäschel](https://arxiv.org/search/cs?searchtype=author&query=Rockt%C3%A4schel,+T), [Sebastian Riedel](https://arxiv.org/search/cs?searchtype=author&query=Riedel,+S), [Douwe Kiela](https://arxiv.org/search/cs?searchtype=author&query=Kiela,+D)
>https://arxiv.org/pdf/2005.11401

## Background
##### 일반적인 LLM 사용 예시
pre-trained on huge dataset -> fine-tuning on specific datas

##### LLM의 단점
- knowledge-intensive task들에 대해서, task-specific architecture들보다 낮은 성능을 보인다.
- 제공하는 정보의 기원이 불분명하다.

=> need for better fine-tuning recipe - RAG...



## Method
**input seq *x*** 으로 **text document *z*** 를 retrieve
**text document *z*** 를 추가적인 context로 사용해서 **target sequence *y*** 를 generate
> [!note] Figure 1
> ![[Pasted image 20240905160244.png]]
> Overview of our approach. We combine a pre-trained retriever (Query Encoder + Document Index) with a pre-trained seq2seq model (Generator) and fine-tune end-to-end. For query x, we use Maximum Inner Product Search (MIPS) to find the top-K documents zi . For final prediction y, we treat z as a latent variable and marginalize over seq2seq predictions given different documents.
 
 

### Main Components
#### retriever $p_{\eta}(z \mid x)$
- parameter $\eta$ : 주어진 query *x* 의 구절들 중 top-K distributions을 return

#### generator $p_\theta(y_i|x,z,y_{1:i-1})$
- parameter $\theta$ : 이전 i-1번째 token $y_{1:i-1}$ & input *x* & retrieved passage *z* 의 context에 기반하여 current token을 generate


### Models
retriever와 generator를 end-to-end로 train하기 위해서 retrieved document를 **latent variable**로 둔다.
latent document들을 각각의 방식으로 처리하여, 생성된 text에 대해서 확률 분포를 만들어내는 2가지 model을 사용한다.

#### Rag-Sequence Model
전체 sequence를 generate(각 target token을 예측)하기 위해서, 
**같은 retrieved document**를 사용한다.

retrieved document를 하나의 latent variable로 보는데,
이 latent variable은 top-K approximation을 통해서 seq2seq probability $p(y|x)$ 을 얻기 위해서 [[marginalize]] 된다.

top-K document들이 retriever를 사용해서 retrieve(검색) 되고, 
generator가 각 document에 대해서 output sequence probability를 만들어내고, 
그 후 [[marginalize]] 된다.

$p_{\text{RAG-Sequence}}(y \mid x) \approx \sum_{z \in \text{top-k}(p(\cdot \mid x))} p_{\eta}(z \mid x) p_{\theta}(y \mid x, z) = \sum_{z \in \text{top-k}(p(\cdot \mid x))} p_{\eta}(z \mid x) \prod_{i}^{N} p_{\theta}(y_i \mid x, z, y_{1:i-1})$ 
#### RAG-Token Model
전체 sequence를 generate(각 target token을 예측)하기 위해서, 
**다른 retrieved document**를 사용한다.

generator가 output을 만들 때, 몇 가지 document들 중에 content를 고를 수 있다. 

top-K document들이 retriever를 사용해서 retrieve 되고,
generator가 각 document에 대해서 다음 output token에 대한 distribution을 만들어낸다.
marginalize 전에, 그 다음 output token에 대해서도 반복해서 수행한다.

$p_{\text{RAG-Token}}(y \mid x) \approx \prod_{i}^{N} \sum_{z \in \text{top-k}(p(\cdot \mid x))} p_{\eta}(z \mid x) p_{\theta}(y_i \mid x, z, y_{1:i-1})$


##### RAG in sequence classification
target class를 length가 1인 target sequence로 보면, 
RAG로 sequence classiciation을 수행 가능하다.

이 경우, RAG-Sequence와 RAG-Token은 동일하다.

### Retriever: [[DPR]]
