# Java IDE
- 요즘은 큰 IT 서비스 회사 중에는 Intellij를 많이 쓴다.
- 단축키 등 다양한 편리한 기능이 eclipse보다 잘 마련되어있다는 것이 큰 장점이다.

<br><br>

# Spring boot 초기 설정하기

- 예전에는 스프링 프로젝트를 밑바닥부터 하나씩 다 만들었다.

- 그러나 요즘 스프링 프로젝트는 스프링 부트를 이용해서 만든다!

- 스프링 부트 스타터 페이지 : https://start.spring.io

<br><br>

👉🏻 다음은 Spring boot의 초기 설정 관련 용어들이다.


## Maven vs Gradle

: 필요한 라이브러리를 가져오고, Build된 Life Cycle를 관리해주는 툴

- **`Maven`** : 과거에 많이 씀. 아직 레거시 프로젝트 등은 Maven으로 남아있는 경우도 있음

- **`Gradle`** : 최근에는 Gradle로 많이 넘어오는 추세. 심지어 스프링 라이브러리 자체도 예전엔 Maven이었지만 Gradle로 넘어옴


<br><br>

## Spring Boot version

- **`SNAPSHOT`** : 아직 만들고 있는 버전

- **`M1`, `M4`** 등 : 아직 정식 Release되지 않은 버전


<br><br>


## Project Metadata

- **`Group`** : 보통 기업명, 기업 도메인 명 등을 작성

- **`Artifact`** : Build되어 나올 때 결과물. 즉, 프로젝트 명이라고 생각하면 된다.


<br><br>


## Dependencies

: Spring boot로 프로젝트를 시작할 건데, 그 중 어떤  library를 가져와서 쓸까?를 정하는 항목

- **Spring Web : 웹 프로젝트를 만들 때 선택

- **`Thymeleaf`** : HTML을 만들어주는 다양한 Template Engine 중 하나. (이는 필수는 아님 - 회사마다 다양한 엔진을 사용한다.)


<br><br>


# 스타터로 생성한 폴더 구조 살펴보기

위의 요소들을 참고하여 생성한 Spring boot의 파일을 살펴보면, 큰 폴더 구조는 다음과 같이 이루어져있다.

```
- .gradle
- .idea
- gradle
- src
	ㄴ main
		ㄴ java
    	ㄴ resources
	ㄴ test

```

그 중 가장 많이 사용할 src 폴더 먼저 살펴보자.

### src 폴더
> 💡 **`main`**과 **`test`**폴더가 있는데, 이는 이제 Gradle이든 Maven이든 이렇게 두 개로 나누는 것이 일반적!

- **`main`** 폴더 : **`java`**와 **`resources`**가 있다.
    - **`java`** 폴더 : 우리가 작성하는 패키지와 소스파일들이 있다.
    - **`resources`** 폴더 : 실제 java 코드 파일을 제외한, xml, html, properties, 설정파일 등이 들어가는 폴더이다.

- **`test`** 폴더 : 테스트코드들과 관련된 소스들이 들어있는 폴더이다.

  ** *👉🏻 테스트코드가 요즘 개발 트렌드에서 그만큼 중요하다는 뜻!* **

<br>

### 그 외 폴더

- `idea` : intellij가 사용하는 설정파일

- `Gradle` : Gradle을 사용하는 폴더

<br>

### 그 외 파일

> 예전에는 Spring이 엄청나게 개발자 친화적인 툴은 아니었다. 그러나 Spring boot가 나오면서, 위에 우리가 했던 스타터 등이 구비됨으로 인해 이제는 개발자 친화적인 프레임워크가 되었다. 특히 다음과 같이 설정파일이 쉽게 제공된다는 점!
> 예를 들면 아래의 build.gradle같은 설정 파일도 예전엔 한 자 한 자 다 작성해야 했다!

- `build.gradle` 파일 : 스타터에서 선택한 version, 언어 등 설정들을 확인할 수 있다. maveCentral이라는 공개된 사이트에서 다운로드 받는 부분도 적혀있으며, 특정 사이트 url을 넣는 것도 가능하다.

  > ❓ **gradle이란?**
>
> 지금은 gradle이 버전 설정 및 라이브러리 import할 수 있게 해주는 툴이라는 정도만 이해하고 넘어가자!
> 당연히 나중에는 알아두면 좋긴 하다.


- `.gitignore` : Git에는 딱 필요한 소스코드 파일만 올라가고, 나머지 build된 결과물 등은 올라가면 안되기 때문에, 그를 기본적으로 스타터가 설정해준 것

- `gradlew`, `gradle.bat` : 나중에 Gradle로 build할 때 살펴보면 된다.

- `setting.gradle` : 이 역시 gradle을 더 심화해서 배워보면 알게 된다.

