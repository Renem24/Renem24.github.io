# SVM(Support Vector Machine)
---
## What is 'SVM'?

![[Pasted image 20241014160514.png|300]]
classification해야하는 data들 사이의 margin을 maximize하는 것이 목적

margin을 통해서 data point들을 분리함


## How?

- classifier equation(linear)
$$w^Tx+b=0$$

- positive samples
$$w^Tx^++b>0$$
- negative samples
$$w^Tx^-+b<0$$

#### Support Vectors?
- positive support vectors
$$w^Tx^++b=1$$
- negative support vectors
$$w^Tx^-+b=-1$$

#### Margin?
$$\frac{2}{\| w \|_2}$$

## Keypoints

기본적으로는 linear classification method로 사용됨(linear SVM)

[[Kernal Function]]을 사용하면 high-dimension에서의 classification도 가능(non-linear SVM)

