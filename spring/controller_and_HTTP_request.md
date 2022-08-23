# Controller와 HTTP Request 메시지

![](https://velog.velcdn.com/images/sw_smj/post/6acdb98a-5e4c-4b24-9d72-d12dd8741221/image.png)


- **`@PathVariable`** : `/변수1/{변수1}/변수2/{변수2}`
    - 생략 불가능

  <br>

- **`@RequestParam`** : `/form/param?변수1=값1&변2수=값2`
    - ❗ 생략 가능 (but 처음 학습할 때에는 다 명시하는 것이 개념 잡기에 좋다)

  > 📌 **GET vs POST**
  >
  > `POST`에서는 Body에 내용을 담는데, 이때는 내용을 감출 수 있기 때문에 이 목적을 위해서라도 `GET`이 아닌 `POST`를 사용할 때가 있다.

  <br>

- **`@ModelAttribute`** : `/form/model`
    - 생략 가능
    - Model 객체에 `@Setter`가 없으면 안됨!
  > 💡 **Lombok**의 **`@Setter`**
  >
  > ```java
  > public void setName(String name) {
  >	  this.name = name
  >    }
  >```
  > ➡ 이렇듯 객체에 대해 멤버변수를 설정해주는 함수 역할을 한 번에 Lommbok이 대신 해주는 것 = `@Setter`

<br>


- **`@RequestBody`** : `/form/json`
    - 생략 불가
    - json 형식으로 출력됨