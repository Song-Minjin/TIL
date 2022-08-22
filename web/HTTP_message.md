# HTTP 메시지

- Server와 Client간 데이터가 교환되는 방식

- 메시지 타입은 두 가지 : Request, Response

- Client와 Server 간의 Request, Response는 HTTP 메시지 규약을 따른다.

> 💡 **Tip**
>
> HTTP 메시지는 웹 서비스 개발자(백/프론트엔드)에게 매우 중요하다.

<br>

## HTTP 메시지의 특징

- ASCII로 인코딩된 텍스트 정보이며, 여러 줄로 되어있음

- HTTP 프로토콜 초기 버전과 HTTP/1.1에서는 클라이언트와 서버 사이의 연결을 통해 공개적으로 전달됨. 사람이 읽을 수 있었음

- HTTP/2에서는 최적화와 성능 향상을 위해 HTTP 프레임으로 나뉨

- HTTP 메시지는 거의 손수 텍스트로 개발자가 작성하지는 않는다. 대신, 소프트웨어, 브라우저, 프록시 또는 웹 서버가 그 역할을 한다.

- HTTP 메시지는 설정파일(프록시 혹은 서버), API(브라우저) 혹은 다른 인터페이스를 통해 제공됨

- HTTP/2이 이진 프레이밍 메커니즘(binary framing mechanissm)은 사용중인 API나 설정 파일 등을 변경하지 않아도 됨 ➡ 사용자가 보고 이해하기 쉬움

<br>

## HTTP 메시지의 구조

1. **시작줄(start-line)** : 실행되어야 할 요청 또는 요청 수행에 대한 성공/실패가 기록됨. 이 줄은 한 줄로 끝남

2. **HTTP 헤더 세트**(옵션) : 요청에 대한 설명 혹은 메시지 본문에 대한 설명

3. **빈 줄(blank line)** : 요청에 대한 모든 메타 정보가 전송되었음을 알림

4. **본문** : 요청에 관련된 내용(옵션 : HTML 폼 콘텐츠), 응답과 관련된 문서 (document). 본문의 존재 유무 및 크기는 첫줄과 HTTP 헤더에 명시됨

> 👉🏻 **용어 정리**
> - **Request Head** : HTTP 메시지의 시작줄 + HTTP 헤더
> 
> - **Body** : HTTP 메시지의 페이로드

<br>

## Request (요청)

### Start-line
```
GET velog.io HTTP/1.1
```


### Header



: 메타정보를 보내는 부분
- **Content Type** (옵션)
- 없음
- HTML `<form>` 태그로 요청시
    ```html
    Content type: application/x-www-form-urlencoded
    ```
- AJAX 요청
    ```ajax
    Content type: application/json
    ```

    > 💡 **Tip**
    > 
    > header에는 다양한 것이 들어갈 수 있지만, 오늘은 content-type만 알고 넘어가자.


### Body



: 클라이언트가 정보를 담아 보내는 부분

- **`GET` 요청** : 보통 없음


- **`POST` 요청** : 보통 사용자가 입력한 폼 데이터

    - HTML `<Form>`
  ```html
  name=홍길동&age=20
  ```
    - AJAX
  ```ajax
  {
      "title":"김영희의 TIL",
      "author":"김영희",
      "content":"이것은 글 내용",
      "password":"1234"
  }
  ```

  <br>

## Response(응답)

### Start-line



: 상태줄. API 요청 결과 (상태 코드, 상태 텍스트)
```
HTTP/1.1 404 Not Found
```


### Header



: 메타정보를 보내는 부분

- **Content Type** (옵션)
    - 없음
    - Response 본문 내용이 HTML인 경우
      ```
      Content type: text/html
      ```
    - Response 본문 내용이 JSON인 경우
      ```
      Content type: application/json
      ```
- **Location**
  : Redirect할 페이지 URL
  ```
  Location : http://localhost:8080/hello.html
  ```


### Body
- HTML `<Form>`
  ```html
<!DOCTYPE html>
   <html>
     <head><title>By @ResponseBody</title></head>
     <body>Hello, Spring 정적 웹 페이지!! </body>
   </html>
   ```

- JSON
  ```ajax
  { 
      "name":"홍길동",
      "age": 20
  }
  ```