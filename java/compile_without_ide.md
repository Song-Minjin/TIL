사실, Eclipse, Intellij와 같은 개발 도구 없이도 java로 만든 프로그램을 컴파일하고 실행할 수 있다.

(개발 도구 없이 개발할 일은 당분간은 거의 없을 것이다.)
(그리고 개발도구 없이 컴파일하는 것은 OS에 대한 충분한 배경 지식이 필요하기 때문에, 어려울 수 있다.)

<br>

## 기본 용어
- **JDK** : Java Development Kit

- **`bin`** : binary폴더. 보통 실행파일을 bin이라고 함

- `Java.exe` : cmd에 `java`라고 치면 실행되는 파일

- `javac.exe` : cmd에 `javac`라고 치면 실행되는 파일. java파일을 컴파일하여 class파일로 만들 때 사용한다.

<br><br>

## Java라고 명령을 내렸을 때 일어나는 일
#### Q. 내가 어느 위치에 있든, java파일이 무조건 실행되는 이유는 무엇인가?
#### A. 환경변수 때문!
- 내 컴퓨터 - 속성 - Advanced System Settings(고급 시스템 설정) - 고급 - 환경변수
: 환경변수 Path가 역할하는 것!
👉🏻 내가 cmd에 java라고 쳤는데 아무 일도 일어나지 않는다? : Path 환경변수를 확인해볼 것!


<br>


## 컴파일 과정

### 1. Compile
> Java 확장자가 붙은 소스코드를 class 확장자가 붙은 실행 파일로 바꾼다.

- `javac Program.java` : Program.java라는 소스코드를 클래스 실행파일로 컴파일하기

<br>


### 2. Run
> Class 확장자가 붙은 파일을 실행하는 것

- `java Program` : 디렉토리에 Program이라는 클래스를 찾아보고, 있으면 그를 실행함
- (linux) `cat Program.java` : Program이라는 파일의 내용을 보여줌

- main 메소드를 먼저 찾고, 그 안의 코드를 순차적으로 실행해줌


#### 다른 사람이 만든 프로그램을 이용하려면?

- `import org.opentutorials.iot.Elevator` : org 폴더 내에 opentutorials 내에 iot 내에 Elevator을 불러오기

👉🏻 `org`부터 `iot` 만큼을 `package`라고 부름

- 소스코드는 내부적으로 패키지 안에 있는 내용들도 필요로 하기 때문에, src 내의 클래스들도 같이 컴파일해줌

- org 폴더를 java 파일과 같은 디렉토리 안에 넣어 주지 않으면 → 오류가 남 : 컴파일하고 있는 파일과 같은 디렉토리에 있지 않기 때문

- `javac --class-path -cp ".:lib"` = `javac -cp ".:lib"` : 다른 경로에 있는 소스파일을 경로를 명시적으로 지정해 실행시켜줌 (`.:`를 적지 않으면 같은 디렉토리에서는 찾지 않음.)

> 💡 **Exception** : Java에서 exception이란 오류가 난 것이라 보면 된다.

<br>

### 3. Input
> 실행할 때, 입력값을 주는 것

```
import javax.swing.JOptionPane;
 
import org.opentutorials.iot.DimmingLights;
import org.opentutorials.iot.Elevator;
import org.opentutorials.iot.Lighting;
import org.opentutorials.iot.Security;
 
public class OkJavaGoInHomeInput {
 
    public static void main(String[] args) {
         
        String id = args[0];
        String bright = args[1];
         
        // Elevator call 
        Elevator myElevator = new Elevator(id);
        myElevator.callForUp(1);
         
        // Security off 
        Security mySecurity = new Security(id);
        mySecurity.off();
         
        // Light on
        Lighting hallLamp = new Lighting(id+" / Hall Lamp");
        hallLamp.on();
         
        Lighting floorLamp = new Lighting(id+" / floorLamp");
        floorLamp.on();
         
        DimmingLights moodLamp = new DimmingLights(id+" moodLamp");
        moodLamp.setBright(Double.parseDouble(bright));
        moodLamp.on();
 
    }
 
}
```


- `javac OkJavaGoInHomeInput.java` : 이 파일이 컴파일 되면서 클래스 파일이 되고, 얘가 참조하는 다른 클래스들도 같이 생길 것임

- `javac OkJavaGoInHomeInput "Java APT 507" 15.0 ` : args[0], args[1]에 각각 들어감 (띄어쓰기로 구분)


