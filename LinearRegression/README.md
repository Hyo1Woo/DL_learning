## (Linear) Hypothesis  

어떤 선이 데이터에 잘 맞는지 찾는 것  

H(x) = Wx + b --> W와 b에 따라 선이 달라질 것  

--> 데이터를 잘 설명하는 W와 b를 찾는 것


## Cost function (Loss function)

제일 기본 적인 것은 H(x) - y 차이를 계산하는 것   

--> 별로 안좋음, 양수도 음수도 될 수 있어서.  

--> 차이를 제곱해서 평균내주는 방법을 취함  

![image](https://user-images.githubusercontent.com/92671224/148325984-8f132cc4-0cd2-41c0-aa18-e643f8fee46f.png)

이걸 최소화하는 W와 b를 구하는 것이 목적인 것  

## Q. 최소화하는 지점을 어떻게 찾을 것인가
### Gradient descent algorithm

![image](https://user-images.githubusercontent.com/92671224/148326216-fee997f2-36c0-46c9-92bc-1b649c3f8dbf.png)

기울기를 따라가서 결국 기울기가 0인 지점에 도달하게 함.  
단, Convex function = 극솟값이 1개인 경우에만 최솟값에 안정적으로 도달 가능

