파이썬 문제를 풀다가 다음과 같은 코드를 발견했다.

```java
for _ in range(...)
```

이에 파이썬에서 _가 갖는 의미에 대해 간단히 정리하고 넘어가고자 한다.

## Pythond에서의 _

우선 다른 몇 언어와는 다르게, 파이썬에서는 이 언더스코어(_)의 의미가 다양하다.

- Interpreter에서 마지막 값을 저장할 때
  ```
  >>>10
  10
  >>> _
  10
  >>> _ * 3
  30
  >>> _ * 20
  600
  ```

- 값을 무시하고 싶을 때 (= I don't care)
  ```python
  # 언패킹시 특정값을 무시
  x, _, y = (1, 2, 3) # x = 1, y = 3
  
  # 여러개의 값 무시
  x, *_, y = (1, 2, 3, 4, 5) # x = 1, y = 5
  
  # 인덱스 무시 - 인덱스를 사용하지 않음
  for _ in range(10):
      do_something()
  
  # 특정 위치의 값 무시
  for _, val in list_of_tuple:
      do_something()
  ```

- 변수나 함수명에 특별한 의미 또는 기능을 부여하고자 할 때
    1. `_single_leading_underscore`
       : 주로 한 모듈 내부에서만 사용하는 private 클래스/함수/변수/메소드 선언시 사용하는 컨벤션
       ```java
       _internal_name = 'one_module' # private 변수
       _internal_version = '1.0' # private 변수
       ```
       > 💡 **Tip**<br>
       > 이 컨벤션으로 선언하게 되면 `from module import *`시 `_`로 시작하는 것들을 import에서 무시할 수 있다.

    2. `single_trailing_underscore_` : 파이썬 키워드와의 충돌을 피하기 위해 사용하는 컨벤션



- 국제화(Internationalization, i18n) / 지역화(Localization, l10n) 함수로써 사용할 때



- 숫자 리터럴값의 자릿수 구분을 위한 구분자로 사용할 때