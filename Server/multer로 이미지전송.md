## multer로 이미지 전송하기
***
React-Native로 express 서버에 파일을 전송하는 방법
### 1. fetch
***
fetch를 사용했을 때 방법. 이미지 업로드시 **miltpart/form-data** encoding type과 맞는 업로드 형식이 필요하다.  
따라서 **FormData**를 이용해서 body를 조합할것 

```js
fetch('MY_API_URL', {
  method: 'POST',
  body: JSON.stringify({
    userId: '123'
  }),
})
```