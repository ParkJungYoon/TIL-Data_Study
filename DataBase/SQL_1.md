# SQL - DDL (Data Definition Language)

DDL은 데이터베이스를 정의하는 언어로 데이터베이스 생성, 수정, 삭제를 할 때 사용하는 언어

## 1. `CREATE`

데이터베이스와 테이블을 생성하는 쿼리문

- 데이터베이스 생성

```sql
CREATE DATABASE `EliceRabbit`;
```

- 데이터베이스 사용

```sql
USE EliceRabbit;
```

- 테이블 생성

```sql
CREATE TABLE `tb_Rabbit`{
    '속성명' 타입,
    '속성명2' 타입,
    …
}
```

- 현재 데이터베이스, 테이블을 확인

```sql
-- 데이터베이스 목록 조회

SHOW DATABASES;

-- 테이블 목록 조회
SHOW TABLES;
```

<br>

## 2. `ALTER`

테이블을 수정하는 쿼리문

- 컬럼 추가

```sql
ALTER TABLE `추가하고자 하는 테이블 명` ADD COLUMN `추가하고자 하는 컬럼 명` `속성 값`;
```

- 컬럼 삭제

```sql
ALTER TABLE `삭제하고자 하는 테이블 명` DROP COLUMN `삭제하고자 하는 컬럼 명`;
```

- 컬럼 변경

```sql
ALTER TABLE `변경하고자 하는 컬럼이 있는 테이블 명` MODIFY COLUMN `변경하고자 하는 컬럼 명` 변경하고자 하는 속성 값;
```

- 컬럼 명도 함께 변경

```sql
ALTER TABLE `변경하고자 하는 컬럼이 있는 테이블 명` CHANGE COLUMN `변경하고자 하는 컬럼 명` `새로운 컬럼 명` 변경하고자 하는 속성 값;
```

- 테이블 이름 변경

```sql
ALTER TABLE `변경하려는 하는 테이블 명` RENAME `새로운 테이블 명`;
```

<br>

## 3. `DROP`

데이터베이스, 테이블을 삭제하는 쿼리문

- 데이터베이스 삭제

```sql
DROP DATABASE `테이블 명`
```

- 테이블 삭제

```sql
DROP TABLE [IF EXISTS] `테이블 명`
```

IF EXISTS : 해당 테이블이 있으면 실행하고 없으면 error 내지 않고 넘긴다.
