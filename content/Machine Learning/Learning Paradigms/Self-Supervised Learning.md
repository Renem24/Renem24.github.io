---
created: 2024-10-15 16:16
modified: 2025-04-02 15:35
---
# Self-Supervised Learning
---
## ref.
- \[NeurIPS 2021 Tutorial] Self-Supervised Learning: Self-prediction and Contrastive Learning
	- https://neurips.cc/media/neurips-2021/Slides/21895.pdf


## What is 'Self-Supervised Learning'?
unlabeled data만 무지막지하게 많다. 
unlabeled data이지만, unsupervised learning으로 하기보다는 supervised learning처럼 학습하고 싶다.
이러한 접근에서 SSL이 출현했다.
Self-Supervised Learning은 label없이 data 그 자체에서 pseudo label을 만들어서 학습에 사용한다.

Self-Supervised Learning은 representation learning 방식에 속한다. (representation learning with unlabeled datas)
이 말인 즉슨, pretrained SSL 모델들이 다른 모델들의 Encoder backbone으로 많이 사용된다는 얘기이다.
그리고 직접 성능을 평가할 수 없기 때문에, downstream task(ex. linear probe)에서 evalution을 수행한다.

현재 Self-Supervised Learning의 접근방식은 2 갈래로 나뉜다.
1. Self-Prediction : 하나의 data 내의 일부분
2. Contrastive Learning : batch 내의 data들 간의 관계로부터 학습

## How?
unlab


이미지를 가리고 이를 채우도록 학습
contrastive learning

유사한 이미지에 대해서 유사한 representation(feature vector)를 추출하도록 학습하는 것

## Example

---
### Self-Prediction

### Contrastive Learning
