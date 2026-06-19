---
created: 2025-04-26 20:17
modified: 2025-04-26 20:42
---
# Perceptron
---
### References
- https://wikidocs.net/24958

### 정의
Frank Rosenblatt가 1957년 제안한 초기 형태의 Neural Network
다수의 입력으로부터 하나의 결과를 내보내는 알고리즘
실제 뇌를 구성하는 신경 세포인 뉴런과 유사하게 동작한다.
- 신호가 역치(threshold)를 넘으면 다음 뉴런으로 신호를 전달한다.

### 방식

![[Pasted image 20250426211952.png|400]]
- x: input 
- y: output
- w: weight

그림 안의 원이 인공 뉴런에 해당한다.
각 input들이 weight과 곱해져서 인공 뉴런에 보내지고, 그 값이 역치(threshold)를 넘으면 1을 출력하고, 넘지 않으면 0을 출력한다.
수학적으로 이러한 형태를 Step Function이라고 한다.

예시 step function
![[Pasted image 20250426212741.png|400]]


(수식 표현)
$$if \ \sum_{i}^{n} w_i x_i \geq \theta \rightarrow y = 1$$
$$if \ \sum_{i}^{n} w_i x_i < \theta \rightarrow y = 0$$
- Θ: step function에 사용된 threshold

여기서 threshold를 좌변으로 넘기고 bias로 표현할 수도 있는데, 이때 input 값 1에bias가 곱해지는 것으로 표현한다.

bias가 포함된 버전
![[Pasted image 20250426213738.png|400]]
(수식 표현)
$$if \ \sum_{i}^{n} w_i x_i + b \geq 0 \rightarrow y = 1$$
$$if \ \sum_{i}^{n} w_i x_i + b< 0 \rightarrow y = 0$$
- b: bias

많은 책들에서는 bias를 그림이나 수식에서 생략해서 표현하지만, 실제로는 bias 또한 weight과 함께 optimize해야할 parameter이다.


### 특징


### 예시