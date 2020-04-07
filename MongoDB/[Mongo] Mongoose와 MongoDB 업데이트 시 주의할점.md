# MongoDB와 Mongoose에서 update를 사용 할 때 주의할 점
Mongoose와 MongoDB는 업데이트 시 서로 차이가 있으므로 주의해야한다.
>  MongoDB는 업데이트 할 내용을 그대로 replace 해버리는 반면, Mongoose는 merge 하는 것 처럼 동작
> 기본적으로 mongoose는 입력받는 데이터에 $set 연산자가 없으면 자기가 알아서 붙여준다는 것입니다. 친절하게도 우리가 실수로 문서를 통째로 덮어씌워버리는 걸 막아줄게라고 명시

```js
var query = { name: 'borne' };
Model.update(query, { name: 'jason bourne' }, options, callback)

// is sent as
Model.update(query, { $set: { name: 'jason bourne' }}, options, callback)
// if overwrite option is false. If overwrite is true, sent without the $set wrapper.
```



# Ref
- https://blog.ull.im/engineering/2019/03/08/update-on-mongodb-and-mongoose.html