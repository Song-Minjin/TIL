# Java의 ArrayList란?

### ArrayList

- java.util 패키지에 소속되어 있음

- Collection 프레임워크의 일부이며, List 인터페이스를 상속받은 클래스 중 하나

  > 관련 포스팅 바로 가기 👉🏻 [ [Java] Collection 프레임워크와 Collection 인터페이스](https://velog.io/@sw_smj/Java-%EC%BB%AC%EB%A0%89%EC%85%98-%ED%94%84%EB%A0%88%EC%9E%84%EC%9B%8C%ED%81%ACCollection-Framework%EC%99%80-%EC%BB%AC%EB%A0%89%EC%85%98-%EC%9D%B8%ED%84%B0%ED%8E%98%EC%9D%B4%EC%8A%A4Collection-Interface)


- 하나의 변수에 같은 자료형을 가진 여러 값을 저장하는 데에 쓰이는 동적 리스트(static list)


<br>

### 특징
- 배열과는 다르게 크기가 가변적으로 변함

- ArrayList 역시 내부에서 처음 설정한 저장 용량이 있지만, 데이터 추가 시 공간이 부족한 경우 배열 크기를 1.5배로 증가시킴

- ArrayList는 초기화시 사이즈를 할당하지 않아도 되는데, 그럼 자동으로 default capacity = 10으로 설정됨

- 메모리 공간을 자동으로 빈 공간이 없게 관리함

- 단, 특정 인덱스를 추가/삭제하면 임시 배열을 생성한 후 처리하는 방식

  👉🏻 잦은 삽입/삭제 시에는 `LinkedList`를 사용하는 것이 보다 효율적임


<br><br>


## Array와 ArrayList의 차이

### 특징

| | Array |ArrayList|
|--|--|--|
|크기|고정적, 정적<br>(초기화시 할당하여 고정)|유동적, 동적<br>(초기화시 사이즈를 표시 X) |
|데이터타입|primitive type, Object 가능 <br>(int, byte, char 등)|Object element만 가능|
|데이터 변경|요소의 추가/삭제 불가| 요소의 추가/삭제 가능|
|타입 안정성|낮음<br>(Generic 사용 불가)|높음<br>(Generic 사용 가능)|
|다차원|가능<br>int[]][] Arr = new int[2][3]|불가능|

> 💡 **Generic**
> : 데이터타입을 일반화(generalize)한다는 의미
>
> 클래스나 메소드에서 사용할 **내부 데이터타입을 컴파일 시 미리 지정**하는 방법이다.
> - **장점**
    >   - 클래스나 메소드 내부에서 사용되는 객체 안정성을 높임
>   - 반환값에 대한 타입변환 및 타입 검사에 들어가는 비용 감소


<br><br>

## ArrayList와 LinkedList의 성능 차이

> 💡 이번 포스팅에서는 LinkedList를 다루지 않지만, ArrayList와 LinkedList는 같은 인터페이스 내에 있는컬렉션들인 만큼 속도, 성능에 대하여 자주 비교되고, 그에 따라 선택되고는 한다.

||ArrayList|LinkedList|
|--|--|--|
|검색|O(1)<br>인덱스 기반의 자료구조|최악의 경우 O(N)<br>앞에서부터 하나씩 탐색|
|삽입/삭제|최악의 경우 O(N)<br>데이터를 복사해서 재할당|O(1)<br>이전, 이후 노드의 참조만 변경|
||

우선 두 리스트는 인터페이스만 같을 뿐 내부적으로 동작하는 방식이 다르다. 따라서 상황에 따라 성능에 차이가 있기 때문에, 상황에 따라 적절한 자료구조를 사용해야 한다.

<br><br>

## Vector란?
: ArrayList와 거의 유사한, 초기 자바 버전의 클래스

- 예전에 Java가 제공했던 레거시 클래스 - Collections 프레임워크가 없던 초기 자바 버전에서 정의한 인터페이스

- 현재는 재구성 및 설계되어 Collections 프레임워크와도 완벽하게 호환됨

- Collection 프레임워크의 일부이며, 역시 java.util 패키지에 속해있음

- ArrayList와 동일한 구조를 가지며, 자동으로 크기가 조절됨

- 동기화(Synchronize)가 되기 때문에 한 번에 하나의 스레드만 접근 가능

- 스레드 안전(Thread Safe) : 멀티 스레드 프로그래밍에서 여러 스레드가 동시에 접근했을 때 문제가 되지 않음. 멀티 스레드 환경에 적절

- Collection 프레임워크에 없는 메서드들을 사용 가능

- 단, 정말 초기에 만들었기 때문에 초기 버전 호환성이 필요한 환경, 멀티 스레드가 아닌 환경에서는 거의 사용되지 않음




<br><br>

# ArrayList의 활용

<br>

## ArrayList 선언

### 필수! 선언 전 import

```java
import java.util.ArrayList;
```
<br>

### 1. 빈 ArrayList 선언
: 배열 변수, 타입만 지정

```java
ArrayList<Integer> integers1 = new ArrayList<Integer>();	// 타입 지정

ArrayList<Integer> integers2 = new ArrayList<>();	// 타입 생략 가능
```

<br>

### 2. 빈 ArrayList 선언 + 초기 용량 설정
```java
ArrayList<Integer> integer3 = new ArrayList<>(10);
```

<br>


### 3. ArrayList 선언 + 다른 Collection 값으로 초기화
```java
ArrayList<Integer> integer4 = new ArrayList<>(integer1);
```

<br>


### 4. ArrayList 선언 + 기본 값들 설정

```java
ArrayList<Integer> integer5 = new ArrayList<>(Arrays.asList(1, 2, 3, 4, 5));
```

- `Arrays.asList` : Arrays의 정적 클래스인 ArrayList를 리턴함

  > 💡**주의! `Arrays.asList`**
  > - `java.util.ArrayList`에 속하는 것이 아닌, `java.util.Arrays`에 속하는 메서드이다.
  > - ArrayList의 자료형이 아닌 Arrays의 정적 클래스를 불러오기 때문에, 아래와 같이 선언하면 삽입/삭제가 되지 않는다.
  > ```java
  > List<String> arrayList1 = Arrays.asList(1, 2, 3, 4, 5);
  > ```
  > 👉🏻 이렇게 초기화를 하면, 변수는 원래 만들어진 배열의 인스턴스를 가리킴.

- 따라서  ArrayList 클래스에 생성자를 활용해서 ArrayList의 인스턴스를 참조하도록 하여야 정상적으로 삽입/삭제가 가능한 ArrayList로 생성된다.

<br><br>


## ArrayList 요소의 삽입 / 변경 / 삭제

### 삽입
#### add 메서드


```java
arr2.add("apple");
arr2.add(0, "grape");
```
- `.add()` : 기본적으로 리스트의 가장 끝에 값을 추가

- 별도로 인덱스를 지정하면, 해당 인덱스에 값이 추가되고 그 인덱스부터 값들이 한 칸씩 밀림

<br>

### 변경
#### set 메서드


```java
arr2.set(0, "apple");
```

- `.set(i, 값)` : i번째 index의 값이 지정한 값으로 변경됨


<br>


### 삭제

#### 1. remove 메서드

```java
arr2.remove(1); 	// 1번째 인덱스의 값 삭제
arr2.remove("apple");	//apple이라는 값 삭제

// value가 1인 element 삭제
arr1.remove(Integer.valueOf(1));	// index 1의 값을 혼동하여 삭제하지 않기 위해 Integer 객체 전달
```

- **`.remove()`** : 인덱스를 입력하거나, 지정한 값을 직접 입력하여 ArrayList에서 삭제

- 지정한 값과 일치하는 값이 여러개라면, 첫 번째 값만 삭제

<br>

```java
String removed_one = arr2.remove(0);
System.out.println("삭제된 과일은" + removed_one);
```
- 값을 지움과 동시에 해당 값으로 별도 작업을 원하는 경우, 바로 리턴 받아서 사용 가능

<br>

```java
// value가 1인 element 모두 삭제
list2.removeAll(list1);
```

- `removeAll(Collection<?> c)` : 파라미터로 Collection을 넘겨줘야 함

- Collection 객체에 담긴 element들을 대상 리스트에서 모두 삭제

- list = list2 - list1이 된다.



<br>

#### 2. clear 메서드

```java
arr2.clear();
```
- `.clear()` : ArrayList 안의 내용을 전체 삭제


<br><br>

## ArrayList에 값의 존재유무 확인

```java
boolean check = arr1.contains("apple");
```
- 값이 있는 경우, check라는 변수에 true값 반환


<br><br>

## ArrayList 정렬하기
### 1. 오름차순

`Collections.sort()` 메소드를 활용한다.

```java
import java.util.Collections;	// 정렬을 위해서 Collections 클래스 import

Collections.sort(arr_list1);		// arr_list1이라는 리스트를 오름차순 정렬
```

<br>

### 2. 내림차순

`Collections.reverseOrder()`를 사용한다.

```java
Collections.sort(arr_list1, Collections.reverseOrder());	// arr_list1이라는 리스트를 내림차순 정렬
```

<br>

> 💡 **Arrays.sort vs Collections.sort**
>
> Array는 왜 Arrays.sort를 쓰고, ArrayList는 Collections.sort를 쓸까?
>
> 👉🏻 **Array**는 `java.util.Arrays`에 포함되어있고, **ArrayList**는 `java.util.Collections`에 포함되어있기 때문!

<br><br>

## Array의 길이 구하기

`.size()` 를 활용하여 배열의 길이를 구할 수 있다.
  ```java
  ArrayList<Integer> sizeTest = new ArrayList<>(Arrays.asList(1, 2, 3, 4, 5));
 System.out.println(sizeTest.size()); 	// => 5
  ```
