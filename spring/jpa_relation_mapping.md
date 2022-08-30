# Spring에서의 연관관계 매핑

> **주의**
>
> 스프링의 연관관계 매핑은 DB의 외래키와 똑같이 생각하면 안 된다.
> DB에서는 외래키라는 하나의 column을 가지고 연관관계를 표현하지만, JPA에서는 객체를 매핑하기 때문이다.
>
> 👉🏻 JPA에서의 연관관계 매핑에서 중요한 것
> - 관계의 방향
> - 다중성 (일대다? 다대일? 다대다?)
> - 연관관계의 주인


# 단방향 연관관계

## 다대일(N:1)

- 예시 : 사람 - 가족

    - 사람은 하나의 가족에만 소속될 수 있다. 👉🏻 사람과 가족은 **다대일 관계**이다.

<br>

이 관계를 객체 연관관계와 테이블 연관관계로 나타내보면 다음과 같다.

### 1. 객체 연관관계 - 다대일(N:1)

- 사람 객체는 Person.family로 가족 객체와 연관관계를 맺는다.

- 사람 객체와 가족 객체는 단방향 관계이다. 즉, 사람은 Person.family를 통해 가족을 알 수 있지만, 가족은 사람을 알 수 없다.

- **`Person` 클래스**
  ```java
  import javax.persistence.*;		// 영속성 컨텍스트 관련 설정

  @Entity
  public class Person {
  
      @Id														// 해당 프로퍼티가 테이블의 기본키(primary key)역할을 한다는 의미
      @GeneratedValue(strategy = GenerationType.IDENTITY)		// 기본키의 값 자동 생성 전략
      private Long id;

      @Column
      private String name;
      
      @ManyToOne		// 다대일관계라는 매핑 정보(다대일 연관관계 매핑시 필수 사용)
      @JoinColumn		// 외래키 매핑시 사용 (name 속성에는 매핑할 외래키 이름 지정(생략시 외래키 매핑 컬럼 이름 자동 생성))
      private Family family;
  ```


- **`Family` 클래스**
  ```java
  import javax.persistence.*;

  @Entity
  public class Family {

      @Id
      @GeneratedValue(strategy = GenerationType.IDENTITY)
      private Long id;

      @Column
      private String address;
  }
  ```

![](https://velog.velcdn.com/images/sw_smj/post/1871f986-7b32-44ba-9748-4ee742401d42/image.png)



<br>

### 2. DB 테이블 연관관계 - 다대일(N:1)

- 사람 테이블은 Family_id 외래키로 가족 테이블과 연관관계를 맺는다.

- 사람 테이블과 가족 테이블은 양방향 관계이다. 즉, 사람 테이블의 Family_id 외래키를 통해 사람과 가족을 join할 수 있고, 반대로 가족과 사람을 join할 수도 있다.

![](https://velog.velcdn.com/images/sw_smj/post/b5b1201b-a41d-48f9-b5de-22863b8096b9/image.png)


> 💡 **정리**<br>
> 참조를 통한 연관관계인 **객체 연관관계** : 단방향
> 따라서 JPA에서 양방향 관계를 만들고 싶다면 반대쪽에도 필드를 추가하여 참조를 해야 함
>
> (↔ DB 테이블 (= 외래키 하나로 양방향 조인 가능))



<br>

# 양방향 연관관계

## 다대일 + 일대다 (N:1 + 1:M ⇒ N:M)

<br>

### 1. Spring 객체 연관관계 - 일대다

위의 예제에서는 항상 Person 클래스에서만 Family 클래스에 접근할 수 있었다. 이에 반대로 Family 클래스에서 Person 클래스를 접근하는 방법을 추가해보도록 한다.

👉🏻 서로 양방향으로 접근할 수 있는 양방향 연관관계로 매핑이 가능해진다.

<br>

#### 📌 일대다 연관관계를 구현하려면?

➡ **collection 이용!** (ex: List 등)

> 💡 **여기서 주의!**
>
> DB에서는 외래키 하나만을 이용해서도 양방향으로 조회 가능!
> 그러나 객체 연관관계에서는 (주로 List 등) collection을 활용해야 함!

<br>


- **`Person` 클래스**

  ```java
  import javax.persistence.*;

   @Entity
   public class Person {

      @Id
      @GeneratedValue(strategy = GenerationType.IDENTITY)
      private Long id;

      @Column
      private String name;

      @ManyToOne
      @JoinColumn
      private Family family;
  ```


- **`Family` 클래스** (List Collection 사용)

  ```java
  import javax.persistence.*;
   import java.util.List;

   @Entity
   public class Family {

       @Id
       @GeneratedValue(strategy = GenerationType.IDENTITY)
       private Long id;
 
       @Column
       private String address;

       @OneToMany(mappedBy = "family")
       private List<Person> people;
  ```


![](https://velog.velcdn.com/images/sw_smj/post/6291a077-7987-4803-919d-2eebc00b0ef0/image.png)

> 👉🏻 **`mappedBy`가 필요한 이유**
> - 엄밀히 말하면 객체에는 양방향 연관관계란 존재하지 않는다. 서로 다른 단방향 연관관계 2개를 묶어서 양방향처럼 기능하게 하는 것 뿐이다 (↔ DB 테이블 : 외래키 하나로 join해서 양방향 연관관계를 맺음)
    > Entity를 양방향으로 매핑하면, 두 곳에서 서로를 참조하게 되기 때문에 객체의 연관관계를 관리하는 포인트가 2곳이 된다.
    > 따라서 이 문제를 해결하기 위해 JPA에서 두 객체 연관관계 중 하나를 정해서 테이블의 외래키를 관리해야 한다. ➡ 이를 **연관관계의 주인**이라고 한다. 

<br>

> 👉🏻 **연관관계의 주인**
> - 연관관계의 주인만이 DB 연관관계와 매핑되며, 외래키를 관리(등록, 수정, 삭제)할 수 있다. 주인이 아닌 쪽은 읽기만 할 수 있다.
> - 주인은 mappedBy 속성을 사용하지 않는다.
> - 주인이 아니면, mappedBy 속성을 사용하여 속성의 값으로 연관관꼐의 주인을 지정해야 한다.


<br><br><BR>

---

**참고자료**

- https://hyeooona825.tistory.com/88