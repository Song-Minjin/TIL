# HTTP 기본 인증 방식 3. 토큰(JWT) 기반 인증 방식

> 모바일/웹의 인증을 책임지는 또 다른 대표주자

- JSON 객체를 사용해 정보를 안정성 있게 전달하는 웹 표준
- 사용자는 Access Token(JWT 토큰)을 HTTP 헤더에 실어 서버로 보냄

<br>

## JWT
> JSON Web Token
> = 인증에 필요한 정보들을 암호화시킨 토큰

![](https://velog.velcdn.com/images/sw_smj/post/8aad2528-7924-4900-8203-6b27790332c2/image.png)

###### ▲ jwt.io 사이트에서 확인할 수 있는 암호화된 토큰

<br>

## 토큰의 구성요소
📌 `토큰` = Encoded `Header` + `.` + Encoded `Payload` + `.` + `Verify Signature`
- `Header` : 암호화할 방식(alg), 타입(type) 등
- `Payload` : 서버에 보낼 데이터. (ex: 유저의 고유 ID값, 유효기간 등)
- `Verify Signature` : Base64방식으로 인코딩한 Header, payload 그리고 SECERT KEY를 더한 후 서명됨


> **❓ 토큰은 전체가 다 암호화되어 있나요?**
>    👉🏻 NO!
> - `Header`, `Payload` : 인코딩될 뿐(16진수로 변경), 따로 암호화되지 않음 ⇒ JWT 토큰에서 Header, Payload는 누구나 디코딩하여 확인 가능.
> - `Verify Signature` : Secret KEY를 알지 못하면 복호화할 수 없음 (즉, 다른 사용자가 Payload의 ID를 조작하여 보내도, Verify Signature가 일치하지 않기에 유효하지 않은 토큰으로 간주됨)

<br><br>

## JWT 기반 인증 과정
1. 클라이언트에서 로그인 <br>
  <br>
2. 서버에서는 계정정보를 읽어 사용자 확인 → 사용자의 고유한 ID값 부여 → 기타 정보와 함께 Payload에 넣음 <br>
   <br>
3. JWT 토큰의 유효기간 설정 <br>
   <br>
4. 암호화할 SECRET KEY를 이용해 ACCESS TOKEN 발급 <br>
   <br>
5. 클라이언트가 Access Token을 받아 저장 → 인증이 필요한 요청마다 토큰을 헤더에 실어 보냄 <br>
   <br>
6. 서버에서는 받은 토큰의 Verify Signature를 SECRET KEY로 복호화 → 조작 여부, 유효기간 확인 <br>
   <br>
7. 검증 완료 → Payload를 디코딩 → 사용자의 ID에 맞는 데이터를 가져옴

<br>

> ### 💡 **쿠키/세션 방식과 가장 큰 차이**
> - **세션/쿠키** : 세션 저장소에 유저의 정보를 넣음<br>
> <br>
> - **JWT** : 토큰 안에 유저의 정보를 넣음
> 

<br>
물론 이는 클라이언트 입장에서는 HTTP 헤더에 세션 ID/토큰을 실어 보내는 것으로 유사하지만, 서버 입장에서는 인증을 위해 암호화를 할 것인가 / 별도의 저장소를 이용할 것인가로 차이가 있다.


<br><br>

## JWT 방식의 장점
- **간편함** : 세션/쿠키와 달리 별도의 저장소가 필요하지 않음
- **<span style='background-color:#fff5b1'>Stateless</span>한 서버를 만들기 적합** : JWT는 발급 후 검증만 하면 됨
  <span style='color:#808080'>*Stateless : 어떠한 별도의 저장소도 사용하지 않는, 즉 상태를 저장하지 않는 것 ⇒ 서버 확장/유지,보수에 유리함</span>
- **뛰어난 확장성** : 토큰 기반으로 하는 다른 인증 시스템에 접근 가능

<br><br>

## JWT 방식의 단점
- **이미 발급된 JWT에 대해서는 돌이킬 수 없음**<br>

  세션/쿠키의 경우, 만일 쿠키가 악의적으로 이용될 시 해당 세션을 삭제해버리면 된다. 하지만 JWT는 한 번 발급되면 유효기간 만료까지는 계속 사용이 가능하다.
  <br>
  > 👉🏻 **해결책** : 기존 Access Token의 유효기간을 짧게 하고, Refresh Token이라는 새로운 토큰을 발급한다.
<br>

- **제한적인 Payload 정보**<br>

  Payload는 따로 암호화되지 않기 때문에 유저의 중요한 정보는 담을 수 없음<br>
  <br>

- **긴 JWT의 길이 → 서버 자원 낭비 발생**
  <br>
  세션/쿠키 방식에 비해 길이가 김 → 인증이 필요한 요청이 많아질수록 서버의 자원 낭비 발생