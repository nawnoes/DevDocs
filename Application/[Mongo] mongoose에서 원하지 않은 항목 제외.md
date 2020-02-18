# [Mongo] mongoose에서 원하지 않은 항목 제외
컬렉션에서 데이터 조회 시, 비밀번호나 특정 정보들을 제외하고 싶은 경우에 사용

```js
// 유저 찾는 함수
getUsers = function(req, res, next) {

    //User 컬렉션에서 제외하고 싶은 항목 정의
    const usersProjection = { 
        PW: false, // 패스워드 제외
        _id: false // _id 제외
    };

    User.find({}, usersProjection, function (err, users) {
        if (err) return next(err);
        res.json(users); // users에 usersProjection에서 false 처리한 항목들은 제외 된다. 
    });    
}

```
