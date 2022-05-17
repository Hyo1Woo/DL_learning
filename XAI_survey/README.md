## Opportunities and Challenges in Explainable Artificial Intelligence (XAI): A Survey

### 0. XAI 정의
"XAI란 인간의 설명이 아닌 AI가 설명을 도출하여, 사람이 AI의 동작과 결과를 이해하고 올바르게 해석할 수 있고, 결과물이 생성되는 과정을 설명 가능하도록 해주는 기술을 의미한다."

### 1. XAI의 필요성
![image](https://user-images.githubusercontent.com/92671224/159242491-7ff62dc1-b641-4627-999a-3683ac234fa9.png)

- 인공지능의 모델이 점점 더 깊어짐으로 인해 각각의 파라미터들이 무엇을 의미하는지 알기가 어려워짐

#### 예시
- 은행 &rarr; 신용대출가능여부 판단
- 병원 &rarr; 암진단
- 자율주행 &rarr; 신뢰성

#### XAI에 대한 움직임
- 2018년 부터 의사 결정 이유에 대한 설명을 요구하는 EU의 General Data Protection Regulation
- 이유를 설명할 수 없다면 의료, 군사 등 중요작업에서는 사용하기 어려울 것으로 예상
- 과학기술정보통신부에서 발표한 R&D전략에도 2025년까지 eXplanable AI에 대한 계획이 포함

<br>

![image](https://user-images.githubusercontent.com/92671224/159244564-b9495074-22ad-418a-b8e8-59415f0bc4c4.png)


<br>

### 2. XAI의 분류
| 관점 | 분류 | 
| ------------ | ------------- | 
| Scope | Local vs Global | 
| Methodology | BackPropagation vs Perturbation |
| Usage | Intrinsic vs Post-Hoc | 

<br>

### 3. Scope
#### Local vs Global
![image](https://user-images.githubusercontent.com/92671224/159246251-56b951a0-aaf6-43ca-98bd-f6040a917fd6.png)![image](https://user-images.githubusercontent.com/92671224/159246338-ae1136f5-fd7d-4f15-923c-8b18782064e9.png)

### GLOBAL
![image](https://user-images.githubusercontent.com/92671224/159254609-7ebf3f9d-47a5-4310-bab1-43f02419ae43.png)
- 복잡한 deep 모델을 linear counterparts로 축소하여 해석하기 쉬운 형태로 만듦
- Rule-based, tree-based model이 대표적
- Non-linear 모델을 선형모델, decision tree로 대체하여 해석가능하게 하는 경우도 존재

<br>

### LOCAL  
#### 1) Activation Maximization  
![image](https://user-images.githubusercontent.com/92671224/159255560-c6c7c762-1639-414a-a7d1-06b79ecc1779.png)  
![image](https://user-images.githubusercontent.com/92671224/159248463-3286d9eb-0098-4b0c-8d7e-2616ffe9daa2.png)  
- layer가 많아질수록 각 layer가 무엇을 의미하는지 알기가 어려워짐  
- CNN의 각 layer의 중요성을 알기 위해 특정 hidden unit activation을 최대화 하는 input pattern을 탐지
- feature map 상의 특정 neuron(뉴런)을 조사 타겟으로 설정하고, 이를 최대 수준으로 활성화시키는 입력 이미지의 형태를 조사하는 것

<br>

#### 2) Saliency Map Visualization  
![image](https://user-images.githubusercontent.com/92671224/159248766-1c943673-b450-43d7-b52f-208e66d1b68c.png)  
- 픽셀별로 gradient를 계산 후 gradient가 클수록 더욱 영향력을 주는 픽셀로 생각함
- visualization 방법에는 class model visualization 과 specific class visualization이 존재
- gradient를 계산한 이후 positive gradient를 갖는 픽셀을 통해 saliency map을 구할 수 있음

<br>

#### 3) Layer-wise Relevance BackPropagation (LRP)
- output prediction을 back propagation을 통해 분해하여 input data의 각 feature의 relevance score를 도출  
- simple nn 일 때 예시  
![image](https://user-images.githubusercontent.com/92671224/159251240-bbc0d34b-cdd3-4679-af3f-9ddf94152672.png)  
![image](https://user-images.githubusercontent.com/92671224/159251261-4938b006-3981-41e3-b212-8ace8f20ea20.png)  
![image](https://user-images.githubusercontent.com/92671224/159251283-c39b767e-309c-466a-9f65-1f45ba4db5c8.png)  

<br>

### GLOBAL
#### 1) Class Model visualization
![image](https://user-images.githubusercontent.com/92671224/159253102-d47c944c-015e-4852-915f-44389b2f7ae0.png)
- Activation Maximization(local)을 global하게 확장한 것 

<br>

#### 2) Concept Activation Vectors (CAVs)
![image](https://user-images.githubusercontent.com/92671224/159254763-bdc5b617-db35-41ef-a585-0468a15e03e6.png)  
- positive 컨셉 : 사람이 구분할 수 있는 컨셉
- negative 컨셉 : 그 외의 random한 컨셉
- positive 컨셉과 negative 컨셉을 구분하는 방법
- 두 컨셉을 구분하는 Binary classification

<br>
   
#### 3) Spectral Relevance Analysis (SpRAy)  
![image](https://user-images.githubusercontent.com/92671224/159256037-21a9ee54-0f69-441f-bf01-9bb6bb7cdae9.png)  
- LRP를 통해 각 입력값의 relevance score를 구한 후, 해당 score를 기준으로 군집화
- 가장 중요한 cluster 값을 도출함

<br>

### 4. Methodology
![image](https://user-images.githubusercontent.com/92671224/159256899-994c360e-2700-4246-8b61-f7bc58a605b9.png)

### BackPropagation
#### 1) Saliency Maps
- CNN의 결과를 해석하는 데에 가장 오래되었으나 가장 자주 쓰이는 방법
- 이미지 안에 어떤 부분이 classification하는데 영향을 끼쳤는지 보여줌

<br>

#### 2) class activation mapping (CAM)
![image](https://user-images.githubusercontent.com/92671224/159257519-aec80f6d-e4ce-4056-ac3b-1be031a3232c.png)  
- 기존의 cnn계열 이미지 분류모델은 feature map을 flatten해서 fc로 변환함
- 그렇게 하게되면 기존의 공간적인 정보를 모두 잃게 됨
- 따라서 Global Average Pooling 사용
- 마지막 feature map을 꺼내와서 채널별로 대응하는 weight를 곱한 후 모두 더해주면 모델이 어느 부분을 보고 class를 분류 했는지 알 수 있음
- 개선 버전 &rarr; **Grad-CAM**  
<img src ='https://user-images.githubusercontent.com/92671224/159259279-55082fc9-783c-4567-9796-78c8c9cb84ae.png' width=50%, height=50%>  

<br>

#### 3) Salient Relevance (SR) Maps
- context 까지 인지할 수 있는 salience map

<br>

### Perturbation
- 입력 데이터 값에 다양한 변화를 주며 학습 모델을 반복적으로 조사함으로써 모델을 설명하고자 하는 것
- ex) blur, making 등

<br>

#### 1) DeConvolution nets for Convolution Visualizations
![image](https://user-images.githubusercontent.com/92671224/159259994-5d8718ee-afb1-41a8-9190-2694266820a0.png)  
![image](https://user-images.githubusercontent.com/92671224/159260059-a8056475-ff9a-4c2c-b1d1-5f23167c7f25.png)  
- Activation map을 생성
- 각 layer가 무엇을 어떻게 학습하는지 알 수 있음

<br>

#### 2) Randomized Input Sampling for Explanation (RISE)
![image](https://user-images.githubusercontent.com/92671224/159260460-401a698e-fec6-491a-b229-17fd7cec75b1.png)  
- random한 mask를 image에 곱하여 perturbation을 더함
- Mask와 confidence score를 weighted sum해서 saliency map을 만듦
- 단점 : 약 8000개의 masked iamge가 필요, 랜덤한 마스크를 사용하기 때문에 수행시 마다 결과가 달라짐

<br> 

### 5. Usage (모델의 복잡성)
![image](https://user-images.githubusercontent.com/92671224/159261300-e58d3b8b-181b-4860-aaa9-e22a2dcb328f.png)![image](https://user-images.githubusercontent.com/92671224/159261343-3265ae6e-32c7-4fe2-8d58-3bbbd8cb3a51.png)  
![image](https://user-images.githubusercontent.com/92671224/159261528-3908f19a-8df4-4cc4-be26-baf25b144bba.png)  

<br>

### 6. Evaluation
#### 1) System Causability Scale (SCS)
![image](https://user-images.githubusercontent.com/92671224/159261903-522fdba2-2bb8-4aa0-ae49-8c24eca920be.png)  
- XAI에서 가장 중요한 요소 10개를 정함
- 사람이 각 요소마다 점수를 부여 (1~5)

<br>

#### 2) Benchmarking Attribution Methods (BAM)

- Model contrast scores
![image](https://user-images.githubusercontent.com/92671224/159262516-ef887d0c-3472-4c3c-b75b-520437317add.png)

- Input dependency rate
![image](https://user-images.githubusercontent.com/92671224/159262589-dfa4a868-ece5-456a-8f3f-c9bacc9ebda4.png)

- Input independence rate
![image](https://user-images.githubusercontent.com/92671224/159262611-7d984b19-eac7-442a-af40-e1d86fb627b8.png)

<br>

#### 3) etc
- Faithfulness and Monotonicity
  - Faithfulness : importance score와 성능에 각 feature가 성능에 주는 영향의 상관관계 계산
  - Monotonicity : feature importance에 따라 모델에 feature를 점진적으로 더하면서 feature가 성능에 주는 영향을 계산
- Human-grounded Evaluation Benchmark
  - 전문가보다는 일반인이 평가하게 함

<br>

### 7. Limitation
![image](https://user-images.githubusercontent.com/92671224/159245476-e3e36327-7274-438d-be3e-9245a6630610.png)
- 사람이 explanation map을 추론하기가 어려움
  - 사람이 보기에는 어떤 것이 옳게 설명된 것인지 알기 어려움
- 정량적 평가를 하기 어려움
  - 어떤 부분이 판단에 기여한 것인지 알 수는 있으나, 정량적으로 얼마나 기여한 것인지는 알기 어려움

<br>

#### 참조
https://kangbk0120.github.io/articles/2018-02/cam  
https://towardsdatascience.com/practical-guide-for-visualizing-cnns-using-saliency-maps-4d1c2e13aeca  
https://realblack0.github.io/2020/04/27/explainable-ai.html  
https://www.cognex.com/ko-kr/blogs/deep-learning/research/overview-interpretable-machine-learning-2-interpreting-deep-learning-models-image-recognition  
