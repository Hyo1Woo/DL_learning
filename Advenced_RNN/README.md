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
