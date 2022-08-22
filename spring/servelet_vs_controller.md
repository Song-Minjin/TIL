실제로, 기업 중에는 스프링을 사용하지 않고도 서블릿을 활용하여 개발하는 경우가 있다.

## Webservelet

실제로 servelet 코드를 실행시켜보면, controller 없이도 webservelet이 제 기능을 다하는 것을 확인할 수 있다.

![](https://velog.velcdn.com/images/sw_smj/post/8b1e93cb-1bb6-4f93-a61f-e4f564987bea/image.png)

위의 그림에 해당하는 Servelet 클래스는 다음과 같다.

```java
@WebServlet(urlPatterns = "/api/search")
public class ItemSearchServlet extends HttpServlet {

    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws IOException {
        // 1. API Request 의 파라미터 값에서 검색어 추출 -> query 변수
        String query = request.getParameter("query");

        // 2. 네이버 쇼핑 API 호출에 필요한 Header, Body 정리
        RestTemplate rest = new RestTemplate();
        HttpHeaders headers = new HttpHeaders();
        headers.add("X-Naver-Client-Id", "zdqMoIkFaK8uKvC2oNY2");
        headers.add("X-Naver-Client-Secret", "LiZfsgtuD5");
        String body = "";
        HttpEntity<String> requestEntity = new HttpEntity<>(body, headers);

        // 3. 네이버 쇼핑 API 호출 결과 -> naverApiResponseJson (JSON 형태)
        ResponseEntity<String> responseEntity = rest.exchange("https://openapi.naver.com/v1/search/shop.json?query=" + query, HttpMethod.GET, requestEntity, String.class);
        String naverApiResponseJson = responseEntity.getBody();

        // 4. naverApiResponseJson (JSON 형태) -> itemDtoList (자바 객체 형태)
        //  - naverApiResponseJson 에서 우리가 사용할 데이터만 추출 -> List<ItemDto> 객체로 변환
        ObjectMapper objectMapper = new ObjectMapper()
                .configure(DeserializationFeature.FAIL_ON_UNKNOWN_PROPERTIES, false);
        JsonNode itemsNode = objectMapper.readTree(naverApiResponseJson).get("items");
        List<ItemDto> itemDtoList = objectMapper
                .readerFor(new TypeReference<List<ItemDto>>() {})
                .readValue(itemsNode);

        // 5. API Response 보내기
        //  5.1) response 의 header 설정
        response.setContentType("application/json");
        response.setCharacterEncoding("UTF-8");
        //  5.2) response 의 body 설정
        PrintWriter out = response.getWriter();
        //     - itemDtoList (자바 객체 형태) -> itemDtoListJson (JSON 형태)
        String itemDtoListJson = objectMapper.writeValueAsString(itemDtoList);
        out.print(itemDtoListJson);
        out.flush();
    }
}
```

#### Step 1.

이를 조금씩 뜯어보면, 우선 처음에는 GET Request에 대한 내용을 정의하고 있다.
```java
@Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws IOException {
        // 1. API Request 의 파라미터 값에서 검색어 추출 -> query 변수
        String query = request.getParameter("query");
```
#### Step 2.

그리고, 그림에서 보면 웹 서버 내에서, 즉 서버에서 서버로 보내는 과정이 있는데 이는 RestTemplate에 해당하는 부분이다.

```java
// 2. 네이버 쇼핑 API 호출에 필요한 Header, Body 정리
        RestTemplate rest = new RestTemplate();
        HttpHeaders headers = new HttpHeaders();
        headers.add("X-Naver-Client-Id", "zdqMoIkFaK8uKvC2oNY2");
        headers.add("X-Naver-Client-Secret", "LiZfsgtuD5");
        String body = "";
        HttpEntity<String> requestEntity = new HttpEntity<>(body, headers);
```
#### Step 3-5.

이후에는 이 호출 결과를 Json 형식으로 변환한 후, 이를 Java 객체 (DTO)로 변환하고, 이를 API Response로 보내게 된다.

Servelet은 이러한 개념과 방식으로 동작한다.

<br><br>

## Servelet vs Controller


### Controller의 장점

- HTTP Request, Response 처리를 위해 매번 작성해줘야 하는 중복 코드들을 생략 가능

- API 이름마다 파일을 만들 필요 없음

<br>

### 👉🏻 위의 Step 1-5를 Controller로 구현

**Controller 가 자동으로 해주는 일**

- Step 1. API Request 의 파라미터 값에서 검색어 추출 -> query 변수
  <br>

- Step 5. API Response 보내기
    - 5.1) response 의 header 설정
    - 5.2) response 의 body 설정

