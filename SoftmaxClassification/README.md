## Multinomial classification
![image](https://user-images.githubusercontent.com/92671224/148333752-49ec5980-9296-4436-8318-eb6b8cf8825e.png)  

각각 입력을 A or not, B or not, C or not 에 해당하는 classifier에 넣은것임.  

## SOFTMAX  
<img src="https://user-images.githubusercontent.com/92671224/148333902-8436169c-a7a0-4b93-96e6-c3c7e3375a7f.png"  width="50%"  height="50%"/>  

각각의 값들을 확률로서 나타내주는 것이 SOFTMAX

<img src="https://user-images.githubusercontent.com/92671224/148333953-a347487f-4ecf-474b-a76b-81028f11f73b.png"  width="50%"  height="50%"/>  

Hot encoding을 통해서 값 하나를 고르게 되는 것임  
? = argmax 함수


## Cost function  

<img src="https://user-images.githubusercontent.com/92671224/148334807-6430e069-1092-4166-8693-59cc82e8475d.png" width="50%" height="50%"/>

좌측은 예측값(확률), 우측은 실제값  

![image](https://user-images.githubusercontent.com/92671224/148341616-5b3460e5-0e37-40e8-b59a-43fddafe0219.png)  

-log 함수  

![image](https://user-images.githubusercontent.com/92671224/148342330-ba20bb82-9aaf-4bf1-8839-335821a24a89.png)  

logistic cost 와 cross entropy는 같은 것임  

![image](https://user-images.githubusercontent.com/92671224/148343755-19af817c-68bf-4482-ad27-9e02e6cfdacd.png)  


## Gradient descent

![image](https://user-images.githubusercontent.com/92671224/148342646-88461f82-d6a4-45e9-a634-fddc53a07573.png)  

사용가능
