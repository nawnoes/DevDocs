# Javascript 시간 관련 Date 사용 방법 

```js
var loadDt = new Date(); //현재 날짜 및 시간   //현재시간 기준 계산

 alert(new Date(Date.parse(loadDt) - 30 * 1000 * 60 * 60 * 24)); //30일전
 alert(new Date(Date.parse(loadDt) - 15 * 1000 * 60 * 60 * 24)); //보름전
 alert(new Date(Date.parse(loadDt) - 7 * 1000 * 60 * 60 * 24)); //일주일전
 alert(new Date(Date.parse(loadDt) - 1 * 1000 * 60 * 60 * 24)); //하루전
 alert(new Date(Date.parse(loadDt) + 1 * 1000 * 60 * 60 * 24)); //하루후
 alert(new Date(Date.parse(loadDt) + 7 * 1000 * 60 * 60 * 24)); //일주일후
 alert(new Date(Date.parse(loadDt) + 15 * 1000 * 60 * 60 * 24)); //보름후
 alert(new Date(Date.parse(loadDt) + 30 * 1000 * 60 * 60 * 24)); //한달후

alert(new Date(Date.parse(loadDt) + 1000 * 60 * 60)); //한시간후
alert(new Date(Date.parse(loadDt) + 1000 * 60)); //1분후
alert(new Date(Date.parse(loadDt) + 1000)); //1초후
```

# Reference
https://blueskai.tistory.com/100 