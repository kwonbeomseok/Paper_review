# FleXOR
## FleXOR: Trainable Fractional Quantization (NeurIPS2020)
Paper:[[link]](https://arxiv.org/abs/2009.04126)

Author's explain(Faceboook): [[link]](https://www.facebook.com/groups/TensorFlowKR/permalink/1309523079388747)
- - -
#### Algorithm
- quantization aware training
- fractional bits quantization < 1bit
- only weight quantization, activation is not quantized
- first, last layer are not quantized
- non-uniform precision quantization(결국 convolution은 1bit)
- N_tap be the number of 1’s in a row of M
- weight 값을 encrypted weight로 저장한 후 forward시 XOR-gate를 통과시켜(convert, reshape) convolution 진행 후 backward로 encrypted weight 학습
- backward시 STE대신 tanh + scale factor를 이용한 방법 사용
- train시 weight뿐만 아니라 S_tanh도 warmup 사용
- - -
#### pros
- memory footprint is less than binary network
- - -
#### cons
- too many hyperparameters(S_tanh, N_in/N_out, N_tap?)
- S_tanh is optimized by empirically
- - -
#### 논문 분석 방식
- Fig5: 다른 방법(STE, Analog XOR)과 Test accuracy curve 비교
- Fig6: Hyperparameter에 따른 Test accuracy curve, histogram 분석
- Fig7: Hyperparameter에 따른 Test accuracy curve
- Table2: stage별로 다른 XOR-gate 사용시 accuracy 
- - -
#### 다른 논문과의 비교 방식
- Table1: ResNet20, ResNet32, FP, quantized acc compare
	-> FP자체가 낮음, memory를 줄이긴 했으나 다른모델(LQ-Net, DSQ) 보다 accuracy가 1~2% 떨어짐
- Table3: 마찬가지로 accuracy 비교
- - -
#### 흥미로운 점
- XOR-Gate 1개를 Network 전체에 공유해서 사용한다고 했는데 가능한건지
- backward시 STE가 아닌 tanh를 사용한 부분
- - -
#### 의문점
- XOR-Gate의 조합은 어떻게 결정되는지
- Algorithm1을 보면 weight의 갯수= k * k * C_in * C_out에다가 /N_out, * N_in하는데 그러면 총 #weight가 줄어드는 것 아닌가?, For 문을 보면 reshape하는데 가능한건지
- Is shorcut quantized?
- 논문에서는 XOR-gate의 area, latency overhead가 무시할 정도라고 하는데 어느정도인지 궁금
- binary quantization이라서 더이상 가속이 의미가 없어서 memory를 줄이는 방식에 대한 연구를 진행한다고 생각해야 하는듯?
- - -
#### 총평
- binary network보다 더 줄일 수 있다고 생각을 못해봤는데 그 가능성을 보여줘서 재미있었던 논문
- Weight quantization만 진행해서 아쉬움
- 이전 논문(XOR-gate network)을 알아야 좀 더 제대로 이해할 수 있을 듯
- 알고리즘 혹은 다른 논문과의 비교에서 주로 test accuracy만을 metric으로 사용했는데 다른 방법은 없는지?(나도 지금은 생각나는게 없음. 다른 논문 읽으면서 생각해보기. quantization 전체에 대한 생각이 될 수도)
- - -
#### 찾아볼 개념, 논문
- XOR-gate 이전 논문 볼 필요 있을 듯
- Hamming distance : [[link]](https://ko.wikipedia.org/wiki/%ED%95%B4%EB%B0%8D_%EA%B1%B0%EB%A6%AC#:~:text=%EB%B8%94%EB%A1%9D%20%EB%B6%80%ED%98%B8%20%EC%9D%B4%EB%A1%A0%EC%97%90%EC%84%9C%2C%20%ED%95%B4%EB%B0%8D,%EB%93%A4%EC%9D%B4%20%EB%AA%87%20%EA%B0%9C%EC%9D%B8%EC%A7%80%EB%A5%BC%20%EC%84%BC%EB%8B%A4)
- tanh derivative for backward

