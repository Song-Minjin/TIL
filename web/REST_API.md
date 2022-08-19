# API
**Application Programming Interface**

- 클라이언트-서버 간의 약속

- 클라이언트가 정한 대로 서버에게 요청(Request)을 보내면, 서버가 요구사항을 처리하여 응답(Response)을 반환함

<br>

# REST

- REST : 프로토콜이나 표준이 아닌, 아키텍처 원칙 세트
- 구성 요소
  - 자원(Resource) : HTTP URI
  - 자원에 대한 행위(Verb) : HTTP Method
  - 자원에 대한 행위의 내용 (Representations) : HTTP Message Pay Load

<br>

# REST API

**Representational State Transfer (=RESTful API)**

- 웹 데이터 전송 방식 중 하나

- 웹에 존재하는 모든 자원에 고유한 이름(***URI***)를 부여하여 해당 자원에 대한 주소를 부여하는 것. 해당 자원의 상태를 주고 받는다.
  > **URI**
  > : Uniform Resource Identifier = 통합 자원 식별자<br>

- 웹 서비스를 만드는 데에 사용되는 REST 아키텍처의 제약조건을 모두 만족해서 만들면 RESTful하다고 말할 수 있다.

> 👉🏻 **제약조건 및 RESTful한 API 동작 방식**
>
> 1. **HTTP URI**를 통해 자원(Resource)을 명시하고
> 2. **HTTP METHOD** (GET, POST, PUT/PATCH, DELETE)를 통해
> 3. 해당 자원(URI)에 대한 **CRUD Operation**을 적용하는 것
     > +. 필요한 정보와 status code를 client server로 응답 보냄
     > ![](https://velog.velcdn.com/images/sw_smj/post/6f5fbebe-fd16-4759-a981-2b2957642c1e/image.png)

> **응답 상태 코드 (Status Code)**
> - 1xx : 전송 프로토콜 수준의 정보 교환
> - 2xx : 클라어인트 요청이 성공적으로 수행됨
> - 3xx : 클라이언트는 요청을 완료하기 위해 추가적인 행동을 취해야 함
> - 4xx : 클라이언트의 잘못된 요청
> - 5xx : 서버쪽 오류로 인한 상태코드

<br>

> 💡 **REST vs RESTful**<br>
> RESTful = REST의 설계규칙을  지켜서 설계된 API를 RESTful하다고 한다. 즉, REST의 원리를 잘 지키는 시스템이라는 뜻!
> - 이해하기 쉽고 사용하기 쉬운 REST API를 만드는 것이 목적
> - 만약 성능이 중요한 상황이라면 굳이 RESTful한 것에만 집중하지 않아도 됨

<br><br>


## REST API Rules

### 주의사항 (컨벤션)
- URI에 들어가는 명사들은 복수형을 사용한다.
  `/post` (X)

- URI에는 가급적 사용하지 않는다.
  `/accounts/edit` (X)

- 슬래시(/)로 계층관계를 표현한다.

- URL 마지막 문자로 슬래시(/)를 포함하지 않는다.

- 언더바(_)를 사용하지 않고, 하이픈(-)을 사용한다.

- URI는 소문자로만 구성한다.

- HTTP 응답 상태코드를 사용한다.

- 파일 확장자는 URI에 포함하지 않는다.
  `https://velog.velcdn.com/images/sw_smj.jpg` (X)


<br><br>

## REST API의 특징

###  1. Server-Client(서버-클라이언트 구조)
- 클라이언트, 서버 및 리소스로 구성되었으며 요청이 HTTP를 통해 관리되는 아키텍처


### 2. Stateless(무상태)
- 요청 간에 클라이언트 정보가 저장되지 않음
- 각 요청이 분리되어있어 서로 연결되어있지 않음

### 3. Cacheable(캐시 처리 가능)
- 클라이언트-서버 상호작용을 간소화함

### 4. Layered System(계층화)
- 요청된 정보를 검색할 때 관련된 서버의 각 유형을 클라이언트가 볼 수 없는 계층 구조로 체계화된 계층 시스템

### 5. Uniform Interface(인터페이스 일관성)
- 정보가 표준 형식으로 전송되도록 하기 위한 구성 요소 간 통합된 인터페이스
  - 요청된 리소스가 식별가능
  - 요청된 리소스가 클라이언트에 전송된 표현과 분리됨
  - 수신한 표현을 통해 클라이언트가 리소스를 조작할 수 있음
  - 클라이언트에 반환되는 self-descriptive 메시지에 클라이언트가 정보를 어떻게 처리해야 할지 설명하는 정보가 충분히 포함되어야 함
  - 하이퍼미디어 : 클라이언트가 하이퍼링크를 통해 현재 수행 가능한 기타 모든 작업을 찾을 수 있어야 함

<br><br>


## REST의 장점

- HTTP 프로토콜의 인프라를 그대로 사용 ➡ REST API 사용을 위한 별도의 인프라 구축 불필요

- HTTP 프로토콜의 표준을 최대한 활용 ➡ 여러 추가 장점을 함께 가져갈 수 있도록 함

- HTTP 표준 프로토콜에 따르는 모든 플랫폼에서 사용 가능

- Hypermedia API의 기본을 충실히 지키면서 범용성 보장

- REST API 메시지가 의도하는 바를 명확히 나타냄 ➡ 의도하는 바를 쉽게 파악 가능

- 여러 가지 서비스 디자인에서 생길 수 있는 문제 최소화

- 서버-클라이언트의 역할을 명확히 분리

<br><br>

## REST의 단점

- 표준이 자체적으로 존재하지 않아 정의가 필요함

- 사용할 수 있는 메소드가 4가지밖에 없음

- HTTP Method 형태가 제한적임

- 브라우저를 통해 테스트할 일이 많은 서비스라면, 쉽게 고칠 수 있는 URL보다 Header 정보의 값을 처리해야 함 ➡ 전문성이 요구됨

- 구형 브라우저에서 호환 되지 않음 ➡ 지원해주지 못하는 동작이 많음


<br><br>


---

**참고자료**

- https://velog.io/@haileeyu21/Session-RESTful-API-%EB%9E%80-Path-parameters-Query-string

- https://gmlwjd9405.github.io/2018/09/21/rest-and-restful.html
