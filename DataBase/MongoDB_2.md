> **Elice  Ai Track**에서 제공하는 강의자료를 바탕으로 작성하였습니다.  

# MongoDB - CRUD

## 1. 구조
```데이터베이스 - 컬렉션 - 도큐먼트```

### Pymongo
이때 DB, collection 자동 생성
```python
import pymongo

connection = pymongo.MongoClient("mongodb://localhost:27017/")

# DB 접속
db = connection.get_database("testDB")

# 컬렉션에 도큐먼트 삽입
collection = db.get_collection("testCollection")
collection.insert_one({"hello": "world"})
```

### 확인하기
```python
# 데이터베이스 목록 조회
print(connection.list_database_names())

# 컬렉션 목록 조회
print(db.list_collection_names())

# pprint로 도큐먼트 목록 조회
pprint(list(collection.find())
```
<br>

## 2. BSON
BSON = Binary JSON
```
{
    _id: ObjectId(""),
    name: "Yoon",
    age: 23,
}
```

* Null : 아무것도 없다.
* Undefined : 정의 되지 않음.
* ObjectId : primary key 값으로 사용된다. <br> (확장성을 고려해서 값을 겹치지 않게 이렇게 설계)

### Pymongo 에서 사용

딕셔너리 형태로 저장
```python
from bson import ObjectId
from datetime import datetime
collection.insert_one({
    "_id": ObjectId("542c2b97bac0595474108b48"),
    "name": "yoon",
    "age": 23,
    "viewTime": datetime(2017, 10, 24, 5, 2, 46)
})
```

<br>

## 3. Create

* pprint <br>
python에서 좀 더 mongoDB에 맞는 출력 결과를 볼 수 있다. 

```python
from pprint import pprint
pprint({ BSON document })
```

### collection에 하나 document 삽입
```python
from pprint import pprint
result = collection.insert_one(
    { document }
)
print(result.inserted_id)
pprint(result.inserted_id)
```

### 다수의 document 삽입
```python
result = collection.insert_many(
    [ { document }, { document }, ... ]
)
print(result.inserted_ids)
```
```inserted_ids```: ObjectId를 볼 수 있다.

<br>

## 4. Read : 기초

```list(collection.find())```

```python
result = collection.find(
    { query },
    { projection }
)
print(result) # 커서 반환
print(list(result))
```

### 커서
커서란 쿼리 결과에 대한 포인터<br>
도큐먼트의 위치정보만 반환 -> 작업 효율

* 커서에서 도큐멘트 불러오기
```python
result = collection.find(
    { query }
)

for document in result:
    print(document)
```

### 쿼리
원하는 정보를 걸러내기 위한 깔데기

* 기본 쿼리 <br>
```{"field": value, "field": value}```

### Projection
boolean이 true이면 해당 field를 표현하고 false면 field를 제외한 결과를 출력한다.

* 예시
     ```python
    users.find(
        {"password": "1111"},
        {"username": False}
    )
    ```

<br>

## 5. Update

### 하나의 document 수정

```python
result = collection.update_one(
    { query },
    { update },
    upsert:Boolean
)
print(result.matched_count)
print(result.modified_count)
```
query로 검색하고, update에 변경할 사항 적는다.

### 다수의 document 수정
```python
result = collection.update_many(
    { query },
    { update },
    upsert:Boolean
)
print(result.matched_count)
print(result.modified_count)
```

* 특정 field 값 수정
```python
inventory.update_one(
    {"item": "canvas"},
    {"$set": {"qty": 10} }
)
```

* 특정 field 제거
```python
inventory.update_one(
    {"item": "canvas"},
    {"$unset": {"qty": True} }
)
```

* 검색 결과가 없을 때 새로 추가 <br>
: True로 설정하면 
```python
inventory.update_one(
    { "item": "flash" },
    { "$set": {"size": {"h": 10, "w": 8} ,"status": "F"} }, 
    True
)
```

* 특정 문자열로 시작하는 도큐먼트 찾기 위한 쿼리
```python
쿼리 = { "date_received": { "$regex": "^2015" } }
```

<br>

## 6. Delete

* 하나의 document 삭제
```python
result = collection.delete_one(
    { query }
)
print(result.deleted_count)
```

* 다수의 document 삭제
```python
result = collection.delete_many(
    { query }
)
print(result.deleted_count)
```

