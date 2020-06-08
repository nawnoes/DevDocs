# Pyenv를 이용한 파이썬 패키지 관리
기존에는 맥에서 아나콘다를 사용해 파이썬 패키지를 관리하였다. 중간 중간 아나콘다를 업데이트 하게되면서 잘 사용 되지 않는 경우가 있어 `pyenv`를 설치해보았다. 

## pyenv 설치
### 1. homebrew를 이용해 pyenv 설치
```
brew install pyenv
```
### 2. 환경변수 설정
zsh 터미널을 사용하지만 나의 경우 `.bash_profile`의 설정과 연결되어 있어 아래와 같이 사용. `~/.zshrc`에도 아래와 같이 설정 가능.
```
open ~/.bash_profile 
```
### 3. 설정 내용.
아래 설정 내용을 저장 후 터미널을 껐다가 다시 킨다.
**설정내용** 
```
...기존설정...
export PATH="$HOME/.pyenv/bin:$PATH"
eval "$(pyenv init -)"
...기존설정...
```
### 4. 파이썬 3.7.5 설치
```
pyenv install 3.7.5
```

### 5. 다른 pyenv 명령어
```
brew upgrade pyenv   #pyenv upgrade

pyenv --version   #pyenv version 확인

pyenv install --list   #설치할 수 있는 것 list

pyenv install <version_name>   #설치하기

pyenv uninstall <version_name>   #삭제하기

pyenv versions   #설치된 것 + 가상환경 version

pyenv global <우쩌고저쩌고>   #전역설정
 
```
# Reference
https://mizykk.tistory.com/17