---
created: 2024-10-17 11:35
modified: 2024-10-17 11:35
---
# Gradient Descent(GD)
---
#optimization
## What is 'Gradient Descent(GD)'?
gradient의 반대방향(반대 부호)으로 weight을 update하는 loss function optimization 알고리즘

## How?
loss function의 gradient를 계산하고, 그 반대 방향으로 weight을 update

$$w = w - \eta \cdot \nabla L(w)$$