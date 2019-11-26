### 1. 도커란
***
![docker1](https://ho1234c.github.io/images/2017-01-31-docker-nodejs/2.png)  
컨테이너 가상화 플랫폼. 기존에는 호스트 OS 위에 게스트 OS를 설치해서 동작 했다면, 도커는 이와 다르게 게스트 OS를 설치하지 않는다. 도커 엔진 위에 시스템 운영에 필요한 최소한의 라이브러리들만 설치하고, 시스템 자원은 호스트OS와 공유. OS는 설치하는것이 아닌, 시스템 파일만 격리시키고, 실행은 호스트OS에 시켜서 속도가 빠르다

### 2. 이미지와 컨테이너
***
![docker2](https://ho1234c.github.io/images/2017-01-31-docker-nodejs/3.png)  
도커에는 이미지를 통해서 컨테이너를 만든다. 이미지만 있다면, 컨테이너를 원하는만큼 만들 수 있다. 도커는 레이어를 겹쳐서 만들어서, 컨테이너 이미지를 겹치는 방식으로 동작. 하나의 이미지에서 파생된 여러가지 이미지를 만들수도 있다. 

### 3. Docker-compose
***
도커 서버 구축 시, 한 컨테이너에 필요한 소프트웨어를 한꺼번에 설치할 수도 있고 각각 컨테이너를 만들어서 연결할 수도 있다. 각각의 컨테이너를 띄우고 설정하는 스크립트를 매번 실행하기 번거롭기 때문에 여러 컨테이너를 한번에 띄울 수 있게하는 docker-compose를 사용한다.

docker-compose는 컨테이너를 stack-service-task라는 세가지  계층으로 구분해서 관리한다.  
_stack_ : 하나의 앱 (facebook, youtube처럼 큰 단위)
_service_ : 앱을 구성하는 하나의 역할 (nodejs, mongodb, nginx 서버등 앱을 작동하기 위한 구성요소)
_task_: serviece를 이루는 컨테이너들
> 컨테이너 안의 데이터는 영속성이 없기 때문에 컨테이너를 지우면 사라진다. 따라서 영속성을 가지는 데이터를 저장하는 용도로는 적합하지 않다.

#### 3.1 docke-compose 사용
여러 컨테이너를 한번에 실행할 수 있는 docker-compose에 대해 소개.
docker-compose는 기본적으로 docker-compose.yml 파일을 기반으로 실행된다.  
  
도커 출시후 pig라는 독립된 개발 환경을 빠르게 구성할 수 있는 프로젝트가 나옴. 그 후 인기를 얻자 도커에서 피그 프로젝트를 흡수하여, 도커 컴포즈라는 이름의 도구로 만든다.  
  
도커 컴포즈를 사용하면, 컨테이너 실행에 필요한 옵션을 docker-compose.yml에 적어둘 수 있고, 컨테이너 간 실행 순서나, 의존성도 관리 할 수 있다.

```
version: '3'
services:
 nginx:
  image: nginx:latest
  ports:
   - "80:80"
 php:
  image: php:7.3-fpm
  ports:
   - "9000:9000"
  voluems:
   - ./source:/source
```
![dc1](https://miro.medium.com/max/1828/1*JCbYpCF4U-fF08Ef3l2o3g.png)
_version_: compose 파일의 버전을 의미. 버전 3이 최신 버전  
_services_: services부터 실제 container 설정을 명시. 컴포즈에서는 컨테이너 대신 서비스 개념을 사용.  
_nginx_: 사용자가 지정하는 이름. 다른 이름으로 변경해도 상관 없음.
_image_: 해당 container가 어떤 image를 기반으로 실행되는지 지정. 
_ports_: container와 host 간의 공유할 포트를 지정. docker compose로 container를 실행한 다음 localhost를 입력하면 nginx 기본 페이지가 보인다. 
_volumes_: container와 host간의 공유할 디렉토리를 지정한다.   
_environment_: docker run 명령어의 -e 옵션에 적어던 내용들. 

```
services:
  django:
    build:
      context: .
      dockerfile: ./compose/django/Dockerfile-dev

```
db 서비스와 달리 앱 서비스는 특정 이미지 대신 build 옵션을 추가한다.
_context_는 docker build 명령을 실행할 디렉터리 경로.  
_dockerfile_에는 개발용 도커 이미지를 빌드하는데 사용할 dockerfile을 지정하면 된다.

> version 3d의 경우 --link 옵션을 주지 않아도 한 네트워크 안에 있는 서비스끼리 서로 통신할 수 있다. 
> 포트로 사용할 수 있는 값은 TCP나 UDP에서 0번 부터 65535 
#### 3.2 docker-compose로 실행 및 정지 명령어
```
docker-compose up   //shell에서 실행
docker-compose up -d //데몬으로 실행
docker-compose down // 정지
docker-compose ps // 현재 환경에서 실행 중인 각 서비스 상태
docker-compose stop  //서비스를 멈춤
docker-compose start //서비스를 시작
docker-compose down --volume // 서비스를 지운다. 컨테이너와 네트워크를 삭제하며, 옵션에 따라 볼륨도 지운다.
docker-compose exec [명령어] // 실행 중인 컨테이너에서 명령어를 실행한다.
docker-compose logs [서비스명] // 서비스 이름에 대한 로그 확인. 안적으면 컴포즈가 관리하는 모든 로그
```
> docker로 실제 환경을 구성하려면 많은 옵션들이 포함된다. 

#### 3.3 도커 컴포즈 단축 명령 등록하기
***
도커 컴포즈 도입후 명령어 자체가 길어서 오히려 귀찮을때,
~/.bashrc나 ~/.zshrc에 아래 내용을 추가

```
alias dco='docker-compose'
alias dcb='docker-compose build'
alias dce='docker-compose exec'
alias dcps='docker-compose ps'
alias dcr='docker-compose run'
alias dcup='docker-compose up'
alias dcdn='docker-compose down'
alias dcl='docker-compose logs'
alias dclf='docker-compose logs -f'

```

#### 3.4 도커 컴포즈 팁
***
##### 3.4.1 docker-compose.yml 수정시
수정하게 되면 stop -> 삭제(rm) -> 시작 (up) 해야 하지만
up 명령어만 실행해도 __알아서 컨테이너를 재생성하고 서비스 재시작__  
> 컨테이너가 재생성 되지 않는거 같을 때 __--force-recreate__ 옵션을 사용

### References
- Docker로 nodejs 서버 배포하기
https://ho1234c.github.io/2017/01/31/2017-01-31-docker-nodejs/index.html
- Docker-compose 소개
https://medium.com/sjk5766/docker-compose-%EC%86%8C%EA%B0%9C-f84840ff7203

- Docker 공식문서 에서 제시하는 개발-배포 Flow 따라가기 (Docker Swarm 사용하기)
http://jaynewho.com/post/21

https://www.44bits.io/ko/post/almost-perfect-development-environment-with-docker-and-docker-compose
