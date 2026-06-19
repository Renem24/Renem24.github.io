---
created: 2024-09-24 10:16
modified: 2024-10-17 11:51
---
# Momentum Encoder
---
## What is 'Momentum Encoder'?

student network의 weight들에 각각 [[Exponential Moving Average(EMA)]]를 적용하는 knowledge distilation 방식

contrastive learning에서의 queue를 대체하기 위한 개념으로 제시됨 
- ["Momentum Contrast for Unsupervised Visual Representation Learning"](https://openaccess.thecvf.com/content_CVPR_2020/html/He_Momentum_Contrast_for_Unsupervised_Visual_Representation_Learning_CVPR_2020_paper.html)

DINO에서는 self-training의 mean teacher의 의미로 사용
- ["Mean teachers are better role models: Weight-averaged consistency targets improve semi-supervised deep learning results"](https://proceedings.neurips.cc/paper/2017/hash/68053af2923e00204c3ca7c6a3150cf7-Abstract.html)
## How?



