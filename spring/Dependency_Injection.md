## Tight Coupling (강한 결합)

### 정의 및 문제점

#### 예제
- **`Controller1`**
  ```java
  public class Controller1 {
	private final Service1 service1;

	public Controller1() {
		this.service1 = new Service1();
	}
  }
  ```
- **`Service1`**
  ```java
  public class Service1 {
	private final Repository1 repository1;

	public Service1() {
		this.repository1 = new Repository1();
	}
  }
  ```
- **`Repository`**
  ```java
  public class Repository1 { ... }
  ```

![](https://velog.velcdn.com/images/sw_smj/post/b195465b-0655-4e41-9779-5a5d86918c15/image.png)


- `Controller` 5개가 각각 `Service1`을 생성하여 사용 중
  ➡ `Repository1` 생성자 변경에 의해 모든 `Contoller`와 모든 `Service`의 코드 변경이 필요!

<br>
<br>

## 해결 방법 (= Loose Coupling, 약한 결합)

> 💡 **원리**
>
> 1. 각 객체에 대한 객체 생성은 딱 한 번만 한다.
> 2. 생성된 객체를 모든 곳에서 재사용한다.

**1. `Repository1`  클래스 선언 및 객체 생성 → `repository1`**

![](https://velog.velcdn.com/images/sw_smj/post/c2ff7fcf-aed4-4102-97d3-8b9dca0bd583/image.png)


```java
public class Repository1 { ... }

// 객체 생성
    **Repository1 repository1 = new Repository1();**
```

<br>


**2. `Service1`  클래스 선언 및 객체 생성 (`repostiroy1` 사용) → `service1`**

> 📌 즉, New로 새로 생성하는 것이 아니라 아까 생성한 것을 사용하겠다!

![](https://velog.velcdn.com/images/sw_smj/post/e51da6dd-6727-46bd-b178-6c42cbbaa25b/image.png)


```java
Class Service1 {
	private final Repository1 repitory1;

	// repository1 객체 사용
	public Service1(Repository1 repository1) {
	  //this.repository1 = new Repository1(); ⬅ 이렇게 하지 않고
		this.repository1 = repository1;
	}
}

// 객체 생성
Service1 service1 = new Service1(repository1);
```

**3. `Controller1` 선언 (`Service1` 사용)**

```java
Class Controller1 {
	private final Service1 service1;

	// service1 객체 사용
	public Controller1(Service1 service1) {
		this.service1 = new Service1();
		this.service1 = service1;
	}
}
```

**4. 변경사항 발생**

`Repository1` 객체 생성 시 DB 접속 `id`, `pw`를 받아 DB 접속시 사용해야 함
➡ 생성자에 DB 접속 `id`, `pw`를 추가

```java
public class Repository1 {

	public Repository1(String id, String pw) {
    // DB 연결
    Connection connection = DriverManager.getConnection("jdbc:h2:mem:springcoredb", id, pw);
  }
}

// 객체 생성
String id = "sa";
String pw = "";
Repository1 repository1 = new Repository1(id, pw);
```

<br>

### 개선 효과

- `Repository1` 생성자 변경은 다른 클래스에 크게 피해를 주지 않음
- 마찬가지로 `Service1` 생성자가 변경되면? 모든 Controller를 변경할 필요 없음

  👉🏻 이것이 **느슨한 결합(Loose Coupling)**!!

<br>
<br>

# 제어의 역전(IoC)



: 프로그램의 제어 흐름이 반대로 됨

- 일반적 : 사용자가 자신이 필요한 `객체`를 **생성**하여 사용


- IoC : 용도에 맞게 필요한 `객체`를 **가져다** 사용

    ➡ **DI(Dependency Injection, 의존성 주입)**
    - 사용할 객체가 어떻게 만들어졌는지는 알 방법도, 필요성도 없음
    - 예) 각기 상황에 따라 부엌가위, 핑킹가위, 전지가위를 쓰는 것처럼
  

