## Advanced RNN (LSTM, GRU)
##### LSTM의 경우 논문을 읽으려 시도하였으나 차마 다 읽지 못하고 어지러움을 호소함
##### 아래의 유튜브와 블로그를 적극 참고하였음
 - [딥러닝 홀로서기](https://www.youtube.com/watch?v=cs3tSnAsyRs&list=WL&index=14&ab_channel=IdeaFactoryKAIST)
 - [colah's blog](https://colah.github.io/posts/2015-08-Understanding-LSTMs/)
 - [ratsgo's blog](https://ratsgo.github.io/deep%20learning/2017/10/10/RNNsty/)

<br>

## Vanishing Gradient
### RNN Archtecture
<img src = "https://user-images.githubusercontent.com/92671224/196660870-567305ff-7b5b-4746-b590-67441ca48124.png" width=50% height=50%>

"나는 **프랑스에서 자랐다**. 나는 **프랑스어**에 유창하다"

<br>

<img src = "https://user-images.githubusercontent.com/92671224/196661450-c868e3ae-2d82-4160-96f5-f556dcc8d7ce.png" width=50% height=50%>

"나는 **프랑스에서 자랐다**. 프랑스의 작은 동네에서...... 그래서 나는 **프랑스어**에 유창하다"

<br>

### Mathmatically
<img src = "https://user-images.githubusercontent.com/92671224/196837695-2628585f-998e-4560-b613-ff11f4ea0b52.png" width=50% height=50%>   

![image](https://user-images.githubusercontent.com/92671224/196837758-678d8c92-0869-4211-aec9-70c4d109668e.png)   

- Sequence가 길어질수록 tanh연산이 점점 많아질 것

<br>

<img src = "https://user-images.githubusercontent.com/92671224/196838473-0a7081dc-65b6-4fc3-8c0a-f7de0bf4d060.png" width=50% height=50%>

- tanh의 미분값의 범위가 [0,1]이므로 연산을 거듭할 수록 앞단에 전달되는 미분값이 감소할 것

<br>

![image](https://user-images.githubusercontent.com/92671224/196838233-a5924678-1396-4aaa-b448-72e9e1ad0727.png)

![image](https://user-images.githubusercontent.com/92671224/196839098-ed13484e-d1bc-4b2c-a97a-d77f97330db8.png)

![image](https://user-images.githubusercontent.com/92671224/196839257-6720c699-bfa2-4459-8aa6-37b85de61afa.png)

- Sequence의 길이만큼 Whh가 곱해질 것
- Whh가 1보다 작은 값이면 그래디언트가 소실될 것이고
- Whh가 1보다 큰 값이면 기울기 폭발이 일어나 NaN값이 전달될 것임

<br>

## LSTM
### Architecture
<img src = "https://user-images.githubusercontent.com/92671224/196839712-f5440607-8c12-4ae6-bdb7-20d433a04511.png" width=80% height=80%>

- 기존의 RNN에서 Cell state를 추가함
- Cell state를 통해 이전 정보를 전달함
- 기억할 것과 잊을 것을 결정하여 현재의 hidden layer에 전달
- 즉 중요한 정보만 Cell state를 통해 계속 전달되도록 함

##### 어떻게 기억하고 잊을거냐?
- Gate

<br>

### Gate가 어떻게 값을 기억하게, 잊게 하는거냐?
<img src = "https://user-images.githubusercontent.com/92671224/196840762-18abb472-c1a0-467b-8047-861c58812edd.png" width=50% height=50%>

##### 그럼 중요한 값인지 아닌지를 어떻게 결정함?
- 각각의 게이트에 non-linear layer를 넣어서 인공지능 알아서 결정하게 함

<br>

### Mathmatically
#### 1. Ct-1에서 불필요한 정보를 지운다
<img src = "https://user-images.githubusercontent.com/92671224/196841495-bb44c3ee-903a-4467-851c-f3f19d550fe4.png" width=70% height=70%>

<br>

#### 2. Input xt와 ht-1을 보고 중요한 정보를 넣는다
<img src = "https://user-images.githubusercontent.com/92671224/196841794-14be0e89-6b42-4320-9a3f-08ad42717c94.png" width=70% height=70%>

<br>

#### 3. Ct-1의 일부 정보를 날리고 현재 정보를 추가한다
<img src = "https://user-images.githubusercontent.com/92671224/196842028-92577206-60af-462e-a289-08f76daa9b57.png" width=70% height=70%>

<br>

#### 4. Ct를 적절히 가공해 해당 t에서의 ht를 만든다
<img src = "https://user-images.githubusercontent.com/92671224/196842282-6eeccc01-cd97-4b39-9a91-c7b5e9343a37.png" width=70% height=70%>

<br>

#### 5. Ct와 ht를 다음 스텝 t+1로 전달한다

<br>

#### Q. 어떻게 기울기 소실 문제를 극복할 수 있는건가? 
1. Activation Fuction(tanh)을 거치지 않고 흘러오기 때문에 상당부분 해결
2. [Gradient 계산](https://medium.datadriveninvestor.com/how-do-lstm-networks-solve-the-problem-of-vanishing-gradients-a6784971a577)

<br>

#### Q. 너무 중복되는 느낌이 든다. 더 간단하게 할 수는 없을까?
## GRU
- LSTM의 cell state를 삭제
- 이전 스텝에서 전달되는 값이 1개로 간소화

<br>

<img src = "https://user-images.githubusercontent.com/92671224/196844515-0dd4972a-3d4c-42ec-a341-c57e8c75cd51.png" width=70% height=70%>

1. Reset gate를 통해 임시 ht를 만든다
2. Update gate를 통해 ht-1과 ht간의 비중을 결정한다
3. zt를 이용해 최종 ht를 계산한다

<br>

#### Q. 그래서 뭐 써야됨?
- 둘 간의 성능차이는 크지 않은 것으로 확인됨
- 하드웨어 성능이 증가함에 따라 파라미터 수가 많은 것이 큰 단점이 아니게 됨
  + 오히려 파라미터가 많으니 더 많은 정보를 수용할 수 있지 않겠냐는 관점도 있음
