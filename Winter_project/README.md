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

<br>

### 220207 중간발표   
 **Model selection**   
 - X-ray image augmentation에 적합한 Gan model 선정   
 - non-paired image   
 - non-conditional Gan   

 <br>

 **DCGAN**   
 - generator와 discriminator에 CNN을 적용   
 - 기존의 학습에 불안정한 부분을 해결 > 대부분의 상황에서 안정적인 학습 가능   
 - BLACK BOX   
  ![image](https://user-images.githubusercontent.com/92671224/152782717-0237daa2-eabb-4db8-afc1-fe4339863293.png)   

 - Discriminator에 학습을 시킨 결과, 필터에서 침대나 창문같이 침실의 특정 부분에서 활성화 되는 필터들을 발견   
 - X-ray 이미지에서 어떤 부분을 보고 이런 이미지를 만들어 냈는지에 대해 확인할 수 있을 것으로 기대 (잘 될지는 모르겠음)   

 <br>

 **현재진행**   
 - DCGAN pytorch tutorial 코드 이해   
 https://pytorch.org/tutorials/beginner/dcgan_faces_tutorial.html   
 
 <br>
 
 **Future plan**   
 - 모델 구현 및 augmentation한 X-ray image 생성   
 
 <br>
 
 **논의점**   
 - GAN이라는 model 자체가 많은 학습데이터가 있어야 유의미한 data를 뽑을 수 있음   
 - 과연 GAN augmentation이 실제 사용할만한 가치가 있는지 의문   
 - 하지만 일단 계속해서 진행할 예정   

<br>

### 220214 중간발표   
![image](https://user-images.githubusercontent.com/92671224/153860175-992bae10-c6cd-469f-ad0e-0d06f175e3eb.png)   

![image](https://user-images.githubusercontent.com/92671224/153860205-3c6fcaf2-9215-4f35-887d-4a96baa73994.png)   

<br>

### 220228 최종발표
 - DCGAN 모델 구현   
    - 학습이 제대로 되지 않는 문제가 발생   
    - learning rate, Ganerator와 Discriminator의 학습횟수를 조정   
<img src = "https://user-images.githubusercontent.com/92671224/155977938-9edd29af-bb1b-40d5-8048-406f0748f4e5.png" width = 50% height = 50%>
<img src = "https://user-images.githubusercontent.com/92671224/155978177-fca009ec-8365-4739-9a4f-16ba7fca5d1f.png" width = 50% height = 50%>

<br>

 - CNN 모델 구현
    - Convolution layer 2개, Linear layer 2개
    - input size = 64x64
    - augmentation 이전 정확도 : 64.89%

<br>

- train
   - normal 400개
   - pneumonia 300개 + **gan augmentation 100개**

- test
   - normal 204개
   - pneumonia 360개
