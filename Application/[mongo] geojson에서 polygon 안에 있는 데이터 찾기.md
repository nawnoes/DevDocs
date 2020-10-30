# MongoDB aggregation으로 Polygon 안에 있는 데이터 찾기
몽고 DB에서 위치기반으로 저장한 데이터에 대해서 geojson으로 검색이 필요한 경우 mongoDB의 기능을 이용해
다양한 타입을 이용해서 검색할 수 있다. find 시 `$geoIntersects`와 `$geometry`를 이용해서 `Polygon`내에 있는 좌표 안에 있는 값들을 구할 수 있다.
## 쿼리
```js
let query = {
        location:{
        $geoIntersects: {
            $geometry: {
            type: "Polygon",
            coordinates: [coords] // 검색할 좌표
            }
        }
        }
    }
```

## 찾기
```js
// query로 polygon 안에 있는 장소 찾기
Place.find(query)
    .exec( (err, results) => {
    if (err) { return next(err); }
    const data = {
        success: true,
        users:results
    }
    return res.send(data)
    })
```