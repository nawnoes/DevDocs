### 1. 헤로쿠란
웹 애플리케이션 배치 모델. 여러 프로그래밍 언어를 지원하는 PaaS 클라우드. 최초 클라우드 플랫폼들 가운데 하나. Java, Node.js, Python 등을 지원한다

### 2. 사용방법
- 1) 회원가입
- 2) Heroku CLI 설치 [Heroku CLI Download](https://devcenter.heroku.com/articles/heroku-cli)
  또는 
  ''''
  brew tap heroku/brew && brew install heroku
  ''''
  으로 설치

- 3) 존재하는 Git 레포지토리에 Heroku 추가
  ''''
  $ heroku git:remote -a razz-9
  ''''
  명령어 실행후 
  set git remote heroku to https://git.heroku.com/XXXXXX.git
- 4) 프로젝트 폴더에 앱과 서버를 동시에 둠. 서버 경로에서 
  ''''
  heroku create
  ''''
  Creating app... done, ⬢ ancient-thicket-91857
https://ancient-thicket-91857.herokuapp.com/ | https://git.heroku.com/ancient-thicket-91857.git
- 5) 헤로쿠 빌드팩이 세팅 되지 않았다는 메세지
  ''''
  HINT: This occurs when Heroku cannot detect the buildpack to use for this application automatically.
remote: 			See https://devcenter.heroku.com/articles/buildpacks
remote:
  ''''
- 6) 프로젝트 폴더 아래 서버 폴더에서 다시 git init 부터 진행하니 빌드까지 성공

### 3. 정리
1) git init
2) heroku login
3) heroku create
4) git remote add heroku [주소]
5) git add .
6) git commit 
7) git push heroku master
8) heroku open