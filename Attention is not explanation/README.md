# Attention is not explanation (2019)

## Motivation
<img src = "https://github.com/Hyo1Woo/DL_learning/assets/92671224/a0e1eb0d-dc4a-4eb3-abad-c4778b457565" width=70% height=70%>  

- NLP 분야의 많은 논문에서 Attention mechanism이 사용되고 있다.
- 그와 함께 Attention이 모델에 대한 설명력을 가지고 있다고 선전되고 있다.
- 그러나 이에 대한 반례들이 있음을 확인한다.

  ![image](https://github.com/Hyo1Woo/DL_learning/assets/92671224/0eb4e907-11db-4135-8d34-6d0c178a22e1)

<br>
<br>

## Assume 
Attention이 정말 설명력을 가지고 있다면...
1. Attention weight가 기존의 feature based measure들과 상관관계가 있어야한다.
2. Attention weight가 변경되었을 때, output에서 유의미한 차이가 있어야한다. (반대로 얘기하자면, 같은 output을 내는 다른 Attention이 있어서는 안된다.)

<br>
<br>

## Experiment
- Model: Bi-LSTM, CNN, Average(linear)
- Data
  ![image](https://github.com/Hyo1Woo/DL_learning/assets/92671224/6feeabf4-bf34-497c-b7b3-f76f9473bfc2)

<br>
<br>

## Statistical terms
- Kendal tau   
  <img src = "https://github.com/Hyo1Woo/DL_learning/assets/92671224/f2a06da2-0aa2-4d01-a87c-63d888b288ac" width=50% height=50%>

- TVD
  - 두 분포의 가능한 측정 값들 중 차이가 가장 큰 값
  - output의 차이를 보기 위해 사용
 
- JSD
  - KL-Divergence의 확장버전
  - 두 분포가 얼마나 비슷한지를 나타냄
  - 0에 가까울수록 두 분포는 같음

- gradient based & LOO   
  ![image](https://github.com/Hyo1Woo/DL_learning/assets/92671224/b2d7c221-c33f-4acd-a520-f38d8706774d)


<br>

## 1. Attention weight가 기존의 feature based measure들과 상관관계가 있는가?

![image](https://github.com/Hyo1Woo/DL_learning/assets/92671224/3cfb302a-ade0-4294-9d10-295e3009c525)

<br>

![image](https://github.com/Hyo1Woo/DL_learning/assets/92671224/e260caaa-cfcb-4e56-9c12-7b54f7c2d11f)

<br>

![image](https://github.com/Hyo1Woo/DL_learning/assets/92671224/09b2678e-4361-4d90-97ad-31eda3a6b29f)

<br>

![image](https://github.com/Hyo1Woo/DL_learning/assets/92671224/79ea2a3e-c42c-4981-80ec-c98dbbb634fe)

<br>

![image](https://github.com/Hyo1Woo/DL_learning/assets/92671224/17411d8b-72fa-44c1-9562-5ad4b39ecff6)

<br>
<br>

## 2. Attention weight가 변경되었을 때, output에서 유의미한 차이가 있는가?

### Permutation
- Attention의 분포를 Permutation으로 변경한 후 output의 분포가 얼마나 달라지는지 관찰
![image](https://github.com/Hyo1Woo/DL_learning/assets/92671224/ed6c0752-f603-4f01-8eef-969a9bb865a2)

<br>
<br>

### Adversarial
- Output은 같지만, Attention의 분포는 다른 model을 탐색
- 다른 parameter들은 고정   

![image](https://github.com/Hyo1Woo/DL_learning/assets/92671224/a94bf372-0039-4804-8a6d-eb89d45d9ffd)

<br>

![image](https://github.com/Hyo1Woo/DL_learning/assets/92671224/bd37ddb1-8363-4ee4-84f9-ac0af65cd39e)

<br>
<br>

## Conclusion
- Attention weight와 기존의 feature based measure들과의 상관성이 있다고 보기 어려움
- Attention weight의 변동과 output의 차이에서도 유의미한 차이를 보기 어려움
- Attention을 모델의 설명력에 대한 뒷받침으로 사용하기에는 무리가 있음 

<br>
<br>

## 개인적인 의견
- 과연 feature based measure와 비교하는 것이 의미있는 비교일까?
- Output은 같지만, Attention의 분포는 다른 경우를 잘 살펴보면 설명력이 있는 것을 확인할 수 있지 않을까?
