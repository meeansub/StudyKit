
# SELECT

```sql
SELECT select_list [ALL, DISTINCT, DISTINCTROW]

[ FROM table_source ]

[ WHERE search_condition ]

[ GROUP BY group_by_expression ]

[ HAVING search_condition ]

[ ORDER BY order_expression [ ASC | DESC ] ]
```

---

## 기본

- 주로 사용하는 테이블을 조회시 사용하는 문장이다.

열 이름에 있는 열을 불러와 조건에 맞도록 데이터를 보여준다.

```sql
SELECT [열] [ALL, DISTINCT, DISTINCTROW]

FROM [테이블]

WHERE [조건]
```

- where은 생략가능,
    - 조건이 없다면 전체 테이블 데이터 조회
- ALL : 전체 컬럼
- DISTINCT : 중복값 제거하고 검색
- DISTINCTROW : 튜플 전체를 대상

---

## WHERE

**WHERE between A and B**

- A에서 B 사이

**NOT IN ( ~ )**

- 포함되지 않는 데이터 의미

**where ~ = ‘A’ OR ~ = ‘B’**

**==  where ~ IN (‘A’, ‘B’)**

**IS NULL**

- WHERE 열 IS NULL

**IS NOT NULL**

- WHERE 열 IS NOT NULL

---

## GROUP BY

- 말 그대로 그룹으로 묶어 주는 역할
그룹에 포함된 수를 나타내줌.
- 특정 속성 기준으로 그룹화하여 검색

## HAVING

- GROUP에 조건을 서술

```sql
SELECT [열, 열, 집계열]

FROM [기존 테이블]

WHERE [조건]

GROUP BY [그룹열,그룹열]

HAVING [그룹조건]
```

- SELECT 에 그룹열이 2개 면 GROUP BY 에도 2개를 적어준다.

---

## order by 문

```sql
SELECT select_list [ INTO new_table ]

[ FROM table_source ]

[ WHERE search_condition ]

[ GROUP BY group_by_expression ]

[ HAVING search_condition ]

[ ORDER BY order_expression [ ASC | DESC ]]
```

가져온 결과를 ORDER BY 문을 통해 정렬 할 수 있다.

보기 쉽게 문장을 만들자면

```sql
select *

from 테이블

[where 조건]

order by 열(컬럼) | asc | desc
```

테이블에 있는 모든 열을 가져와 order by 에 지정된 열을 기준으로 정렬된다.

기본 정렬은 ASC 오름차순 정렬이다.

내림차순 정렬 DESC

---

# JOIN

```sql
SELECT 열1, 열2

FROM 테이블1

JOIN 테이블2

ON 조건
```

## EQUI 조인 VS NON- EQUI 조인

### EQUI 조인

- JOIN 절 사용

### NON- EQUI 조인

- 비교연산자 사용 ( >, <, >=, <=...)
- 잘 사용하지 않음

---

## INNER JOIN

교집합으로, 기준 테이블과 join 테이블의 중복된 값을 보여준다.

떡하니 JOIN만 있는 경우는 INNER JOIN(내부조인 )이다.

```sql
SELECT
A.NAME, B.AGE
FROM EX_TABLE A
INNER JOIN JOIN_TABLE B ON A.NO_EMP = B.NO_EMP
```

### NATURAL JOIN == INNER JOIN

- 조인시 중복된 속성 제거

조인에서는 테이블도 DB도 이곳저곳으로 옮겨다니기에

as a    as b 로 만들어

a.column  b.column 처럼 사용한다..

**ex)**

```sql
select a.colum1,  b.colum2
from  table1 as a
join table2 as b
on a.colum1 = b.colum2
```

---

## OUTER JOIN

- 조건에 해당되지 않는 튜플도 표시

### LEFT OUTER JOIN / RIGHT OUTER JOIN

```sql
SELECT *

FROM 테이블1 [as 별칭]

LEFT(RIGHT, FULL) OUTER JOIN 테이블2 [as 별칭]

ON 조건
```

**LEFT  OUTER JOIN**

기준테이블값과 조인테이블과 중복된 값을 보여준다.

왼쪽테이블 기준으로 JOIN을 한다고 생각하면 편하다.

- 좌측 모두 표시, 우측 JOIN 관련 튜플 표시

```sql
SELECT A.NAME, B.AGE
FROM EX_TABLE A
LEFT OUTER JOIN JOIN_TABLE B ON A.NO_EMP = B.NO_EMP
```

**RIGHT OUTER JOIN**

LEFT OUTER JOIN과는 반대로 오른쪽 테이블 기준으로 JOIN하는 것이다.

- 우측 모두 표시, 좌측 JOIN 관련 튜플 표시

```sql
SELECT A.NAME, B.AGE
FROM EX_TABLE A
RIGHT OUTER JOIN JOIN_TABLE B ON A.NO_EMP = B.NO_EMP
```

### FULL OUTER JOIN

합집합을 말한다. A와 B 테이블의 모든 데이터가 검색된다.

```sql
SELECT A.NAME, B.AGE
FROM EX_TABLE A
FULL OUTER JOIN JOIN_TABLE B ON A.NO_EMP = B.NO_EMP
```

---

## CROSS JOIN

모든 경우의 수를 전부 표현해주는 방식이다.

A가 3개, B가 4개면 총 3 * 4 = 12개의 데이터가 검색된다.

```sql
SELECT A.NAME, B.AGE
FROM EX_TABLE A
CROSS JOIN JOIN_TABLE B
```

---

## SELF JOIN

- 테이블에서 2개의 속성을 연결하여 EQUI JOIN 하는 방식

자기자신과 자기자신을 조인하는 것이다.

하나의 테이블을 여러번 복사해서 조인한다고 생각하면 편하다.

자신이 갖고 있는 칼럼을 다양하게 변형시켜 활용할 때 자주 사용한다.

```sql
SELECT 별칭1.속성, 별칭2.속성

FROM 테이블 1 [as] 별칭 JOIN 테이블1 [as] 별칭2

ON 별칭1.속성 = 별칭2.속성
```

---
---

# SQL - DML(조작어)

## INSERT

**기본**

```sql
INSERT INTO 테이블 이름 (열1, 열2, ...)

VALUE (값1, 값2 , ….)
```

- 열을 직접 지정해서 맞게 써줘도 되고, 직접 쓰지 않으면 벨류 값을 열 순서에 맞게 적어야한다.

**응용**

- 다른 테이블에 있는 값들을 조건에 맞춰서 가지고 오는 방법

```sql
INSERT INTO 테이블이름 ( 열1, 열2, 열3, 열4 ….)

SELECT 테이블에 들어갈 값

FROM select값을 구하기 위한 테이블

WHERE 조건
```

**ex)**
```
insert into usertb1 (username, userid) value ('춘배', 'daf123');
insert into usertb1 (username, userid) value ('정배', 'afdf98');
insert into usertb1 (username, userid) value ('순배', 'favxz1');
insert into usertb1 (username, userid) value ('창배', 'qewr12');

```
```
insert into itemtb1 (userid)
select userid
from usertd1
where userid <> ''

select * from itemtb1
```

```
insert int itemtb1 (userid)
-- itemtb1에 있는 userid 필드에 입력을 할것이다.

select userid
-- 조건에서 가지고올 값. userid만 가지고 온다
from usertb1
-- 위 select에 userid값을 가지고올 테이블
where userid <> ''
-- 조건은 userid에 값이 있을 경우


```

### INSERT 구문 사용시 주의사항

1. 기존에 테이블이 존재해야 입력이 가능합니다.
2. 입력된 열이름의 순서에 따라서 값도 순서대로 입력이 되어야 합니다..
3. 컬럼명이 명시 되어있지 않을 경우에는 모든 컬럼에 대하여 값을 입력해주어야 합니다.이런 경우에는 not null로 지정되어 있으면 오류순서에 맞게 하나하나 입력을 다 해주어야 합니다.
4. 3번과 마찬가지로 not null 일 경우에는 필수로 입력을 해주어야 합니다.

---

## UPDATE

```sql
UPDATE [테이블]

SET [열] = '변경할값'

WHERE [조건]
```

- 조건이 없는 경우에는 테이블에 있는 열 전체가 변경할값으로 UPDATE 된다.

---

## DELETE

```sql
DELETE

FROM 테이블

[WHERE [조건]]
```

---
---

# SQL - DDL(정의어)

- DDL로 정의된 내용은 메타데이터가 되며 시스템 카탈로그에 저장

### CREATE

- 정의

```sql
CREATE TABLE
```

```sql
CREATE TABLE 테이블명 (
	속성명 데이터타입[NOT NULL] ...

	[primary key (기본키_속성명...)]

	[, unique (대체키_속성명…)]

	[, foreign key(외래키_속성명, ....)

			references 참조테이블명(기본키_속성명...)]

			[ON DELETE 옵션]

			[ON UPDATE 옵션]

	[,CONSTRAINT 제약조건명] [CHECK (조건식)];

	)
```

CREATE SCHEMA

CREATE DOMAIN

CREATE VIEW

CREATE TRIGGER

CREATE INDEX

---

## ALTER

- 변경

```sql
ALTER TABLE 테이블명 ADD 속성명 데이터타입 [DEFAULT ‘기본값’];

ALTER TABLE 테이블명 ALTER 속성명 [SET DEFAULT ‘기본값’];

ALTER TABLE 테이블명 DROP COLUMN 속성명 [CASCADE];
```

---

## DROP

- 제거

```sql
DROP TABLE [테이블]
```

---
---

# SQL-DCL(제어어)

- DBA( DB 관리자) 가 사용
- 보안, 무결성, 회복, 병행제어등을 정의하는데 사용

## COMMIT

 : 트랜잭션 변경 내용 반영 (완료)

## ROLLBACK

: 이전 상태 되돌림 (복구)

## GRANT

: 권한 부여

## REVOKE

: 권한 취소

---
