# String to Json

## JSON.parse()
JSON.parse() 메서드는 JSON 문자열의 구문을 분석하고, 그 결과에서 JavaScript 값이나 객체를 생성합니다. 선택적으로, reviver 함수를 인수로 전달할 경우, 결과를 반환하기 전에 변형할 수 있습니다.

```js
const json = '{"location":{"result":true, "count":42}}';
const obj = JSON.parse(json);

console.log(obj.count);
// expected output: 42

console.log(obj.location);
// expected output: true
```

# Ref
https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/JSON/parse