## BERT: Pre-training of Deep Bidirectional Transformers for Language Understanding (2019)
##### Appendix와 Ablation Study는 발표에서 주내용으로 다루지 않음
##### 논문과 chatgpt만으로 학습하였음

<br>

### Abstract
- Transformer의 encoder를 기반으로 하고 있는 모델
- Bidirectional model >> 양방향 학습이 가능
- Pretrain된 model이 있는 경우 각각의 task에 대해 새로 학습하거나 모델구조를 전반적으로 바꾸거나 하지않음
- task에 맞는 하나의 추가 output layer만 필요
- Pretrained model에서 각 task 마다 fine-tunning을 진행
- 11개의 평가 task에서 SOTA(State-of-the-art) 달성

<br>

### 평가지표
#### GLUE
- 9개의 task에 대해서 평가한 avg지표
- 다양한 NLP task에 robust한지 확인 가능
- 감정분석(classification, regression)
- 두 문장의 유사성(classification)
- 두 질문이 동일한지(cls)
- 두 문장의 관계파악(cls: 모순, 함의, 중립)
- 대명사 참조

#### SQuAD
- Question Answering
- 질문을 통해 올바른 답변을 하는지

<br>

### Pretrain? Fine-tunned?
#### Pretrain (다양하고 많은 경험 혹은 지식)
- 대량의 dataset(특정task에 국한되지 않은)을 통해서 사전에 학습을 진행함
- dataset 자체가 양이 많기 때문에 학습을 하는데 computing power가 많이 소모됨
- 수 일 혹은 수 주까지도 학습을 하기도 함
- 이렇게 학습된 데이터를 가져다 쓰는 것을 Transfer learning이라고도 함

#### Fine-tunned (특정 분야에 대한 경험 혹은 지식)
- Pretraining된 model을 내가 원하는 task에 맞게 추가학습을 시키는 것을 뜻함
- 단어 그대로를 풀어보자면 '미세조정' 정도라고 볼 수 있음
- 이미 대량의 dataset에서 pretrain된 model을 추가학습하기 때문에 많은 computing power가 필요없음
- 실제 BERT에서도 fine-tunning시 3-5epoch 정도만 진행함 (1시간에서 수 시간)

##### >> 여러 학문을 섭렵해본 사람이 특정 분야를 공부할 때 쉽게 하는 것과 같은 이치

<br>

### Related Work
![image](https://user-images.githubusercontent.com/92671224/220243376-bcf8173d-d5ce-47f8-8732-312ff312554d.png)

<br>

#### ELMo
- 당시 sota를 달성했던 word embeding 기법
- ELMo 논문에서 여러 task들에 대한 성능을 평가하기 위해 Bi-LSTM을 사용함 >> 양방향 학습이 가능
- 한계가 있다면, 각 task마다 모델구조도 달라지고(참조하는 baseline code가 모두 다름) 각 LSTM이 left to right 과 right to left를 따로 학습하는 방식

#### GPT
- Transformer의 decoder를 사용
- left to right language model (masked)

<br>

### Architecture
![image](https://user-images.githubusercontent.com/92671224/220242314-f916f738-f276-417a-9f1a-a9e301ce88a5.png)

<br>

- token
    - [CLS]
    - [SEP]
    - [MASK]
- pre-train
    - Masked LM
    - NSP (classification)

<br>

![image](https://user-images.githubusercontent.com/92671224/220242860-bf33d5d1-c242-487e-92ac-925cfaa11af7.png)

<br>

- pretrained data
    - BookCorpus (800,000,000 words)
    - Wikipedia (2,500,000,000 words)
- input
    - token + segment + position
- fine-tunning

![image](https://user-images.githubusercontent.com/92671224/220243510-08056272-8f35-40cd-8071-ab3542e5b443.png)

<br>

### Result
![image](https://user-images.githubusercontent.com/92671224/220243673-03793ded-aa7a-4eba-80f5-c768363d1ab0.png)

<br>

![image](https://user-images.githubusercontent.com/92671224/220243868-ea750139-b2e4-4811-940a-706b9d6c6fe7.png)
