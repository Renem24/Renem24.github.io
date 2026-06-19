---
created: 2024-10-15 17:23
modified: 2024-10-17 16:25
---
# BYOL
---
#metric_learning
## What is 'BYOL'?
- ["Bootstrap Your Own Latent - A New Approach to Self-Supervised Learning"](https://arxiv.org/pdf/2006.07733)

image representation learning을 위한 self-supervised learning 방법



## How?
두 개의 network을 사용하며, 서로 상호작용하며 학습
- online network
- target network

한 image의 augmented view(crop)에서 online network가 target network의 다른 augmented view(crop)를 예측하도록 학습하다가, 
target network는 online network의 weight를 늦은 평균으로 업데이트하는 것

서로 다른 변형 이미지의 표현을 예측하는 방식으로 학습