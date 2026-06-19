---
created: 2024-10-30 11:17
modified: 2024-10-30 11:17
---
> "DINOv2: Learning Robust Visual Features without Supervision"  
> 2024-01  
> Transactions on Machine Learning Research  
> Maxime Oquab, Timothée Darcet, Théo Moutakanni, Huy V. Vo, Marc Szafraniec, Vasil Khalidov, Pierre Fernandez, Daniel Haziza, Francisco Massa, Alaaeldin El-Nouby, Mahmoud Assran, Nicolas Ballas, Wojciech Galuba, Russell Howes, Po-Yao Huang, Shang-Wen Li, Ishan Misra, Michael Rabbat, Vasu Sharma, Gabriel Synnaeve, Hu Xu, Hervé Jegou, Julien Mairal, Patrick Labatut, Armand Joulin, Piotr Bojanowski  
> Meta AI Research / Inria  
> https://arxiv.org/pdf/2304.07193 

> [!abstract]  
> The recent breakthroughs in natural language processing for model pretraining on large quantities of data have opened the way for similar foundation models in computer vision. These models could greatly simplify the use of images in any system by producing general-purpose visual features, i.e., features that work across image distributions and tasks without finetuning. This work shows that existing pretraining methods, especially self-supervised methods, can produce such features if trained on enough curated data from diverse sources. We revisit existing approaches and combine different techniques to scale our pretraining in terms of data and model size. Most of the technical contributions aim at accelerating and stabilizing the training at scale. In terms of data, we propose an automatic pipeline to build a dedicated, diverse, and curated image dataset instead of uncurated data, as typically done in the self-supervised literature. In terms of models, we train a ViT model with 1B parameters and distill it into a series of smaller models that surpass the best available general-purpose features, OpenCLIP on most of the benchmarks at image and pixel levels.



## 1. Introduction
task-agnostic pretrained representation들을 학습하는 것이 NLP에서 표준이 되었다.
- task-agnostic pretrained representation:
	- feature들을 있는 그대로("as they are"), fine-tuning없이 사용이 가능

downstream task들에 대해서, task-specific model들보다 상당히 나은 성능을 달성
language modeling 또는 word vector들과 같은 pretext objective를



## 3. Data Processing
대용량의 비정제(uncurated) data들에서 정제된(uncurated) LVD-142M dataset의 image들을 retrieve하여 이와 유사한 image들을 가져옴
![[Pasted image 20241031121816.png|800]]
data processing pipline
(curated data로 retrieval -> uncurated data들을 선택)
1. embedding으로 변환(feature extraction) 
2. 중복 제거(deduplication)
3. Retrieval

### Data sources
- curated datasets:
	- ImageNet-22k, the train split of ImageNet-1k, Google Landmarks and several fine-grained datasets
- uncurated data source: a raw unfiltered dataset of images from a publicly available repository of crawled web data
	- 1.2B unique images

### Deduplication
uncurated data에 **copy detection pipeline**을 적용 & near-duplicate image들을 제거
- from "[A self-supervised descriptor for image copy detection](https://openaccess.thecvf.com/content/CVPR2022/html/Pizzi_A_Self-Supervised_Descriptor_for_Image_Copy_Detection_CVPR_2022_paper.html)"
- image들의 redundancy 감소 & diversity 증가 
- any benchmark의 test, validation set에 포함된 near-duplicates of images도 모두 제거

### Self-supervised image retrieval



## 4. Discriminative Self-supervised Pre-training
- **DINO의 loss**
- **iBOT의 loss**
- **SwAV의 centering**
- features와 a short high-resolution training phase를 spread하기 위해서 regularizer를 추가
### Image-level objective(DINO loss)

student와 teacher network로부터 추출된 feature들 간의 cross-entorpy loss를 고려
두 feature들은 ViT에서 생성된 `[cls]` token으로, 같은 image의 서로 다른 crop들로부터 얻어짐

student `[cls]` token:
- student `[cls]` token에 **student DINO head**를 적용해서 student **prototype score**를 얻어냄
- $p_s$를 얻기위해 softmax를 적용

[cls] -> student network -> student DINO head -> softmax -> p_s
 
teacher `[cls]` token:
- student와 비슷하게 적용
- teacher `[cls]` token에 teacher DINO head를 적용해서 teacher prototype score를 얻어냄
- moving average기반 centering을 사용하는 softmax를 적용

- 위 과정으로 얻어지는 **DINO loss term**:
	$$\mathcal{L}_{DINO} = - \sum p_t \log p_s$$



위의 과정으로 student의 parameter를 학습하고, [[Exponential Moving Average(EMA)]]를 통해 teacher head를 build

### Patch-level objective(iBOT loss) 
- [[iBOT Image BERT Pre-Training with Online Tokenizer]]

1. **student**에게 주어지는 input patch들을 random하게 **mask**하고, teacher는 원래대로 사용
2. **student mask tokens**에 **student iBOT head**를 적용 
3. student에서 mask된 것들과 일치하는 **(visible) teacher patch tokens**에 **teacher iBOT head**를 적용 
4. softmax와 centering을 적용

- 위 과정으로 얻어지는 **iBOT loss term**:
	$$L_{iBOT} = - \sum_{i} p_{ti} \log p_{si}$$
	-  i: mask된 token들에 대한 patch index들(indices)

위의 과정으로 student의 parameter를 학습하고, [[Exponential Moving Average(EMA)]]를 통해 teacher head를 build

#### Untying head weights between both objectives
DINO와 iBOT의 head들은, 크기가 큰 model에서는 parameter를 공유하면 성능이 나빠졌기에, 따로 학습함

### Sinkhorn-Knopp centering(SwAV centering)
- [[Unsupervised learning of visual features by contrasting cluster assignments]]

DINO와 iBOT의 **teacher softmax-centering** 단계를, **SwAV**의 **Sinkhorn-Knopp(SK) Batch Normalization**으로 대체
본 논문에서는 Sinkhorn-Knopp 알고리즘 단계를 3번 반복하였음
student에서는 softmax normalization을 적용

모든 클러스터가 고르게 활성화되도록 하기 위함

### KoLeo regularizer

- **KoLeo regularizer**:
	- Kozachenko-Leonenko differential entropy estimator로부터 유래됨
	- batch내의 feature들의 분포를 비슷하게 만듦
	- n개의 vector들 $(x_1, ..., x_n)$에 대해서,
		$$L_{koleo} = -\frac{1}{n}\sum_{i=1}^{n} \log(d_{n,i})$$
		- minimum distance($x_i$와 batch 내의 다른 point 사이의):
			- $d_{n,i} = \min_{j \neq i} \| x_i - x_j \|$
	- 이 regularizer를 계산하기 전에, L2-normalization 적용

### Adapting the resolution
image resolution을 높이는 것은 pixel-level의 downstream task들(segmentation, detection)에 매우 중요함
low resolution에서 작은 object들은 사라지기 때문

하지만 high resolution에서 training하려면 time과 memory가 많이 소요됨

따라서 high-resolution에서 시작하는 대신, 
pre-training과정의 마지막의 짧은 기간동안 518x518의 resolution으로 높여서 돌리는 방법을 사용
- from "[[Fixing the train-test resolution discrepancy]]"






## DINOv1과 DINOv2의 차이

1. 학습한 data의 크기
2. 
3. 
