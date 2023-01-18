## 1-1. 싱글톤 패턴(Singleton Pattern)


: 하나의 클래스에 오직 하나의 인스턴스만 가지는 패턴

- 하나의 클래스를 기반으로 단 하나의 인스턴스를 만들어, 이를 기반으로 로직을 만드는 데에 쓰임

- 생성자가 여러 차례 호출되더라도 실제로 생성되는 객체는 하나이고 최초 생성 이후에 호출된 생성자는 최초의 생성자가 생성한 객체를 리턴함

- 하나의 인스턴스를 만들어놓고, 해당 인스턴스를 다른 모듈들이 공유하여 사용하기 때문에 인스턴스 생성 비용이 감소됨

- 모듈 간의 결합을 강하게 만든다는 단점이 있음

  > 💡 이러한 모듈 간의 결합을 조금 느슨하게 하기 위해 의존성 주입(Dependency Injection)이라는 개념을 사용할 수 있다.

### 사용 예시

- 보통 데이터베이스 연결 모듈(DBCP, DataBase Connection Pool)에 많이 사용함
  (DB 연결 과정이 부하가 크고, 한 번 연결된 객체를 계속 사용해야 하기 때문)

- 스프링 컨테이너도 객체를 싱글톤으로 관리함


### 구현

**Java에서의 싱글톤 구현**
```java
class Singleton {
	private static class singleInstanceHolder {
    	private static final Singleton INSTANCE = new Singleton();
    }
    public static Singleton getInstance() {
    	return singleInstanceHolder.INSTANCE;
    }
}

public class HelloWorld {
	public static void main(String[] args) {
    	Singleton a = Singleton.getInstance();
        Singleton b = Singleton.getInstance();
        System.out.println(a.hashCode());
        System.out.println(b.hashCode());
        if (a == b) {
        	System.out.println(true);
        }
    }
}
```


**JDBC에서 싱글톤을 활용하여 DB 연결하기**

```java
// 데이터베이스와 연결과 끊어주기위한 클래스

import java.sql.Connection; 
import java.sql.DriverManager;
import java.sql.SQLException;


public class DBConn {

       private static Connection dbConn;
       public static Connection getConnection() throws SQLException, ClassNotFoundException{
             if (dbConn == null){
                   //dbConn이 null이면, 연결된 것이 없으니 연결해야한다.
                  String url = "jdbc:oracle:thin:@127.0.0.1:1521:xe" ;
                  String user = "hr";
                  String pass = "12345";
                  Class. forName("oracle.jdbc.driver.OracleDriver");
                   dbConn = DriverManager.getConnection(url, user, pass);
            }
             return dbConn ;
      }
       //db와의 연결을 맺어주기 위한 메소드.
      
       public static void close() throws SQLException {
             if (dbConn != null){
                   if(!dbConn .isClosed()){
                         dbConn.close();
                  }
            }
      }
       //db와의 연결을 끊어주는 메소드
}
```
```java
// ex) 연결하기 예제

import java.sql.Connection;


public class jdbcTest {

       public static void main(String[] args) {

             try{
                  Connection conn = DBConn.getConnection ();
                  //정의한 DBConn 클래스로 손쉽게 연결.
                  System. out.println("오라클에 연결되었습니다." );
            } catch(Exception e){
                  System. out.println(e.toString());
            }
      }

}
```



### 문제점

- 객체지향 프로그래밍의 핵심인 **상속**과 **다형성**을 해친다.

- 객체지향 프로그래밍의 또 다른 핵심인 **정보 은닉**을 해친다. 공유의 목적으로 생성된 클래스이기 때문에, 객체를 요청하는 메소드를 public으로 강제할 수밖에 없다.

- Java의 고정적 싱글턴 패턴은 객체가 하나인 것을 보장할 수 없다.

> 💡 **싱글턴 패턴을 사용할 땐 조심하자!**
>
> 즉, 싱글턴 패턴은 굉장히 많이 활용되는 패턴이나, 앞서 말한 객체지향 프로그래밍의 기본 사상들을 많이 침해하기 때문에 굉장히 비판을 많이 받는 디자인 패턴이다.
>
> 따라서 싱글턴 패턴은 사용 시 매우 조심해서 사용해야 한다.
>
> 그것이 아니라면 위의 고전적인 싱글턴 패턴이 아닌 개선된 방식으로 객체의 싱글턴 방식을 구현하여 사용해야 한다.
