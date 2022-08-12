# Java IDE
- 요즘은 큰 IT 서비스 회사 중에는 Intellij를 많이 쓴다.
- 단축키 등 다양한 편리한 기능이 eclipse보다 잘 마련되어있다는 것이 큰 장점이다.

<br><br>

# Spring boot 초기 설정하기

- 예전에는 스프링 프로젝트를 밑바닥부터 하나씩 다 만들었다.

- 그러나 요즘 스프링 프로젝트는 스프링 부트를 이용해서 만든다!

- 스프링 부트 스타터 페이지 : https://start.spring.io

<br><br>

👉🏻 다음은 Spring boot의 초기 설정 관련 용어들이다.


## Maven vs Gradle


: 필요한 라이브러리를 가져오고, Build된 Life Cycle를 관리해주는 툴

- **`Maven`** : 과거에 많이 씀. 아직 레거시 프로젝트 등은 Maven으로 남아있는 경우도 있음

- **`Gradle`** : 최근에는 Gradle로 많이 넘어오는 추세. 심지어 스프링 라이브러리 자체도 예전엔 Maven이었지만 Gradle로 넘어옴


<br><br>

## Spring Boot version

- **`SNAPSHOT`** : 아직 만들고 있는 버전

- **`M1`, `M4`** 등 : 아직 정식 Release되지 않은 버전


<br><br>


## Project Metadata

- **`Group`** : 보통 기업명, 기업 도메인 명 등을 작성

- **`Artifact`** : Build되어 나올 때 결과물. 즉, 프로젝트 명이라고 생각하면 된다.


<br><br>


## Dependencies


: Spring boot로 프로젝트를 시작할 건데, 그 중 어떤  library를 가져와서 쓸까?를 정하는 항목

- **Spring Web : 웹 프로젝트를 만들 때 선택


- **`Thymeleaf`** : HTML을 만들어주는 다양한 Template Engine 중 하나. (이는 필수는 아님 - 회사마다 다양한 엔진을 사용한다.)
