---
title: db MySQL review
date: 2020-12-31 11:19:26
category: "database"
draft: false
---

# MySQL

- 20201217 mysql 스터디

## 기초 명령어

- show databases;
  - 데이터 베이스 보는명령어
- create database test1;
  - test1이라는 데이터베이스 생성
- use test1;
  - test1이라는 데이터베이스 선택
- show tables;
  - 그 데이터베이스 안의 테이블들의 정보를 조회
- create table qwe (qq int primary key) ;
  - 테이블 생성
- select \* from qwe;
  - qwe이라는 테이블 조회
- insert into qwe (qq,name) values (3,'..');
  - 테이블 안에 데이터 넣기
- delete from qwe where qq='2';
  - qq가 2인 데이터를 삭제

**select from, where**

- 테이블에서 조건에 맞는 컬럼을 찾아서 보여준다

```mysql
select 컬럼 이름
from 테이블 이름
where 조건
```

- 컬럼이름 변경 가능

**연산자**

- between : 범위 연산
- OR
- AND
- IN : where continent in ("Asia", "Africa")
- NOT IN
- !
- LIKE

**ORDER BY**

- ASC: 오름차순
- DESC 내림차순

**LIMIT**

**GROUP BY HAVING**

그룹 함수

- count , max, min, avg, var_samp, stddev

- having
