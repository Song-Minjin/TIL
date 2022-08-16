# Lombok


: Java 프로젝트를 진행하는데에 거의 필수적으로 필요한 메소드/생성자 등을 자동생성해주는 라이브러리
- 코드를 절약할 수 있음

<br>

## 설치하는 법
1. IDE의 Settings(환경설정)에 들어가서 'Annotation Processors'를 입력한다.

2. 우측 'Enable ~' 체크 박스에 체크하고 OK 클릭
   ![](https://velog.velcdn.com/images/sw_smj/post/2d8eca1a-47b3-4ff4-8276-92b2c014e761/image.png)


3. `Shift` 두 번 누르고 `plugins` 입력 후 `엔터`

4. 'lombok' 입력 후 `install` → IDE 재시작

5. 다시 `shift` 두 번 누르고 plugins 입력 후 `엔터`

<br>

## 사용하는 법

#### Example
- `Post.java`
    - `Post` 클래스 `Getter`, `NoArgsConstructor` 적용 가능
- `PostService.java`
    - `PostService` 클래스 `RequiredArgsConstructor` 적용

  