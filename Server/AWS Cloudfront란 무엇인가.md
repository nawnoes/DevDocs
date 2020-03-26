# AWS Cloudfront란 무엇인가
서버로부터 받는 이미지 로딩 속도가 느리게 되서 자료를 찾아보다보니 구조상 cloudfront라는 것이 눈에 자주 보이기 시작했다. 

## 정의
정적 콘텐츠를 더 빨리 배포하도록 지원하는 웹서비스. **엣지위치**라 하는 데이터 센터를 통해 콘텐츠를 즉시 제공하는것.  
  
`http://example.com/sunsetphoto.png` URL을 탐색할때 복잡한 네트웤을 탐색하는것이 아닌 컨텐츠를 가장 효과적으로 서비스 할 수 있는 엣지로 이동하여, 가장 빠르게 컨텐츠 배포를 가능하게 한다.

# Reference
https://docs.aws.amazon.com/ko_kr/AmazonCloudFront/latest/DeveloperGuide/Introduction.html