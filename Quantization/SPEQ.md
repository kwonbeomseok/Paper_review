# SPEQ
## Stochastic Precision Ensemble: Self-Knowledge Distillation for Quantized Deep Neural Networks (AAAI2020)
Paper:[[link]](https://arxiv.org/abs/2009.14502)

- - -
#### Algorithm
- Quantization aware training with KD
- KD를 사용할 때 따로 Teacher model이 존재하지 않고 같은 모델을 high bit precision으로 만든 모델을 통해 KD를 진행한다.
 ![speq](https://user-images.githubusercontent.com/49312486/106075066-481bee00-6150-11eb-99c8-efd665330d34.png)
- 위 그림처럼 n_A bit는 student의 target bit, n_H는 Teacher model의 high precision.
- Teacher model의 high precision을 항상 선택하는 것이 아닌 stochastic하게 선택을 하게 된다.
- KD loss를 학습할 때 KL Divergence가 아닌 Cosine Similarity를 사용한다.
    --> Teacher model의 output의 confidence가 항상 높지않기 때문에 KL보다는 Cosine이 confidence에 따라 적절히 학습시켜 줄 수 있다.
- 
- - -
#### pros
- Model sharing하므로 추가적인 model이 필요하지 않다
- - -
#### cons
- 왜 잘 동작하는지에 대한 이유가 없다
- - -
#### 논문 분석 방식
- Table1: Motivation
- Fig2: precision에 따른 다양한 softmax, 8bit ratio 분석
- Fig3: KL, CS Loss의 gradient 분석 (CS가 더 적합한 이유 설명)
- Table2: 여러가지 KD configure에 대한 결과 (CS, u=0.5가 제일 좋다는 결과)
- Table3: hyperparameter sweep experiment (hyperparameter의 sweet spot 찾음)
- - -
#### 다른 논문과의 비교 방식
- Table4: 다른 방법들과 성능 비교 (CIFAR10-VGG16, ResNet20 / CIFAR100-ResNet32, MobileNetV2)
- Table5: 다른 방법들과 성능 비교 (ImageNet-AlexNet, ResNet18, ResNet34)
- - -
#### 흥미로운 점
- 항상 Teacher model이 좋지 않아도 KD 학습이 가능한 부분
- - -
#### 의문점
- Activation quantization이 Noise라면 high precision model을 teacher로 사용한다는게 Student를 다양한 noise에 대해 학습을 시킨다고 생각함. 그러면 왜 다양한 노이즈를 통해 학습한 모델이 성능이 좋아지는건지?
- - -
#### 총평
- KD에 대해 많이 알지는 못하지만 기존에 알고 있던 Teacher model이 좋아야한다는 생각을 사라지게 해준 논문이었다.
- - -
#### 찾아볼 개념, 논문
- 

