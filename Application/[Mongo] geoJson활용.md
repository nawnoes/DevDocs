### MongoDB에서 geoJson 활용.
***
nodejs + mongoose 조합으로 좌표 기반으로 특정 데이터들을 반환하는 경우 geoJson 활용 가능.

#### 1. geoJson이란?
: json 형태로 만든 위치 정보. 

#### 2. 사용방법
: mongoose 에서 schema 작성 예시  
  
##### 2.1 스키마 작성
> location의 형식은 아래와 같이 치켜야 한다.  
> __2dshere__ 는 2차원 형식의 일반 좌표를 사용한다는 의미
```js
var Schema = mongoose.Schema;


const geoSchema = new Schema(
{   name : String,
    location: {
        type: { type: String }, //추후에 Point 등 다른 설정 가능
        coordinates: []
    }
});

geoSchema.index({ location: "2dsphere" }); // location 기준으로 2dsphere(구면을 2d로 표현)

module.exports = mongoose.model('geoSchema', geoSchema);
```

##### 2.2 데이터 저장 
```js
var geo = new geoSchema({ // geo에 새로운 데이터 타입 지정
  name : "jamsil",
  location: {
   type: "Point",
   coordinates: [36.098948, -112.110492]
  }
 });
geo.save((err, message) => { //save로 데이터 저장 
  if (err) console.log(err);
  console.log(message);
 });
```
  
##### 2.3 반경 안 데이터 검색  
- $maxDistance는 반경 거리를 
- $geometry는 위치의 기준
- coordinates 는 long(경도), latt(위도) 순서
```js
geoSchema.find({
    location : {
        $near : {
            $maxDistance : 1000,
            $geometry : {
                type: "Point",
                coordinates: [long, latt]
            }
        }
    }
}).find((error, results) => {
       if(error) console.log(error);
       else return results;
});
```

### References
- https://medium.com/@dltkdals2202/mongodb%EC%97%90%EC%84%9C-geojson%EC%9D%84-%ED%99%9C%EC%9A%A9%ED%95%9C-%EB%B0%98%EA%B2%BD%EA%B3%84%EC%82%B0-179d4f0dcf9
- https://g6ling.github.io/2016/09/17/mongoose-geo-ko/