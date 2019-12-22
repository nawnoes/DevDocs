# dotenv사용
## 1. 설치
```
$ npm install react-native-dotenv --save-dev
```
## 2. 사용
### 2.1 .env 작성
### 2.2 사용
```
import { API_KEY, ANOTHER_CONFIG } from 'react-native-dotenv'
 
ApiClient.init(API_KEY, ANOTHER_CONFIG)
```


