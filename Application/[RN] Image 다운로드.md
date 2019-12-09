### React-Native Image Download
***
리액트 네이티브에서 이미지 다운로드 받는 방법 

#### 1. expo FileSystem
***
```js
FileSystem.downloadAsync(uri, fileUri, options)
```
uri를 이용해서 파일 다운로드. local 파일 디렉토리는 먼저 존재해야한다. 

__Example__
```js
FileSystem.downloadAsync(
  'http://techslides.com/demos/sample-videos/small.mp4',
  FileSystem.documentDirectory + 'small.mp4'
)
  .then(({ uri }) => {
    console.log('Finished downloading to ', uri);
  })
  .catch(error => {
    console.error(error);
  });
```


#### References
- https://reactnativecode.com/download-image-from-url-into-gallery-folder/
- https://docs.expo.io/versions/latest/sdk/filesystem/
- node.js 파일 다운로드 방법
https://m.blog.naver.com/PostView.nhn?blogId=hyoun1202&logNo=220675944242&proxyReferer=https%3A%2F%2Fwww.google.com%2F