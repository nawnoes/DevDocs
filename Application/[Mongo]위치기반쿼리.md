# 상황 별 MongoDB 위치 기반 쿼리
자신의 위치를 기반으로 주변의 장소, 혹은 업소등을 추천하는 기능을 제공하는 경우가 많습니다. 이 글은 MongoDB를 이용해 현재 나의 위치에서 가까운 업소를 찾거나, 해당 업소와의 거리를 구하는 방법을 소개
  
## 1. GeoJson
- JSON 형태로 지형 데이터를 정의하는 포맷. 
- GeoJSON의 type에는 Point, LineString, Polygon, MultiPoint, MultiLineString, MultiPolygon, GeometryCollection이 있습니다. 정의된 타입들에서 볼 수 있듯이, 좌표점 뿐만이 아니라 선분에서 폴리곤, 여러 도형 집합들까지 다양하게 지원하고 있습니다. 
- 문법 형식에서 coordinates 필드는 type에 따라 여러 좌표점을 포함 할 수 있습니다.
```js
<field>: { type: <GeoJSON type>, coordinates: <coordinates> }
```

## 2. 지형 인덱스 (Geospatial Indexes)
- 지형 정보에 대한 쿼리를 지원하기 위해 MongoDB는 지형 인덱스를 지원합니다. 
- 인덱스는 2dsphere, 2d의 두 종류입니다. 
- 2dshphere는 지구와 같은 구형태의 지형을 기반으로 계산하는데 사용되고, 
- 2d는 x, y축의 평면 지형을 기반으로 계산하는데 사용됩니다.

```js
db.collection.createIndex({ <location field>: '2dshpere' })
db.collection.createIndex({ <location field>: '2d' })
```
> 쿼리 연산자로 무엇을 쓰느냐보다 어떤 종류의 인덱스가 걸려있는가에 따라 계산 방식이 달라진다.

- [예제로 배워보는 상황 별 MongoDB 위치 기반 쿼리](https://blog.ull.im/engineering/2019/03/06/mongodb-geospatial-queries.html)