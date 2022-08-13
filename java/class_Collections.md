Java collection과 관련된 이름들이 아주 많고, 따라서 어떻게 표현하는지에 따라 가리키는 값이 달라진다.

저번 포스팅에 이어, 오늘은 Collections에 대해 집중적으로 파고 넘어가고자 한다.

> 지난 포스팅 바로 가기 👉🏻 [ [Java] Collection 프레임워크와 Collection 인터페이스](https://velog.io/@sw_smj/Java-%EC%BB%AC%EB%A0%89%EC%85%98-%ED%94%84%EB%A0%88%EC%9E%84%EC%9B%8C%ED%81%ACCollection-Framework%EC%99%80-%EC%BB%AC%EB%A0%89%EC%85%98-%EC%9D%B8%ED%84%B0%ED%8E%98%EC%9D%B4%EC%8A%A4Collection-Interface)

<br>

# collection vs Collection vs Collections

## collection


: 데이터의 집합이나 그룹

  - 객체가 저장되고 반복되는 자료구조

<br>

## Collection


: 인터페이스
(`java.util.Collection` 프레임워크)
 <br>

- `Collection` '프레임워크' 내에 있는 `Collection` '인터페이스'

  <br>

- 여러 요소들을 담기 위해 만들어졌기 때문에, Container 객체라고도 불림

  <br>
- `Set`, `List`, `Queue` 인터페이스가 하위 인터페이스로서 있음
<br>
  <br>
  - ex) `ArrayList` : `Collection` 인터페이스 → `List` 인터페이스 → `ArrayList` 클래스로 구현을 하는 것!

    <br>

## Collections &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  << 🚩 Today!


: utility 클래스 <br>

(`java.util.Collections` 클래스)


<br><br>


이처럼 **`Collection`**과 **`Collections`**는 뒤의 **`s`**자 하나로 칭하는 것이 다르다.

오늘은 **3번, Collections 클래스**에 대해 Collection과 비교하며 확실히 알아보자.


<br><br>

# Collection
Collection은, 지난 포스팅에서 알아봤듯 인터페이스이며, Iterable을 상속받는다.

![](https://velog.velcdn.com/images/sw_smj/post/f1b360e8-51c8-4f18-87f5-f7e992939c78/image.png)


> 💡 **Iterable?**<br>
> 
> JCF에서 봤던 구조 그림을 떠올리면 된다. Collection 인터페이스의 상위에 있던 인터페이스이다.
> <br>
> 
> ![](https://velog.velcdn.com/images/sw_smj/post/ed0a8b0f-25dc-4df0-a205-0d563a130475/image.png)

<br>

# Collections


: Object를 상속받는 클래스이다.


![](https://velog.velcdn.com/images/sw_smj/post/33aff3ed-5b04-4fd5-a9f6-f7061ed29daf/image.png)

<br>


# Collection vs Collections
![](https://velog.velcdn.com/images/sw_smj/post/3372991e-fb96-4569-b290-c325e77e6163/image.png)


위의 그림을 보면 두 가지 이름이 가리키는 대상이 확실히 다름을 알 수 있다. 이에 조금 보충설명을 하면 다음과 같다.

- **Collection**(인터페이스) : Set, List, Queue 등의 인터페이스의 상위(부모) 인터페이스
  <br> 


- **Collections**(클래스) : Collection을 이용하기 위한 클래스<br>
  
<br>

이렇게 `Collection` 인터페이스와 연관하여 `Collections`라는 클래스가 하는 역할에 대해 알았으니, `Collections`의 구체적인 기능들에 대해 알아보자.


<br><br>

# Collections 클래스

- Collection 인터페이스를 구현한 클래스에 대한 객체 생성, 정렬, 병합, 검색 등의 기능을 안정적으로 수행하도록 도와주는 utility 클래스이다.

- Generic 기술을 사용하여 작성되었으며, 정적 메소드의 형태로 되어있다.

  > 💡 **Generic?**
  > : 데이터타입을 일반화(generalize)한다는 의미
  >
  > 클래스나 메소드에서 사용할 내부 데이터타입을 컴파일 시 미리 지정하는 방법이다.
  > 이렇게 컴파일시 미리 타입 검사(type check)를 하면 다음과 같은 장점이 있다.
  > - 클래스나 메소드 내부에서 사용되는 객체 안정성을 높임
  > - 반환값에 대한 타입변환 및 타입 검사에 들어가는 과정 감소

<br>

- **자주 사용되는 알고리즘** <br>
   <br>
    - 정렬 (Sortiing)
  <br>
      
    - 섞기 (Shuffling)
  
    - 탐색 (Searching)

  <br>


- **주요 method**<br>
<br>

  - **`max`** : 지정된 컬렉션에서 최대 요소를 반환<br>
    <br>
  - **`min`** : 지정된 컬렉션에서 최대 요소를 반환<br>
    <br>
  - **`sort`** : 지정된 컬렉션 정렬<br>
    <br>
  - **`shuffle`** : 지정된 컬렉션의 요소들의 순서를 무작위로 섞기<br>
    <br>
  - **`synchronizedCollection`** : 지정된 컬렉션에 의해 지원되는 동기화 된 컬렉션을 재생성해 반환<br>
    <br>
  - **`binarySearch`** : 지정된 컬렉션에서 이진 탐색 알고리즘을 사용해 지정된 객체를 검색해 인덱스를 반환<br>
    <br>
  - **`disjoint`** : 2개의 지정된 컬렉션들에서 공통된 요소가 하나도 없는 경우 true 를 반환<br>
    <br>
  - **`copy`** : 지정된 컬렉션의 모든 요소를 새로운 컬렉션으로 복사해 반환<br>
    <br>
  - **`reverse`** : 지정된 컬렉션에 있는 순서를 역으로 변경<br>

  <br><br>


## Collections.max() / min()

> 💡 **주의!**<br>
> 
> 리스트가 비어있을 경우 NoSuchElementException이 발생함
> <br>
> 👉🏻 리스트가 비어있을 경우에 대한 기본값 처리 필수
> ```java
> List<Integer> numbers = List.of(4, 0, 5, 2, 7, 1, 8, 6, 9, 3);
> int max = numbers.isEmpty() ? -1 : Collections.max(numbers);
> System.out.println("Max: " + max); // Max: 9
> ```

<br>  

## Collections.sort()

- 정적(static) 메소드

- List 인터페이스를 구현하는 컬렉션에 대하여 정렬을 수행함

- 속도가 비교적 빠르고, 안정성이 보장되는 **합병 정렬 (Merge sort)** 이용

  > 💡 **안전성?**<br>
  > 
  > 동일한 값을 가지는 원소를 다시 정렬하지 않는 성질<br>
  > 같은 리스트를 반복하여 다른 기준에 따라 정렬할 때 중요하다.<br>
  > ex) 상품 주문 리스트를 날짜를 기준으로 먼저 정렬하고 이후 주문처를 기준으로 정렬<br>
  > 
  > 즉, 한번 정렬된 것이 유지됨 = 안정성 있는 정렬

  <br>

- 정렬은 ***Comparable 인터페이스***를 이용하여 이루어짐<br>
  <br>
    - `List` 인터페이스 : Comparable 인터페이스를 상속 → `Collections.sort()` 이용 가능

<br>

###  📌참고)  Comparable 인터페이스란?


: Java에서 같은 타입의 인스턴스를 서로 비교해야만 하는 클래스들은, 모두 Comparable 인터페이스를 구현하고 있음

- **`Wrapper`** 클래스의 인스턴스들 : Byte, Short, Character, Integer, Float, Double, Boolean, Long 등 👉🏻 정렬 가능 ( ↔ Boolean : 정렬 불가능)
  
  <br>

- **`String`**, **`Time`**, **`Date`** 등의 클래스의 인스턴스들 👉🏻 정렬 가능

  <br>

- 기본 정렬 순서 : 오름차순

  <br>
- `compareTo()` 메소드 : 매체 변수 객체를 현재의 객체와 비교하여 작으면 음수, 같으면 0, 크면 양수 반환


> 💡 (번외) **Comparator<T>**
> : Comparable 인터페이스와 같이 객체를 정렬하는 데에 사용되는 인터페이스<br>
> 
> - 기본은 오름차순 정렬이지만 다른 기준 정렬 가능<br>
> 👉🏻 내림차순, 다른 기준으로 정렬하고 싶을 때 사용 가능<br>
> <br> 
> - compare() 메소드를 재정의하여 사용!



<br><br>

## Collections.shuffle()

- 리스트에 존재하는 정렬을 파괴

- 정렬과는 반대 동작 수행

<br><br>

## Collections.binarySearch()

- 정렬된 리스트에서 지정된 원소를 이진탐색함

  > 💡 **주의!** '정렬된 리스트'에 한해서만 탐색을 진행한다는 점!

- 반환값 = 양수이면 찾고자 하는 원소의 인덱스값을 출력

- 반환값 = 음수 : 탐색이 실패하여 원소를 찾지 못했음을 의미
    - 그러나, 현재 데이터가 삽입될 수 있는 위치 정보를 알려줌
    - 해당 데이터를 삽입할 수 있는 위치 : (-반환값-1)


<br><br>


## Collections.reverse()

- 리스트의 원소들을 역순으로 바꿈

> 💡**주의!** **내림차순 정렬**이 아니라, **현재 순서**를 **거꾸로** 뒤집는 것!
  
  

  
  
