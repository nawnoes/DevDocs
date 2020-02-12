# Anaconda환경에서 pip install 사용하기
아나콘다 환경에서 **pip install [패키지명]**을 사용하려고 하면 잘 동작하지 않는다.  
아래 stackoverflow에서 해결책 찾음

1. 아나콘다 환경에서 pip 설치
```
conda install pip
```
  
2. 아나콘다 경로 아래 bin 폴더에서 pip 찾아서 실행
```
[아나콘다_설치_경로]/anaconda3/bin/pip install [패키지 명]
```

# Ref
https://stackoverflow.com/questions/41060382/using-pip-to-install-packages-to-anaconda-environment