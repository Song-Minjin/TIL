# UML

우선, 우리가 볼 클래스 다이어그램이 UML의 한 종류이다. 우선 UML에 대해 살펴보면 다음과 같다.

## UML이란?



**: Unified Modeling Language**

- 도메인(해결하고자 하는 목표)을 모델로 표현해주는 대표적인 모델링 언어

- 소프트웨어를 설계하며 필요에 의해 사용됨

- UML 작성의 목적

    - 의사소통 또는 설계 논의

    - 전체 시스템의 구조 및 클래스의 의존성 파악

    - 유지보수를 위한 설계의 back-end 문서 제작


<br>

# Class Diagram



: 클래스의 구성요소 및 클래스간의 관계를 표현하는 대표적인 UML

- 정적 다이어그램

- 시스템의 일부 또는 전체의 구조를 나타낼 수 있음

- 의존관계를 명확히 보여줌

- 순환 의존이 발생하는 지점을 찾아내서 어떻게 이 순환고리를 깰 수 있을지를 결정하게 해줌

<br>

## 클래스 다이어그램의 사용처

- 문제 해결을 위한 도메인 구조를 나타냄 ➡  추상적인 개념을 기술할 수 있음

- 소프트웨어의 설계 혹은 완성된 소프트웨어의 구현 설명

<br>

## 클래스 다이어그램의 기본 요소

![](https://velog.velcdn.com/images/sw_smj/post/83273235-bac3-44e9-86d4-f655c8dacbad/image.png)

### 접근 제어자

- `+` : `public`
- `-` : `private`
- `#` : `protected`



### Attribute

- 양식 : `접근제어자 클래스이름 : 타입 = 기본값`
- 예시 : `- id : Long`

### Method

- 양식 : `접근제어자 이름(파라미터 속성): 리턴값`
- 예시 : `+ getPassword() : String`
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`+ update(CommentRequestDto) : void`

### etc

- interface : `<<interface>>`
- abstract : `<<abstract>>`

<br>

## 클래스 다이어그램의 관계 표현

![](https://velog.velcdn.com/images/sw_smj/post/d233d1d2-4145-425e-bb53-68d2f02fdbb5/image.png)

<br>

### 👉🏻 관계 1. 일반화(Generalization)



: 우리가 알고 있는 일반적인 '상속'
- 실선 + 비어있는 화살표

![](https://velog.velcdn.com/images/sw_smj/post/325ec13a-e952-4c8a-b1be-01f5afd2d523/image.png)


<br>

### 👉🏻 관계 2. 실체화(Realization)



: interface에 있는 기능을 오버라이딩하여 실제로 구현하는 것

- 점선 + 비어있는 화살표

![](https://velog.velcdn.com/images/sw_smj/post/d85a5e87-8fa6-4f65-88e3-2e2f8120b4d5/image.png)


<br>

### 👉🏻 관계 3. 의존 (Dependency)

> 📌  클래스 다이어그램에서 일반적으로 제일 많이 사용되는 관계!



: 클래스간의 참조가 일어나는 것

- 메소드 내에서 대상 클래스의 객체를 생성, 사용, 리턴받아 사용하는 것

- 참조는 해당 클래스와의 관계를 계속 유지하지는 않음

![](https://velog.velcdn.com/images/sw_smj/post/1d75ebb0-b1fc-4680-b737-54603c6edbd1/image.png)


> 💡 **주의**
>
> 객체 참조 (dependency)는 계속 유지하지 않고, 메소드의 호출이 끝나면 의존관계의 클래스와 관계가 끝난다.


### 👉🏻 관계 4. 연관 (Association, Directed Association)



: 다른 객체의 참조를 가지는 필드

- 실선으로 표현
- 방향성이 존재하는 경우에는 화살표를 넣어 표현

- 둘의 연관관계가 어떻게 되는지 숫자로 표현할 수 있음

**연관관계 숫자 표현**

- `1` : 1개
- `*` : ~n개
- `n...m` : n부터 m까지 연관관계를 맺음

![](https://velog.velcdn.com/images/sw_smj/post/85e4519b-7109-4e3f-bd5b-c0408d3315f5/image.png)

➡ 두 클래스의 관계
- 1(board) : n(Comment)
- 양방향 연관관계
  <br>

**연관관계의 종류**

![](https://velog.velcdn.com/images/sw_smj/post/0114b5ba-b50c-4a9b-bcc5-3c6bfd537d82/image.png)

- **일반적인 Association**
    - 실선 하나로 클래스 연결
    - 방향이 없으므로 User가 Phone을 참조할 수도, Phone이 User를 참조할 수도, 둘 다일수도 있다.

- **Direcred Association**
    - 클래스를 실선으로 연결한 후, 끝에 화살표를 추가함
    - User에서 Phone으로 화살표가 향함 : User가 Phone을 참조함
    - 화살표 옆의 `-Phones` : roleName(역할명) : 어떤 역할로 참조되는지를 의미함

<br>

### 👉🏻 관계 5. 집합(Aggregation) & 합성(Composition)



: Association의 특수한 관계

**Aggregation**

- Association의 집합관계
- Collection이나 Array를 이용하는 관계
- 사실, 1:N 연관관계를 나타낸 것이기 때문에 위의 Association으로 충분히 표현할 수 있다. (사실 이때문에 Aggregation과 Association의 모호성은 지속적으로 논란이 되고 있으며, 아직 결론이 나지 않았다.)

**Composition**

- 클래스 연관관계에서 강한 결합의 관계를 의미함
- 참조하는 클래스의 라이프 사이클이 종속적
- 실선에 채워져있는 다이아몬드로 표시

![](https://velog.velcdn.com/images/sw_smj/post/40796071-6da6-43e0-817f-f0117397edab/image.png)
