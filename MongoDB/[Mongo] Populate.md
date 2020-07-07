# 몽고DB에서 Populate 사용하기
몽고디비를 사용하다보면 object id로 저장한 항목에 대해 조인해서 결과를 보여줘야할때가 있다. 이때 몽고디비와 몽구스에서는 `populate` 기능을 사용한다.

## 사용 예
### 기존
```js
Home.find(query)
    .exec( (err, data) => {
      if (err) { return next(err); }
      //...조회된 결과 처리...
    })
});
```

### Populate 사용 
```js
Home.find(query)
    .populate('owner','owner_name') // 오너 항목에 대해서 owner_name만 조회하겠다는 의미
    .exec( (err, data) => {
      if (err) { return next(err); }
      //...조회된 결과 처리...
    })
});
```