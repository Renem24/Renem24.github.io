# NCE(Noise Contrastive Estimator)
---
#self-supervised_learning 

## What is 'NCE'?
"Unsupervised Feature Learning via Non-Parametric Instance Discrimination"에서 처음 제시

instance들을 classify하는 대신, compare만 수행

#### Cons.
- 모든 image들에 대한 비교를 해야함
	- 많은 batch 또는 memory 공간을 필요로 함

## Varients
자동으로 clustering 형태로 instance들을 그룹핑하는 방식도 존재