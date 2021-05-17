---
title: db Day1 settings
date: 2020-11-23 18:07:25
category: "database"
draft: false
---

# 데이터베이스 Day1

- ubuntu 기초 사용
- aws EC2 인스턴스에 Mysql 설치
- 모델링
- SELECT FROM WHERE

**데이터베이스**

db / 데이터를 통합하여 관리하는 데이터의 집합

DBMS

데이터 베이스를 관리하는 미들웨어 시스템, 데이터 베이스 관리 시스템

- mongoDB
- mysql

- RDBMS

  - Oracle, Mysql, Postgresql, Sqlite
  - 데이터의 테이블 사이에 키값으로 관계를 가지고 이쓴 데이터 베이스

- NoSQL

  - Mongodb, Hbase, Cassandra
  - 데이터 테이블 사이의 관계가 없이 데이터를 저장하는 데이터 베이스
  - 데이터 사이의 관계가 없으므로 복잡성이 작고 많은 데이터의 저장이 가능

**MySQL**

오픈소스 이며 다중사용자와 다중스레드지원

인터넷 망을 통해 여러 아이피에서 접속가능

다양한 운영체제에 다양한 프로그래밍 언어 지원

표준 SQL 사용

- dbms 마다 SQL 문법이 조금씩 다른데 MySQL은 표준 SQL을 따른다.

- License
  -

server > database > table > row > value

테이블과 테이블사이의 관계를 가짐

여러개의 데이터베이스안에 여러개의 테이블을 만들고 여러개의 row 데이터를 넣을 수 있다.

RDBMS 쪽에서는 행에 대해서 row tuple record , 열에대해서 column field attribute 로 명명해서 부름

**aws**

서버 컴퓨터가 여러개가 있다.

클라우드 기술은 여러개의 컴퓨터를 물리적으로 묶어서 여러개의 계정을 단독컴퓨터로 다룰수있다.

클라우드 서비스가 이슈가 되는이유

- 인간의 노동력을 대체
  - 서버 구축을 위해서 400~700정도의 서버컴퓨터를 구입
  - ssd 를구매해서 끼운다.
  - os설치
  - 회사에 대한 데이터베이스 어플리케이션 설치
  - 테스트 후 들고 lg idc
  - 빨라야 일주일
  - 클라우드 사용시 5분만에 할 수 있다.

**프로그래밍 및 웹구조**

os

- cpu ram harddisk를 컨트롤

pc - internet - server

브라우저를열고 url 입력

dns라는 서버

- 도메인을 아이피로 바꾸어줌
- url형태로 서버를 찾아감
- 서버를 찾아주는것이 라우터임

서버에서 받는다.

서버에는 웹 어플리케이션이 있다.

url에는 아티클 아이디가 있어서 요청을 보낸다.

서버에서는 db로 연결되어 있어 아이디에 맞는 데이터를 가져온다.

html코드에db에서 가져온 데이터를 입력해서 응답한다.

node js 에서 자바스크립트언어를 사용하여 프론트엔드도 백엔드영역

cookie sessoion cache

cookie

- 문자열 데이터를 도메인 별로 따로 저장
- 로그인 정보, 내가 봤던 상품 정보, 팝업 다시보지 않음
- 하나의 클라이언트에 300개 도메인당 20개, 쿠키 하나당 4Kbyte

session

- server에 저장하는 객체 데이터, 브라우저와 연결시 session id 생성

cache

- ram에 있는데이터가 연산속도가 빠르다.
- ram이꽉차면 가상메모리 사용

private public

- 회사내에서는 외부로 접속이 안되지만 사내에서 쓸수있는 intranet이 있다.
- 공유기는 인터넷망과 연결되어있다.
- 공유기로 네이버에 들어가면 같은 아이피를 공유한다.
- 내부에서 공유자를 구분해주는 ip 값이 필요하다.
- private ip로 구분해준다.
- 하나의 서버에도 public ip와 private ip를 갖는ㄴ다.
- 인트라넷에서 특정사이트 접속을 막으면 공유기에서 설정을 한다.
- 사내 웹페이지만 접속하게 할 수도있다.
- 인터넷 망에서 사용하는것이 public ip
- 인트라넷에서 사용하는 것이 private ip 이다

## Mysql 설치 및 설정

- AWS EC2(elastic compute cloud) 인스턴스에 ubuntu os 및 MySQL 5.7.x버전 설치

**EC2 인스턴스 생성**

- t2.micro
- Ubuntu 18.04버전
- 보안그룹에서 3306 포트 추가

**EC2 인스턴스에 접속**

- (mac) pem 파일 400권한으로 변경

- ssh -i ~/.ssh/pdf.pem ubuntu@{접속 ip}

**apt-get 업데이트**

```
$ sudo apt-get update -y
$ sudo apt-get ubgrade -y
```

**MySQL Server 설치**

```
$ sudo apt-get install -y mysql-server mysql-client
```

**MySQL secure 설정**

```
$ sudo mysql_secure_installation
// y or no list
// validate password plugin / new password / re-enter new password
// remove anonymous users / disallow root login remotely
// remove test database and access to it / reload privilege tables now
```

**MySQL 패스워드 설정**

```
$sudo mysql
```

**ALTER USER**

- 비밀번호
- 운영체제 인증
- 디폴트 테이블 스페이스
- 임시 테이블 스페이스
- 테이블 스페이스 분배 할당
- 프로파일 및 디폴트 역할

```
// user 수정 문법
ALTER USER user_name
[ IDENTIFIED {BY password | EXTERNALLY}]
[ DEFAULT TABLESPACE tablespace]
[ TEMPORARY TABLESPACE tablespace]
[ PASSWORD EXPIRE]
[ ACCOUNT { LOCK | UNLOCK}]
```

**mysql 로그인**

```
mysql -u root -p
```

**mysql 데이터베이스에 접근**

```
use mysql;
```

**비밀번호 변경**

```
ALTER user 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY '
변경할 비밀번호';
```

**변경사항 저장**

```
mysql> flush pivileges;
```

**설정한 패스워드를 입력하여 접속**

```
$ mysql -u root -p
Enter password: `비밀번호`
```

**외부접속 설정**

```
$ sudo vi /etc/mysql/mysql.conf.d/mysqld.cnf
//vim 에디터를 이용해서 mysql 설정파일을 불러온다

//bind-adress 변경
//127.0.0.1 > 0.0.0.0

//127 ~~ : 자체 컴퓨터를 나타내는 ip 주소
//0.0.0.0 : 로컬시스템의 모든 IPv4 주소 /
```

**외부 접속 패스워드 설정**

```
mysql> grant all privileges on *.* to root@'%' identified by '비번'
```

**서버 재시작으로 설정내용 적용**

```
$ sudo systemctl restart mysql.service
```

**샘플 데이터 추가**

```
// 서버로 sql 파일을 전송
$ scp -i ~/.ssh/fds.pem {파일 경로} ubuntu@{서버 ip주소}:{서버내의 경로}

//데이터 베이스 생성
$mysql -u root -p
sql> create database {데이터베이스 이름};

//데이터베이스에 데이터 추가
$mysql -u root -p {데이터베이스} > {sql파일}

```

## Mysql Workbench 사용

**데이터 베이스 모델링**

- 데이터 베이스 모델링은 데이터 베이스에서의 테이블 구조를 미리 계획해서 작성하는 작업
- RDBMS 는 테이블간에 유기적으로 연결되어 있기 때문에 모델링을 잘하는것이 중요
- 기본적으로 개념적 모델링, 논리적 모델링, 물리적 모델링 절차로 설계

**개념적 모델링**

- 업무 분석을 통해 핵심 데이터의 집합을 정의하는 과정
- ex ) 사람(고객정보) 과 상품(상품명, 가격)

**논리적 모델링**

- 개념적 모델링을 상세화 하는 과정
- ex) 고객정보 (나이, 주소, 성별)와 구매정보(고객, 상품), 상품(상품명, 카테고리, 가격)

**물리적 모델링**

- 논리적 모델링을 DBMS 에 추가하기위해 구체화 하는 과정

**실습**

- EER 다이어그램 (객체관계 다이어그램)
  - File - New Model 선택
  - 이름설정
  - EER - ADD Diagram
  - 테이블 추가
  - 컬럼추가
  - 테이블 관계연결
  - 모델링 파일을 실제 데이터베이스에 야ㅕㄴ결
  - file -save model 선택 후 저장
- EER 다이어그램 파일을 적용
  - File - open Model
  - database - forward engineer
  - MySQL Server 연결정보를 선택하고 continue 선택
  - 실행 쿼리에서 visiable 제거 후 실행
- 데이터 베이스를 EER 다이어그램으로 변경
  - database -reverse engineer

**관계선**

실선 : 식별관계 : 부모가 있어야 자식이 생성됨

점선: 비식별관계 부모가 없어도 자식이 생성됨

![image-20201124112832430](C:\Users\Jung\AppData\Roaming\Typora\typora-user-images\image-20201124112832430.png)

## SQL 문

**DML**

- data manipulation language

데이터 조작어

데이터 검색, 삽입, 수정, 삭제등에 사용

- SELECT
- INSERT
- UPDATE
- DELETE

트랜젝션이 발생하는 SQL문

- **트랜젝션**
  - 비동기로 처리될 태스크를 트랜젝션으로 묶어서 동기식으로 처리한다.

**DDL**

- data definition language

데이터 정의어

데이터 베이스, 테이블, 뷰, 인덱스등의 데이터 베이스 개체를 생성, 삭제, 변경에 사용

- CREATE
- DROP
- ALTER
- TRUNCATE

실행즉시 DB에 적용

**DCL**

- data control language

데이터 제어어

사용자의 권한을 부여하거나 빼앗을 때 사용

- GRUNT
- REVORKE
- DENY

### SELECT FROM

- 데이터를 검색할 때 사용하는 문법

- crud에서 read에 해당

**기본 포맷**

```
SELECT <column_name_1>, <column_name_2> . ...
FROM <table_name>
```

**전체 컬럼 데이터 조회**

```
sql> SELECT * FROM wold.country
```

**code, name 세개의 컬럼 데이터 조회**

```
sql> SELECT code, name
FROM world.country
```

**데이터 베이스 선택: FROM 절에 world.을 사용할 필요가 없다.**

```
sql> USE world;

sql> SELECT *
FROM country
```

**alias: 컬럼의 이름을 변경할 수 있다**

```
sql> SELECT code as country_code, name as country_name
FROM country
```

**데이터 베이스, 테이블, 컬럼 리스트 확인**

```
sql> SHOW DATABASES;
sql> SHOW TABLES;
sql> DESC city;
```

### WHERE

- 특정 조건을 주어 데이터를 검색하는데 사용되는 문법

**비교연산**

```
// 인구가 1억이 넘는 국가를 출력
SELECT *
FROM country
WHRER Poplutaion >= 1000000000
```

**논리 연산 : AND, OR**

```
// 인구가 7000만에서 1억인 국가를 출력
SELECT *
FROM country
WHERE Population >= 700000000 AND Popluation <= 1000000000
```

**- 범위 연산: BETWEEN**

```
// 인구가 7000만에서 1억인 국가를 출력
SELECT *
FROM country
WHERE Popluation BETWEEN 700000000 AND 1000000000
```

**-OR**

```
// 아시아와 아프리카 대륙의 국가 데이터를 출력
SELECT *
FROM country
WHERE Continent = "Asia" OR Continent = "Africa"
```

**특정 조건을 포함 : IN, NOT IN**

```
//아시아와 아프리카 대륙의 국가 데이터를 출력

SELECT *
FROM country
WHERE Continent IN ("Asia", "Africa")

//아시아와 아프리카 대륙의 국가가 아닌 데이터를 출력

SELECT *
FROM country
WHERE Continent In ("Asia", "Africa")

// 아시아와 아프리카대륙의 국가가 아닌 데이터를 출력 (논리연산)
SELECT *
FROM country
WHERE Continent != "Asia" AND Continent != "Africa"

```

**특정 문자열이 포함된 데이터 출력 : LIKE**

```
//정부 형태에 Republic이 포함된 데이터 출력
SELECT *
FROM country
WHERE GovernmentForm LIKE "%Republic%"
```

### ORDER BY

- 특정 컬럼의 값으로 데이터 정렬에 사용되는 문법

**오름차순 인구순으로 국가의 리스트를 출력**

```
SELECT *
FROM country
ORDER BY popluation ASC
```

**내림차순 인구순으로 국가의 리스트를 출력**

```
SELECT *
FROM country
ORDER BY population DESC
```

**국가 코드를 알파벳순으로 정렬, 같은 국가코드를 가지면 인구순으로 내림차순 정렬**

```
SELECT *
FROM city
ORDER BY CountryCode ASC, Population DESC
```

### LIMIT

- LIMIT 은 조회하는 데이터의 수를 제한할 수 있다.
-
