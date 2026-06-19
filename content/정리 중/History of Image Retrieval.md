# History of Image Retrieval
---

## 1. Text-Based Image Retireval(TBIR)
### Image meta search
키워드나 설명 같은 **meta 데이터**를 기반으로 한 검색

- [[TBIR(Text-Based Image Retireval)]]

## 2. Content-Based Image Retireval(CBIR)
texture, color, shape 등의 visual content를 기반으로 한 검색

- [[CBIR(Content-Based Image Retireval)]]

## 3. Local Features
scale과 rotation에 invariant(불변)하는 feature들을 추출

### What is 'Local Features'?

- [[Image Feature]]

## 4. Bag of Visual Words(BoVW)

local feature들을 Visual Word들로 표현 -> histogram으로 확인
high-dimensional feature space에서의 더 효율적인 indexing과 retrieval이 가능 해짐

- [[Bag of Visual Words]]

## 5. Machine Learning의 도입

### Support Vector Machine(SVM)
traditional linear classfication machine learning method

- [[SVM(Support Vector Machine)]]

### Clustering

- [[Clustering]]

## 6. Deep Learning의 도입(CNN)
CNN기반의 딥러닝 모델들을 통해 model이simage의 feature를 이해하며 학습하여 classification을 수행

### Convolutional Neural Networks

- [[Convolutional Neural Network (CNN)]]

### Models
- AlexNet
- VGG Network
- GoogLeNet
- ResNet

여기서 Deep learning model들이 추출하는 image feature들은 global과 local을 모두 포함하는 feature라고 생각

## 7. Transfer Learning

pre-trained model을 특정 dataset에 대하여 fine-tuning하여 특정 작업에 대한 성능을 향상시킴

## 8. Hashing Method의 발전

검색 속도의 향상

### Locality-Sensitive Hashing

- [[LSH(Locality-Sensitive Hashing)]]

## 9. Metric Learning

embedding space에서의 distance를 minimize하는 방식을 학습하는 것

- [[Triplet Loss]]
- [[Contrastive Loss]]

## 10. GAN의 활용
[[Data Augmentation]]에 [[GAN(Generative Adversarial Networks)]]를 사용

## 11.Attention Mechanism의 도입

image의 각 patch에 대한 중요도를 다르게 적용하는 attention mechanism을 사용

### ViT(Vision Transformer)

[[Vision Transformer (ViT)]]

