# DAO




**: Data Access Object**

- **DB의 data**에 **접근**하기 위한 **객체**
- DB 접근을 위한 로직과, 비즈니스 로직을 분리하기 위해 사용

- DB와 연결할 Connection까지 설정되어있는 경우가 많다.

- 현재 많이 쓰이는 MyBatis 등을 사용할 경우, Connection Pool까지 제공되고 있기 때문에 DAO를 별도로 만드는 경우는 드물다.

> 📌 **참고 - DBCP(Database Connection Pool)**
> ### **Connection**
> : Client측에서 DB에 접속하여 read/write을 수행한 경우, 결과를 받고 접속을 종료하는 일련의 과정
> ```javascript
> mysql.createConnection() -> connection.connect() -> connection.query() -> connection.end()
> ```
> 👉🏻 서버와 DB가 connection을 맺음 → Query를 실행하여 데이터를 read/write함 → connection을 close함
>
> ### Connection Pool
> 위의 과정은 사용자의 요청이 적을 경우 부담이 적지만, 대규모 트래픽의 경우 서버에 과부하를 야기한다.
> connection을 맺고 끊는 작업은 비용이 많이 들기 때문! 따라서 수많은 요청마다 connection을 맺고 끊는 것은 비용, 성능 측면에서 불리하다.
> 따라서 DB의 데이터를 read/write할 때마다  connection을 맺는 방식이 아닌, Connection Pool 방식을 이용한다.
>
> #### Connection Pool
> : 서버에서 미리 DB와 일정수의 connection을 맺어놓고, 이 connection 객체들을 pool에 저장해두었다가 요청마다 저장된 connection을 빌려주고 요청 해결 후 다시 connection을 받아 pool에 저장하는 것
> ![](https://velog.velcdn.com/images/sw_smj/post/7ba72dd9-4c0b-4af8-84a4-79015bb6ff3b/image.png)

> 💡 **참고**
> MySQL을 비롯한 각 DBMS가 언어마다 driver를 제공함 ➡ Connection Pool 방식을 사용하기도 아주 간단하고 편리하다.

<br>

### DAO의 예시

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.SQLException;

public class TestDao {

    public void add(TestDto dto) throws ClassNotFoundException, SQLException {
        Class.forName("com.mysql.jdbc.Driver");
        Connection connection = DriverManager.getConnection("jdbc:mysql://localhost/test", "root", "root");

        PreparedStatement preparedStatement = connection.prepareStatement("insert into users(id,name,password) value(?,?,?)");


        preparedStatement.setString(1, dto.getName());
        preparedStatement.setInt(2, dto.getValue());
        preparedStatement.setString(3, dto.getData());
        preparedStatement.executeUpdate();
        preparedStatement.close();
        
        connection.close();

    }
}
```

<br><br>

# DTO



**: Data Transfer Object**

- 계층간 데이터 교환을 위한 Java Beans
  > 📍 **Java Beans?**
  > : Java로 작성된 소프트웨어 컴포넌트

  *&nbsp; 계층간 : Controller, View, Business Layer, Persistent Layer 등

- 로직을 가지지 않는 순수한 데이터 객체
- `getter`, `setter` 메소드만 가진 객체

- Java에서의 Property : get, set 뒤에 오는 단어. 이 property는 멤버변수로 결정되는 것이 아닌, getter과 setter로 설정한 것임을 명심해야 한다.

👉🏻 즉, 멤버변수와는 별개로 getter과 setter로 property(data)를 표현한다는 것이다.

> 💡 잠깐! **Layer간 데이터 전송에는 DTO를 쓰면 편한 이유는?**
> - Java는 여러 프레임워크에서 데이터 자동화처리를 위한 ***리플렉션 기법***을 사용한다. 이는 프레임워크 내부에서 실행되어 우리 눈에 보이지 않는다.
> - Layer간에 데이터를 넘길 때, 해당 필드 값을 property에 맞춰 넘기면, 받아야 하는 곳에서는 일일히 처리하는 것이 아니라, 속성의 이름과 매칭되는 property에 자동적으로 DTO가 인스턴스화됨 → DTO를 자료형으로 값을 받을 수 있게 됨
    > ➡ 따라서 key-value로 존재하는 데이터는 자동화처리된 DTO로 변환되어 쉽게 데이터가 셋팅된 오브젝트를 받을 수 있다.

<br>

### DTO의 예시
```java
public class PersonDTO {

    private String name;
    private int age;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }
}
```

<br><br>

# VO



**: Value Object**

- 값 오브젝트

- DTO와 혼용해서 쓰이긴 하지만 미묘한 차이가 있음

- 값을 위해 쓰임. Java는 값 타입을 표현하기 위해 불변(readOnly) 특징의 클래스를 생성한다.
    - 이런 불변의 클래스는 중간에 값을 바꿀 수 없고, 새로 만들어야 한다.

<br>

### VO 예시

```java
@Getter
@Setter
@Alias("article")
class ArticleVO {

    private Long id;
    private String title;
    private String contents;

      @Override
      public boolean equals(Object o) {
          if (this == o) return true;
          if (o == null || getClass() != o.getClass()) return false;
          Article article = (Article) o;
          return Objects.equals(id, article.id);
      }

      @Override
      public int hashCode() {
          return Objects.hash(id);
      }
}
```

<br><br>

# DTO vs VO

- 공통점 : 둘 다, 넣어진 데이터를 getter를 통해 사용함

- 차이점 : DTO는 가변의 성격을 가진 반면, VO는 불변의 성격을 지님