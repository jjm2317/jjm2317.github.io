---
title: db MySQL Day2
date: 2020-12-31 11:20:34
category: "database"
draft: false
---

# Mysql Day2

## GROUP BY HAVING

- GROUP BY 는 여러개의 동일한 데이터를 가지는 특정 컬럼을 합쳐주는 역할을 하는 명령
- COUNT , MAX, MIN, AVG, VAR_SAMP, STDDEV

**count**

```mysql
# city 테이블의 countrycode를 묶고 각 코드마다 몇개의 데이터가 있는지 확인
SELECT CountryCode, COUNT(CountryCode)
FROM city
GROUP BY CountryCode
```

```mysql
#countrylanguage 테이블에서 전체언어가 몇개 있는지 구하시오.
#DISTINCT 중복을 제거해주는 문법
sql> SELECT COUNT(DISTINCT(Language)) as language_count
FROM countrylanguage
```

**MAX**

```mysql
#대률별 인구수와 GNP 최대ㅣ값을 조회

SELECT continent, MAX(Population) as Population, MAX(GNP) as GNP
FROM country
GROUP BY continent
```

**MIN**

```mysql
# 대륙별 인구수와 GNP 최소 값을 조회 (GNP와 인구수가 0이 아닌 데이터 중에서)
SELECT continent, MIN(Population) as Population, MIN(GNP) as GNP
FROM country
WHERE GNP != 0 AND Population != 0
GROUP BY continent
```

**SUM**

```mysql
#대륙 별 총 인구수와 총 gnp

SELECT continent, SUM(population), SUM(gnp)
FROM country
GROUP BY continent
```

**AVG**

```mysql
#대륙별 평균 인구수와 평균 gnp 결과를 인구수로 내림차순 정렬
SELECT continent, AVG(population) as pop, AVG(GNP)
FROM country
GROUP BY continent
ORDER BY pop DESC
```

**HAVING**

```mysql
# 대륙별 전체인구를 구하고 5억이상인 대륙만 조회

SELECT continent, SUM(population) as population
FROM country
GROUP BY continent
HAVING population >= 500000000;
```

```mysql
#대륙별 평균 인구수, 평균 GNP, 1인당 gnp한 결과를 1인당 gnp가 0.01 이상인 데이터를 조회하고 1인당 gnp를 내림차순으로 정렬

SELECT continent, AVG(population) as pop, AVG(gnp) as gnp, (AVG(gnp) / AVG(pop)) as gpp
FROM country
GROUP BY continent
HAVING gpp >= 0.01
ORDER BY gpp DESK
```

**WITH ROLLUP**

```mysql
#고객과 스탭별 매출과 고객별 매출의 총합을 출력
use sakila;

SELECT   customer_id, staff_id,SUM(amount)
FROM payment
GROUP BY customer_id, staff_id
WITH ROLLUP
```

## CREATE USE ALTER DROP

**CREATE**

```mysql
# 데이터 베이스 생성
CREATE DATABASE <databas_name>;

# test 데이터 베이스 생성
CREATE DATABASE test;
```

**USE**

```mysql
#test 데이터 베이스 선택
USE test;

#현재 데이터 베이스 확인
SELECT DATABASE();

#테이블 생성
CREATE TABLE <table_name>(
	column_name_1 column_data_type_1 column_constraint_1,
    column_name_2 column_data_type_2 column_constraint_2,
    ...
);

#제약조건이 없는 user1 테이블 생성

CREATE TABLE user1(
	user_id INT,
    name Varchar(20),
    email Varchar(30),
    age INT(3),
    rdate DATE
);

#제약조건이 있는 user2 테이블 생성
CREATE TABLE user2(
	 user_id INT PRIMARY KEY AUTO_INCREMENT,
    name Varchar(20), NOT NULL,
    email Varchar(30), UNIQUE NOT NULL,
    age INT(3) DEFAULT '30',
    rdate TIMESTAMP
)
```

**ALTER**

```mysql
# Database

#사용중인 데이터베이스의 인코딩 방식 확인
SHOW VARIABLES LIKE "character_set_database"
```
