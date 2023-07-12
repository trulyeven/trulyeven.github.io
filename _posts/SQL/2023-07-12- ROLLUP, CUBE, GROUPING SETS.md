---
title : "[SQL] ROLLUP, CUBE, GROUPING SETS"
date : 2023-07-12 00:00:00 +0900 # +/-TTTT
categories : [SQL]
tags : [sql, sql query, rollup, cube, grouping sets, mySQL]
---

![image](https://github.com/trulyeven/trulyeven.github.io/assets/113951017/a501aac9-a6ed-463f-a10a-9b5b641cbf78)

> 사용할 테이블

여기서는 mySQL을 사용했다

아래 글을 읽어보면 아시겠지만 mySQL은 지원하지 않는 그룹핑 함수가 있어서 추가 작업이 필요하다

---

## GROUP BY

```sql
SELECT 학년, 반, AVG(점수) AS 점수
FROM 점수
GROUP BY 학년, 반;
```
![image](https://github.com/trulyeven/trulyeven.github.io/assets/113951017/055b8511-2b99-4793-93f6-7b68587c1bda)

그냥 GROUP BY를 할 경우, 학년과 반에 따른 점수 평균이 나온다

---


## ROLLUP

```sql
SELECT 학년, 반, AVG(점수) AS 점수
FROM 점수
GROUP BY 학년, 반 WITH ROLLUP; 
-- 위의 예제는 mySQL에서 사용방법이다
-- 다른 SQL : GROUP BY ROLLUP(학년, 반);
```
![image](https://github.com/trulyeven/trulyeven.github.io/assets/113951017/04428eb6-c470-4d65-bb1f-8d9d45d3e0d1)

ROLLUP을 사용하면 학년의 평균, 총 평균이 추가된다

---


## CUBE

```sql
SELECT 학년, 반, AVG(점수) AS 점수
FROM 점수
GROUP BY 학년, 반 WITH ROLLUP
UNION
SELECT 학년, 반, AVG(점수) AS 점수
FROM 점수
GROUP BY 반, 학년 WITH ROLLUP;
-- mySQL은 cube를 지원하지 않기 때문에 ROLLUP을 UNION 시키면
-- 순서는 다르지만 같은 결과를 볼 수 있다.
-- 다른 SQL : GROUP BY CUBE(학년, 반);
```
![image](https://github.com/trulyeven/trulyeven.github.io/assets/113951017/f3eb9731-ab58-4205-bf2a-39ae5bcc183e)

CUBE을 사용하면 학년의 평균, 총 평균 그리고 학년이 상관없는 반별 평균이 추가된다

---


## GROUPING SETS

### mysql

```sql
SELECT 학년, 반, AVG(점수) AS 점수
FROM 점수
GROUP BY 학년, 반 WITH ROLLUP
HAVING 학년 IS NULL XOR 반 IS NULL
UNION
SELECT 학년, 반, AVG(점수) AS 점수
FROM 점수
GROUP BY 반, 학년 WITH ROLLUP
HAVING 학년 IS NULL XOR 반 IS NULL;
-- mySQL은 GROUPING SETS도 지원하지 않아 추가 작업이 필요하다
-- 다른 SQL : GROUP BY GROUPING SETS (학년, 반)
```
![image](https://github.com/trulyeven/trulyeven.github.io/assets/113951017/fdfc4bb9-9446-462f-897d-9d2a96c15fa3)

`GROUPING SETS()`를 위처럼 사용하면 총계를 포함하지 않고 괄호 안에 포함된 열의 부분 집계만을 나타낸다. 


### 사용 예

```sql
SELECT column1, column2, aggregate_function(column3)
FROM your_table
GROUP BY GROUPING SETS (
    (column1),                        -- 그룹화 조합 1
    (column2),                        -- 그룹화 조합 2
    (column1, column2),               -- 그룹화 조합 3
    ()                                -- 전체 집계 (그룹 없음)
);
```
이처럼 사용하고 싶은 부분 집계, 전체 집계를 사용할 수 있다

---
