# 1. Controller


: 프론트와 소통하는 창구

- 클라이언트의 요청(Request)을 전달받는 코드

- 요청(Request)/응답(Response)를 처리함

> 💡 **클라이언트 단의 작업을 수행하는 부분!**

<br>

## RestController


: JSON 형식만을 돌려주는 Controller

- Rest : 서버의 응답이 JSON 형식임을 나타냄
- HTML, CSS 등을 주고 받을 때에는 Rest를 붙이지 않는다.

```java
@RestController
public class PostController {
	
    @GetMapping("/posts")
    public Post getPosts() {
    	Post post = new Post();
        post.setTitle();
        post.setAuthor();
        post.setDatetime();
        return post;
    }
}
```
- **`@GetMapping`**
    - 브라우저에서 주소를 치는 행위 = GET 방식으로 정보를 요청하는 것
    - 스프링 주소 뒤의 주소가 위의 코드를 예시로 들면 `/posts`일 때, getPost 메소드를 실행함




<br>


# 2. Service


: 중간 부분

- 실제 중요한 작동이 많이 일어나는 부분

> 💡 즉, 요청 / 응답 보내는 부분은 Controller가, DB 만지는 쪽은 Repository가, **나머지 부분**은 거의 모두 Service에서 처리하는 것이라고 보면 됨!!!


<br><br>

# 3. Repository


: DB와 소통하는 창구

> ** 서버 - DB 사이의 작업을 수행하는 부분!**
