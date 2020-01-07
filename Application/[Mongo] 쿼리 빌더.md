# mongo 쿼리 빌더
몽구스에서 사용하는 쿼리 빌더

```js
User.find({
  name: 'zerocho',
  birth: { $gt: 20 },
  role: { $in: ['owner', 'admin'] }
 }, {
  name: 1,
  birth: 1,
  medals: 1,
}).sort({ medals: -1 }).limit(5);
```
위와 같은 Json형식으로 정의된 쿼리를 쿼리 빌더를 통해 아래와 같이 바꿀 수 있다.

```js
User.find()
  .where('name').equals('zerocho')
  .where('birth').gt(20)
  .where('role').in(['owner', 'admin'])
  .sort('-medals')
  .limit(5)
  .select('name birth medals')
```
1. where  
2. equal, ne
3. exits
4. gt, lt, gte, lte
5. in, nin, all
6. and, or, nor
7. size, mode, slice
8. within, box, circle, geometry, near, intersects, maxDistance
9. distinct
10. regex
11. select
12. skip, limit
13. sort
14. find, findOne, findOneAndRemove, findOneAndUpdate


# References
https://www.zerocho.com/category/MongoDB/post/59bd148b1474c800194b695a