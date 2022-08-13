# [DB] 관계형 데이터베이스(RDBMS)의 비교 - MySQL, MariaDB, Oracle, Postgre

<br>


## MySQL

![](https://velog.velcdn.com/images/sw_smj/post/ee6a19ec-eea4-491a-ba19-7b8c6710e33e/image.png)

: 최초의 오픈 DBMS 중 하나이며, 가장 널리 사용되고 있는 관계형 데이터베이스 관리 시스템(RDBMS)다.

- 단순 쿼리 처리 성능이 어떤 제품보다도 압도적임

- 이미 오래 사용되어 왔기 때문에 성능과 신뢰성 등에서 꾸준히 개선되어옴

- 오픈 소스이며, 다중 사용자와 다중 스레드를 지원함

- C, C++, Java, PHP 등 여러 프로그래밍 언어를 위한 다양한 API를 제공하고 있음

- 오픈 소스 라이센스를 따르기는 하지만, 상업적으로 사용할 때에는 상업용 라이센스를 구입해야 함



<br>

## MariaDB


: 오픈 소스의 관계형 데이터베이스 관리 시스템(RDBMS)

![](https://velog.velcdn.com/images/sw_smj/post/3317ea63-0e84-4cbf-bd44-c30f265e0610/image.png)

- MySQL의 개발자 Monty가 회사를 나와 MontyProgram AB라는 회사를 차리며 만들어짐

- MariaDB의 공식 문서에는 MySQL과의 차이점만 있음 →  공통된 부분은 MySQL을 알고 참고해야만 함

- MySQL를 기반으로 fork한 서비스로, MySQL의 개선된 버전 (MySQL과 동일한 소스 코드 기반)

- MySQL과 호환성이 매우 높음

- MySQL에는 없는 내장된 기능과 유용성, 보안 및 성능 개선사항이 함께 제공됨ㅁ

<br>

## MySQL vs MariaDB


### 공통점

- 모든 클라이언트 API와 통신 프로토콜이 서로 호환됨

- MariaDB의 실행 프로그램들과 유틸리티는 MySQL과 이름이 동일하며, 호환됨

- MySQL Connector는 모두 MariaDB에서 변경 없이 사용 가능 (Connector : Java 및 C 클라이언트 라이브러리)

- MySQL 클라이언트 프로그램은 그대로 MariaDB 서버에 연결하여 사용 가능
<br>

### 차이점

- 두 DBMS는 기능, 성능에서 아직까지 큰 차이점이 있지는 않다. 단, MariaDB의 개선사항 및 MySQL과의 면밀한 비교를 조금 정리해보면 다음과 같다.

- MariaDB가 스토리지 엔진이 더 많다.

- MariaDB가 보안 패치 릴리즈가 빠르고 투명하다.

- MariaDB 개발이 더 개방적이고 활발하다.

- MariaDB는 오픈 소스인 반면 MySQL은 Enterprise Edition에서 일부 독점 코드를 사용한다.

- MariaDB는 데이터 마스킹 및 동적 열을 지원하지 않지만, MySQL은 지원한다.

- MariaDB가 상대적으로 사용 점유율이 아직 낮다.

<br><br>




## Oracle


: Oracle 회사에서 만든 DBMS. 세계 점유율 1위

![](https://velog.velcdn.com/images/sw_smj/post/51420dc4-44af-484f-b6b3-8f9e71cfe494/image.png)

- 대용량 DB 다루는 데에 있어, 최고의 성능을 보임

- **분산 처리**를 통해 효율성이 매우 높음

- **대규모의 DB**와 **영역 관리**에 유리 :  고가의 HW를 효율적으로 사용하도록 **영역 사용을 완벽히 제어**

- **다중 동시 데이터베이스 사용자 지원**

- 고성능의 트랜잭션 처리 가능

- 많은 기능으로 초보자에게는 어려움

- 유료


<br><br>


## PostgreSQL



![](https://velog.velcdn.com/images/sw_smj/post/78bfd86d-4cd7-40e2-b4ad-4bae950a9eb9/image.png)

- 대용량 데이터 처리를 위한 기능이 있음

- DB 보안을 위해 데이터 암호화, 접근 제어, 접근 감시 세 가지로 구성되어 있음

- 신뢰성과 안정성이 매우 높음

- 오픈소스 - 무료로 사용 가능

- Instagram, CISCO, Skype, TripAdvisor, IKEA 등에서 사용





