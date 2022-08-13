우선, Collection이라는 용어 자체가 Java에서 다양한 용도로 사용된다. 이에 혼동되지 않도록 정리하고 넘어가겠다.

오늘은 셋 중 한 가지에 대해서만 집중적으로 파고 넘어가고자 한다.

<br>

# collection vs Collection vs Collections

## collection


  : 데이터의 집합이나 그룹
  - 객체가 저장되고 반복되는 자료구조

<br>


## Collection &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  << 🚩 Today!


  : 인터페이스
  (`java.util.Collection` 프레임워크)

- `Collection` '프레임워크' 내에 있는 `Collection` '인터페이스'

- 여러 요소들을 담기 위해 만들어졌기 때문에, Container 객체라고도 불림

- `Set`, `List`, `Queue` 인터페이스가 하위 인터페이스로서 있음

    - ex) `ArrayList` : `Collection` 인터페이스 → `List` 인터페이스 → `ArrayList` 클래스로 구현을 하는 것!

<br>

## Collections


  : utility 클래스<br>
  (`java.util.Collections` 클래스)



<br><br>

위에서 읽었다시피 **`Collection`** 과 **`Collections`** 는 뒤의 **`s`** 자 하나로 칭하는 것이 다르다.

오늘 알아볼 **2번, 컬렉션 인터페이스**는 **우선 컬렉션 프레임워크(Collection Framework)라는 개념을 알아야 제대로 이해할 수 있겠다.**

따라서 **컬렉션 프레임워크**에 대해 먼저 알아본다.

<br><br>

# Collection 프레임워크

> **자바 컬렉션 프레임워크 (JCF, Java Collection Framework)** 라고도 한다.


: **`Array`** 의 문제점을 보완하기 위해, 널리 알려진 자료구조를 바탕으로 **collection**과 관련된 인터페이스, 클래스들을 **`java.util`** 패키지에 포함시킨 것

- 따라서 **`java.util`** 패키지에 포함되어 있으며, JDK 1.2부터 제공됨

- 프레임워크를 사용하면 👉🏻 코딩 시간 감소, 코드 품질 보장, 유지 보수 용이

- Java Interface를 사용하여 구현됨
  <br>

## 1. Collection 프레임워크의 구조


![](https://velog.velcdn.com/images/sw_smj/post/11d99c3f-649a-4e7c-b799-26bac280b210/image.png)

<br>

## 2. Collection 프레임워크의 구성 요소

- **Collection Interface** : `java.util` 패키지에 있음


- **Collection class** : `java.util` 또는 `java.util.concurrent` 패키지에 있음


- **Collection Algorithm** : 검색, 정렬, 셔플 등의 기능 제공

<br>

> 💡 **인터페이스란? (Interface)**
>
> : 동일한 목적 하에 동일한 기능을 수행하도록 강제하는 것
> - Java의 ***다형성***을 극대화하여 개발코드 수정을 줄이고 프로그램 유지 보수성을 높이기위해 사용
>
>> 💡 **Java의 다형성 (Polymorphism)**
>> - 하나의 객체가 여러 가지 자료형 타입을 가질 수 있는 성질
>> - 상속, 추상화와 더불어 객체 지향 프로그래밍(OOP)를 구성하는 중요한 특징 중 하나
> - 다형성을 구현하는 대표적 방법 : 오버라이딩(Overriding), 오버로딩(Overloading), 함수형 인터페이스(Functional Interface)

<br>

## 3. Collection 프레임워크의 대표적인 인터페이스들

- **`List`** : `Collectoin` 인터페이스를 상속 받음<br>
  <br>
    - `ArrayList`, `LinkedList`, `Stack` 등
  <br><br>


- **`Set`** : `Collection` 인터페이스를 상속 받음<br>
  <br>
  - `HashSet`, `LinkedHashSet`, `TreeSet`
    <br><br>


- **`Map`**  : `Collection` 인터페이스를 상속받지 않음<br>
  <br>
    - `HashMap`, `LinkedHashMap`, `IdentityHashMap`, `Hashtable`, `TreeMap`
      <br><br><br>

> 👉🏻 **Map 인터페이스는 왜 따로?**<br>
> 
> 이해가 가지 않을 수 있다. 우선 위의 Collection Framework 구조 그림을 다시 뜯어보면 조금 쉽겠다.
> 
> ![](https://velog.velcdn.com/images/sw_smj/post/e3c8073b-bb8e-4add-9ac7-f257dd4fc409/image.png)
>
> 즉, `Collection` '프레임워크' 내에 Interface가 여러 가지 있는데, 그 중 `Collection`이라는 '인터페이스'도 또 있는 것이다.
> 그림에서 보여지다시피, `Map` 인터페이스는 따로 가지를 쳐서 나간다. `Collection` '인터페이스'의 하위 인터페이스가 아니다.

> 💡 **그럼 Map이 따로 가지를 친 이유는?**<br>
> 구조상 차이가 있기 때문이다. Map 인터페이스는 Key-Value 구조로 매핑한다. 각 키는 하나의 값만 가질 수 있다. 이는 나중에 Map 게시글로 따로 정리해본다.

<br><br>