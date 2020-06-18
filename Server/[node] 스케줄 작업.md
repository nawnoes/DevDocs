# Nodejs에서 스케줄 작업

## 모듈을 활용한 방법
### 모듈의 종류
Agenda, Node-cron, Node-schedule 
### 모듈의 동작 방식
위 3 모듈 다 `cron` 형식으로 시간을 일정 규칙에 맞춰 지정해주면 고정된 작업을 시간 규칙에 따라 동작한다.

## cron 이란
![](https://media.vlpt.us/post-images/filoscoder/e658d5b0-230d-11ea-a062-816d6d5610ef/cron-format.png)
유닉스와 같은 컴퓨터 운영체제에서 사용되는 시간 기반 작업 스케줄러이다. 

## 모듈 간 비교
![](https://media.vlpt.us/post-images/filoscoder/fd207050-230d-11ea-9236-0b590657d7d8/comparison.png)

위 표를 보면 Agenda를 사용해야겠다는 생각이 1차적으로 든다. 참고글을 작성하신 분의 경우 mongoDB를 사용하지 않기 때문에 고려하지 않기로 결정. 하지만 MongoDB를 사용하는 경우 충분히 고려할만하다. 

## Node-schedule
모듈 유지 인원, 다운로드수, star 수, non-cron 스타일 지원, 레퍼런스등 을 볼때 적절하다고 생각된다. 
### 정보
- github: https://github.com/node-schedule/node-schedule#readme
### 설치
```
npm install node-schedule
```
### cron 포맷
```
*    *    *    *    *    *
┬    ┬    ┬    ┬    ┬    ┬
│    │    │    │    │    │
│    │    │    │    │    └ day of week (0 - 7) (0 or 7 is Sun)
│    │    │    │    └───── month (1 - 12)
│    │    │    └────────── day of month (1 - 31)
│    │    └─────────────── hour (0 - 23)
│    └──────────────────── minute (0 - 59)
└───────────────────────── second (0 - 59, OPTIONAL)
```
### 사용 예
1. 매 42분 마다 스케줄 작업
```
var schedule = require('node-schedule');

var j = schedule.scheduleJob('42 * * * *', function(){
  console.log('The answer to life, the universe, and everything!');
});
```
2. non-cron 스타일의 예
매 일요일 2:30에 동작
```
var j = schedule.scheduleJob({hour: 14, minute: 30, dayOfWeek: 0}, function(){
  console.log('Time for tea!');
});
```

3. Job 취소
```
j.cancel();
```

# References
[스케줄 업무 자동화: Node-cron vs Node-schedule 비교](https://velog.io/@filoscoder/%EC%8A%A4%EC%BC%80%EC%A4%84-%EC%97%85%EB%AC%B4-%EC%9E%90%EB%8F%99%ED%99%94-Node-cron-vs-Node-schedule-%EB%B9%84%EA%B5%90-clk4dyynve)