# CBIR(Content-Based Image Retireval)
---
#CBIR
## What is 'CBIR'?

finding the **similar images** from a large database for **query image**

---
## Evolution of 'CBIR'
### 1. Hand-Crafted Descriptor Based Image Retrieval

가장 초기에 등장한 CBIR method

**visual content**(**color**, **texture**, **shape**, **gradient**, etc.)에 기반한 retrieval

image의 **feature descriptor representation**에 크게 의존

**Feature descriptor representation**:
- **discriminating ability**, **robustness**, **low dimensionality** 필요
- **hand-designed** 또는 **hand engineered feature description**으로도 불림 

#### Cons.
- 정확한 비교에 사용하기는 어려움
	ex. recognition

#### Related Works
- "Features for image retrieval: An experimental comparison"
- "Distinctive image features from scale-invariant key-points"
- "Multiresolution gray-scale and rotation invariant texture classification with local binary patterns"
- "Rotation and illumination invariant interleaved intensity order-based local descriptor"
- "Local oppugnant color texture pattern for image retrieval system"
- "Biologically inspired feature manifold for scene classification"
- "Aggregating local image descriptors into compact codes"
- "Local tetra patterns: A new feature descriptor for content-based image retrieval"
- "Local wavelet pattern: A new feature descriptor for image retrieval in medical CT databases"
- "Iterative quantization: A procrustean approach to learning binary codes for large-scale image retrieval"
- "A novel local pattern descriptor—Local vector pattern in high-order derivative space for face recognition"
- "Multichannel decoded local binary patterns for content-based image retrieval"
- "Local gradient hexa pattern: A descriptor for face recognition and retrieval"


### 2. Distance Metric Learning Based Image Retrieval

Machine Learning의 발전과 함께 등장한 CBIR method

image들간의 similarity를 계산하는 distance function을 학습하는 방식  

feature space에서 비슷한 image들은 가깝게, 비슷하지 않은 image들은 멀게 배치하는 것이 목적

일반적으로 [[#1. Hand-Crafted Descriptor Based Image Retrieval]]보다 높은 성능을 보임

#### Cons.
- 대다수의 방법들은 linear distance function을 사용하고 있음
	-> non-linear data에 대한 retrieval은 어려움

#### Related Works
- Contextual constraints distance metric learning
	- "Learning distance metrics with contextual constraints for image retrieval”
- Kernel-based distance metric learning
	- "Kernel-based distance metric learning for content-based image retrieval”
	- "Supervised hashing with kernels"
- Visuality-preserving distance metric learning
	- "A boosting framework for visuality-preserving distance metric learning and its application to medical image retrieval"
- Rank-based distance metric learning
	- "Rank-based distance metric learning: An application to image retrieval"
- Semi-supervised distance metric learning
	- "Semi-supervised distance metric learning for collaborative image retrieval and clustering"
- Hamming distance metric learning
	- "Hamming distance metric learning"
	- "Fast structural binary coding"
- Rank based metric learning
	- "Rank preserving hashing for rapid image search"
	- "Top rank supervised binary coding for visual search"


### 3. [[Deep Learning Based Image Retrieval]]

deep learning model을 사용해서 feature를 extract하는 방식

**Deep Learning Architectures**:
- [[Convolutional Neural Network (CNN)]]
- [[Transformer]]
