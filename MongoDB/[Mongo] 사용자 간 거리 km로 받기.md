# MongoDB 사용자 간 거리 받기
mongo에서 $near를 통해 주변 사용자를 받을 수 있지만, 구체적인 거리를 받기에는 부족한다. 이때 aggregate쿼리로 구체적인 거리를 받아올 수 있다. 

**aggregate 예**
```js
db.collection-name.aggregate (
    [{ 
       $geoNear: { 
         near : {
           type: “Point”, 
           coordinates: [-95.9953, 41.2000] 
         }, 
         distanceField: “dist.calculated”, 
         maxDistance: 2000, 
         includeLocs:”dist.location”, 
         num: 10, 
         spherical :true
       }
    }]
 )
```

**쿼리 결과**  
dist안의 calculated 항복을 보면 계산된 거리를 얻을 수 있다.
```json
{ “_id” : ObjectId(“561988b97265889f025790c6”), “name” : “Kayveo”, “address” : { “street” : “05 Calypso Hill”, “city” : “Omaha”, “state” : “Nebraska”, “postCode” : “68117”, “country” : “United States”, “latitude” : “41.2064”, “longitude” : “-95.9953”, “loc” : { “type” : “Point”, “coordinates” : [ -95.9953, 41.2064 ] } }, “dist” : { “calculated” : 712.4406081376109, “location” : { “type” : “Point”, “coordinates” : [ -95.9953, 41.2064 ] } } }
```

> $near의 경우 구체적인 필드를 지정해야하는데 #geoNear의 경우 구체적인 필드 지정 없이 찾을 수 있다.
쿼리 결과에 dist로 calculated에 구체적인 

# References
[GeoNear and Mongo](https://medium.com/optional-type/geonear-and-mongo-c58039f3adb7)