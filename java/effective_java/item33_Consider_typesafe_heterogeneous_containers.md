# 들어가기 전에 - Container란?

객체의 저장이라는 관점에서, 가장 쉽게 떠올릴 수 있는 것은 배열(Array)이다. 특히 원시(Primitive)타입의 값들을 저장하여 다룰 때 많이 사용한다. 하지만 배열은 동적 할당이 쉽지 않다는 제약이 존재한다.

따라서 이러한 문제의 해결 방안으로, `java.util` 라이브러리에는 컨테이너(`Container`) 클래스들이 있으며, 기본 타입들로는 `List`, `Set`, `Queue`, `Map` 등이 있다.

## Container Usage (feat. Generics)

```java
import java.util.ArrayList;

class Apple {

    private static long counter;
    private final long id = counter++;

    public long id() {
        return id;
    }
}

class Orange {
}

/**
 * @author Jupyo Hong
 */
public class ApplesAndOrangesWithoutGenerics {

    @SuppressWarnings("unchecked")
    public static void main(String[] args) {
        
        @SuppressWarnings("rawtypes")
        ArrayList apples = new ArrayList();
        
        for(int i = 0; i < 3; i++) {
            apples.add(new Apple());
        }
        
        // 같은 컨테이너에 다른 타입의 객체(Orange)를 추가해도 막지 않는다
        apples.add(new Orange());
        
        for(int i = 0; i < apples.size(); i++) {
            // Orange 타입의 요소를 가져와 id() 메서드를 호출할때 
            // RuntimeException 이 발생한다.
            ((Apple)apples.get(i)).id(); 
        }
    }
}
```

- 위 코드의 주석처럼, ArrayList 컨테이너를 생성할때 Generic을 지정하지 않으면, 아무 Type 이나 객체를 저장할 수 있다. 
- 이는 당연히 두번째 for 문에서처럼 Apple 타입으로 캐스팅 후에 id() 메서드를 호출할때 발생하는 RuntimeException 때문에 문제가 된다. (Orange 클래스에는 id() 메서드가 없기 때문이다.)

 따라서 아래와 같이 제네릭을 지정해두면, 지정한 Type외에 다른타입을 추가하려고 할때 Compile 시점에서 Error를 발생시켜 실수를 방지 할 수 있다. 또한 컨테이너에서 요소를 꺼낼때도, 캐스팅을 할 필요없이 제네릭으로 지정한 Type으로 알아서 캐스팅해준다. 아래와 같다.

```java
ArrayList<Apple> apples = new ArrayList<Apple>();

apples.add(new Orange()); // Compile Error 발생!
```

따라서 제네릭을 사용하면 컨테이너에 넣는 객체의 Type을 컴파일러가 확인해주고, 구문도 더 깔끔해진다.

```java
ArrayList<apple> apples = new ArrayList<apple>();
        
for(int i=0; i<3; i++) {
    apples.add(new Apple());
}       
        
for(int i=0; i<apples.size(); i++) {
    System.out.println(apples.get(i).id()); // 캐스팅을 하지 않는다.
}
```
<br>

## Container Library

자바 컨테이너 라이브러리는 다음과 같은 두 개의 서로 다른 개념으로 나뉜다.

### Collection


: 하나 이상의 규칙이 적용되는 개별적인 요소들을 모아 놓은 것
- List : Sequencial 하게 객체들을 저장함
- Set : 중복요소를 가질 수 없음
- Queue : Queuing Discipline 에 의해 결정된 순서로 요소들을 산출함

### Map


: 키(key)와 그에 대응되는 값(value)의 쌍으로 구성되는 객체들을 모아 놓은 것
- key를 사용하여 값을 검색할 수 있다.
- 연관 배열(associative array)이라고도 한다.

<br>

## 단일 원소 컨테이너

### 1. ThreadLocal
일반 변수의 수명은 특정 코드 블록(예, 메서드 범위, for 블록 범위 등) 범위 내에서만 유효하다.

```java
{
    int a = 10;
    ...
   // 블록 내에서 a 변수 사용 가능
}
// 변수 a는 위 코드 블록이 끝나면 더 이상 유효하지 않다. (즉, 수명을 다한다.)
```

반면에 ThreadLocal을 이용하면 쓰레드 영역에 변수를 설정할 수 있기 때문에, 특정 쓰레드가 실행하는 모든 코드에서 그 쓰레드에 설정된 변수 값을 사용할 수 있게 된다. 아래 그림은 쓰레드 로컬 변수가 어떻게 동작하는 지를 간단하게 보여주고 있다.

![](https://velog.velcdn.com/images/sw_smj/post/ff532a8d-bccd-4d75-944c-05ef5d8829c2/image.png)

위 그림에서 주목할 점은 동일한 코드를 실행하는 데, 쓰레드1에서 실행할 경우 관련 값이 쓰레드1에 저장되고 쓰레드2에서 실행할 경우 쓰레드2에 저장된다는 점이다.


#### ThreadLocal 기본 사용법

1. `ThreadLocal` 객체를 생성한다.
2. `ThreadLocal.set()` 메서드를 이용해서 현재 쓰레드의 로컬 변수에 값을 저장한다.
3. `ThreadLocal.get()` 메서드를 이용해서 현재 쓰레드의 로컬 변수 값을 읽어온다.
4. `ThreadLocal.remove()` 메서드를 이용해서 현재 쓰레드의 로컬 변수 값을 삭제한다.

```java
// 현재 쓰레드와 관련된 로컬 변수를 하나 생성한다.
ThreadLocal<UserInfo> local = new ThreadLocal<UserInfo>();

// 로컬 변수에 값 할당
local.set(currentUser);

// 이후 실행되는 코드는 쓰레드 로컬 변수 값을 사용
UserInfo userInfo = local.get();
```

### 2. AtomicReference

#### AtomicReference 사용법

- **`get`**
  ```java
  public void atomicReference1() {
      AtomicReference<Integer> atomic = new AtomicReference<>();
      System.out.println("atomic : " + atomic.get());
  
      AtomicReference<Integer> atomic2 = new AtomicReference<>(10);
      System.out.println("atomic2 : " + atomic2.get());
  }
  ```
  ```
  atomic : null
  atomic2 : 10
  ```

- **`getAndSet`**
  ```java
  public void atomicReference3() {
      AtomicReference<Integer> atomic = new AtomicReference<>(10);
      System.out.println("value(before setting) : " + atomic.getAndSet(20));
      System.out.println("value(after setting) : " + atomic.get());
  }
  ```
  ```
  value(before setting) : 10
  value(after setting): 20
  ```

<br>

# item 33 - Generic And Container

제네릭은 컬렉션(`Set<E>`, `Map<K, V>` 등)과, 단일 원소 컨테이너(`ThreadLocal<T>`, `AtomicRederence<T>`)에도 흔히 사용된다. 이런 모든 쓰임에서, 매개변수화 되는 대상은 원소가 아닌, 컨테이너 자신이다.

따라서 하나의 컨테이너에서 매개변수화할 수 있는 타입의 수가 제한된다. 예를 들어, `Set`에는 단 하나의 타입 매개변수, `Map`에는 2개의 타입 매개변수가 필요한 식이다.

<br>

## Type safe heterogeneous container pattern(타입 안전 이종 컨테이너 패턴)

하지만 더 유연한 수단이 필요할 때가 있다. 이럴 경우, 컨테이너 대신 키를 매개변수화한 다음, 컨테이너에 값을 넣거나 뺄 때 매개변수화한 키를 함께 제공하는 방법이 있다. 이렇게 하면 제네릭 타입 시스템이 값의 타입이 키와 같음을 보장해줄 수 있다. 이러한 설계 방식을 타입 안전 이종 컨테이너 패턴이라 한다.

### 예시 : Favorites Class


: 타입별로 즐겨찾는 인스턴스를 저장하고 검색할 수 있는 클래스

- 각 타입의 Class 객체를 매개변수화한 키 역할로 사용하면 되는데, 이 방식이 동작하는 이유는 class의 클래스가 제네릭이기 때문이다.

  > ** 📌 즉! class 리터럴의 타입은 Class가 아니라 Class<T>이다.**
  >- `String` class의 타입 : `Class<String>`
  >- `Integer` class의 타입 : `Class<Integer>`

- 컴파일타임 타입 정보와 런타임 타입 정보를 알아내기 위해 메서드들이 주고받는 class 리터럴을 타입 토큰(type token)이라 한다.

```java
public class Favorites {
    public <T> void putFavorite(Class<T> type, T instance);
    public <T> T getFavorite(Class<T> type);
}
```

클라이언트는 즐겨찾기를 저장하거나 얻어올 때 Class 객체를 알려주면 된다.

```java
public static void main(String[] args) { 
    Favorites f = new Favorites();
    
    f.putFavorite(String.class, "Java");
    f.putFavorite(Integer.class, 0xcafebabe);
    f.putFavorite(Class.class, Favorites.class);

    String favoriteString = f.getFavorite(String.class);
    int favoriteInteger = f.getFavorite(Integer.class); 
    Class<?> favoriteClass = f.getFavorite(Class.class);

    System.out.printf("%s %x %s%n", favoriteString, favoriteInteger, favoriteClass.getName());
}
```

- `Favorites` 인스턴스는 타입 안전하다. 즉, `String`을 요청했는데 `Integer`를 반환하는 일은 절대 없다.

- 또, 모든 키의 타입이 제각각이라 일반적인 맵과 달리 여러 가지 타입의 원소를 담을 수 있다.

➡️ Favorites는 타입 안전 이종(heterogeneous) 컨테이너이다.

<br>

### Favorites의 구현

```java
public class Favorites {
    private Map<Class<?>, Object> favorites = new HashMap<>();

    public <T> void putFavorite(Class<T> type, T instance) {     
        favorites.put(Objects.requireNonNulKtype), instance);
    }

    public <T> T getFavorite(Class<T> type) { 
        return type.cast(favorites.get(type));
    } 
}
```

- `Favorites`가 사용하는 private 맵 변수인 `favorites`의 타입은 `Map<Class<?>，Object〉`이다.
  - 비한정적 와일드카드 타입이라 이 맵 안에 아무것도 넣을 수 없다고 생각할 수 있지만, 사실은 그 반대다. 와일드카드 타입이 중첩(nested)되었다는 점을 깨달아야 한다.
  - 맵이 아 니라 키가 와일드카드 타입인 것이다.
  ➡️ 이는 모든 키가 서로 다른 매개변수화 타입일 수 있다는 뜻으로, 첫 번째는 `Class<String>`, 두 번째는 `Class<Integer>` 식으로 될 수 있다. 다양한 타입을 지원하는 힘이 여기서 나온다.

- `favorites` 맵의 값 타입은 단순히 Object이다. 즉, 이 맵은 키와 값 사이의 타입 관계를 보증하지 않는다는 말이다. 즉, 모든 값이 키로 명시한 타입임을 보증하지 않는다.
  - 사실 자바의 타입 시스템에서는 이 관계를 명시할 방법이 없다. 하지만 우리는 이 관계가 성립함을 알고 있고, 즐겨찾기를 검색할 때 그 이점을 누리게 된다.

- `putFavorite` 구현은 아주 쉽다. 주어진 Class 객체와 즐겨찾기 인스턴스를 `favorites`에 추가해 관계를 지으면 끝이다. 말했듯이, 키와 값 사이의 ‘타입 링크(type linkage)’ 정보는 버려진다. 즉, 그 값이 그 키 타입의 인스턴스라는 정보가 사라진다. 하지만 `getFavorite` 메서드에서 이 관계를 되살릴 수 있으니 상관없다.

- `getFavorite` 코드는 `putFavorite`보다 강조해두었다. 먼저, 주어진 Class 객체에 해당하는 값을 `favorites` 맵에서 꺼낸다. 이 객체가 바로 반환해야 할 객체가 맞지만，잘못된 컴파일타임 타입을 가지고 있다. 이 객체의 타입은 (favorites 맵의 값 타입인) Object이나, 우리는 이를 T로 바꿔 반환해야 한다.
  - 따라서 getFavorite 구현은 Class의 cast 메서드를 사용해 이 객체 참조를 Class 객체가 가리키는 타입으로 동적 형변환한다.

  > **cast 메서드**
  > : 형변환 연산자의 동적 버전
  > 이 메서드는 단순히 주어진 인수가 Class 객체가 알려주는 타입의 인스턴스인지를 검사한 다음，맞다면 그 인수를 그대로 반환하고, 아니면 `ClassCastException`을 던진다. 
> 클라이언트 코드가 깔끔히 컴파일된다면 `getFavorite`이 호출하는 cast는 `ClassCastException`을 던지지 않을 것임을 우리는 알고 있다. 다시 말해 `favorites`맵 안의 값은 해당 키의 타입과 항상 일치함을 알고 있다.

> **그런데 cast 메서드가 단지 인수를 그대로 반환하기만 한다면 굳이 왜 사용하는 것일까?**
> 그 이유는 cast 메서드의 시그니처가 Class 클래스가 제네릭이라는 이점을 완벽히 활용하기 때문이다. 
> 다음 코드에서 보듯 cast의 반환 타입은 Class 객체의 타입 매개변수와 같다.
> ```java
> public class Class<T> { 
>     T cast(Object obj);
> }
> ```
> 이것이 정확히 getFavorite 메서드에 필요한 기능으로, T로 비검사 형변환하는 손실 없이도 Favorites를 타입 안전하게 만드는 비결이다.

<br>

#### Favorites 클래스의 제약

#### 1. 악의적인 클라이언트가 Class 객체를 (제네릭이 아닌) 로 타입(아이템 26)으로 넘기면 Favorites 인스턴스의 타입 안전성이 쉽게 깨진다.

하지만 이렇게 짜여진 클라이언트 코드에서는 컴파일할 때 비검사 경고가 뜰 것이다. 
- `HashSet`과 HashMap 등의 일반 컬렉션 구현체에도 똑같은 문제가 있다.
  - HashSet의 로 타입을 사용하면 HashSet<Integer>에 String을 넣는 건 아주 쉬운 일이다.
  - 그렇기는 하지만, 이 정도의 문제를 감수하겠다면 런타임 타입 안전성을 얻을 수 있다. 

Favorites가 타입 불변식을 어기는 일이 없도록 보장하려면 putFavorite 메서드에서 인수로 주어진 instance의 타입이 type으로 명시 한 타입과 같은지 확인하면 된다. 그 방법은 이미 알고 있듯，다음 코드와 같이 그냥 동적 형변환을 쓰면 된다.

```java
public <T> void putFavorite(Class<T> type, T instance) {     
    favorites.put(Objects.requireNonNull(type), type.cast(instance));
}
```

> **`java.util.Collections` - `checkedSet`, `checkedList`, `checkedMap`**
> : 바로 위의 그 방식을 적용한 컬렉션 래퍼들이다.
> - 이 정적 팩터리들은 컬렉션(혹은 맵)과 함께 1개(혹은 2개)의 Class 객체를 받는다.
> - 이 메서드들은 모두 제네릭이라 Class 객체와 컬렉션의 컴파일타임 타입이 같음을 보장한다.
> - 또한 이 래퍼들은 내부 컬렉션들을 실체화한다.
>    예컨대 런타임에 Coin을 Collection<Stamp>에 넣으려 하면 ClassCastException을 던진다.
> - 이 래퍼들은 제네릭과 로 타입을 섞어 사용하는 애플리케이션에서 클라이언트 코드가 컬렉션에 잘못된 타입의 원소를 넣지 못하게 추적하는 데 도움을 준다.

#### 2. 실체화 불가 타입(아이템 28)에는 사용 할 수 없다.

- 다시 말해, 즐겨 찾는 `String`이나 `String[]`은 저장할 수 있어도 즐겨 찾는 `List<String>`은 저장할 수 없다. 
  - `List<String>`을 저장하려는 코드는 컴파일되지 않을 것이다. List<String>용 Class 객체를 얻을 수 없기 때문이다.
  - `List<String>.class`라고 쓰면 문법 오류가 난다.
     `List<String>`과 `List<Integer>`는 `List.class`라는 같은 Class 객체를 공유하므로, 만약 `List<String>.class`와 `List<Integer>.class`를 허용해서 둘 다 똑같은 타입의 객체 참조를 반환한다면 Favorites 객체의 내부는 아수라장이 될 것이다.

- 이 두 번째 제약에 대한 완벽히 만족스러운 우회로는 없다.

<br>

## 한정적 타입 토큰
  

: 단순히 한정적 타입 매개변수(아이템 29)나 한정적 와일드카드(아이템 31)를 사용하여 표현 가능한 타입을 제한하는 타입 토큰
  

- `Favorites`가 사용하는 타입 토큰은 비한정적이다. 즉，`getFavorite`과 `putFavorite`은 어떤 Class 객체든 받아들인다. 때로는 이 메서드들이 허용하는 타입을 제한하고 싶을 수 있는데，한정적 타입 토큰을 활용하면 가능하다. java 애너테이션 API(아이템 39)는 한정적 타입 토큰을 적극적으로 사용한다. 예를 들어 다음은 `AnnotatedElement` 인터페이스에 선언된 메서드로，대상 요소에 달려 있는 애너테이션을 런타임에 읽어 오는 기능을 한다. 이 메서드는 리플렉션의 대상이 되는 타입들，즉 클래스(`java.lang.Class<T>`)，메서드(`java.lang.reflect.Method`), 필드(`java.lang, reflect.Field`) 같이 프로그램 요소를 표현하는 타입들에서 구현한다.
  
```java
public <T extends Annotation>
  	T getAnnotation(Class<T> annotationType);
```

여기서 `annotationType` 인수는 애너테이션 타입을 뜻하는 한정적 타입 토큰이다. 이 메서드는 토큰으로 명시한 타입의 애너테이션이 대상 요소에 달려 있다면 그 애너테이션을 반환하고，없다면 `null`을 반환한다. 즉，애너테이션된 요소는 그 키가 애너테이션 타입인，타입 안전 이종 컨테이너인 것이다.
  
`Class<?>` 타입의 객체가 있고，이를 (getAnnotation처럼) 한정적 타입 토큰을 받는 메서드에 넘기려면 어떻게 해야 할까? 객체를 `Class<? extends Annotation>`으로 형변환할 수도 있지만，이 형변환은 비검사이므로 컴파일
하면 경고가 뜰 것이다(아이템 27). 운 좋게도 Class 클래스가 이런 형변환을 안전하게 (그리고 동적으로) 수행해주는 인스턴스 메서드를 제공한다. 바로 `asSubclass` 메서드로，호출된 인스턴스 자신의 `Class` 객체를 인수가 명시한 클래스로 형변환한다(형변환된다는 것은 이 클래스가 인수로 명시한 클래스의 하위 클래스라는 뜻이다). 형변환에 성공하면 인수로 받은 클래스 객체를 반환하고, 실패하면 `ClassCastException`을 던진다.

다음은 컴파일 시점에는 타입을 알 수 없는 애너테이션을 `asSubclass` 메서드를 사용해 런타임에 읽어내는 예다. 이 메서드는 오류나 경고 없이 컴파일된다.

```java
static Annotation getAnnotation(AnnotatedElement element,
String annotationTypeName) {

	Class<?> annotationType = null; // 비한정적 타입 토큰
	try {
		annotationType = Class.forName(annotationTypeName);
	} catch (Exception ex) {
  		throw new IllegalArgumentException(ex);
	}
	
  	return element.getAnnotation(
  		annotationType.asSubclass(Annotation.class));
}
```
`asSubclass`를 사용해 한정적 타입 토큰을 안전하게 형변환한다.



<br><br>

—-

**참고 자료**
- [Hong’s Store House](http://asuraiv.blogspot.com/2015/05/java-container.html)