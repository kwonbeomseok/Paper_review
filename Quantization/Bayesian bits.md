# Bayesian bits
## Bayesian Bits: Unifying Quantization and Pruning (NeurIPS2020)
Paper:[[NeurIPS2020]](https://proceedings.neurips.cc/paper/2020/file/3f13cf4ddf6fc50c0d39a1d5aeb57dd8-Paper.pdf)
      [[Arxiv]](https://arxiv.org/pdf/2005.07093.pdf)

- - -
#### Algorithm
- Bayesian Bits, a practical method for joint mixed precision quantization and pruning through gradient based optimization.
- quantized residual error마다 gate를 두고 bit를 정하게 한다(2의 지수승 bits). 이때 0-bit는 pruning 역할을 하게 된다. 
- what is quantized residual error? quantization error를 의미하는건가? no, quantized residual error는 quantization error를 다시 quantization한 결과
- post-training quantization
- 2bit를 4bit로 만드는 방법: Fig1을 보면 이해가 쉽다. quantization error 부분을 다시 quantize해서 quantization level을 추가하는 방식
- final quantization equation is Eq6: 여기서 z가 gate 역할을 한다.
- gate 전체가 0이면 pruning이 된다. filter 단위로 gate를 둬서 structure pruning. 근데 grid step size를 share한다는데 여러 filter 중 어떻게 grid step size 계산하는지?
- 수식 증명 너무 어렵다.....(2.2, 2.3, 2.4, 3. 다시 꼭 읽기!!)
- quantization aware training도 가능 한듯?


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
- bernoulli
- log-likelyhood
- vae objective function
- reference[18][19] paper 읽어보기: We refer the reader to [18] and [19] for overviews of hardware-friendly quantization and compression techniques, respectively

