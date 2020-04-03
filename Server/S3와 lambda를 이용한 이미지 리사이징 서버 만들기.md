# S3와 lambda를 이용해 리사이징 서버 만들기

나의 경우 [[AWS] CloudFront Lambda@edge 를 이용한 이미지 리사이징](https://devhaks.github.io/2019/08/25/aws-lambda-image-resizing/#7-Lambda-edge-%ED%95%A8%EC%88%98%EC%97%90-Lambda-%ED%95%A8%EC%88%98-%EB%B0%B0%ED%8F%AC) 블로그를 보고 lambda resizing 서비스를 완성. 여러가지 블로그 글이 있었지만 2020-03월에 적용하기에 가장 적합했다.   
> exif등의 메타정보를 유지하기 위해서는 위 블로그 내용에 추가로 sharp 부분을 수정해줘야 한다.


이미지를 원본과 썸네일을 한번에 저장하게 되면, 저장소 용량을 많이 사용하게 된다. lambda와 cloudfront,  lambda@edge를 이용해 리사이징 서버 

## 1. 설정
### 1.1. IAM
AWS Identity and Access Management(IAM)는 AWS 리소스에 대한 액세스를 안전하게 제어할 수 있는 웹 서비스. IAM을 사용하여 리소스를 사용하도록 인증(로그인) 및 권한 부여(권한 있음)된 대상을 제어.  
   1. IAM으로 접속
   2. 메뉴의 [역할] -> [역할만들기] 클릭
   3. 역할만들기 에서 [AWS서비스] -> 이 역할을 사용할 서비스로 [Lambda] 선택
### 1.2. S3
### 1.3. CloudFront
### 1.4. Lambda

# References
https://swtpumpkin.github.io/backend/aws/lambdaResizing/