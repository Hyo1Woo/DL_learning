## Attention Is All You Need (2017)
##### 수 많은 유튜브영상과 블로그를 참고하였음
##### 수식보다는 직관적인 설명을 위주로 준비 (사실 수식 이해 못함)

### Abstract
- Recurrent와 Convolution을 사용하지 않음
- 대신 Attention Machanism을 사용
- 병렬화 가능
- 영어-독일어, 영어-프랑스 번역 작업에서 우수한 성능
- 다른 작업에 일반화도 잘 됨

<br>

### 1 Introduction
- Recurrent model은 입력 및 출력 sequence의 위치에 따라서 결과를 도출함. 따라서 훈련 시, 병렬화가 불가함
- Attention Machanism은 sequence의 위치와 관계없이 모델링이 가능함. 입력 sequence 전체가 input으로 한 번에 들어가고, 각각 단어의 유사도를 한번에 계산하기 때문.
- 보통은 RNN과 함께 사용되었으나 해당 논문에서는 Attention만을 사용한 Transformer를 제시

<br>

### 2 Background
- CNN이나 RNN은 멀리 떨어진 위치 간의 관계를 학습하는 것이 어려움. Transformer에서는 이를 해결 (Self-attention)

<br>

### 3 Model Archtecture

<img width="328" alt="스크린샷 2023-02-17 오전 11 37 54" src="https://user-images.githubusercontent.com/92671224/219535545-63a053cf-2904-47f9-a706-f56d7a0c1963.png">

<br>

#### Embeding
- 기본적으로 512차원으로 Embeding

<br>

#### Positional Encoding
- RNN에서는 문장의 단어가 순차적으로 입력되기 때문에 따로 고려할 필요가 없었음 (구조 자체가 seqential함)
- 하지만, transfomer에서는 문장의 sequence가 vector형태로 병렬적으로 입력되기 때문에 순서에 대한 정보를 따로 입력해줘야함

<img width="227" alt="스크린샷 2023-02-17 오후 12 18 56" src="https://user-images.githubusercontent.com/92671224/219541223-b5e14517-d8f9-40b5-bc2c-1bf4f3cfa219.png">
<img width="610" alt="스크린샷 2023-02-17 오후 12 24 50" src="https://user-images.githubusercontent.com/92671224/219541888-05ad4f43-e6b1-4d87-83d9-fda5952b5fe7.png">


- 위치정보가 위 식에 의해 정의되고 Embeding vector에 더해져서 Transformer에 들어감
- 위치정보를 input에 함께 넣음으로써 NN이 위치에 대한 중요도를 자동으로 학습하게 됨 (모델이 위치와 의미 모두를 통괄)

<br>

#### Attention
![image](https://user-images.githubusercontent.com/92671224/219542301-26aaf0e3-b422-4e12-9be9-de2201f440a7.png)

- 번역에 있어 문장의 어순이 바뀌는 경우 Attention(어느 단어에 더 집중할 것인가)을 통해 올바른 번역을 할 수 있음

<br>

#### Self-Attention
- 번역을 예로 들면, 단어를 번역하는데 있어 어디에 더 Attention하겠는가에 대한 것을 번역하는 문장 그 자체에서 학습하겠다는 것

<img width="1125" alt="스크린샷 2023-02-17 오후 12 43 39" src="https://user-images.githubusercontent.com/92671224/219544110-e0bdab8a-c8a4-4c69-bb8c-7933e86f6631.png">

![image](https://user-images.githubusercontent.com/92671224/219544754-1c4ef76c-6d9d-441d-a906-07d54e4fceee.png)

![image](https://user-images.githubusercontent.com/92671224/219544860-e341a9b9-6b3d-46b5-b43c-258a52ca2fd4.png)

<br>

#### Multi-Haed Attention
![image](https://user-images.githubusercontent.com/92671224/219546023-d40d45ed-4d5d-4d6d-9c00-7f63d962da32.png)

![image](https://user-images.githubusercontent.com/92671224/219545849-4554970d-ec69-4fa9-b1e4-b946b2f25ea7.png)

<br>

#### Decoder side
<img width="816" alt="스크린샷 2023-02-17 오후 12 55 58" src="https://user-images.githubusercontent.com/92671224/219545704-e5403a60-8cbb-4512-92dc-af1ddfbb0d18.png">
