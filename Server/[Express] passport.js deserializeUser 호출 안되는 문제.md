# Passport DeserializeUser 문제
갑자기 passport에서 DeserializeUser가 안되는 문제가 있다.
  
여러가지 방법 시도 중
cors() 부분에 아무것도 없다가 아래 부분을 추가. 
```js
app.use(
  cors({
    origin: "http://localhost:3000", // server의 url이 아닌, 요청하는 client의 url
    credentials: true
  })
);

```

# References
- https://helloinyong.tistory.com/129