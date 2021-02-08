# HAWQ-V2
## HAWQ-V2: Hessian Aware trace-Weighted Quantization of Neural Networks
Paper:[[link]](https://proceedings.neurips.cc/paper/2020/file/d77c703536718b95308130ff2e5cf9ee-Paper.pdf)
Supplemental:[[link]](https://proceedings.neurips.cc/paper/2020/file/d77c703536718b95308130ff2e5cf9ee-Supplemental.pdf)


- - -
#### Algorithm
- HAWQ-V1의 문제점을 개선시킨 알고리즘(1. Hessian top eigenvalue만으로 sensitivity를 측정하기 때문에 나머지 eigenvalue를 무시해서 정확하지 않다. 2. 상대적인 sensitivity만 제공하기 때문에 manual selection이 필요하다. 3. mixed-precision activation quantization을 고려하지 않았다.
- Hessian eigenvalue의 average trace를 구해서 sensitivity를 측정 
- Computation을 간단하게 하기 위해 second-order로 구하고 hutchinson algorithm을 이용하여 빠르게 계산한다?
- V1은 weight에만 적용했지만 V2는 Activation에도 적용하려면 계산이 더욱 힘듬 -> diagonal matrix의 특성을 이용하여 계산 할 수 있다.
- Manual bit precision selection을 preto frontier를 이용하여 자동화 함.
- - -
#### pros
- 
- - -
#### cons
- 
- - -
#### 논문 분석 방식
- 
- - -
#### 다른 논문과의 비교 방식
- 
- - -
#### 흥미로운 점
-
- - -
#### 의문점
- 
- - -
#### 총평
- 
- - -
#### 찾아볼 개념, 논문
- HAWQ-V1  

