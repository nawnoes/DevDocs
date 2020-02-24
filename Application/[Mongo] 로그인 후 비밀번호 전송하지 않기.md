# [Mongo] 로그인 후 비밀번호 전송하지 않기
mongo 디비로 회원 로그인 후 원하지 않는 정보를 보내지 않아야할 때 있음.

예) 로그인 후 사용자 비밀 번호 같은 경우

```js 
//비밀번호 체크 함수 
user.chackPassword(password, (err, isMatch) => {
            if (err) {return done(err);}
            if (isMatch) {
                //  user의 정보가 _doc object 안에 있음
                user._doc.password = null;
                return done(null, user);
            } else {
                return done(null, false, { message: "비밀번호가 틀렸습니다." });
            }
        });
```
