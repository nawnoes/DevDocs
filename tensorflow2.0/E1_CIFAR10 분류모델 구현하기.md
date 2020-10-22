# Image Classification
CIFAR 10 데이터 셋 분류하기. 
![](https://user-images.githubusercontent.com/15958325/63308580-41b7fe80-c32e-11e9-827f-98052675c0ea.png)


## CIFAR 데이터 로드

```
# Load training and eval data from tf.keras
(train_data, train_labels), (test_data, test_labels) = \
    tf.keras.datasets.cifar10.load_data()

train_data, valid_data, train_labels, valid_labels = \
    train_test_split(train_data, train_labels, test_size=0.1, shuffle=True)
```

## 데이터 노말라이즈
신경망의 웨이트 값들은 굉장히 작은 값들도 초기화 된다. 하지만 이미지 데이터는 0~255의 값을 가지므로, 그대로 사용하게 된다면, 크게 출렁이게 된다. 따라서 안정적으로 학습하기 위해 픽셀값들을 0과 1사이 값으로 정규화를 거친다.
```
# 데이터 노말라이즈
train_data = train_data/255.0
train_labels = train_labels.reshape([-1])
print(train_data) 
print(train_labels)

valid_data = valid_data/255.0
valid_labels = valid_labels.reshape([-1])

test_data = test_data/255.0
test_labels = test_labels.reshape([-1])
```

## model.Compile
모델의 학습에 필요한 옵티마이저와 로스를 설정해준다.
### Loss Function
케라스에 구현된 categorial Crossentropy를 사용한다.
`tf.keras.losses.CategoricalCrossentropy`
### Optimizers
모델의 웨이트를 어떻게 효과적으로 업데이트 시킬것인가
`tf.keras.optimizer.Adam()`를 사용

## model.fit
모델을 설정 후 학습하는 과정. 기존에 케라스에서 사용하던 함수로 텐서플로 2.0부터 사용할 수 있게 되었다. 
- step per epoch: 내가 가진 트레이닝 데이터가 100, batch 사이즈가 10인경우 step per epoch은 10 이다.
# References
- https://medium.com/@ericabae/tensorflow-2-0-%ED%95%A9%EC%84%B1%EA%B3%B1-%EC%8B%A0%EA%B2%BD%EB%A7%9D-cnn-bfd925298c9b

