# K-Means

## What is 'K-Means'?
k개의 중심점(centroid)를 기준으로, 각 중심점들 주위의 data point들을 같은 그룹(cluster)으로 분류(classify)

## How?
##### Algorithm
1. k로 얼마를 사용할지 선택
2. 랜덤하게 k개의 centroid를 선택(다른 기준으로 시작 가능) & centroid들과의 distance를 계산하여, data point들을 군집화하기(cluster)
3. 각 cluster의 average를 구해서, 이를 새로운 centroid로 선택
4. 