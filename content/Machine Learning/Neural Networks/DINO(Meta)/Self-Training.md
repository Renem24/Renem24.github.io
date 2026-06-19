# Self-Training
---
## What is 'Self-Training'?
a small initial set of annotations(labels)    -propagate->     a large set of unlabeled instance

### Type?
#### Hard assignment Self-Training

hard assignment(하나의 label로 예측) 방식을 사용하여,
unlabeled instance들에 model이 예측한 **단일 label**을 부여하는 방식
#### Soft assignment Self-Training

soft assignment(label일 확률로 예측) 방식을 사용하여,
unlabeled instance들에 model이 예측한 **각 data들에 대한 확률 분포(soft pseudo label)**를 부여하는 방식


- [[Knowledge Distilation]]
