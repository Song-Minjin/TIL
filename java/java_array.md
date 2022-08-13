# Java의 Array란?
### 배열(Array)
- 하나의 변수에 여러 값을 저장하는 데에 쓰이는 정적 리스트(static list)
- 즉, 지정된 자료형(String, int, ···)의 집합을 담는 또 하나의 자료형

  > 💡 **Python의 List와 비교**
  > 
  > Python에서는 `Array`, `ArrayList`, `LinkedList` 등의 자료형이 별도로 존재하지 않으며, 이와 가장 유사한 `List` 자료형이 존재한다.
  Python으로 코딩에 입문한 사람들에게는 많이 생소할 수 있는데, 가장 간단한 특징 즉, 가장 큰 외양에서의 차이점은 아래와 같다.
  
  <br>
  
  > - **Python** : List에 다양한 자료형을 넣을 수 있음
  > ```python
  > person = ['james', 17, 175.3, True]
  > ```
  > 
  > - **Java** : 지정된 자료형만을 넣을 수 있음
  > ```java
  > String[] weekdays = {"월", "화", "수", "목", "금", "토", "일"};
  > int[] days = {1, 2, 3, 4, 5, 6, 7};
  > ```

<br><br>


### 특징
- Array는 처음 생성할 때 지정한 자료형만 넣을 수 있다.

- Array의 배열의 길이는 고정되어 있다.

- 따라서 Array는 길이를 먼저 할당해줘야 한다.

- 이 포스팅에서 주로 살펴볼 것은 1차원 배열이지만, 2차원·3차원 등 다차원 배열도 가능하다. 단, 2차원이 넘어가는 배열은 잘 사용하지 않는다.
<br>

> 💡 **배열에서 `[]`와 `{}`의 차이**
> - `[]` : 자료형과 함께 이것이 배열임을 선언할 때 사용
> - `{}` : 요소들이 있는 배열을 표현할 때 사용  

<br>

### 기초 용어
- **배열 변수 (Array Variable)** : 다른 자료형의 선언과 마찬가지로, 배열을 담는 변수를 말한다. '배열 참조변수'라고도 한다.

- **요소 (element)** : 배열에 들어있는 각각의 값
  
- **인덱스 (index)** : 배열의 요소마다 붙여진 일련 번호이자 고유값. 0부터 시작.

> 👉🏻 **예시**로 살펴보기<br>
>    ```java
>    String[] weekdays = {"월", "화", "수", "목", "금", "토", "일"};
>    ```
>    
>    - 배열 변수 : `weekdays`<br>
>    - 요소 : `"월"`, `"화"`, `"수"`, `"목"`, `"금"`, `"토"`, `"일"`<br>
>    - "월"의 인덱스 : 0<br>
>    - "화"의 인덱스 : 1<br>

<br><br>

## Array 선언

### 1. 빈 Array 선언
: 배열 변수만 선언하기
```java
int[] arr;
int arr[];
```

> 👉🏻 두 방법 중, 이것이 어떤 자료형 Array인지 한 눈에 더 잘 보이기 때문에 위의 표현방식이 조금 더 권장됨!

- 자료형 타입 바로 옆 혹은 배열 변수 옆에 `[]` 기호를 사용하여 선언
- 현재는 배열의 크기를 안 설정해준 상태
- 따라서 현재 `arr`이라는 변수의 값은 `null`

<br><br>


> ❗  그렇다면! **아래의 코드가 에러가 나는 이유**
> 
> - **경우 1**
>  ```java
>   int arr[5];					// 컴파일 오류 발생!
>   ```
>   배열 변수 선언과 동시에 배열의 크기를 지정해서는 안된다. 
>   👉🏻 배열의 **크기**는 **`new`**를 통해 **새 인스턴스**를 만들 때 **지정**!<br><br>
> - **경우 2**
>  ```java
>   String[] arr = new String[];	// 컴파일 오류 발생!
>   ```
>  같은 이유로, 이제는 `new` 연산자로 배열을 초기화해야 하는데 하지 않았기 때문에 역으로 발생하는 오류이다.
>  👉🏻 올바른 순서 : **배열 변수 선언** → 배열의 **길이 할당** → **`new` 연산자**로 **배열 초기화**

<br><br>


### 2. 빈 Array 선언 + 크기 할당
```java
int[] arr = new int[5];		// arr라는 배열의 크기를 5로 고정
```
이는 다음과 같은 과정을 축약한 것일 뿐이다.
```java
int[] arr;
arr = new int[5];
```

<br>


### 3. Array 선언 + 크기 할당 + 초기값 설정
```java
int[] arr = {1, 2, 3, 4, 5};
int[] arr = new int[] {11, 12, 13, 14, 15};
```

<br><br>

## Array 요소의 삽입 / 삭제

### 삽입

- Java에서 Array는 크기를 일단 할당하면, 수정할 수 없다. 따라서 추가 요소를 삽입하기 위해 **Array의 크기를 재조정할 수 있는 방법은 없다.**

- 동적 Array 자료구조가 필요한 경우, Array 대신 ArrayList를 활용하면 된다.

- 그러나 굳이!! Array로 사용하고 싶다면, 새 Array를 인스턴스화해서 사용할 수도 있다. 이 구현에는 또 다양한 방법이 있겠는데, 이 내용은 다음에 다시 깊이 있게 살펴보도록 하겠다.
<br>

### 삭제

- 같은 원리로, Java에서 Array는 고정 크기이기 때문에 Array의 지정된 위치의 요소를 쏙 빼서 삭제하는 것은 불가능하다.

- 따라서 요소의 삭제는 배열 중 해당 인덱스의 요소를 초기값으로 바꾸거나 비우는 방법이 있겠다.

- 예를 들어 각 배열 인덱스에 null값을 설정하거나, 배열 참조에만 null값을 설정할 수 있다. 또 `Arrays` 클래스의 `fill()` 메소드를 사용하여 배열에 기본값을 설정할 수도 있다.

```java
arr[i] = 0;			// arr라는 배열의 i번째 인덱스의 값을 0으로 초기화

Arrays.fill(arr, 0);		// arr이라는 배열의 모든 값을 0으로 초기화
```

<br><br>

## Array 정렬하기
### 1. 오름차순

`Arrays.sort()` 메소드를 활용한다.

```java
import java.util.Arrays;	// 정렬을 위해서는 Arrays 클래스 import

Arrays.sort(arr);		// arr이라는 배열을 오름차순 정렬
```

<br>

### 2. 내림차순

`Collections.reverseOrder()`를 사용한다.

```java
Arrays.sort(arr, Collections.reverseOrder());	// arr이라는 배열을 내림차순 정리
```

단, 주의할 점! int 타입일 때에는 Integer 타입으로 변경 후 정렬해야 한다.
```java
Integer[] new_arr = Arrays.stream(arr).boxed().toArray(Integer[]::new);
```
<br>

> **`Integer` vs `int`**
> 
> 이 내용은 다음 포스팅에서 더욱 심도 있게 알아보도록 하고, 간단히 차이를 알아보자.
> - `int` : primitive 자료형 : long, double, float ...
> - `Integer` : Wrapper 클래스 : 한 객체를 의미

<br><br>

## Array의 길이 구하기

`.length` 를 활용하여 배열의 길이를 구할 수 있다.
  ```java
  int[] arr = {1, 2, 3};
  arr.length	// => 3
  ```

<br>

> 💡 **length의 다른 사용처**
> - `.length()` : 문자열의 길이 구하기
>   ```java
>   str.length() 	// str이라는 문자열의 길이 구하기
>   ```




<br><br><br>


----

**참고 자료**
- https://medium.com/@lunay0ung/java-array-feat-string-vs-char-fea4875fc7ec
- https://dojang.io/mod/page/view.php?id=2200
