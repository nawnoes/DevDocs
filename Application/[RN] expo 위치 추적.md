### Expo Location을 이용한 device 위치 추적
***
#### 1. getCurrentPositionAsync
```js
Location.getCurrentPositionAsync(options)
```
디바이스의 현재 위치 반환
> 매우 높은 정확도가 필요한것이 아니라면, ios에서는 위치 정보를 받는데 수초가 걸리므로 "Location.getLastKnownPositionAsync " 고려하는것이 좋다. 
 
 __options__  
 - accuracy:  Location manager 정확도. Location.Accuracy의 enum value들을 넘겨준다. 정확도가 높으면, 에너지 소비가 크다.


#### 2. watchPositionAsync


#### 3. startLocationUpdatesAsync  <= Background Location

#### 4. Location.setApiKey(apiKey)
 

### References  
- https://docs.expo.io/versions/latest/sdk/location/#locationgetlastknownpositionasync