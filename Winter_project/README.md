# Winter Project

## 프로젝트 주제 및 목표  
### 주제
- 폐렴 X-ray image에 대하여 Gan data augmentation을 하였을 때 얼마나 성능의 향상이 있는지를 확인하고자 함  

### 목표
- 다양한 Gan model들을 공부
- Classification accuracy 에 있어서 3% 이상 향상

<br>

## 프로젝트 상세 내용 
### Task
 1. Gan모델을 통해 기존 train data set의 유사 이미지를 생성 (main)
 2. CNN기반 classification 모델을 사용하여 data augmentation 전/후 성능이 얼마나 달라지는지 확인

<br>

### Dataset
 - Chest X-Ray Images (Pneumonia) in Kaggle  
 - https://www.kaggle.com/paultimothymooney/chest-xray-pneumonia/code  
![image](https://user-images.githubusercontent.com/92671224/150946550-51191c17-0403-4b15-b481-887c29851690.png)  

 - **train**   
    normal 1311개  
    pneumonia 3845개  
 - **test**   
    normal 204개  
    pneumonia 360개  
    
    <br>
    
 **논의점** 
  - Gan을 활용한 data augmentation 논문을 보면 train data가 적을 때 성능 상승폭이 큰 것을 볼 수 있음  
  - train data를 전부 사용할 것인지, 일부를 가지고 할 것인지에 대한 논의가 필요함  

<br>

### Model  
 **GAN**  
 - 미정   
 - Gan, cycleGan, pix2pix, pgGan, starGan 등 공부해보고 Task에 가장 알맞는 모델을 채택할 예정  

 **classification**  
 - 간단한 CNN 모델

 **implemetation**  
 - Google Colab  
 - pytorch  

<br>

### Evaluation
 - Gan 모델이 폐렴이미지를 잘 모방했는지에 대한 평가가 어려움
 - 따라서 Classification 모델에 통과 시킨 이후 Accuuracy 변화로 평가하겠음
 - 한계 : 실제 폐렴 데이터를 생성했는지를 직접적으로 알기는 어려움.   
          data augmentation의 효과가 있는지만 확인 가능.
          
<br>

### Milestone  
<img src="https://user-images.githubusercontent.com/92671224/150964739-c9cb1aae-bcc9-402a-b7da-7d48814bc8f0.png"  width=70% height=70%/>
