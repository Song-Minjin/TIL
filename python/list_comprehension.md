# List Comprehension



**: 쉽고 간결하게 List를 만들 수 있는 Python의 문법**

- Python의 List : Java 등 타 언어의 배열과 매칭되는 선형 자료구조

<br><br>

## 📌 유형 1 - 표현식 + for문

![](https://velog.velcdn.com/images/sw_smj/post/522ca38e-289b-40a2-8572-9a8ef8f5bce6/image.png)

`result`에 새로운 리스트가 저장되는 과정은 위의 그림과 같다.

즉, 표현식과 for 반복문을 통해 리스트를 한 줄로 정의할 수 있는 것이다.

### 👉🏻 활용 예시

- **n개의 0으로 리스트 초기화하기**
  ```python
  new_list = [ 0 for i in range(5) ]		# => [0, 0, 0, 0, 0]
  ```
<br>

- **0부터 n-1까지 순차적인 숫자로 리스트 초기화하기**
  ```python
  new_list = [ i for i in range(5) ]		# => [0, 1, 2, 3, 4]
  ```
<br>

- **다른 리스트의 값을 그대로 복사하기**
  ```python
  list1 = [ 0, 1, 2, 3, 4, 5, 6, 7, 8, 9 ]
   new_list = [ n for n in list1 ]		# => [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
  ```
<br>

### 👉🏻 활용 예시 2 : 표현식에 연산식/함수를 쓰는 경우

- **다른 리스트의 제곱값을 구하는 리스트 생성하기**
  ```python
  list1 = [0, 1, 2, 3, 4]
   new_list = [ n*n for n in list1 ]		# => [0, 1, 4, 9, 16]
   ```
<br>

- **문자열 리스트의 각 문자열 길이를 저장하는 리스트 생성하기**
  ```python
  str_list = [ "List", "Comprehension", "python"]  
   new_list = [ len(string) for string in str_array]		# => [4, 13, 6]
  ```
<br>

- **5로 나눈 나머지를 저장하는 리스트 생성하기**
  ```python
  list1 = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
<br>

- **5로 나눈 나머지를 return하는 함수 생성**
  ```python
  def mod_5 (number) :
      return number % 5
  ```
<br>

- **표현식에 함수 활용**
  ```
  result = [mod_5(n) for n in list1]   # [0, 1, 2, 3, 4, 0, 1, 2, 3, 4]
  ```

<br><br>

## 📌 유형 2 - 표현식 + for문 + 조건문

![](https://velog.velcdn.com/images/sw_smj/post/b7a5968e-5809-4ef7-a556-1f66a5ceec01/image.png)

유형 1에서 조건문이 하나 더 붙은 유형이다.

### 👉🏻 활용 예시

- **범위 내 짝수만 저장하는 리스트 생성**
  ```python
  new_list = [ n for n in range(10) if n%2 == 0 ]		# => [0, 2, 4, 6, 8]
  ```
  
- **배열에서 양수만 저장하는 리스트**
  ```python
  list1 = [ -1, 0, -4, 24, 5, -10, 2 ]
  new_list = [ n for n in array if n > 0 ]		# => [24, 5, 2]
  ```

<br>


> 💡 **주의!**
>
> 이런 표현 방법이 매우 편리하긴 하지만, 조건문을 100% 자유롭게 활용할 수 있는 것은 아니다.
> - 단일 조건문만 사용이 가능하다. 즉, `else`나 `elif`를 사용할 경우에는 문법 오류가 난다.
>
> - 그렇지만 `if`를 여러 번 사용하는 것은 가능하다. 이 경우에는 두 조건문이 and로 묶인 것과 같은 결과가 나온다.
> ```python
> # 예시 : 3의 배수 중 홀수만 저장하는 리스트 생성하기
> 
> # 방법 1. if를 두 번 사용
> new_list = [ n for n in range(50) if n%3 == 0 if n%2 != 0 ] 		# => [3, 9, 15, 21, 27, 33, 39, 45]
> 
> # 방법 2. 두 if 조건문을 and로 연결
> new_list = [ n for n in range(50) if n%3 == 0 and n%2 != 0 ] 		# => [3, 9, 15, 21, 27, 33, 39, 45]
> ```

<br><br>

## 📌 유형 3 - 표현식 + 조건문 + for문

![](https://velog.velcdn.com/images/sw_smj/post/9ca11f11-b463-45ae-a7b4-00c1dd50d49a/image.png)

### 👉🏻 활용 예시

- **양수는 그대로, 음수는 0으로 저장하는 리스트**
  ```python
  list1 = [-1, 10, -4, 0, 24, 5, -10, 2]
  new_list = [n if n>0 else 0 for n in list1]		# => [0, 10, 0, 0, 24, 5, 0, 2]
  ```
- **짝수라면 'even', 홀수라면 'odd'를 저장하는 리스트**
  ```python
  list1 = [0, 1, 2, 3]
  new_list = ['even' if n%2==0 else 'odd' for n in list1]		# => ['even', 'odd', 'even', 'odd']
  ```

> 💡 **주의**
> 이 경우에는 `if`와 `else`를 사용할 수 있다!


<br><br>

## 📌 유형 4 - 중첩 for문

![](https://velog.velcdn.com/images/sw_smj/post/8f8897f3-3a84-49a7-908f-097f1b8b1f5b/image.png)

중첩된 `for`문도 list comprehension 안에서 사용할 수 있다.

### 👉🏻 **활용 예시**

- **`i*j`를 원소로 넣는 리스트 생성** *(i = 1~3, j = 1~2)*
  ```python
  pos = [ i*j for i in range(1, 4) for j in range(1, 3) ]		# => [1, 2, 2, 4, 3, 6]
  ```

<br><br>

## 📌 유형 5 - 중첩 List Comprehension

![](https://velog.velcdn.com/images/sw_smj/post/373af3b2-a6c0-4362-b7a4-28f81c676861/image.png)

다차원 배열도 List Comprehension으로 선언할 수 있다. 대괄호`[]` 안에 다시 대괄호`[]`를 넣어 중첩된 List Comprehension을 사용하는 방식이다.

이때, 밖에 있는 `for`문부터 확인해나간다.

### 👉🏻 활용 예시

- 2차원 배열 생성
  ```python
  result = [ [ 0 for i in range(2) ] for j in range(3) ] 		# => [ [0, 0], [0, 0], [0, 0] ]
  ```






<br><br>

---

**참고자료**

- mtww2820님 블로그 ([링크 바로가기](https://velog.io/@mttw2820/List-Comprehension-%EB%AC%B8%EB%B2%95-%EC%A0%95%EB%A6%AC#%ED%91%9C%ED%98%84%EC%8B%9D--for%EB%AC%B8--%EC%A1%B0%EA%B1%B4%EB%AC%B8))