# Long-Tail Learning
---
### What is 'Long-tail Learning'?

class들 간의 sample 개수의 불균형을 해결하기 위한 학습 방법

대부분의 sample들은 **head class**에 모여있고, **long-tail class**에는 적은 sample들만이 포함됨

### 주요 approach 방법
1. **re-weighting** : 적은 class에 더 큰 가중치를 주기
2. **re-sampling** : class당 sample 수의 균형을 맞추기 위해서, 다시 sample을 뽑기
3. **transfer-learning** : long-tail class에 transfer하기


### Datasets
![[Pasted image 20240923141531.png|250]]
- Places-LT(long-tail)
- CIFAR100-LT
- iNaturalist
- ImageNet-LT