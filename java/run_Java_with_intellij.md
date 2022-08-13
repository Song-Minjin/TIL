## Java 실행 속도를 조금 더 빠르게 하는 꿀팁!


인텔리제이에서, 요즘은 가끔 자동 설정으로 Build할 때 Java를 인텔리제이가 직접 실행하는 것이 아니라 Gradle을 통해 실행 시킬 때가 있다.

👉🏻 이렇게 되면 실행 속도가 조금 느려지는데, 이를 방지하기 위해 설정을 직접 바꿀 수 있다.


<br>

### 방법

우선 설정 창(Settings)을 연다!


> 💡 **Settings 단축키**
> IntelliJ에서 `ctrl` + `alt` + `s`를 누르면 바로 Settings 창을 띄울 수 있다.
> (만약 까먹었다면 그냥 상단 바에서 File -> Settings를 찾으면 됨)

<br>

그 다음 아래와 같이 설정을 바꿔준다.


1. Settings에서 'Gradle'을 검색

   ![](https://velog.velcdn.com/images/sw_smj/post/15581578-dd59-401e-84e0-07eec060a2a6/image.png)


2. Gradle project → Build and run 부분을 찾음

   ![](https://velog.velcdn.com/images/sw_smj/post/3462951b-645e-458b-a038-a6b98adab059/image.png)


3. Build and run using 이 `Gradle(Default)`로 설정되어 있다면 이를 `Intellij IDEA`로 바꿔준다!

   ![](https://velog.velcdn.com/images/sw_smj/post/760d892a-4dec-4cb2-9f7d-4c847841d65c/image.png)


4. 바로 아래 Run tests using도 똑같이 Intellij IDEA로 바꿔주면 끝!
   
   ![](https://velog.velcdn.com/images/sw_smj/post/3a813cde-28b7-4461-88bd-5b65929ea305/image.png)




<br>

이렇게 설정을 해주면 Gradle을 통하지 않고 Intellij에서 Java를 바로 실행시켜주기 때문에, 훨씬 빨리 실행이 되게 된다.
