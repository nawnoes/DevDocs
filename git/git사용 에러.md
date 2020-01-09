- git remote add 시, fatal: not a git repository (or any of the parent directories): .git
에러 발생.  
현재 폴더에 git 정보를 담은 파일이 없어서 그렇다. 따라서 **git init**을 수행 후 다시 **git remote add** 명령어를 실행하면 된다.
