## Binary classification
spam detection : Spam or Ham?  
facebook feed : show or hide? ...  

in logic : 0 or 1  --> 이런 경우에 linear hypothesis를 그대로 쓰기는 무리가 있음  

## Logistic Hypothesis
![image](https://user-images.githubusercontent.com/92671224/148327974-88ebf65f-363f-494a-900f-fdcd6c37d8b6.png)  
--> 얘를 0과 1사이의 값으로 압축해주는 함수가 있으면 좋겠다~  
--> Sigmoid  
![image](https://user-images.githubusercontent.com/92671224/148328057-a270c6b8-8c80-4d99-a815-0a25c0e5effc.png)  
  
<img src="https://user-images.githubusercontent.com/92671224/148330147-f33df9c6-0e57-4a74-a261-ae1583ecbedd.png" width=50% height=50%/>


![image](https://user-images.githubusercontent.com/92671224/148328158-06339928-6bbc-4cae-ac2f-df200aa3a8fa.png)


## Cost function
![image](https://user-images.githubusercontent.com/92671224/148328301-6c45780a-7f6c-475e-ae21-276cc2400390.png)   
**Problem**   
기존의 cost function사용 시에 구불구불해짐 --> Gradient descent 사용 불가능.  
어디서 시작하느냐에 따라 값이 달라질 수 있음.  


## Cost function for logistic  
![image](https://user-images.githubusercontent.com/92671224/148329030-cdb9d810-7c42-4f40-a927-0041c6d7ba0e.png)  

exponential이 구부러짐을 유발하는데 e와 상극인것이 log

**y=1**  
![image](https://user-images.githubusercontent.com/92671224/148330558-71cba25d-2339-44de-b408-80a65980a22f.png)  
H(x) = 1 --> cost = 0  correct!!!  
H(x) = 0 --> cost = infinite  (system에 틀린 것에 대한 벌을 주는 것)

**y=0**
![image](https://user-images.githubusercontent.com/92671224/148330708-64ca315b-c37f-4771-bdb7-06e6a682d486.png)  
H(x) = 1 --> cost = infinite  
H(x) = 0 --> cost = 0  correnct!!!  

--> 그래프가 매끈하므로 Gradient descent 사용 가능  

if condition이 있으면 코딩에 있어서 복잡함.  
![image](https://user-images.githubusercontent.com/92671224/148331030-251ef32a-829c-402c-9dc7-7fd4864752a1.png)  
![image](https://user-images.githubusercontent.com/92671224/148331217-c8cd1b2a-10f3-4148-a3a5-93d39b89a9e9.png)  







