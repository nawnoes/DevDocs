# MongoDB aggregate
: 몽고DB를 사용하다 보면 find로 원하는 데이터를 가공하는데 어려울 때 있다. 나의 경우는 사용자 위치를 $near로 받아왔었는데, $near로는 구체적인 거리를 표시해줄 수 없어 알아보다가 `aggreate`를 찾게 되었다.

## 1. 주요 명령어  
| RDMBS | aggregate | 설명 |
|---|---|---|
|where| $match| RDB에서 where 절에 해당|
|group by| $group||
|having|$match||
|select|$project| 실제로 가져올 데이터를 표시하는 부분. 0이면 false 1이면 true|
|order by|$sort||
|limit| $limit||
|sum()|$sum||
|count()|$sum||

## 2. 기타
| RDMBS | aggregate | 설명 |
|---|---|---|
||$toLower|소문자 출력|
||$toUpper|대문자 출력|
|substr|$substr|해당 필드의 부분만 가져온다|
||$strcasecmp|문자열을 비교하는 명령. 1이면 true -1이면 false|
|nvl|$ifNull| null일 경우 뒤에 쓴 것으로 대체. |
||$add, $subtract, $multiply, $divide| 사칙연산|
||$sort| 1: 오름차순, -1: 내림차순|
||$limit| 제한된 숫자만큼 document|
||$skip| 어떤 doc을 스킵할지 |


# References
[[mongoDB]몽고디비 aggregate](https://hongtaey.tistory.com/entry/mongoDB%EB%AA%BD%EA%B3%A0%EB%94%94%EB%B9%84-aggregate)