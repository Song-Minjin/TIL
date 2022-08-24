## 스프링 시큐리티 사용시 로그인
- 클라이언트의 요청은 모두 Spring Security를 거침
- Spring Security는 인증/인가의 역할을 함
    - 성공시 : Controller로 Client 요청+사용자 정보 전달
    - 실패시 : Controller로 전달 보내지 않고, Client에게 Error Response 보냄

<br>

## 로그인 처리 과정

![](https://velog.velcdn.com/images/sw_smj/post/c31791c2-dd2d-44d4-983c-c57a95a52303/image.png)

- Authentication Manager : 세션 ID도 발급해줌

- Authentication Manager & UserDetails Service : 스프링 시큐리티에서 저장해줌

<br>


## 로그아웃 처리 과정
- **"GET /user/logout"** 요청 시 로그아웃
- 서버 세션에 저장되어 있는 로그인 사용자 정보 삭제

- 로그아웃 시에는 기본적으로 POST로 처리 필요
    - CSRF protection이 기본적으로 enable 되어있기 때문
    - CSRF protection을 disable하면 GET으로도 사용 가능

