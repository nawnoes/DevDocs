### 정리
***
- passport 인증 성공 후 req.user에 인증된 사용자가 담긴다.
- req.session에는 DB에 저장될 세션 정보들이 저장
- req.sessionID에는 세션 ID만 따로 저장 
- multer는 multipart/form-data를 다루기 위한 node.js 의 미들웨어
- multer에서 주의 사항  
이때 주의할 점은 iOS에서는 formData의 tyep을 'jpg'라고 입력해도 정상적으로 동작하지만,Android에서는 반드시 'image/jpeg'로 작성해야만 한다!! (이것때문에 하루 날려먹음)
- emulator에서 주의사항
 ios 에뮬레이터는 localhost로 정상 동작하지만, android의 경우 반드시 실제 IP 주소를 작성해야만 정상 메세지를 수신할 수 있다.

- 