지난 번 스타터를 활용하여 Spring Boot 초기 설정을 하면서, Spring의 라이브러리를 함께 다운로드 받았다.

- Spring boot에서 오른쪽의 작은 코끼리 모양 (Gradle) 탭을 누르면 Dependencies에서 현재 내가 다운로드 받은 라이브러리들을 확인할 수 있다.


- 자신이 선택한 라이브러리 개수보다 훨씬 많은 수의 라이브러리가 다운로드 된다.

  - 한 라이브러리를 선택하면, 그 라이브러리와 서로 의존관계가 있는 라이브러리들을 함께 가져오기 때문이다.

- 라이브러리들도 처음부터 무작정 외울 필요 없이 프로젝트를 하다 보면 자연스럽게 감을 잡을 수 있다고 한다. 따라서 우선은 큰 흐름만 알고 가면 된다.

<br>

웹 개발을 하면서 주로 사용하는 Spring의 라이브러리들을 큼직하게 몇 가지만 뽑아보자면 다음과 같다.

<br>

## Spring boot Libraries


- **`spring-boot-starter-web`**
    - `spring-boot-starter-tomcat` : 톰캣(웹서버)
    - `spring-webmvc` : 스프링 웹 MVC
      <br>

- **`spring-boot-starter-thymeleaf`** : 타임리프 템플릿 엔진 (View)
  <br>
- **`spring-boot-starter(공통)`** : 스프링 부트 + 스프링 코어 + 로깅<br>
    - **`spring-boot`**
        - `spring-core`
          <br>
    - **`spring-boot-starter-logging`** : 로깅 관련
        - `logback`	: 성능이 빠르고 지원하는 기능이 좋음
        - `slf4j` : 인터페이스 (실제 로그를 구현체로 출력)
          *👉🏻 요즘 트렌드로는 로깅 관련해서 이 두 조합을 많이 씀. 표준이라고 봐도 무방*

<br>

## Test Libraries

- **`spring-boot-starter-test`**<br>

    - **`junit`** : 테스트 프레임워크
      <br>

    - `mockito` : 목 라이브러리
      <br>
    - `assertj` : 테스트코드를 좀 더 편하게 작성
      <br>
    - `spring-test` : 스프링 통합 테스트 지원<br>