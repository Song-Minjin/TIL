# HttpEntity



: HTTP 요청(Request)과 응답(Response)의 HttpHeader와 HttpBody를 포함하는 클래스

- Spring Framework에서 제공하는 클래스이다.

<br>

```java
public class HttpEntity<T> {

	private final HttpHeaders headers;

	@Nullable
	private final T body;
}
```

<br>

## ResponseEntity



: HttpEntity 클래스를 상속받았으며, 사용자의 HttpRequest에 대한 응답 데이터를 포함하는 클래스

```java
public ResponseEntity(HttpStatus status) {
	this(null, null, status);
}
```

이처럼 상태코드만 받을 수 있는 생성자가 있으며,

```java
public ResponseEntity(@Nullable T body, HttpStatus status) {
	this(body, null, status);
}
```

상태코드(Status), 헤더(headers), 응답 데이터(ResponseData)를 담는 생성자도 존재한다.

### ResponseEntity 예제

```java
@Transactional
public ResponseDto<?> login(LoginRequestDto requestDto, HttpServletResponse response) {
	Member member = isPresentMember(requestDto.getNickname());

    ...


	TokenDto tokenDto = tokenProvider.generateTokenDto(member);
    tokenToHeaders(tokenDto, response);

    return ResponseDto.success(
        MemberResponseDto.builder()
            .id(member.getId())
            .nickname(member.getNickname())
            .build()
  	);
}
```

```java
  return new ResponseEntity<MoveResponseDto>(moveResponseDto, headers, HttpStatus.valueOf(200));
```

```java
return ResponseEntity.ok()
      .headers(headers)
      .body(moveResponseDto);
```
