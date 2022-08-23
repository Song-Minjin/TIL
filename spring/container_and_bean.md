# Bean



: 스프링이 관리하는 객체


# Spring IoC container



: 빈(Bean)을 모아둔 통

  <br>


### 등록 방법

**방법 1. `@Component`**

- 클래스 선언 위에 설정
  ```java
  @Component
   public class ProductService { ... }
  ```
  <br>


- 스프링 서버가 뜰 때 스프링 IoC에 Bean 저장
  👉🏻  `@Component` 클래스가 있으면, 스프링이 다음과 같은 일을 해준다.

  ```java
  // 1. ProductService 객체 생성
  ProductService productService = new ProductService();
  
  // 2. 스프링 IoC 컨테이너에 빈 (productService) 저장
  // productService -> 스프링 IoC 컨테이너
  ```
    - 스프링 Bean 이름 규칙 : 클래스의 앞글자만 소문자로 변경됨

  <br>


- Bean 아이콘 확인 : 스프링 IoC에서 관리할 Bean이라는 클래스 표시
  ![](https://velog.velcdn.com/images/sw_smj/post/40f60ed9-c608-47b5-868d-85f051a5244c/image.png)

  <br>

- `@Component` 적용 조건
    - `@ComponentScan`에 설정해준 packages 위치와 하위 packages들
  ```java
  @Configuration
   @ComponentScan(basePackages = "com.example.springcore")
   class BeanConfig { ... }
  ```

  > 📌 **참고**
  > 이 `@ComponentScan`은 `@SpringBootApplication`에 의해 default 설정이 되어 있음

  <br>
- 테스트 코드
  ```java
  package com.example.abc;

   import org.springframework.stereotype.Component;

   @Component
   public class TestClass {

   }
  ```

<br>  <br>


**방법 2. `@Bean`**



: 직접 객체를 생성하여 Bean으로 등록을 요청한다.


- 스프링 서버가 뜰 때 스프링 IoC에 Bean 저장

  ```java
  // 1. @Bean 설정된 함수 호출
  ProductRepository productRepository = beanConfiguration.productRepository();
  
  // 2. 스프링 IoC 컨테이너에 Bean (productRepository) 저장
  // productRepository -> 스프링 IoC 컨테이너
  ```  

  <br>

- 스프링 Bean 이름 : `@Bean`이 설정된 함수명

  <br>

- Bean 아이콘 확인 → 스프링 IoC에 Bean에 등록될 것이라는 표시
  ![](https://velog.velcdn.com/images/sw_smj/post/ccc071aa-d071-4b81-9540-a76669360481/image.png)


<br><br>

## 스프링 Bean 사용 방법

### 1. @AutoWired : 자동 가져오기

**방법 1** : **멤버변수 선언 위**에 **`@Autowired`** → 스프링에 의해 DI(의존성 주입)됨
  ```java
  @Component
   public class ProductService {
		
       @Autowired
       private ProductRepository productRepository;
		
	   	// ...
   }
  ```
  <br>


**방법 2** : **Bean을 사용할 함수 위**에 **`@Autowired`** → 스프링에 의해 DI됨
  ```java
  @Component
   public class ProductService {
  
       private final ProductRepository productRepository;

       @Autowired
       public ProductService(ProductRepository productRepository) {
        this.productRepository = productRepository;
        }
		
         // ...
    }
  ```

<br>  <br>


### Autowired 활용시 주의사항

**1. `@Autowired` 적용 조건**
: 스프링 IoC 컨테이너에 의해 관리되는 클래스에만 사용 가능
<br>

**2. `@Autowired` 생략 조건**

- Spring 4.3 버전부터 생략 가능

- 생성자 선언이 1개일 때에만 생략 가능
    - 예시) 파라미터가 다른 생성자들 여러개 → 생성 불가
      ```java
      public class A {
         @Autowired // 생략 불가
         public A(B b) {...}
         
         @Autowired // 생략 불가
         public A(B b, C c) {...}
      }
      ```

<br>

**cf. Lombok의 `@RequiredArgsConstructor` 사용**

   ```java
   @RequiredArgsConstructor // final로 선언된 멤버 변수를 자동으로 생성합니다.
    @RestController // JSON으로 데이터를 주고받음을 선언합니다.
    public class ProductController {

        private final ProductService productService;
    
           // 생략 가능
           // @Autowired
       	// public ProductController(ProductService productService) {
           //     this.productService = productService
           // }
    }
   ```

<br>  <br>


### 2. ApplicationContext : 수동 가져오기




: 스프링 IoC 컨테이너에서 Bean을 수동으로 가져오는 방법

```java
@Component
public class ProductService {
    private final ProductRepository productRepository;

    @Autowired
    public ProductService(ApplicationContext context) {
        // 1.'빈' 이름으로 가져오기
        ProductRepository productRepository = (ProductRepository) context.getBean("productRepository");
        // 2.'빈' 클래스 형식으로 가져오기
        // ProductRepository productRepository = context.getBean(ProductRepository.class);
        this.productRepository = productRepository;
    }

		// ...		
}
```