# forEach 반복문


: Java 1.5버전부터 추가된 양식

- 실제로 Java에서는 `foreach`라는 명령어가 아니라, 기존과 동일하게 `for`를 사용한다.

> 다른 언어에서는 `foreach`라는 용어를 사용하여 구분!


<br>

### forEach 사용 방법

➡ **`collection.forEach(변수 -> 반복처리(변수))`**

- collection에 저장되어있는 값(변수)을 하나씩 대입한다.

이는 enhanced for문(향상된 for문)과 forEach를 비교하며 확실히 알아볼 수 있다.

- **enhanced for**
  ```java
  import java.util.ArrayList;
   import java.util.List;
  
   public class Main {
   	 public static void main(String[] args) {
     		 List<String> list = new ArrayList<>();
 		 list.add("a");
 		 list.add("p");
 		 list.add("p");
 		 list.add("l");
		 list.add("e");

		 System.out.println("확장 for문 출력");
		 for (String s : list) {
		 	 System.out.println(s);
	 	 }
   	   }
   }
  ```

- **forEach** + Lambda
  ```java
  import java.util.ArrayList;
   import java.util.List;
  
   public class Main {
   	 public static void main(String[] args) {
     		 List<String> list = new ArrayList<>();
 		 list.add("a");
 		 list.add("p");
 		 list.add("p");
 		 list.add("l");
		 list.add("e");

		 System.out.println("forEach 함수 출력");
		 list.forEach(s -> System.out.println(s));
	 	 }
   	   }
   }
  ```

다른 예시를 하나 더 들어보자.


- **forEach** + lambda
  ```java
  List<String> items = new ArrayList<>();
   items.add("Paris");
   items.add("Seoul");
   items.add("Tokyo");
   items.add("Valencia");

   items.forEach(name -> System.out.Println(name));
  ```

