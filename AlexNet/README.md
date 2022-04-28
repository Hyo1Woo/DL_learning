## ImgageNet ClassiClassification with Deep Convolutional Neural Networks
### 2012 NIPS, ILSVRC2012 winner in classification & detection, ResNet  

<br>

## 0. Abstract
- 학습속도 및 성능 향상 (Section3)
- 오버피팅 감소 (Section4)

<br>

## 1. Introdution
### Imagenet을 사용한 이유
- MNIST와 같은 Task는 적은 데이터로도 human performance에 도달할 수 있음
- 그러나, 실제환경에서 객체를 탐지하는데 있어서는 **훨씬 큰 학습데이터**가 필수적임
- Imagenet은 22,000개의 카테고리 안에 1,500만개의 label된 고해상도 이미지를 가지고 있음

<br>

### CNN을 사용한 이유
- 수천 개의 이미지를 학습하기 위해서는 그저 학습용량을 키우면 됨
- 하지만, ImageNet과 같이 아주 큰 dataset에서는 학습용량을 dataset에 맞게 키우면 복잡도가 과하게 증가함
- CNN은 깊이와 너비를 통해 용량조절이 가능
- Fully-connected에 비해서 같은 layer-size 대비 훨씬 적은 파라미터를 가지고 있음
- 학습이 쉬운 반면 이론적으로 최고성능이 다소 감소할 가능성이 있음

<br>

## 2. The Dataset
### ImageNet
- 실험 자체는 ILSVRC - 2010 버전을 주로 사용
- 일반적으로 Top1, Top5 error rate로 평가함

### Data preprocess
- 기존의 ImageNet: 다양한 해상도의 이미지  
    &rarr; 256x256 으로 downsample  
        1.  width와 height 중 작은 축을 256에 맞게 downsample한다.  
        2.  긴 축은 여전히 256보다 클텐데, 256에 맞게 center crop한다.  
<br>

- 이외에 다른 preprocess는 진행하지 않음  
    &rarr; 가공하지 않은 RGB data를 사용  
    
<br>

## 3. The Architecture
#### 학습속도 및 성능을 향상시킨 주요요소 순으로 설명

<br>

### ReLu Nonlinearity
![image](https://user-images.githubusercontent.com/92671224/165654456-cf0ca569-fda2-4f8b-81d7-1d941fa01fec.png)   

- 기존에 ReLu를 쓰지 않은 것은 아님
- 하지만, 기존에는 오버피팅을 방지하기 위해 ReLu를 사용하였다면
- 저자는 **학습속도 향상**을 위해 ReLu를 사용

<br>

![image](https://user-images.githubusercontent.com/92671224/165654682-c0f95b28-b1a4-4b0d-a3b2-6b1dddfc5afc.png)  
- CIFAR-10, six-time faster

<br>

### Training on Multiple GPUs
![image](https://user-images.githubusercontent.com/92671224/165656963-304bdf43-69eb-43ec-9e82-26634b513ca1.png)  

- 동일한 파라미터 수를 가지는 single GPU 구조와 비교했을 때 
- 성능에서는 top-1: 1.7%, top-5: 1.2% 향상이 있었음
- 학습 속도에 있어서도 slightly less time을 가짐

<br>

### Local Response Normalization
#### Lateral inhibition: 측면억제
![image](https://user-images.githubusercontent.com/92671224/165655844-4480ff6d-05e7-4318-bcc9-3c90ca2c9a4f.png)  

- 실제 뉴런에서 영감을 받은 Normalization 기법  
- 현재는 Batch Normalization으로 대체되어 사용되지 않음  
- top-1: 1.4%, top-5: 1.2% 향상이 있었음  

![image](https://user-images.githubusercontent.com/92671224/165656123-a5e70333-4378-4a2f-8524-6cc4886b5abb.png)  
![image](https://user-images.githubusercontent.com/92671224/165656355-caaf55ee-6dc5-4a2f-b95b-808f9f78d8fa.png)  

<br>

### Overlapping Pooling
<img src = 'https://user-images.githubusercontent.com/92671224/165656521-eeec16eb-29d6-47e7-8fad-b5e761ec15af.png' width=20%, height=50%>  

- 본 모델에서는 stride = 2, kernel size = 3 사용  
- top-1: 0.4%, top-5: 0.3% 향상이 있었음  

<br>

### Overall Architecture
![image](https://user-images.githubusercontent.com/92671224/165657004-86052f24-91ea-4c4c-8500-e80eed25f415.png)  

- 5-conv layer
- 3-FC layer

<br>

## 4. Reducing Overfitting
### Data Augmentation
#### crop and horizontal reflection
<img src = 'https://user-images.githubusercontent.com/92671224/165657844-4769c661-a0f5-4f96-9a6e-9b6766fc03ef.png' width=50%, height=50%>  
- 1 256x256 image &rarr; 10 224x224 cropped image

<br>

#### PCA (주성분 분석, 차원축소)
![image](https://user-images.githubusercontent.com/92671224/165658647-39c954a0-b963-4240-8740-0c0df720b98a.png)   

- top-1: 1% 향상이 있었음 

<br>

### Dropout
![image](https://user-images.githubusercontent.com/92671224/165658789-742e5a39-2e65-4e03-90d3-4a32d52f29b0.png)  

- 뉴런간의 상호적응을 줄임으로서 더 좋은 feature를 학습하게 함
- 다양한 model을 combination하는 효과를 줄 수 있음
- 평가 시에는 모든 뉴런을 활성화함.

<br>

## 5. Details of learning
- batch size: 128
- momentum: 0.9
- learning rate: 0.0005 (최종)
    - 초기값 = 0.01
    - validation error가 더이상 떨어지지 않으면 10으로 나눠줌

<br>

## 6. Result
![image](https://user-images.githubusercontent.com/92671224/165659413-e75324db-cea5-4936-9ccf-7ed60f2a7240.png)  
![image](https://user-images.githubusercontent.com/92671224/165659431-d57e8eac-ab38-4f75-8e05-ccfc41f73fed.png)  

<br>

### Qualitative Evaluation
![image](https://user-images.githubusercontent.com/92671224/165659890-b9a85aed-297f-43d7-8a8e-aa749865583f.png)  
![image](https://user-images.githubusercontent.com/92671224/165659572-9a7f150e-b706-4d1d-b66f-5bf004f7f6d9.png)  
![image](https://user-images.githubusercontent.com/92671224/165659661-d901771a-3c18-4956-a4b6-e7718bf71c79.png)  
