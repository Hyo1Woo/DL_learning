# Deep Residual Learning for Image Recognition (2015)

## Introdution
visual recognition 분야에서 very deep model은 많은 이점이 있다.

### 그렇다면, layer를 쌓을수록 학습이 더 잘되는가?

아니다. 여러 장애물이 존재하는데, 

대표적으로 vanishing gradient문제가 있다. 하지만 vanishing gradient의 경우 

Batch normalize와 initialization으로 어느정도 문제가 해결되었다.

<br>

논문에서는 새로운 **degradation problem**을 제기한다.

- 모델이 deep해질수록 성능이 더 좋아지는 것이 직관적
- but accuracy가 saturation되면서 layer의 개수가 증가하더라도 모델의 성능이 더 이상 증가하지 않고 오히려 감소하는 문제

<br>

![image](https://user-images.githubusercontent.com/92671224/168707323-d88f885b-9914-4047-9478-421bce99b79e.png)

- 이러한 degradation은 깊은 모델이 쉽게 최적화되지 않음을 보여준다.

<br>

본 논문은 이 문제에 대하여 두 가지 목표를 가지고 문제를 해결한다.   

**1. 최적화(학습)가 더 쉽게 되도록**   
**2. accuracy 향상**   

<br>

위 두 목표를 위해 새로운 model architecture를 제시한다.

<br>

## Deep Residual Learning
### Residual 
- 뜻: 나머지

![image](https://user-images.githubusercontent.com/92671224/168708197-5f24f1a4-daf1-44dc-be8a-0cdb79bf9bcc.png)

- 기존의 cnn구조에서는 이전의 것이 다음으로 전달되어 영향을 미치게 됨   

- 그런데 앞선 부분의 feature가 뒤쪽까지 직접 영향을 끼치는 것이 아니라   

- 중간을 거쳐서 전달되기 때문에 학습의 과정에서 feature가 많이 변하게 됨   

- **(학습해야할 것이 많다 = 최적화가 쉽지 않다)**   

<br>

### shortcut connection 추가
![image](https://user-images.githubusercontent.com/92671224/168707612-84c2cbe1-9c43-474d-b8cf-9cbc433d4e61.png)

- 이전으로부터 얼만큼 변하는지 나머지(residual)만 계산하는 문제로 바뀌게 됨   
- 따라서 학습과정에서 그 '조금'을 하면 되는 것이고 최적화를 더 쉽게(빠르게) 할 수 있게 됨. [참고](https://lv99.tistory.com/25)   

<br>

### Shortcut connection   
**1. Identity Mapping**    
   ![image](https://user-images.githubusercontent.com/92671224/168710391-fcd66694-d0b8-4001-8a1d-b82fb931c0a1.png)   

<br>

**2. Projection**         
   ![image](https://user-images.githubusercontent.com/92671224/168710421-10f218a3-84da-4827-8204-b5896da1a1f6.png)   


#### 결론
- 2의 방법은 연산량을 증가시키므로, 목표(최적화)와 맞지 않음   
- 따라서 기본적으로 1번의 방법을 채택   

<br>

## Network Architectures
![res](https://user-images.githubusercontent.com/92671224/168711527-dbd9d7bc-24aa-4727-99f5-0b5aa286e5e0.PNG)   

<br>

## Bottleneck Architecture
<img src='https://user-images.githubusercontent.com/92671224/168716875-b31de0f7-6a0a-471c-982d-031fb1dec914.png' width=50% height=50%>   

- 복잡도에서는 유사
- 연산량 절감

<br>

## Implementation
- Batch normalization 적용
- Batch size : 256
- Iteration : 600,000
- Learning Rate: 0.0001
- Drop-out 미적용

<br>

## Experiments
### 실험 모델
![image](https://user-images.githubusercontent.com/92671224/168712890-02910154-98e8-41dc-9f5d-82b94157c335.png)  

<br>

### Training on ImageNet
![image](https://user-images.githubusercontent.com/92671224/168712954-4663c343-d7ca-484e-93e9-aa80039c81a7.png)  

<br>

### Validation on ImageNet
![image](https://user-images.githubusercontent.com/92671224/168713103-fbcc8e40-682b-48c8-bd89-de5725428934.png)

<br>

### Error Rates on ImageNet
![image](https://user-images.githubusercontent.com/92671224/168713408-85c53478-472f-4395-af42-1106f710c4fb.png)

**A. identity mapping :** zero padding   
**B. Projection:** 1x1 convolution을 차원이 증가하는 shortcut에만 적용   
**C.** 모든 shortcut에 B를 적용   

<br>

### Comparision with SOTA (Ensembles Model)
![image](https://user-images.githubusercontent.com/92671224/168714856-1f137451-ea6d-42a1-8806-d806fe5b33c7.png)

<br>

### Test on CIFAR-10
![image](https://user-images.githubusercontent.com/92671224/168715129-f1dd1cf2-eeec-4b25-8dcf-a1b316603661.png)

<br>

### Training on CIFAR-10
![image](https://user-images.githubusercontent.com/92671224/168715406-fc880c12-63a2-40ff-adea-f446bd1cc658.png)

<br>

### Analysis of Layer Response
![image](https://user-images.githubusercontent.com/92671224/168715470-9a53c132-47cb-467f-a196-cffa461e2c43.png)   

**std**: 평균을 기준으로 할 때 **얼마나 기복이 있는지**를 나타내는 것


<br>

## Contribution
- residual representation이나 shortcut connection이 image recognition분야에서 없었던 것은 아님   
- 그러나, 두 개념을 동시에 가져가면서 deep model에 대한 성능향상과 최적화문제를 해결한 것에 큰 기여   








