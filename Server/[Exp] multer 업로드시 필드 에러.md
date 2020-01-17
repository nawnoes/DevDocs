# Multer 관련 에러
## 1. MulterError: Unexpected field
upload.single([fieldname]) 을 미들 웨어로 넣는데,
필드네임과 전송시에 같아야 한다.

**클라이언트**
```js
data.append("profile", {
        // name: photo.fileName,
        // type: photo.type,
        name: 'hello_images',
        type: 'jpg',
        uri:
            Platform.OS === "android" ? photo.uri : photo.uri.replace("file://", "")
    });
```

**서버**
```js
router.post('/api/upload', upload.single('photo'), (req, res) => {
    console.log('file', req.files)
    res.status(200).json({
      message: 'success!',
    })
  })
```

#출처
- https://m.blog.naver.com/PostView.nhn?blogId=pjt3591oo&logNo=220517017431&proxyReferer=https%3A%2F%2Fwww.google.com%2F
