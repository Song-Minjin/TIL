# Mock vs MockBean

### 공통점

- 둘 다 가짜객체이며, 테스트 스텁의 한 종류이다.

- given, when, verify 등을 사용하여 행위를 테스트한다.


### 차이점

- MockBean은 가짜 Bean을 스프링에 등록하는 것이다.

    - 스프링 컨테이너가 기존에 갖고 있는 Bean 객체는 MockBean 객체로 치환되어 DI에 사용된다.


- Mock은 가짜 객체를 만들지만, 스프링 빈에 등록이 안되는 객체이다.

    - 스프링 컨테이너가 DI를 하는 방식이 아니라, 객체 생성 시에 생성자에 Mock 객체를 직접 주입해준다.

    - 생성자 주입을 사용해야 편하게 사용할 수 있다.

    - 스프링을 띄우지 않으므로, MockBean을 사용할 때보다 빠르다.

<br>

# Mockito 모듈

예를 들어 API 요청/응답에 대해서만 테스트를 한다면, Controller만 Bean으로 등록하고 Service는 Bean으로 등록하지 않음으로써 Controller와 Service의 의존을 끊을 수 있다. 이로 인해 Controller만 테스트만 진행하는 것이 가능해진다.