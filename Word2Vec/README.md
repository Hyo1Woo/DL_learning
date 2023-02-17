## Efficient Estimation of Word Representations in Vector Space (2013)
##### 매우 다양한 youtube와 블로그를 참조하였음
##### 수식은 최소화하고 직관적인 설명 위주로 진행(사실 수식 이해 못함) 

<br>

### Abstract
- 매우 큰 dataset에서 단어의 vector 표현을 위한 두 가지 모델 제안
- 단어 사이의 유사도 측정을 통해 vector 표현이 얼마나 잘 되었는지를 확인할 수 있음
- 이전 기술(NNLM)에 비해 학습시간 단축

<br>

### 1 Introduction
- 이전 기술에 대한 설명
- 기본적으로 sparse representation 이었다. 예를들어 one-hot-encoding의 경우 [0,0,0,0,1,0,0,0,0]와 같이 data를 가지고 있는 곳이 sparse(희소)하다. 
- 이는 효율적이지도 않고 NN에 학습될 때에도 많은 웨이트들을 무시하게 된다. 
- 본 논문에서 제시하고 가장 큰 문제점은 단어간의 유사도를 고려할 수 없다는 것에 있다.

<br>

#### 1.1 Goals of the Paper
- 유사한 의미의 단어가 서로 유사한 vector를 가지도록 하겠다.
- "car"와 "automobile"이 동의어라거나 "king"과 "prince"가 유사어인 것과 같은 단순한 예시를 넘어서 
- vector("King")-vector("Man")+vector("Woman")=vector("Queen")의 결과를 내기도 한다.
- 문법적, 의미적 특성을 잘 측정할 수 있는 test dataset을 설계해서 높은 정확도로 학습

<br>

#### 1.2 Previous Work
![image](https://user-images.githubusercontent.com/92671224/219515531-9d6f1644-d21e-4904-8224-e90179f3b15e.png)
- NNLM vs Word2Vec
- 구조적인 차이도 있고, 목적자체가 다르다.
- 활성화함수를 제거했고, Hidden layer도 없다.
- NNLM은 다음 단어를 예측하기 위해 제안된 반면, Word2vec은 워드 임베딩만을 위해 제안되었다.
- 모델의 구조도, 목적도 단순해진만큼 학습에 있어서도 훨씬 효율적이다.

<br>

### 2 Model Architectures
- 이전 모델에서의 모델복잡도 (NNLM, RNNLM ...)
- 모델의 복잡도는 대부분 비선형함수에 의해 발생함
- 비선형함수가 포함된 NN모델들보다 정확하게 데이터를 표현할 수는 없지만 훨씬 더 많은 데이터를 효율적으로 훈련할 수 있다.

<br>

### 3 New Log-Linear Models
- "학습을 위한" 두 개의 모델을 제안함

<br>

#### Continuous Bag-of-Words Model(CBOW)
![image](https://user-images.githubusercontent.com/92671224/219517995-16644930-b91f-48a0-9028-1304a079d4c6.png)
- 예문 : "The fat cat sat on the mat"
- 주변단어를 통해 중심단어를 예측(표현)
- projection시에 차원마다 평균을 냄

<br>

#### Continous Skip-gram Model
- CBOW와 유사함
- 중심단어를 통해 주변단어를 예측(표현)
- 주변단어와의 거리가 멀어지면 그만큼 적은 weight를 부과함
- 당연한 얘기지만 예측하고자하는 주변단어의 개수가 많아질수록 모델복잡도 증가

<img width="516" alt="스크린샷 2023-02-17 오전 9 30 00" src="https://user-images.githubusercontent.com/92671224/219519035-6a6c1a27-2886-45ab-bcb1-0c7125d93649.png">

<br>

### 4 Result
- 이전 언어모델들은 가장 유사한 단어를 단어 테이블에서 보여주는 방식을 채택함
- 하지만 단어 사이에는 더 복잡하고 다양한 유사성이 존재
- 우리는 "big-biggest" 와 "small-smallest" 사이의 유사성도 보여줄 수 있다.
- X = vector("biggest") - vector("big") + vector("small") 을 찾고, X와 가장 유사한 단어를 찾으면 vector("smallest")를 찾을 수 있다.
- 굉장히 미묘한 의미를 담고 있는 국가와 도시(한국, 서울) 사이에서도 관계성을 발견할 수 있었음.

<br>

#### 4.1 Test Dataset
<img width="539" alt="스크린샷 2023-02-17 오전 9 49 30" src="https://user-images.githubusercontent.com/92671224/219521307-099d5c68-fe99-4ace-8179-5ec44301bcdc.png">

- 단어간의 문법적(8869), 의미적(10675) 관계를 갖는 질문들을 구성

<br>

#### 4.2 Result tabel

<img width="543" alt="스크린샷 2023-02-17 오전 9 53 36" src="https://user-images.githubusercontent.com/92671224/219521851-944968dc-ee1c-4cd5-bf01-cefd49f402b0.png">


<img width="564" alt="스크린샷 2023-02-17 오전 9 55 50" src="https://user-images.githubusercontent.com/92671224/219522193-a59a0acd-2a59-4d8b-b977-96f8fa8fc9de.png">


<img width="547" alt="스크린샷 2023-02-17 오전 9 56 07" src="https://user-images.githubusercontent.com/92671224/219522204-fce3fdfc-1154-4aa0-bdd2-bb0fa966d0a9.png">


<img width="539" alt="스크린샷 2023-02-17 오전 9 56 29" src="https://user-images.githubusercontent.com/92671224/219522226-6262caa0-4cf8-46a7-8b49-640181e9a901.png">
