# MongoDB Update

### 1. Update

**MongoDB**

```js
db.monsters.update({ name: 'Slime' }, { $set: { hp: 30 } }); // WriteResult({ nMatched: 1, nUpserted: 0, nModified: 1 });

```
**Mongoose**
```js
var query = { name: 'borne' };
Model.update(query, { name: 'jason bourne' }, options, callback)
```
> mongoose는 $set을 알아서 붙여준다.


### 2. FindAndModify
- update 메소드와는 달리 upsert과 remove까지 같이 수행할 수 있다.
- 인자는 Option 객체 하나에 여러 개 속성을 넣어준다.
- 수정 후, 수정된 결과까지 가져온다. 

