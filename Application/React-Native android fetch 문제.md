# React Native 안드로이드 fetch 문제
리액트 네이티브에서 안드로이드 폰을 테스트하다가 fetch가 아이폰과 달라서 하루 꼬박 날렸다. 여러가지 방법을 고려해보았지만 생각보다 간단한 방법을 통해 해결할 수 있었다.
## 내용
**express**에서 `passport`를 이용해 local 로그인을 구현.
ios에서는 로그인 완료 후 `isAuthenticated` true로 API를 정상적으로 사용할 수 있었다
하지만 안드로이드에서는 `isAuthenticated` 에서 결과 값이 계속 **false**로 떨어져 서버 내에서 
로그인 되지 않은것으로 판단하여 API들을 이용할 수 없었다.  
  
추가로 세션이 계속 갱신되어, mongoDB `sessions` 컬렉션에도 계속 쌓이는 문제가 발생했다.

## 고려한 방법
- AsyncStorage
- fetch의 헤더나 session을 건드리는 방법

## 해결방법  
**기존 소스**  
```js
fetch(api_url, {
        method: 'POST',
        headers: {
            Accept: 'application/json',
            'Content-Type': 'application/json',
        },
        body: JSON.stringify(body),
    })
```  
  
**변경 소스**  
**credentials: 'include',**을 추가 했다

```js
fetch(api_url, {
        method: 'POST',
        headers: {
            Accept: 'application/json',
            'Content-Type': 'application/json',
        },
        credentials: 'include',

        body: JSON.stringify(body),
    })
``` 
## Credentials include란?
credentials: 'include'란 아래 Mozilla 사이트에 나와 있듯이 Cross-origin 호출이라 해도 언제나 사용자의 credentials을 전송한다. 이때 credential들은 쿠키, basic http auth등을 말한다.
> include: Always send user credentials (cookies, basic http auth, etc..), even for cross-origin calls.



# References
https://developer.mozilla.org/ko/docs/Web/API/Request/credentials