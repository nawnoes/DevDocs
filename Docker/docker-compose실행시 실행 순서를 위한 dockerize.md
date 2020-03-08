# docker-compose실행시 실행 순서를 위한 dockerize
나의 경우 docker-compose 실행시 이미지를 이용해 mongodb를 사용한다. 하지만 nodejs 서버와 함께 docker-compose up 실행시 error가 발생.

## 조치방법
- docker-compose up, build, down 명령어로 테스트
- DB 소스 부분들 주석처리
- 에러 발생 부분 확인

## 에러 부분
express 서버 내에 mongoose를 불러와서 connect 하는 부분에서 에러
```js
import mongoose from 'mongoose';

...중략...

mongoose.Promise =global.Promise; //기존 몽구스 프로미스를 노드의 프로미스로 연결한것.
mongoose.connect(DOCKER_DATABASE_URL); <== 에러 발생 부분

...중략...

```

## 조치 방법

# References