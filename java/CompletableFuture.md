
## Future

- Java 5에서 추가됨
- 비동기 작업에 대한 결과값을 반환받을 수 있게 됨

- 한계점
	- 외부에서 완료시킬 수 없으며, get의 타임아웃 설정으로만 완료 가능
	- 블로킹 코드(get)를 통해서만 이후의 결과를 처리할 수 있음
	- 여러 Future를 조합할 수 없음. ex) 회원 정보 가져오기, 알림 발송하기 등
	- 여러 작업을 조합하거나 예외 처리할 수 없음


<br>


## CompletableFuture 클래스

: 기존의 Future를 기반으로 외부에서 완료시킬 수 있어서 CompletableFuture라는 이름을 갖게 됨

- Java 8에서 추가됨

- Future 외에도 [CompletionStage](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/CompletionStage.html) 인터페이스도 구현하고 있음 

- 예를 들어 Future에서는 불가능했던 "몇 초 이내에 응답이 안 오면 기본값을 반환한다." 와 같은 작업이 가능해진 것

- 즉, Future의 진화된 형태로써 외부에서 작업을 완료시킬 수 있을 뿐만 아니라 콜백 등록 및 Future 조합 등이 가능하다는 것이다.

>💡 **CompletionStage 인터페이스** 
>
> : 작업들을 중첩시키거나 완료 후 콜백을 위해 추가됨

<br>



# fk
### 기능들

CompletableFuture가 갖는 작업의 종류는 크게 다음과 같이 구분할 수 있는데, 이에 대해서는 자세히 코드로 살펴보도록 하자.

-   비동기 작업 실행
-   작업 콜백
-   작업 조합
-   예외 처리

<br>


### 비동기 작업 실행

**`runAsync`**
- 반환값이 없는 경우
- 비동기로 작업 실행 콜

**`supplyAsync`**
- 반환값이 있는 경우
- 비동기로 작업 실행 콜

<br>


### 작업 콜백

**`thenApply`**
- 반환 값을 받아서 다른 값을 반환함
- 함수형 인터페이스 Function을 파라미터로 받음

**`thenAccpet`**
- 반환 값을 받아 처리하고 값을 반환하지 않음
- 함수형 인터페이스 Consumer를 파라미터로 받음

**`thenRun`**
- 반환 값을 받지 않고 다른 작업을 실행함
- 함수형 인터페이스 Runnable을 파라미터로 받음

<br>


### 작업 조합

**`thenCompose`**
- 두 작업이 이어서 실행하도록 조합하며, 앞선 작업의 결과를 받아서 사용할 수 있음
- 함수형 인터페이스 Function을 파라미터로 받음

**`thenCombine`**
- 두 작업을 독립적으로 실행하고, 둘 다 완료되었을 때 콜백을 실행함
- 함수형 인터페이스 Function을 파라미터로 받음

**`allOf`**
- 여러 작업들을 동시에 실행하고, 모든 작업 결과에 콜백을 실행함

**`anyOf`**
- 여러 작업들 중에서 가장 빨리 끝난 하나의 결과에 콜백을 실행함

<br>

### 예외 처리

**`exceptionally`**
- 발생한 에러를 받아서 예외를 처리함
- 함수형 인터페이스 Function을 파라미터로 받음

**`handle`, `handleAsync`**
- (결과값, 에러)를 반환받아 에러가 발생한 경우와 아닌 경우 모두를 처리할 수 있음
-   함수형 인터페이스 BiFunction을 파라미터로 받음
<br><br>
----

**참고 자료**

- https://mangkyu.tistory.com/263