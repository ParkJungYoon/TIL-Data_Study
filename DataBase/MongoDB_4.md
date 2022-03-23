> **Elice Ai Track**에서 제공하는 강의자료를 바탕으로 작성하였습니다.

# MongoDB - 고급 활용 기능

## 1. Flask와 연결

- flask 설정

( 백엔드 )

```python
import pymongo
from bson import ObjectId
import csv
from flask import Flask, render_template, request, redirect

app = Flask(__name__)
client = pymongo.MongoClient('localhost', 27017)
db = client.get_database("elice")
col = db.get_collection("post")
```

## 2. 집계 방법론

1. 데이터베이스의 정보를 불러와 애플리케이션 단계에서 집계하는 방법

2. MongoDB의 맵-리듀스 기능을 이용하는 방법

3. MongoDB의 집계 파이프라인 기능을 이용하는 방법
   - {$group: {_id: "$rating", count: {$sum: 1}}}

- < 처리 속도 > <br>
  애플리케이션 < 맵-리듀스 < 집계 파이프라인 (C언어로 이루어져서 조금 더 효율적)

- < 자유도 > <br>
  애플리케이션 > 맵-리듀스 > 집계 파이프라인

## 3. 인덱스

- 인덱스 기능: 인덱스는 색인과 거의 같은 기능을 수행한다. 인덱스는 검색과 순서 정렬을 효율적으로 만들어준다.

- 인덱스 특징
  1. 인덱스는 쿼리 작업을 매우 효율적으로 만든다
  2. 인덱스를 만들면 도큐먼트 생성 수정 시 속도 저하가 생긴다
  3. 다수의 필드를 대상으로 조회를 할 때는 복합 인덱스가 유용하다
  4. a-b 복합 인덱스는 a 단순 인덱스와 같은 기능을 할 수 있다

## 4. 복제 세트

같은 정보를 공유하는 Data Set 이다.

- 왜 복제?

  1. 높은 가용성
  2. 정보의 안전한 보호를 위해

- 프라이머리가 죽게 되면
  1. 과반수 세컨더리가 감지 -> 선거를 개최
