# PROFIT
## PROFIT: A Novel Training Method for sub-4-bit MobileNet Models
Paper:[[link]](https://arxiv.org/abs/2008.04693)

Code: [[link]](https://github.com/EunhyeokPark/PROFIT)
- - -
#### Algorithm
- 1. AIWQ를 이용한 PROFIT 2. DuQ + negative padding
- activation instability를 측정하는 AIWQ라는 metric을 소개하고 그것에따라 profit 적, AIWQ를 per-layer sensitivity로 생각, training iteration 전,후 KL divergence 값, 계산량 때문에 second-order로 계산
- AIWQ를 training 하면서 sampling -> sampling한 AIWQ를 sorting후 N_profit만큼 interation을 돌면서 모든 layer의 weight를 순차적으로 freezing -> BN만 조금만 training
![image](https://user-images.githubusercontent.com/49312486/106682584-2a460180-6606-11eb-8efe-45dd9dee7bb7.png)
- h-swish 같은 activation에도 quantization을 적용하기 위해 DuQ + negative padding 적용
- - -
#### pros
- MB network quantization accuracy including depthwise convolution.
- - -
#### cons
- KL divergence compute time?
- negative padding시 추가적인 연산, 메모리, 하드웨어 필요?
- 2bit 결과는 없음
- - -
#### 논문 분석 방식
- Fig1. MB network의 quantization 성능을 비교하여 motivation? 설명
- Fig2. A32, W32 -> W2로 가면서 AIWQ, running_mean, running_var을 측정하여 MB network에서 weight quantization시 accuracy degradation이 생기는 이유 설명
- Fig3. Weight quantization level이 줄어들 시 AIWQ가 커지는 이유를 설명, threshold 근처 값들이 다른 값으로 변하기 때문
- Fig4. MB network AIWQ 분석, layer별로 다른 AIWQ
- Fig5. h-swish같은 activation quantization시 challenging한 부분
- Fig6. other quantization method를 소개하면서 각각의 한계를 설명, PACT, QIL: asymmetric 불가, LSQ: negative range에 Q_n만큼 할당
- Fig7. Negative padding에 대한 설명 
- Fig8. Model size vs accuracy, cost vs accuracy를 보여주면 PROFIT의 성능 설명
- Table1. Model별 profit 적요 accuracy
- - -
#### 다른 논문과의 비교 방식
- Table2. 다른 Method와 MB1, MB2 bit에 따른 accuracy 비교
- Table3. PACT, QIL, DuQ 성능 비교
- - -
#### 흥미로운 점
- 일정 부분의 weight만 고정한채로 학습을 하더라도 성능이 계속 올라갈 수 있다는 부분
- - -
#### 의문점
- AIWQ sampling 하는 동안 weight, activation은 quantization 된 상태인지
- Weight만 freezing 하는지 activation도 freezing 하는지? activation은 freezing이 불가능 한거 아닌가?
- duq 적용시 interval parameter의 gradient 어떻게 가져가는지
- negative padding이 필요한건지
- - -
#### 총평
- MB network의 quantization의 문제점을 분석하고 그것을 metric을 만들어 quantization sensitivity를 측정한 부분이 좋은 것 같다.
- metric을 이용하여 quantization의 성능을 올리는 알고리즘을 제시한 방법이 좋은 것 같다.
- - -
#### 찾아볼 개념, 논문
- 

