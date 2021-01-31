# PSG
## Position-based Scaled Gradient for Model Quantization and Pruning
Paper:[[link]](https://proceedings.neurips.cc/paper/2020/file/eb1e78328c46506b46a4ac4a1e378b91-Paper.pdf)
Appendix: [[linke]](https://proceedings.neurips.cc/paper/2020/file/eb1e78328c46506b46a4ac4a1e378b91-Supplemental.pdf)

Code: [[link]](https://github.com/Jangho-Kim/PSG-pytorch)
- - -
#### Algorithm
- Weight이 position마다 gradient를 다르게 가져가서 FP에서도 Quantization한 것 같은 weight convergence를 보인다. 그래서 quantization 적용시에도 적은 Acc degradation이 생김
- Post Training Quantization, QAT는 추가적인 학습이 필요하므로 edge device같은 embedded에서 실현 가능성이 제한적
- Weight들을 원하는 target point로 수렴하도록 warp function 사용(아래 그림 참고)
![image](https://user-images.githubusercontent.com/49312486/106386681-813ab380-6419-11eb-9590-070f33d90632.png)
- Weight Quantization method / activation은 reference[31],[1]처럼 batchnorm parameter 사용
- - -
#### pros
- 학습시 기존 SGD와 동일한 overhead, 다른 논문과 달리 training에 추가적인 부분이 없음.  
- - -
#### cons
- PTQ의 장점은 QAT와 다르게 training을 안해도 된다는 점(기존 PTQ에서 training이 필요해도 약간만 함)인데 PSGD는 Training이 필요함 --> 애초에 pretrained model 만들 때부터 PSGD를 쓰라는 건가보네
- - -
#### 논문 분석 방식
- Fig1, SGD vs PSGD를 bit에 따른 Acc, Quantization error(=mean squared error), distribution을 보여주면서 PSGD의 장점, 문제해결 능력을 제시
- Fig2, Toy example를 사용하여 algorithm 동작 방식을 보여줌
- 
- - -
#### 다른 논문과의 비교 방식
- Table1 : pruning acc vs sparse ratio 비교
- Table2 : regularization method which do not have post training procedure 비교
- Table3 : PTQ acc 비교
- Table4 : Extremely low bits accuracy experiments
- - -
#### 흥미로운 점
- PSG를 사용하면 Full precision에서도 quantized value 처럼 학습되는 부분
- Warp function을 통해 weight의 convergence position을 조작할 수 있는 부분
- - -
#### 의문점
- Quantized value를 target point로 설정하는데 scratch부터 학습 할 때는 어떻게 설정하는 건지?
- gradient scale을 어떻게 SGD와 동일하게 가져가는지는 이해했는데 warp function을 어떻게 정하는지는 모르겠음.(임의로 하는건가)
- - -
#### 총평
- Weight 자체를 quantization-friendly하게 만든다는 생각이 참신해서 좋은 논문이었습니다.
- Quantization 관련 디테일한 부분은 코드를 보며 참고를 하면 좋을 것 같습니다.
- - -
#### 찾아볼 개념, 논문
- reference 30, 32에서 directly minimize quantization error method를 소개했다고 나옴. 확인하면 좋을 듯

