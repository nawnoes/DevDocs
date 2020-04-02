# S3와 lambda를 이용해 리사이징 서버 만들기
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