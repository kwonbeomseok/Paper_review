# SLM
## Searching for Low-Bit Weights in Quantized Neural Networks)
Paper:[[link]](https://proceedings.neurips.cc/paper/2020/file/2a084e55c87b1ebcdaad1f62fdbbac8e-Paper.pdf)

Code: [[link]](https://github.com/huawei-noah/Binary-Neural-Networks/tree/main/SLB)
- - -
#### Algorithm
- using continuous relaxation instead of STE
- In train, use expeceted weight
- In inference, use quantization weight with maximum probability
- Quantization gap is between expected weight and quantized weight. To reduce it, gradually decrease temperature by theorem 1
- At the beginning of optimization, high temperature(uniform distribution). At the end, low temperature(categorical distribution) -> TAS에서 사용하는 gumbel temperature와 동일한 기능
- Instead of conventional BN, to reduce quantization gap(expected vs quantized), use State BN(SBN) which adds BN of quantized weights to conventional BN of expected weights
- Activation quantization = Dorefa
- tau scheduler = exponent
- - -
#### pros
- Differentiable quantization method
- - -
#### cons
- weight마다 distribution이 존재하면 연산이 오래 걸릴 것 같다.
- SBN 역시 convolution을 두번해야하기 때문에 오래 걸릴 것 같다.
- - -
#### 논문 분석 방식
- Fig2. temperature scheduler에 따른 Test Accurracy
- - -
#### 다른 논문과의 비교 방식
- Table 1,2. CIFAR10-ResNet20, VGG-small / Quantization Accuracy 비교(1/1, 2/2, 4/4, ...)
- Table 3. ImageNet-ResNet18 / Bits에 따른 Accuracy 비교

  -> 다른 모델은 왜 없는지
  
  -> LSQ 성능 빠짐
- Fig3. Super Resolution 비교 
- - -
#### 흥미로운 점
- NAS에서 사용하던 continuous relaxation을 응용한 부분 (어느정도는 생각하고 있던 부분)
- Super Resolution에도 quantization 적용한 결과
- - -
#### 의문점
- index는 softmax의 maximum value로 정하는건 알겠는데 scale factor는 어떤 방식으로 구하는건지?
- SBN이 왜 좋은건지? gap을 줄여줘서?
- pretrain부터 시작?
- - -
#### 총평
- Weight quantization method가 궁금함.
- NAS에서 항상 생각하던 부분을 실제로 논문으로 낸 부분이 재미있었음.
- 아이디어가 있으면 빨리 실행해야 한다...
- - -
#### 찾아볼 개념, 논문
- 

