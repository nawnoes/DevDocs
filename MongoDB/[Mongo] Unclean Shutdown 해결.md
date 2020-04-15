# MongoDB Unclean Shutdown 문제
몽고 디비를 사용하다보면 컴퓨터가 꺼지거나, 강제로 프로세스를 죽이는 경우에 몽고 디비 unclean shutdown을 볼 수 있다.  
  
복구하는 방법은 크게 2가지로
- mongod.lock 파일을 삭제하는 방법
- mongod.lock 파일을 삭제하지 않는 방법 
보통 삭제하지 않는 방법을 추천한다.

나는 아래와 같은 방법으로 복구를 진행했다.

```sh
mongod --dbpath [몽고DB저장경로] --repair
```

![](https://t1.daumcdn.net/cfile/tistory/2157BA3E55FE55AF04)


# References
https://apple77y.tistory.com/27
https://docs.mongodb.com/master/tutorial/recover-data-following-unexpected-shutdown/#repair-data-files-without-preserving-original-files