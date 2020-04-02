# lambda로 이미지 리사이즈 시 사진 회전하는 현상
AWS 람다로 이미지 리사이즈 서비스를 올렸는데, 실제 서비스에 적용해보니 이미지가
맘대로 회전되는 현상이 발견되었다.
  
최초에는 앱 내에서 이미지를 회전 시키려고 시도했지만, 만족스럽지 않은 결과라 여러가지로 검색해보았다. 찾아보니 이미지는 고유의 메타 정보를 가지고 있고, 리사이즈 되면서 그 정보가 유실된것으로 판단했다.
  
나의 경우 `.withMetadata()`를 추가한 후 다시 lambda와 cloudfront를 배포한 후 고칠 수 있었다.
## 1. 기존 코드
nojs의 sharp를 이용해서 이미지 리사이즈 과정을 거쳤다.

```js
resizedImage = await Sharp(s3Object.Body)
      .resize(width, height)
      .toFormat(format, {
        quality
      })
      .toBuffer();
```

## 2. 해결방법
### 2.1 .withMetadata()
exif데이터를 포함할 수 있도록 withMetadata()를 추가
```js
S3.getObject({Bucket: BUCKET, Key: originalKey}).promise()
.then(data => Sharp(data.Body)
      .resize(width, height)
      .withMetadata() // add this line here
      .toBuffer()
    )
```
> toFormat('png')의 경우 jpeg와 동일한 exif를 지원하지 않으므로 빼야한다.

### 2.2 .rotate()
resize() 하기전에 .rotate() 호출하는 방법.
```js
Sharp(data.Body)
      .rotate()
      .resize(width, height)
      .toBuffer()
```

# Reference
https://stackoverflow.com/questions/48716266/sharp-image-library-rotates-image-when-resizing