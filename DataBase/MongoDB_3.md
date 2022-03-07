> **Elice  Ai Track**에서 제공하는 강의자료를 바탕으로 작성하였습니다.  

# MongoDB - Query

## 1. 구조
```{ <field>: {<operator1>: <value>, <operator2>: <value>}, <field>: ... }```

* 기본적으로 쿼리는 필드가 가장 바깥에 있고, 안쪽에 연산자가 들어간다.
    * 연산자는 일반적으로 $표시를 쓴다.

* 예외: ```$or, $and, $nor```

```python
{ "$or": [ { "status": "A" }, { "qty": { "$lt": 30 } } ] }
```

<br>

## 2. 점 표기법

* 객체 내부로 접근
    * ```name.first```
* 배열 요소 접근
    * ```list.0```

<br>

## 3. 연산자
* [연산자](https://docs.mongodb.com/manual/reference/operator/query/)

### 비교 연산자

* 숫자 이외 타입도 비교 연산 가능

* 정규 표현식으로 비교 연산
```python
inventory.find( { "tags": { "$nin": [
    re.compile("^be"), 
    re.compile("^st")
]} } )
```

* 예시
```python
import re
# date 값이 2010년도 혹은 2020년도가 아닌 조건을 작성하세요.
query = {"date_received": 
    {"$nin": [
        re.compile("^2010"), 
        re.compile("^2020")
     ]}
}
```

* 특정 문자열로 시작하는 도큐먼트 찾기 위한 쿼리
```python
쿼리 = { "date_received": { "$regex": "^2015" } }
```

### 문자열 연산자

* ```$regex``` : 특정 정규 표현식과 맞는 Document 선택  

```python
{ <field>: { "$regex": 'pattern', "$options": '<options>' } }
```

* ```$text``` : 문자열 검색 기능을 수행

```python
{
    "$text": { "$search": <string>, "$language": <string>,
    "$caseSensitive": <boolean>, "$diacriticSensitive": <boolean> }
}
```

* text 연산자 사용하기 위해서 문자열 인덱스 설정
```python
collection.create_index([('field', pymongo.TEXT)], default_language='english')
```

* 검색 <br>
baking 이렇게 들어있어도 매칭된다.
```python
articles.find( { "$text": { "$search": "bake coffee cake" } } )
```
```python
query = { "$text": { "$search": "bake coffee cake" } }
cursor = col.find(query)

for food in cursor:
    pprint(food)
```

* 구절 검색
```python
articles.find( { "$text": { "$search": "\"coffee shop\"" } } )
```

< 전체 예시 >
```python
import pymongo
from pprint import pprint

# 데이터베이스와 Collection을 생성하는 코드
connection = pymongo.MongoClient("mongodb://localhost:27017/")
db = connection.get_database("library")
col = db.get_collection("books")

# 텍스트 인덱스를 title 필드에 생성하는 코드
col.create_index([('title', pymongo.TEXT)], default_language='english')


# 제목에 yoon이 있는 책을 $search 연산자를 활용해 조회하세요.
query = {"$text": {"$search": "yoon"}}
cursor = col.find(query)

# 결과를 출력합니다.
for book in cursor:
    pprint(book)
```

### 배열 연산자

* document에서 배열은 값이 여러 개인 것으로 인식한다.

* ```$all```
순서와 상관없이 배열 안의 요소가 모두 포함되면 선택한다.
```
items.find( { "tags": { "$all": [ "book", "appliance" ] } } )
```

* ```$elemMatch```
$elemMatch 조건과 맞는 배열 속 요소를 가진 Document를 선택한다.
(배열 속 여러 요소 중에서 일치하는 것)
```
{ <field>: { "$elemMatch": { <query1>, <query2>, ... } } }
```

```
survey.find(
    {"results":{"$elemMatch":{"product":"xyz","score": { "$gte": 8 } } }}
)
```

* ```$size```
해당 배열의 크기가 같은 Document를 선택한다.
```
{ <field>: { "$size": <array size> } }
```