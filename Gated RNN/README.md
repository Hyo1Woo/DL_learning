## RNN
![image](https://user-images.githubusercontent.com/92671224/169951799-64d88bb6-edfc-496d-b7ae-a7c03ec03200.png)   
![image](https://user-images.githubusercontent.com/92671224/169951874-31364f27-a70c-40a8-9caa-83d6a2f7f805.png)   

<br>

![image](https://user-images.githubusercontent.com/92671224/169951973-aa76a309-3f03-4527-a173-ddaf6fb3d9b5.png)

<br>

## RNN의 단점
- Back Propagation 할 때의 gradient vanishing problem
- long input data에 대하여 학습이 제대로 되지 않는 경향

<br>

## Gated RNN
![image](https://user-images.githubusercontent.com/92671224/169952328-813c4352-b46f-410a-b072-b944c68b723d.png)

- LSTM: 4개의 게이트
- GRU: 2개의 게이트
- GRU는 LSTM의 축소버전이라고 보면 됨

## LSTM
![image](https://user-images.githubusercontent.com/92671224/169952533-37ff6fea-1e94-41dc-8046-2255e8e2d7fb.png)

- Cell state: 게이트들에 의해서 어떤 정보가 허용되는지 결정됨
- Forget gate: 정보를 forget할지 keep할지 결정
- input gate: 새로운 cell value를 위해 가해지는 input 조절
- output gate: 다음 hidden state를 결정


## GRU
![image](https://user-images.githubusercontent.com/92671224/169952753-4e49e3a5-de25-4d5c-b764-50e3ab891c35.png)

- Reset gate: 과거 hidden info를 얼마나 제외할지 결정
- update gate: 어떤 info를 담을지, 제외할지를 결정. LSTM의 input,forget gate를 합쳐놓은 형태
- (1-) Activation: ![image](https://user-images.githubusercontent.com/92671224/169952962-11938526-d899-47f9-b401-deb5e7597924.png)
- LSTM에 비해 빠르게 학습하는 것으로 알려짐
