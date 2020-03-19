# Express passport.js deseiralizeUser 호출 안되는 문제
stackoverflow와 구글들을 일주일 동안 뒤져서 해결하려고 했는데 해결이 잘 안되었다.
어디서는 CORS 문제라고 하고, 어디서는 session에서 cookie 설정 문제였다.
정확하진 않지만 나의 경우 앱에서 서버를 호출하기 때문에 CORS 문제에 해당 되지 않을거라 생각했다. 하지만 위 두 방법을 모두 적용해보았는데 모두 소용 없었다.
  
  
다시 처음부터 만들어보면서 **require('http').Server(app);**를 삭제하고 
  

## http서버 사용 문제
이런저런 소스 코드를 사용하다 보니 require('http').Server(app)을 사용.
server.listen 부분을 없애고 app.listen으로 사용하니 다시 deserializeUser 정상 호출 된다.

```js
const server = require('http').Server(app);

database.then(async () => {
  //http 서버에 대한 listen
  server.listen(process.env.PORT, () =>
    console.log(`Example app listening on port ${process.env.PORT}!`),
  );
});
```