# url 스트링을 통한 정보전달

## 1. Query스트링을 통한 전달
```
http://a.com/topic?id=1
```
위와 같이 쿼리 스트링을 사용하고 싶은경우. **req.query**를 사용한다. 복수의 쿼리스트링을 가져오는 것도 가능

```js
app.get('/topic', function(req, res) {
  // url이 http://a.com/topic?id=1&name=siwa 일때
  res.send(req.query.id+','+req.query.name); // 1,siwa 출력
})
```
## 2. Semantic URL
: path 방식을 통한 url의 경우 params를 통해서 값을 가져올 수 있다.
- 깔끔한 URL을 유지하고, 사용자가 URL을 기억하기 쉽다
- 주요 정보를 변수로 처리하지 않으므로 디렉토리인것 처럼 다룬다.

```js
app.get('/topic/:id/:mode', function(req, res){
// 라우터 경로의 변경 /:id/:mode 를 통해 path 방식 url 값을 가져올 수 있다.
	var topic = [
		'javascript is...',
		'nodejs is...',
		'express is...'
	];
	var li = `
	<li><a href="/topic/0">js</a></li>
	<li><a href="/topic/1">nodejs</a></li>
	<li><a href="/topic/2">express</a></li>
	`
	res.send(li + '<br>' + topic[req.params.id] + req.params.mode);
	//path 방식을 사용하는 url의 경우 params를 통해서 값을 가져올 수 있음
})
```

# References
https://wayhome25.github.io/nodejs/2017/02/18/nodejs-11-express-query-string/