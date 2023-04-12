# Improving Language Understanding by Generative Pre-Training
##### Bert 이전에 openai에서 제시한 논문
##### 본 논문이 처음 제시한 것처럼 말하는 것이 많으나, Bert에서도 유사하게 다 차용하였음.
## Abstract
- pre-training과 fine-tunning을 이용하여 NLP분야에서 다양한 작업에서 높은 성능을 보이는 방법을 제안
- task aware input transformation을 이용하여 모델 구조의 변경을 최소화하면서 전이 학습 효과를 높임
- 다양한 벤치마크에서 각 task별로 따로 만든 모델보다 더 나은 성능을 보임

<br>

## Introduction
- 대부분의 딥 러닝 방법은 수작업으로 라벨링된 대량의 데이터가 필요
- 라벨링되지 않은 텍스트에서 단어 수준 이상의 정보를 활용하는 것은 어려움. 그렇기 때문에 word embeding에서 주로 사용됨
    - Q1. 어떤 목적함수로 unsupervised learning을 진행해야 supervised learning으로 tranfer시킬 때도 효과적인가?
        - A. Unsupervised learning시에 Language Modeling 목적함수를 활용하며 Transformer Decoder 구조를 차용
    - Q2. Fine-tuning input으로는 어떻게 넣는게 가장 효과적인가?
        - A. Fine tuning시에 여러 entity를 그냥 순서대로 넣는다. (ex. [Premise $ Hyphothesis] in entailment task)

![image](https://user-images.githubusercontent.com/92671224/231388613-627692cf-1666-4d00-bdee-694ef290a68c.png)

<br>

## Related Work
### Semi-supervised learning for NLP
- Word-embedding 기반의 semi-supervised learning(pre-training -> fine-tuning)이 효과적임이 이전부터 보여졌음
- 그러나 해당 embedding은 word-level representation 수준인 것이 한계점

### Unsupervised Learning
- unsupervised learning은 supervised learning이전에 좋은 initial point를 찾아주는 작업

### Auxiliary training objectives
- semi-supervised learning의 대안으로 사용되는 방법 중 하나
- 목적함수 자체에 unsupervised 항을 넣어서 학습시키기도 함
- 추가적인 NLP 작업을 모델 학습에 활용하여 성능을 향상시키는 방법 (POS tagging, chunking, named entity recognition...)
- 논문에서는 pre-training 할 때 이미 linguistic aspects relevant가 학습되었다고 보고 있음

<br>

## Framework
### Unsupervised pre-training
1. corpus를 tokenization
2. positional embeding
3. transformer decoder
4. softmax

### Autoregressive
<img width="340" alt="스크린샷 2023-04-12 오후 4 48 07" src="https://user-images.githubusercontent.com/92671224/231389230-7fe6491f-32c9-4648-83d6-e82fdaa690d0.png">
![image](https://user-images.githubusercontent.com/92671224/231387729-de330e6a-2c77-42f8-ab38-2b4f71c8927d.png)

### Supervised fine-tuning
<img width="295" alt="스크린샷 2023-04-12 오후 4 49 33" src="https://user-images.githubusercontent.com/92671224/231389407-7281d022-fad8-4428-a363-38c0ff4df579.png">
<img width="233" alt="스크린샷 2023-04-12 오후 4 50 42" src="https://user-images.githubusercontent.com/92671224/231389673-5fbe9d3e-42ad-4f74-8754-690d12ffd0f2.png">

- fine-tuning시에 pre-traing에서 활동했던 loss를 auxiliary training objectives로 추가해 lambda(λ)로 가중치를 주면서 jointly하게 학습
- supervised model의 generalization, convergence acceleration에 이점

### Task-specific input transformations
<img width="642" alt="스크린샷 2023-04-12 오후 4 53 32" src="https://user-images.githubusercontent.com/92671224/231390374-f10b3319-b6f2-42ba-bd65-21d4b502df06.png">

- Bert와 굉장히 유사
- input transformation과 output layer의 간단한 변경만으로 여러 task에 맞는 학습, 추론 가능

<br>

### 그래서 bert와 차이가 뭔데?
- GPT-1: Transformer 디코더 구조를 사용하여 다음 단어를 예측하고 ***문장을 생성***하는 것에 중점을 둠
- BERT: Transformer 인코더 구조를 사용하여 입력 시퀀스의 모든 단어를 동시에 처리하고, 이를 기반으로 ***문장의 의미***를 파악

<br>

### Zero-shot
- pre-training만으로 여러 task들을 커버하겠다는 것
<img width="643" alt="스크린샷 2023-04-12 오후 5 01 39" src="https://user-images.githubusercontent.com/92671224/231392426-50ba44d0-5c4c-4731-a77f-3e0ea93a2d96.png">
