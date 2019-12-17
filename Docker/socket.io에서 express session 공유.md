# express-socket.io-session
***
쿠키 베이스의 express session을 socket.io를 통해 공유한다.
express >4.0 , socket.io > 1.0 이상 사용

## Install
```sh
$ npm install express-socket.io-session
```

## 사용
소켓이 연결된 이후 **socket.handshake.session**을 **socket.handshake.session**와 같이 사용할 수 있다. express-session을 사용할때와 똑같이.
```js
var session = require("express-session")({
    secret: "my-secret",
    resave: true,
    saveUninitialized: true
});
var sharedsession = require("express-socket.io-session");
 
// Use express-session middleware for express
app.use(session);
 
// Use shared session middleware for socket.io
// setting autoSave:true
io.use(sharedsession(session, {
    autoSave:true
})); 

//Sharing session data with a namespaced socket
io.of('/namespace').use(sharedsession(session, {
    autoSave: true
}));
```