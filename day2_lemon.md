# 레모네이드 판매 예측(강의)

> 강의링크: https://opentutorials.org/course/4570/28974

#### 1. 과거의 데이터를 준비한다.
#### 2. 모델의 구조를 만듭니다.
#### 3. 데이터로 모델을 학습(FIT)합니다.
#### 4. 모델을 이용합니다.

우리는 지도학습 강의에서 다음과 같은 순서로 진행을 하기로 배웠습니다. 이제 이 부분을 자세하게 코드로 알아보는 시간을 가지도록 하겠습니다.

![image](https://user-images.githubusercontent.com/55734436/103661017-9b67aa00-4fb1-11eb-9fd8-d489f4e24714.png)
출처:https://opentutorials.org/course/4570/28974

먼저 전체적인 코드의 구조는 다음과 같습니다. 조금더 구체적으로 코드를 알아보도록 하겠습니다.

### 1. 과거의 데이터를 준비한다.
```
# 데이터를 준비합니다.
파일경로 = 'https://raw.githubusercontent.com/blackdew/tensorflow1/master/csv/lemonade.csv'
레모네이드 = pd.read_csv(파일경로)
레모네이드.head()
# 종속변수, 독립변수
독립 = 레모네이드[['온도']]
종속 = 레모네이드[['판매량']]
print(독립.shape, 종속.shape)
```
앞에 강의에서 한번 언급했던 내용입니다. 먼저 과거의 데이터를 준비하고 읽어온 후 종속변수와 독립변수를 분리를 해줘야 합니다.

### 2. 모델의 구조를 만듭니다.
```
X = tf.keras.layers.Input(shape=[1])
Y = tf.keras.layers.Dense(1)(X)
model = tf.keras.models.Model(X, Y)
model.compile(loss='mse')
```
다음은 모델 구조를 만드는 부분입니다. 다음 코드는 가장 간단한 형태로 신경망을 구현한 코드입니다. 이 단계는 아직 학습이 되기 전 상태입니다.
여기서 우리가 중요하게 봐야 할 부분이 있습니다.

X = tf.keras.layers.Input(shape=[**1**]) 
Y = tf.keras.layers.Dense(**1**)(X) 

바로 숫자입니다! 이 숫자의 의미는 무엇일까요?? 먼저 X 변수에 담긴 **1** 의 의미는 바로 우리가 가지고 있는 독립변수의 수가 1이기 때문에 1을 넣어주는 것입니다. 다음으로 Y 변수에 담긴 변수는 종속변수의 수가 1개 이기 때문에 마찬가지로 **1** 을 넣어주는 것입니다. 모델의 구조를 만들때 이 숫자의 역할이 굉장히 중요합니다!!

### 3. 데이터로 모델을 학습(FIT)합니다.
```
model.fit(독립, 종속, epochs=1000, verbose=0)
model.fit(독립, 종속, epochs=10)
```
다음은 모델을 학습하는 부분입니다. **fit** 이라는 도구가 모델을 학습시키는 도구입니다. 여기서 **epochs** 의미는 무엇일까요?? 우리는 한번만 듣고 알아들을 수 있지만 더 많이 학습을 하고 반복을 하면 더 잘 이해하게 됩니다. 그 의미가 바로 epochs의 의미입니다. 즉 전체 데이터를 몇번 반복해서 학습을 하는가를 의미하게 됩니다. 이제 우리는 학습을 완료한 모델을 얻었습니다.

### 4. 모델을 이용합니다.
```
print(model.predict(독립))
print(model.predict([[15]]))
```
이제 우리가 만든 모델에게 새로운 값을 넣어서 반환해주는 값을 확인할 수 있습니다.


전체 코드는 [여기](https://github.com/jaaaamj0711/Machine_learning_yahac/blob/main/lemon.ipynb)에서 확인할 수 있습니다.
