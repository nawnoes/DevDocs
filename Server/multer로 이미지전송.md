## multer로 이미지 전송하기
***
React-Native로 express 서버에 파일을 전송하는 방법
### 1. fetch
***
fetch를 사용했을 때 방법. 이미지 업로드시 **miltpart/form-data** encoding type과 맞는 업로드 형식이 필요하다.  
따라서 **FormData**를 이용해서 body를 조합할것 

```js
fetch('MY_API_URL', {
  method: 'POST',
  body: JSON.stringify({
    userId: '123'
  }),
})
```

### 2. multer
- 폼 데이터나 폼 태그를 통해 업로드한 이미지를 올리면 req.file에 정보가 들어오고, dest 속성에 지정해둔 경로에 이미지가 저장

### 3. FormData
보통은 ajax 전송시 폼 전송을 할일은 거의없음. 하지만 이미지 업로드시 폼 전송을 사용한다.  
폼 데이터의 이름과 타임에 항목이 있어야 multer의 미들웨어를 거치게 된다. 
```js
var formData = new FormData();
formData.append('name', 'zerocho');
formData.append('item', 'orange');
formData.append('item', 'melon');
``` 
- 폼데이터는 append 메소드로 키-값 형식으로 하나씩 추가해주면 된다.
- 값은 문자열로 자동 변환된다. 배열, 숫자 -> 문자열, 객체는 무시된다.
#### 3.1 메소드
***
```js
formData.has('item'); // true
formData.has('money'); // false
formData.get('item'); // orange
formData.getAll('item'); // ['orange', 'melon']
```
- has(): 해당 키가 존재하는지 확인
- get(): 직접 값을 가져온다. 단, 처음 저장한 값 하나만 불러온다.
- getAll(): 키에 매칭되는 모든 값을 배열로 반환

#### 3.2 이터레이션
***
```js
var keys = formData.keys();
keys.next(); // { done: false, value: 'name' }
keys.next(); // { done: false, value: 'item' }
keys.next(); // { done: false, value: 'item' }
keys.next(); // { done: true, value: undefined }
var values = formData.values();
values.next(); // { done: false, value: 'zerocho' }
values.next(); // { done: false, value: 'orange' }
values.next(); // { done: false, value: 'melon' }
values.next(); // { done: true, value: undefined }
var entries = formData.entries();
entries.next(); // { done: false, value: ['name', 'zerocho'] }
entries.next(); // { done: false, value: ['item', 'orange'] }
entries.next(); // { done: false, value: ['item', 'melon'] }
entries.next(); // { done: true, value: undefined }
```
폼데이터는 이터레이션을 사용했다. 

#### 3.3 delete 
***
```js
formData.append('test', ['hi', 'zero']);
formData.get('test'); // hi, zero
formData.delete('test');
formData.get('test'); // null
formData.set('item', 'apple');
formData.getAll('item'); // ['apple']
```
- formdata에 저장된 값은 delete 메소드로 삭제할 수있다.
- append와 비슷한 set 메소드가 있지만, set의 경우 기존 값이 있으면, 덮어쓴다. 
  
#### 3.4 주의
***
> 여러 개를 append할 때 항상 키값(위에서는 img)은 같아야 여러 파일이 같은 키로 업로드
### 4. ERROR
- limits 항목에서 fieldSize를 지정해줘야한다. 