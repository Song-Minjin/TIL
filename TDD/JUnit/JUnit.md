# JUnit



: 단위 테스트 작성을 위한 산업 표준 Framework

<br>

## JUnit 5



: **JUnit Platform** + **JUnit Jupiter** + **JUnit Vintage**가 합쳐진 프레임워크 (Java8부터 사용 가능)

### JUnit 5의 모듈 구성

![](https://velog.velcdn.com/images/sw_smj/post/7c0db74e-2f37-42f2-b208-b33c2acaebec/image.png)


- **JUnit Platform** : 테스팅 프레임워크를 구동하기 위한 launcher와 테스트 엔진을 위한 API를 제공한다. Test Engine API로 테스트 프레임워크 개발 가능

- **JUnit Jupiter** : JUnit 5를 위한 테스트 API와 실행 엔진을 제공한다.

- **JUnit Vintage** : JUnit 3과 4로 작성된 테스트를 JUnit 5 Platform에서 실행하기 위한 모듈을 제공한다.