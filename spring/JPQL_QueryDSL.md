# Spring Data JPA



**: spring framework에서 JPA를 편리하게 사용할 수 있도록 지원하는 프로젝트**

- CRUD 처리를 위한 공통 인터페이스 제공

- repository 개발시 인터페이스만 작성하면 실행 시점에 Spring Data JPA가 구현 객체를 동적으로 생성해서 주입

- 데이터 접근 계층을 개발할 때, 구현 클래스 없이 인터페이스만 작성해도 개발을 완료할 수 있도록 지원

- 공통 메소드는 `count`, `delete`, `deleteAll`, `deleteById`, `existsById`, `findById`, `save` ..
> 🔗 **참고**
> Spring Data JPA 링크 : https://docs.spring.io/spring-data/jpa/docs/current/api/org/springframework/data/jpa/repository/JpaRepository.html

<br><br>

# JPQL


**: 객체지향 쿼리**

Spring Data JPA가 기본적으로 제공해주는 CRUD 메소드 및 쿼리 메소드 기능을 사용 하더라도, 딱 원하는 데이터만을 수집하기 위해서는 필연적으로 JPQL을 작성하게 된다.

- JPA를 사용하면 Entity 객체를 중심으로 개발을 하게 되는데, 문제는 검색을 할 때에도 테이블이 아닌 Entity 객체를 대상으로 검색을 해야 한다는 것이다.

- 이때, 모든 DB 데이터를 객체로 변환해서 검색하는 것은 불가능하다. 필요한 데이터만 DB에서 불러오려면 결국 검색 조건이 포함된 SQL이 필요하기 때문!

- 따라서 JPA는 SQL을 추상화한 JPQL이라는 객체지향 쿼리 언어를 제공한다.

- SQL과 문법이 유사하고, `SELECT`, `FROM`, `WHERE`, `GROUP BY`, `HAVING`, `JOIN` 등을 지원한다.

- **JPQL**은 Entity 객체를 대상으로 쿼리를 질의하고, **SQL**은 DB 테이블을 대상으로 쿼리를 질의한다는 것이 차이점이다.


<br><br>

# QueryDSL



**: 정적 타입을 이용해서 SQL 등의 쿼리를 생성해주는 프레임워크**

> 📌 **왜 필요한가?**
>
> 위의 JPQL을 활용할 때에, 간단한 로직을 작성하는 데에는 큰 문제는 없지만 복잡한 로직의 경우 개행을 포함한 쿼리 문자열의 길이가 상당히 길어진다.
>
> 심지어 JQPL 문자열에 오타 혹은 문법적인 오류가 존재하는 경우, 정적 쿼리라면 로딩 시점에 이를 발견할 수는 있지만 그 외에는 런타임 시점에서 에러가 발생한다.
>
> 이러한 문제점을 해소하는 데에 기여하는 프레임워크가 QueryDSL이다.


### 장점

- 문자가 아닌 코드로 쿼리를 작성함으로써, 컴파일 시점에 문법 오류를 쉽게 확인할 수 있다.

- 자동완성 등 IDE의 도움을 받을 수 있다.

- 동적인 쿼리 작성이 편리하다.

- 쿼리 작성시 제약 조건 등을 메소드 추출을 통해 재사용할 수 있다.

> 💡 **주의**
>
> QueryDSL을 사용하기 위해서는 다소 번거로운 Gradle 설정 및 사용법 등을 익혀야 한다는 단점이 있다. 그러나 JPQL이 익숙한 경우에는 QueryDSL을 이해하는 데에 큰 어려움은 없을 것이다.

