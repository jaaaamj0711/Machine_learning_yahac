# 학습의 실제
> 강의링크: https://opentutorials.org/course/4570/28977

저번시간에 종속변수에 값에 가장 큰접한 가중치들을 찾아야 한다고 배웠습니다. 그렇다면 가중치를 어떻게 찾는걸까요??  
직접 계산을 해보면서 그 의미를 알아보도록 하겠습니다! 워크북은 강의링크를 들어가면 확인할 수 있습니다.  

|순서|
|------|
|1. 초기값 생성기를 통해 나오는 값을 복사하여 W와 B값을 넣어준다.|
|2. 결과인 W, B 그리고 자동으로 생성되는 Loss 값을 복사하여 history에 넣는다.|
|3. prevLoss 에 Loss 값을 복사하여 넣어준다.|
|4-1. W값을 0.0001을 더한 값으로 고쳐주고 dLoss / dt의 값 변화를 관찰한다.|
|4-2. 결과값 dLoss / dt를 dLoss / dW에 넣어준다.|
|4-3. W값을 원래대로 고친다.|
|5-1. B값을 0.0001을 더한 값으로 고쳐주고 dLoss / dt의 값을 관찰한다.|
|5-2. 결과값 dLoss / dt를 dLoss / dB에 넣어준다.|
|5-3. B값을 원래대로 고친다.|
|6. next W, next B의 값을 복사하여 W, B에 넣어주고 Loss를 확인한다.|
|7. 2번부터 다시 반복한다.|

다음 순서대로 가중치 업데이트가 어떻게 진행되는지 확인하도록 하겠습니다.

![image](https://user-images.githubusercontent.com/55734436/103888781-a3962580-5128-11eb-9936-5904bf66f216.png)

이 상태에서 시작을 하게 됩니다.


### 1. 초기값 생성기를 통해 나오는 값을 복사하여 W와 B값을 넣어준다.
![image](https://user-images.githubusercontent.com/55734436/103888789-a5f87f80-5128-11eb-91d6-60b95af3dcac.png)

여기서 값을 붙일때 수식은 제외하고 값으로만 복사를 해줘야 합니다.


### 2. 결과인 W, B 그리고 자동으로 생성되는 Loss 값을 복사하여 history에 넣는다.
![image](https://user-images.githubusercontent.com/55734436/103888794-a7c24300-5128-11eb-951b-75b51fe14fe4.png)


### 3. prevLoss 에 Loss 값을 복사하여 넣어준다.
![image](https://user-images.githubusercontent.com/55734436/103888803-aabd3380-5128-11eb-8fda-4ac0b5c722c1.png)


### 4-1. W값을 0.0001을 더한 값으로 고쳐주고 dLoss / dt의 값 변화를 관찰한다.
이제 그 다음 W와 b를 찾기 위한 과정입니다. 그 전에 Loss를 다시 생각해 봅시다. 지금 이 상태는 학습이 되기 전에 랜덤하게 찾아진 모델입니다. 이 모델에 의해서 독립변수에 값들을 W곱하고b를 넣어서 예측 결과가 h열입니다.  
이제 W, b를 학습 해보도록 하겠습니다. 

이때 우리에게는 미분이 필요합니다. W가 어떤 방향으로 가야 loss를 작게 할 수 있는지 그 방향을 찾아야 합니다. 이때 우리는 W를 아주 조금씩 키우면서 loss값을 확인하도록 하겠습니다.

우리는 loss를 낮추는게 목표입니다. W를 키웟는데 loss가 작아지면  w를 키워야 하는 것입니다. 

![image](https://user-images.githubusercontent.com/55734436/103888821-b3156e80-5128-11eb-97cb-4d746c2b8e62.png)

loss가 줄어든 것을 확인하였습니다. 즉 W를 키웠을때 loss 값이 작아졌으므로 다음 단계에서는 W값이 커져야 합니다.  

여기서 그냥 값을 키우는 것이 아닙니다. 3번째 행에 있는 dLoss / dt 는 미분값입니다.  W를 조금 키웠을때 loss가 변하는 미분값 그 값의 차이를 미분값으로 나눠준 값입니다.


### 4-2. 결과값 dLoss / dt를 dLoss / dW에 넣어준다.
![image](https://user-images.githubusercontent.com/55734436/103888831-ad1f8d80-5128-11eb-859d-0ebdad4232a5.png)


### 4-3. W값을 원래대로 고친다.
![image](https://user-images.githubusercontent.com/55734436/103888833-b7da2280-5128-11eb-8053-61adc17384ac.png)


### 5-1. B값을 0.0001을 더한 값으로 고쳐주고 dLoss / dt의 값을 관찰한다.
![image](https://user-images.githubusercontent.com/55734436/103888839-b9a3e600-5128-11eb-8b18-c69e650a40b2.png)


### 5-2. 결과값 dLoss / dt를 dLoss / dB에 넣어준다.
![image](https://user-images.githubusercontent.com/55734436/103888849-bc9ed680-5128-11eb-9f75-9ee1a4b82891.png)


### 5-3.B값을 원래대로 고친다.
### 6.next W,next B의 값을 복사하여W,B에 넣어주고Loss를 확인한다.
![image](https://user-images.githubusercontent.com/55734436/103888852-bf013080-5128-11eb-9ed0-66201af2d64b.png)


### 7. 2번부터 다시 반복한다.

이 과정을 반복하다 보면 loss값이 점점 줄어드는 것을 알게됩니다. 이 과정을 이해하는 과정이 어렵지만 계속해서 반복해서 복습을 해야겠습니다!!
