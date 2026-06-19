---
created: 2024-10-08 11:14
modified: 2024-10-14 15:34
---
# Bag of Visual Words
---
## What is 'Bag of Visual Words'?
Bag of Words를 Image에 적용한 것

전체 image들로부터, 각 image마다 n개의 feature vector들을 추출하고 
K-means같은 방법으로 클러스터링(그룹화)한다.
이 클러스터들의 중심(centroid)들이 각각의 visual word가 된다.
(클러스터의 개수 = visual word의 개수)

## How?

#### TF-IDF weighting
$$t_i = \frac{n_{id}}{n_d} \log \frac{N}{n_i}$$
- $n_{id}$ : occurance of word i in a document (image) $d$
- $n_{d}$ : total number of words in a document $d$
- $n_i$ : number of documents (images in the database) that contain the word $i$
- $N$ : number of documents (images in the database)
![[Pasted image 20241008155222.png|600]]
![[Pasted image 20241008155334.png|600]]
##### Reweighted histograms
![[Pasted image 20241008155437.png|600]]

##### Original histograms
![[Pasted image 20241008155455.png|600]]

##### Euclidean distance
![[Pasted image 20241008155531.png|900]]

---
### references
https://www.youtube.com/watch?v=a4cFONdc6nc
