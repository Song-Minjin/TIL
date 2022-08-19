# REST API의 endpoint 설계 방식

상황에 따라 Path parameter와 Query string을 통해 통신할 수 있다. (두 가지 다 데이터 중심으로 요청, 반환이 이루어진다!)

## 1. Path parameter 이용하기

### Path Parameter란?
= Path Variable (자주 혼용)

- 필요한 상황과 내가 원하는 정보에 따라 URI를 다르게 요청하는 방식

- 데이터를 넘기는 방법 중 하나로, 경로를 변수로서 사용하는 방법

- 한 URI 내에서도 메소드별로 주고 받는 데이터의 Request body, Response body가 다르다. 따라서 같은 URI, 같은 path param을 쓰더라도 같은 API라는 보장은 절대 없음!



### 예시

- `GET /posts/{id}`  : 이러한 형식으로, {id} 부분에 해당 데이터의 ID를 넣는다

- `GET /posts` → 강의 전체 목록 조회 요청

- `GET /posts/1` → ID가 1번인 녀석 조회 요청

- `GET /posts/1/comments` → ID가 1번인 녀석의 댓글 조회 요청

- `POST /posts` → 강의 생성 요청

- `PUT /posts/3` → ID가 3번인 녀석 수정 요청

- `DELETE /posts/2` → ID 2번인 녀석 삭제 요청



<br>

## 2. Query string 이용하기

### Query String이란?



: URL의 뒤에 입력 데이터를 함께 제공하는 가장 단순한 데이터 전달 방법

- URL의 끝에 `?`와 함께 key-value값을 가지는 요청 파라미터

- URL에 조회조건을 표시하기 때문에 특정 페이지를 링크하거나 북마크할 수 있음
- 클라이언트가 어떤 특정 리소스에 접근하고 싶어하는지에 대한 정보를 담음


### 사용 방법
- 정해진 엔드포인트 주소 이후 `?`를 쓰는 것으로 쿼리스트링이 시작
- `parameter = value` 형식으로 필요한 파라미터의 값을 적음
- 파라미터가 여러 개일 경우 `&`를 붙여 여러 개의 파라미터를 넘김
- `=`로 `key`와 `value`가 구분됨

### 예시

- `GET /posts?ordering=-id` → DB 내 데이터를 역순으로 호출하여 보여줌

- `GET /posts?offset=0&limit=100` → 0부터 100개까지 범위 지정 (pagination 등에 사용)


<br><br>



> 💡 **두 방식 비교**
> - **`Path parameter`** : 정제되지 않은 데이터를 호출해옴
    > &nbsp;&nbsp;&nbsp;👉🏻 resource 식별에 적절!
    >    <br>
> - **`Query string`** : 좀 더 복잡한 조건을 줘서 내가 원하는 정제된 결과물을 얻을 수 있음
    > &nbsp;&nbsp;&nbsp;👉🏻 filtering, sorting, searching에 적절!
