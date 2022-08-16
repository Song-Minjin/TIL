# RDBMS


**Relational DataBase Management System**
: 관계형 데이터베이스 관리 시스템

- 컴퓨터에 정보를 저장하고 관리하는 기술

<br>

## RDBMS의 종류

- MySQL (무료)
- MyBatis (무료)
- PostgreSQL (무료)
- Oracle Database (유료)

&nbsp;&nbsp;+) H2DB

> 자세한 내용은 다음 포스팅을 참고하세요.
> 👉🏻 [[DB] 관계형 데이터베이스(RDBMS)의 비교 - MySQL, MariaDB, Oracle, Postgre
](https://velog.io/@sw_smj/MySQL-%EA%B4%80%EA%B3%84%ED%98%95-%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4RDBMS%EC%9D%98-%EC%A2%85%EB%A5%98-1)

<br>

## H2


: Java 기반의 오픈소스 관계형 데이터 베이스 관리 시스템(RDBMS)

- In-memory DB의 대표주자
  > 🔍 **In-memory DB란?**
  > - 서버가 작동하는 동안에만 내용을 저장
  > - 서버가 작동을 멈추면 데이터가 모두 삭제됨


- 어플리케이션 개발 단계의 테스트 DB로서 많이 이용됨


- 별도의 설치과정이 없고 용량도 2MB(압축버전) 이하로 매우 저용량 👉🏻 DB 자체가 매우 가볍고 빠름


- ***JDBC*** API를 지원함
  > 🔍 **JDBC란?**
  > : Java DataBase Connectivity
  > - Java에서 DB에 접속할 수 있도록 하는 Java API
  > - DB에서 자료를 쿼리하거나 업데이트하는 방법을 제공함



<br><br>

# SQL


**Structured Query Language**
: 데이터를 읽고, 저장하고, 변경하고, 삭제하는 구체적인 문법

## SQL 기초 문법
### 1. 테이블 생성
```sql
CREATE TABLE IF NOT EXISTS posts(
    id bigint(5) NOT NULL AUTO_INCREMENT, 
    title varchar(50) NOT NULL,
    author varchar(8) NOT NULL,
    content varchar(2000) NOT NULL,
    password varchar(6) NOT NULL,ID POSTS POSTS POSTS 
    delYN varchar(1) NOT NULL,
    PRIMARY KEY (id)
);
```

<br>

### 2. 데이터 삽입
```sql
INSERT INTO posts (title, author, content, password, delYN) VALUES
    ('철수의 TIL','김철수','오늘 익힌 것은 SQL 기초 문법과 RDBMS이다. RDBMS는 관계형 데이터베이스 관리 시스템을 이야기한다. 대표적인 RDBMS로는 MySQL, MyBatis, Oracle, PostgreSQL 등이 있다.','1234','N');
```

<br>

### 3. 데이터 조회하기
```sql
SELECT * FROM posts;
```


