# JPA
**Spring Data JPA**

![](https://velog.velcdn.com/images/sw_smj/post/9dcadd3e-3a6d-45aa-81af-69ed856c2baa/image.png)


- SQL문으로 코드를 작성하지 않고도 데이터를 생성, 조회, 수정, 삭제할 수 있도록 해주는 번역기

- 즉, Java로 코드를 작성하면, SQL로 번역해줌

- 기본적인 기능이 거의 완벽하게 갖춰져있음

- Spring에서의 `Domain` = SQL에서의 `Table`
- &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`Repository` =  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`SQL`


> 👉🏻 **Repository**<br>
> JPA는 Repository를 통해서만 사용할 수 있음!



<br>

## JDBC


: Java DataBase Connectivity

Java에서 DB에 접속할 수 있도록 하는 Java API
DB에서 자료를 쿼리하거나 업데이트하는 방법을 제공함

> 💡 **요약**<br>
> 즉, JPA와 JDBC가 Java와 DB 사이에서 번역 및 쿼리 등 소통을 담당해주고 있다고 생각하면 됨!


<br>

