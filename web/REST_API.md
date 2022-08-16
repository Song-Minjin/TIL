# API
**Application Programming Interface**

- 클라이언트-서버 간의 약속

- 클라이언트가 정한 대로 서버에게 요청(Request)을 보내면, 서버가 요구사항을 처리하여 응답(Response)을 반환함

<br>

# REST


: 주소에 명사, 요청 방식에 **동사**를 사용함으로써 의도를 명확히 드러냄

- **동사** : 생성(POST), 조회(GET), 수정(PUT/PATCH), 삭제(DELETE)를 지칭

### 예시
- `GET /posts`
  → 강의 전체 목록 조회 요청

- `GET /posts/1`
  → ID가 1번인 녀석 조회 요청

- `POST /posts`
  → 강의 생성 요청

- `PUT /posts/3`
  → ID가 3번인 녀석 수정 요청

- `DELETE /posts/2`
  → ID 2번인 녀석 삭제 요청
  <br>

### 주의사항 (컨벤션)
- URI에 들어가는 명사들은 복수형을 사용한다.
  `/post` (X)

- URI에는 가급적 사용하지 않는다.
  `/accounts/edit` (X)


