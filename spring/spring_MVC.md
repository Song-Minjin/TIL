# MVC



: Model-View-Controller 디자인패턴

- 디자인 패턴의 일종

- 이때, 서버에서 HTML을 어떻게 내려주는가(정적/동적)에 따라 MVC의 동작 원리에 차이가 있다.

<br>

### 정적 웹페이지
![](https://velog.velcdn.com/images/sw_smj/post/98a843f6-dc6a-4122-ae5a-75964df0f5aa/image.png)

- **Controller** : Client의 요청을 Model로 받아 처리함 (ex: 회원가입을 위한 개인정보 - id, pw, name)
- **View** : Controller가 클라이언트한테 내려주는 정적 웹페이지(HTML)

<br>

### 동적 웹페이지

![](https://velog.velcdn.com/images/sw_smj/post/82042620-13b6-48b0-a7c8-992a9bb51f02/image.png)

- **Controller** : Client의 요청을 Model로 받아 처리. Template Engine에게 View, Model을 전달한다.


- **Template Engine** : View에 Model을 적용하는 역할 (➡ 동적 웹페이지 생성)
    - ex) 로그인 성공시 로그인된 사용자의 id를 페이지에 추가
    - 종류
        - Thymeleaf(타임리프)
        - Groovy
        - FreeMarker
        - Jade
        - JSP (단, 스프링에서 추천하지는 않고 있음)

- **View** : 동적 HTML파일

- **Model** : View에 적용할 정보들

<br><br>

# 스프링 MVC 동작원리

> 💡 @Controller는 스프링 서버 개발자 입장에서는 시작점과 끝점으로 보이지만, 사실 스프링이 뒤에서 많은 부분을 보이지 않게 처리해 주고 있다.

![](https://velog.velcdn.com/images/sw_smj/post/d24f94fa-c222-4e36-b008-c9fb086c7828/image.png)

**1. Client → DispatcherServelet**
- 가장 앞 단에서 요청을 받아 FrontController 라고도 불림

<br>

**2. Handler mapping**
- Handler mapping에는 API path와 Controller함수가 매칭되어 있음

- *Sample*
    - GET /hello/html/dynamic → `HomeController` 의 `helloHtmlFile()` 함수
    - GET /user/login → `UserController` 의 `login()` 함수
    - GET /user/signup → `UserController` 의 `signup()` 함수
    - POST /user/signup → `UserController` 의 `registerUser()` 함수


<br>

**3. DispatcherServelet → Controller**

- API 를 처리해 줄 Controller를 찾아 요청을 전달


- Controller에서 요청하는 Request의 정보(Model) 전달
   ```java
   @Controller
   public class ItemSearchController {
	       @GetMapping("/api/search")
        @ResponseBody
        public List<ItemDto> getItems(@RequestParam String query) {
			// ...
	 	}
   }
   ```

<br>

**4. Controller → DispatcherServelt**
> 💡 **주의!**
>
> `@ResponseBody` 활용하여 Json 형식 리턴하는 경우에는 ➡ Model과 View를 전달해주지는 않음

- HTML을 내려주는 경우, Model과 View 전달해줌

- Controller 가 Client 으로 받은 API 요청을 처리

<br>

**5. ViewResolver**
- Template Engine : View랑 Model을 합치기. 즉, View에 Model을 적용해줌

<br>

**6. DispatcherServelet → Client**
- View를 Client에게 응답