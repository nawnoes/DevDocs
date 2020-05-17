# React-Native 웹소켓 사용 시 Unrecognized WebSocket connection option(s) 에러
: 웹소켓 연결 시 아래와 같은 에러 메세지 발생  
```
Unrecognized WebSocket connection option(s) `agent`, `perMessageDeflate`, `pfx`, `key`, `passphrase`, `cert`, `ca`, `ciphers`, `rejectUnauthorized`. Did you mean to put these under `headers`?
```

## 기존
```js
this.socket = io.connect('SOCKET_URL');
```
## 변경
변경 후 헤더에 `-` 값을 넣어 추후에 문제 발생여지가 있을지..
```js
this.socket = io.connect('SOCKET_URL', { jsonp: false, agent: '-', pfx: '-', cert: '-', ca: '-', ciphers: '-', rejectUnauthorized: '-', perMessageDeflate: '-' });
```

# References
[React Native + Expo: Unrecognized WebSocket connection option(s) #1855](https://github.com/feathersjs/feathers/issues/1855)