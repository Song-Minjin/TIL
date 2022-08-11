**'프로그램'**이라는 것은 **'입력을 받아 출력을 만들어내는 것'**이라고 정의할 수 있다.

Java에 한정짓지 않고 프로그램에서는 다양한 것들이 입력값이 될 수 있다.

- Argument : 프로그램을 실행할 때 텍스트 정보를 입력할 수 있음
- File : 파일의 내용을 읽어와서 입력할 수 있음
- Network : 웹상에서 정보를 읽어와 입력값으로 사용할 수 있음
- Audio : 음성을 입력할 수 있음
- Program : 다른 프로그램이 출력한 결과를 입력할 수 있음

<br>


## 입력값을 받기

### 간단한 입력대화상자로 받기(Swing)
`JOptionPane.showInputDialog()`

```
import javax.swing.JOptionPane;
 
import org.opentutorials.iot.DimmingLights;
import org.opentutorials.iot.Elevator;
import org.opentutorials.iot.Lighting;
import org.opentutorials.iot.Security;
 
public class OkJavaGoInHomeInput {
 
    public static void main(String[] args) {
         
        String id = JOptionPane.showInputDialog("Enter a ID");        
        
        // Elevator call 
        Elevator myElevator = new Elevator(id);
        myElevator.callForUp(1);
         
        // Security off 
        Security mySecurity = new Security(id);
        mySecurity.off();
         
 
```


### 입력할 대상과 내가 입력할 값의 타입을 일치시키기!
> **Parsing(파싱)** : 구문 분석. 컴퓨터과학에서는, 주어진 정보를 내가 원하는대로 가공하여 원하는 때 불러올 수 있도록 하는 것을 칭한다.

```
import javax.swing.JOptionPane;

import org.opentutorials.iot.DimmingLights;
import org.opentutorials.iot.Lighting;
 
public class OkJavaGoInHomeInput {
 
    public static void main(String[] args) {
         
        String id = JOptionPane.showInputDialog("Enter a ID");
        String bright = JOptionPane.showInputDialog("Enter a Bright level");
         

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


- `Double.parseDouble()` : 문자열에서 더블형으로 바꾸는 메소드
