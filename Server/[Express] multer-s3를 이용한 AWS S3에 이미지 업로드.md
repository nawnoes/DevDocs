# Express multer-s3를 이용한 AWS에 S3 이미지 업로드
: 저장할 이미지가 늘어날것에 대비하여 아마존 AWS S3에 이미지 업로드 필요성이 생겼다. 따라서 기존 multer를 이용해 express 서버 public 경로가 아닌 S3에 업로드를 구현한다. 
### 1. AWS 계정 생성
### 2. AWS Access Key와 Seceret Key 발급
: 액세스 키와 시크릿 키는 AWS API와 라이브러리 사용 시, 필요한 인증 도구
**키를 모든 API 사용이 가능하고 과금**이 되기 때문에 유출에 유의 해야한다.
github에 올라가지 않게 중요
#### 2.1 Key 생성
  - 내 보안 자격 증명 클릭 
  - [새 액세스 키 만들기 ] 클릭 
  - rootkey.csv로 파일 다운로드 <- **유출되면 안됨** 
### 3. AWS S3 버킷 생성
### 4. express의 config 경로에 awsconfig.json 파일 생성
**유출에 절대 주의**
```js
{
    "accessKeyId": "access key를 입력해주세요.",
    "secretAccessKey": "secret key를 입력해주세요.",
    "region": "ap-northeast-2"
  }
```

### 5. 4에서 설정한 파일을 이용해 AWS S3 객체 생성
```js
const AWS = require("aws-sdk");
AWS.config.loadFromPath(__dirname + "/../config/awsconfig.json");

let s3 = new AWS.S3();
```

### 6. multer와 multer-s3 모듈 설치
```sh 
$ npm install multer
$ npm install multer-s3
```

# References
https://victorydntmd.tistory.com/70
https://victorydntmd.tistory.com/66