# 이도영 202230123
## 6월 5일 (13주차)
### 자바의 이벤트 처리
독립 클래스로 Action 이벤트 리스너 만들기

```java
import java.awt.*;
import java.awt.event.*;
import javax.swing.*;

public class ex9_1 extends JFrame{
    public ex9_1() {
        setTitle("Action 이벤트 리스너 예제");
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);

        Container c = getContentPane();
        c.setLayout(new FlowLayout());
        JButton btn = new JButton("Action");
        btn.addActionListener(new MyActionListener()); //Action 이벤트 리스너 달기
        c.add(btn);

        setSize(250,120);
        setVisible(true);
    }
    public static void main(String [] args){
        new ex9_1();
    }
}

//독립된 클래스로 이벤트 리스너를 작성한다
class MyActionListener implements ActionListener{
    public void actionPerformed(ActionEvent e){
        JButton b = (JButton)e.getSource(); // 이벤트 소스 버튼 알아내기
        if(b.getText().equals("Action")) // 버튼의 문자일여 "Action"인지 비교
            b.setText("액션"); // 버튼의 문자열을 "액션"으로 변경
        else
            b.setText("Action"); // 버튼의 문자열을 "Action"으로 변경
    }
}
```

내부 클래스로 Action 이벤트 리스너 만들기


```java
import java.awt.*;
import java.awt.event.*;
import javax.swing.*;

public class ex9_2 extends JFrame{
    public ex9_2() {
        setTitle("Action 이벤트 리스너 예제");
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);

        Container c = getContentPane();
        c.setLayout(new FlowLayout());
        JButton btn = new JButton("Action");
        btn.addActionListener(new MyActionListener());
        c.add(btn);

        setSize(200,120);
        setVisible(true);
    }

    //내부 클래스로 Action 리스너를 작성한다.
    private class MyActionListener implements ActionListener {
        public void actionPerformed(ActionEvent e) {
            JButton b = (JButton)e.getSource();
            if(b.getText().equals("Action"))
                b.setText("액션");
            else
                b.setText("Action");

            ex9_2.this.setTitle(b.getText());
        }
    }
    public static void main(String [] args) {
        new ex9_2();
    }
}
```

익명 클래스로 이벤트 리스너 작성

  익명 클래스(anonymous class) : 이름 없는 클래스
  (클래스 선언 + 인스턴스 생성)을 한번에 달성
  간단한 리스너의 경우 익명 클래스 사용 추천
  메소드의 개수가 1, 2개인 리스너(ActionListener, ItemListener) 에 대해 주로 사용
  마우스 이벤트 리스너 작성 연습 - 마우스로 문자열 이동시키기

```java
import java.awt.*;
import java.awt.event.*;
import javax.swing.*;

public class ex9_4 extends JFrame{
    private JLabel la = new JLabel("Hello"); // "Hello" 문자열을 출력하기 위한 레이블

    public ex9_4() {
        setTitle("Mouse 이벤트 예제");
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        Container c = getContentPane();
        c.addMouseListener(new MyMouseListener()); // 컨텐트팸에 이벤트 리스너 달기

        c.setLayout(null); // 컨텐트팬의 배치관리자 삭제
        la.setSize(50,20); // 레이블의 크기 50x20 설정
        la.setLocation(30, 30); // 레이블의 위치 (30, 30)으로 설정
        c.add(la); // 레이블 삽입
        
        setSize(200, 200);
        setVisible(true);
    }

    class MyMouseListener implements MouseListener {
        public void mousePressed(MouseEvent e) {
            int x = e.getX();
            int y = e.getY();
            la.setLocation(x, y);
        }
        public void mouseReleased(MouseEvent e) {}
        public void mouseClicked(MouseEvent e) {}
        public void mouseEntered(MouseEvent e) {}
        public void mouseExited(MouseEvent e) {}
    }

    public static void main(String [] args) {
        new ex9_4();
    }
}
```

어댑터 클래스

  이벤트 리스너 구현에 따른 부담
  리스너의 추상 메소드를 모두 구현해야 하는 부담
  예) 마우스 리스너에서 마우스가 눌러지는 경우(mousePressed())만 처리하고자 하는 경우에도 나머지 4 개의 메소드를 모두 구현해야 하는 부담

어댑터 클래스(Adapter)
  리스너의 모든 메소드를 단순 리턴하도록 만든 클래스(JDK에서 제공)
  추상 메소드가 하나뿐인 리스너는 어댑터 없음
  ActionAdapter, ItemAdapter 클래스는 존재하지 않음

Key 이벤트와 포커스

  키 입력 시, 다음 세 경우 각각 Key 이벤트 발생

  키를 누르는 순간
  누른 키를 떼는 순간
  누른 키를 떼는 순간(Unicode키의 경우에만)
  키 이벤트를 받을 수 있는 조건

모든 컴포넌트
  현재 포커스(focus)를 가진 컴포넌트가 키 이벤트 독점

포커스(focus)

  컴포넌트나 응용프로그램이 키 이벤트를 독점하는 권한
  컴포넌트에 포커스 설정 방법: 다음 2 라인 코드 필요

KeyListener

응용프로그램에서 KeyListener를 상속받아 키 리스너 구현
유니코드(Unicode) 키

  유니코드 키의 특징

  국제 산업 표준
  전 세계의 문자를 컴퓨터에서 일관되게 표현하기 위한 코드 체계
  문자들에 대해서만 키 코드 값 정의: AZ, az, 0~9, !, @, & 등
  문자가 아닌 키 경우에는 표준화된 키 코드 값 없음

  Function 키, Home 키, UP 키, Delete 키, Control 키, Shift 키, Alt 키 등은 플랫폼에 따라 키 코드 값이 다를 수 있음
  유니코드 키가 입력되는 경우

  keyPressed(), keyTyped(), keyReleased() 가 순서대로 호출
  유니코드 키가 아닌 경우
  keyPressed(), keyReleased() 만 호출됨
  가상 키와 입력된 키 판별

KeyEvent 객체

  입력된 키 정보를 가진 이벤트 객체
  KeyEvent 객체의 메소드로 입력된 키 판별
  KeyEvent 객체의 메소드로 입력된 키 판별

  char KeyEvent.getKeyChar()
  키의 유니코드 문자 값 리턴
  Unicode 문자 키인 경우에만 의미 있음
  입력된 키를 판별하기 위해 문자 값과 비교하면 됨

### 스윙 컴포넌트 활용
자바의 GUI 프로그래밍 방법

컴포넌트 기반 GUI 프로그래밍

스윙 컴포넌트를 이용하여 쉽게 GUI를 구축
자바에서 제공하는 컴포넌트의 한계를 벗어나지 못함
그래픽을 이용하여 GUI 구축

그래픽 기반 GUI 프로그래밍
개발자가 직접 그래픽으로 화면을 구성하는 부담
독특한 GUI를 구성할 수 있는 장접
GUI 처리의 실행 속도가 빨라, 게임 등에 주로 이용
스윙 컴포넌트의 공통 메소드, JComponent의 메소드

JComponent
스윙 컴포넌트의 멤버를 모두 상속받는 슈퍼 클래스, 추상 클래스
스윙 컴포넌트들이 상속받는 공통 메소드와 상수 구현










## 5월 29일 (12주차)
### 자바 GUI 스윙 기초
#### 컨테이너와 컴포넌트

컨테이너
  다른 컴포넌트를 포함할 수 있는 GUI 컴포넌트 : java.awt.Container를 상속받음
  다른 컨테이너에 포함될 수 있음
  AWT 컨테이너 : Panel, Frame, Applet, Dialog, Window
  Swing 컨테이너 : JPanel, JFrame, JApplet, JDialog, JWindow


컴포넌트
  컨테이너에 포함되어야 화면에 출력될 수 있는 GUI 객체
  다른 컴포넌트를 포함할 수 없는 순수 컴포넌트
  모든 GUI 컴포넌트가 상속받는 클래스 : java.awt.Component
  스윙 컴포넌트가 상속받는 클래스 : Javax.swing.Jconponent
  최상위 컨테이너

  다른 컨테이너에 포함되지 않고도 화면에 출력되며, 독립적으로 존재 가능한 컨테이너
  스스로 화면에 자신을 출력하는 컨테이너 : JFrame, JDialog, JApplet
  컨테이너와 컴포넌트의 포함관계

  최상위 컨테이너를 바닥에 깔고,
  그 위에 컨테이너를 놓고,
  다시 컴포넌트를 쌓아가는 방식,
  즉 레고 블록을 쌓는 듯이 GUI 프로그램을 작성

Swing GUI 프로그램 만들기
  스윙 GUI 프로그램을 만드는 과정
  스윙 프레임 만들기
  main() 메소드 작성
  스윙 프레임에 스윙 컴포넌트 붙이기
  스윙 프로그램 작성에 필요한 import문

```java
import java.awt.*; // 그래픽 처리를 위한 클래스들의 경로명
import java.awt.event.*; // AWT 이벤트 사용을 위한 경로명
import java.swing.*; // 스윙 컴포넌트 클래스들의 경로명
import java.swing.event.*; // 스윙 이벤트를 위한 경로명****
```

Swing 프레임
  스윙 프레임: 모든 스윙 컴포넌트를 담는 최상위 컨테이너
  JFrame을 상속받아 구현
  컴포넌트들은 화면에 보이려면 스윙 프레임에 부착되어야 함
  프레임을 닫으면 프레임에 부착된 모든 컴포넌트가 보이지 않게 됨

스윙 프레임(JFrame)기본 구성
  프레임: 스윙 프로그램의 기본 틀
  메뉴바: 메뉴들이 부착되는 공간
  컨텐트팬: GUI 컴포넌트들이 부착되는 공간
  프레임 만들기, JFrame 클래스 상속

스윙프레임
  JFrame 클래스를 상속받은 클래스 작성
  프레임의 크기를 반드시 지정: setSize() 호출
  프레임을 화면에 출력하는 코드 반드시 필요: setVisible(true) 호출
  300x300 크기의 스윙 프레임 만들기

```java
import javax.swing.*;

public class ex8_1 extends JFrame {
    public ex8_1() {
        setTitle("300x300 스윙 프레임 만들기");
        setSize(300, 300); // 프레임 크기 300x300
        setVisible(true); // 프레임 출력
    }

    public static void main(String[] args) {
        ex8_1 frame = new ex8_1();
    }
}
```
Swing 응용프로그램에서 main()의 기능과 위치

  스윙 응용프로그램에서 main()의 기능 최소화 바람직
  스윙 응용프로그램이 실행되는 시작점으로서의 기능만
  스윙 프레임을 생성하는 정도의 코드로 최소화

```java
public static void main(String [] args) {
  MyFrame frame = new MyFrame(); // 스윙 프레임 생성
}
```
frame 객체를 생성하고 사용하지 않기 때문에 worrying이 발생
실무에서는 다음과 같이 코딩하는 것이 일반적




## 5월 15일 (11주차)

### 모듈과 패키지 개념, 자바 패키지 활용

###모듈 개념

  Java 9에서 도입된 개념
  패키지와 이미지 등의 리소스를 담은 컨테이너
  모듈 파일(.mod)로 저장
  자바 플랫폼의 모듈화

자바 플랫폼

  자바의 개발 환경(JDK)와 자바의 실행 환경(JRE)를 지칭. Java SE(자바 API) 포함
  자바 API의 모든 클래스가 여러 개의 모듈로 재구성됨
  모듈 파일은 JDK와 jmods 디렉터리에 저장하여 배포
  모듈 파일로부터 모듈을 푸는 명령
  jmod extract "C:\Program Files\Java\jdk-1.0.3+7\jmods\java.base.jmod"
  현재 디렉터리에 java.base 모듈이 패키지와 클래스들로 풀림
  테스트를 할 때는 temp 디렉토리를 만들어서 하는 것이 좋음
  자바 모듈화의 목적

  자바 컴포넌트들을 필오에 따라 조립하여 사용하기 위함
  컴퓨터 시스템의 불필요한 부담 감소
  세밀한 모듈화를 통해 필요 없는 모듈이 로드되지 않게 함
  소형 IoT 장치에도 자바 응용프로그램이 실행되고 성능을 유지하게 함

JDK의 주요 패키지

  java.lang
    스트링, 수학 함수, 입출력 등 자바 프로그래밍에 필요한 기본적인 클래스와 인터페이스
    자동으로 import 됨- import 문 필요 없음
  java.util
    날짜, 시간, 벡터, 해시맵 등의 유틸리티 클래스와 인터페이스
  java.io
    키보드, 모니터, 프린터 등의 입출력 클래스와 인터페이스
  java.awt
    GUI 프로그래밍에 필요한 AWT 클래스와 인터페이스
  javax.swing
    스윙 GUI 프로그래밍에 필요한 클래스와 인터페이스
  
Object 클래스

  모든 자바 클래스는 반드시 Object를 상속받도록 자동 컴파일
  모든 클래스의 수퍼 클래스
  모든 클래스가 상속받는 공통 메소드 포함
  주요 메소드
  boolean equals(Object obj)
  Class getClass()
  int hashCode
  String toString()
  void notify()
  void notifyAll()
  void wait()

객체 속성

  Object 클래스는 객체의 속성을 나타내는 메소드 제공
  hashCode() 메소드
  객체의 해시코드 값을 리턴하며, 객체마다 다름
  getClass() 메소드
  객체의 클래스 정보를 담은 Class 객체 리턴
  Class 객체의 getName() 메소드는 객체의 클래스 이름 리턴
  toString() 메소드
  객체를 문자열로 리턴
  
  
  Object 클래스로 겍체의 속성 알아내기
```java
class Point {
    private int x, y;
    public Point(int x, int y){
        this.x = x; this.y = y;
    }
}

public class ex6_1 {
    public static void main(String[] args) {
        Point p = new Point(2,3);
        System.out.println(p.getClass().getName());
        System.out.println(p.hashCode());
        System.out.println(p.toString());
    }
}
결과: Point
804564176
Point@2ff4acd0
```
toString() 메소드, 객체를 문자열로 변환

각 클래스는 toString()을 오버라이딩하여 자신만의 문자열 리턴 가능
  객체를 문자열로 반환
  원형: public String toString();


Point 클래스에 toString() 작성
```java
class Point {
    private int x, y;
    public Point(int x, int y){
        this.x = x; this.y = y;
    }
    public String toString() {
        return "Point(" + x + "," + y + ")";
    }
}

public class ex6_2 {
    public static void main(String[] args) {
        Point a = new Point(2,3);
        System.out.println(a.toString());
        System.out.println(a); // a는 a.toString()으로 자동 변환됨
    }
}
결과: Point(2, 3)
Point(2, 3)
```




## 5월 8일 (10주차)

### 상속
추상 클래스

추상 메소드(abstract method): abstract로 선언된 메소드, 메소드의 코드는 없고 원형만 선언

```java
abstract public String getNane(); //추상 메소드
abstract public String fail() { retrun "Good Bye";} // 추상 메소드 아님. 컴파일 오류
```

### 추상 클래스(abstract class)

  추상 메소드를 가지며, abstract로 선언된 클래스
  추상 메소드 없이, abstract로 선언한 클래스

```java
// 추상 메소드를 가진 추상 클래스
abstract class shape {
  public Shape() {...}
  public void edit() {...}

  abstract public void draw(); //추상 메소드
}

// 추상 메소드 없는 추상 클래스
abstract class JComponent{
  String name;
  public void load(String name){
    this.name = name;
  }
}
```
추상 클래스의 인스턴스 생성 불가

  추상 클래스는 온전한 클래스가 아니기 때문에 인스턴스를 생성할 수 없음

```java
JComponent p; // 오류 없음. 추상 클래스의 레퍼런스 선언
p = new JComponent(); // 컴파일 오류. 추상 클래스의 인스턴스 생성 불가
Shape obj = new Shape(); //컴파일 오류. 추상 클래스의 인스턴스 생성 불가
```

### 추상 클래스의 상속과 구현

  추상 클래스 상속
  추상 클래스를 상속받으면 추상 클래스가 됨
  서브 클래스도 abstract로 선언 해야 함

```java
abstract class A { // 추상 클래스
  abstract public int add(int x, int y); //추상 메소드
}
abstract class B extends A {  // 추상 클래스
  public void show() {System.out.println("B");}
}

A a = new A(); // 컴파일 오류. 추상 클래스의 인스턴스 생성 불가
B b = new B(); // 컴파일 오류. 추상 클래스의 인스턴스 생성 불가
```

### 추상 클래스 구현
  서브 클래스에서 슈퍼 클래스의 추상 메소드 구현(오버라이딩)
  추상 클래스를 구현한 서브 클래스는 추상 클래스 아님

```java
class C extends A { // 추상 클래스 구현. C는 정상 클래스
  public int add (int x, int y) {return x+y; } //추상 메소드 구현. 오버라이딩
  public void show() {System.out.println("C"); }
}

C c = new C(); // 정상
```

### 추상 클래스의 목적

추상 클래스의 목적
상속을 위한 슈퍼 클래스로 활용하는 것
서브 클래스에서 추상 메소드 구현
다형성 실현

### 추상 클래스의 구현

```java
abstract class Calculator {
    public abstract int add(int a, int b); // 두 정수위 합을 구하여 리턴
    public abstract int substract(int a, int b); // 두 정수의 차를 구하여 리턴
    public abstract double average(int[] a); // 정수 배열의 평균 리턴
}
```
```java
public class ex5_5 extends Calculator {
    @Override
    public int add(int a, int b) { // 추상 메소드 구현
        return a + b;
    }
    @Override
    public int substract(int a, int b){ // 추상 메소드 구현
        return a - b;
    }
    @Override
    public double average(int[] a) { // 추상 메소드 구현
        double sum = 0;
        for(int i=0; i<a.length; i++)
            sum += a[i];
        return sum/a.length;
    }
    public static void main(String [] args) {
        ex5_5 c = new ex5_5();
        System.out.println(c.add(2,3));
        System.out.println(c.substract(2,3));
        System.out.println(c.average(new int [] {2,3,4}));
    }
}
결과: 5
-1 
3.0
```

### 자바의 인터페이스

  소프트웨어를 규격화된 모듈로 만들고, 인터페이스 맞는 모듈을 조립하듯이 응용프로그램을 작성 하기 위해서 사용


  클래스가 구현해야 할 메소드들이 선언되는 추상형
  인터페이스 선언: Interface 키워드로 선언.

```java
interface PhoneInterface { // 인터페이스 선언
  public static final int TIMEOUT = 10000; // 상수 필드. public static final 생략 가능
  public abstract void sendCall(); // 추상 메소드. public abstract 생략 가능
  public abstract void receiveCall(); // 추상 메소드. public abstract 생략 가능
  public default void printLogo() { // 디폴트 메소드는 public 생략 가능
    System.out.println("** Phone **");
  } //디폴트 메소드
}
```

### 인터페이스 구성 요소들의 특징

  상수: public만 허용, public static final 생략
  추상 메소드: public abstract 생략 가능
  default 메소드:
  인터페이스에 코드가 작성된 메소드
  인터페이스를 구현하는 클래스에 자동 상속
  public 접근 지정만 허용. 생략 가능
  private 메소드:
  인터페이스 내에 메소드 코드가 작성되어야 함
  인터페이스 내에 있는 다른 메소드에 의해서만 호출 가능
  static 메소드: public, private 모두 지정 가능. 생략하면 public

### 자바 인터페이스 특징
  인터페이스의 객체 생성 불가


```java
new PhoneInterface(); // 오류. 인터페이스 PhoneInterface 객체 생성 불가
```

인터페이스 타입의 레퍼런스 변수 선언 가능
```java
PhoneInterface galaxy; //galaxy는 인터페이스에 대한 레퍼런스 변수
```

### 인터페이스 상속

  인터페이스 간에 상속 가능:
  인터페이스를 상속하여 확장된 인터페이스 작성 가능
  extends 키워드로 상속 선언

```java
interface MobilePhoneInterface extends PhoneInterface {
  void sendSMS(); // 추상 메소드 추가
  void receiveSMS(); // 추상 메소드 추가
}
```

### 인터페이스 구현

  인터페이스의 추상 메소드를 모두 구현한 클래스 작성
  implements 키워드 사용
  여러 개의 인터페이스 동시 구현 가능
  
  인터페이스 구현 사례
    PhoneInterface 인터페이스를 구현한 SamsungPhone 클래스
```java
class SamsungPhone inplemets PhoneInterface { // 인터페이스 구현
  // PhoneInterface의 모든 메소드 구현
  public void sendCall() {System.out.println("띠리리리링");}
  public void receiveCall() {System.out.println("전화가 왔습니다.");}

  // 메소드 추가 작성
  public void flash() {System.out.println("전화기에 불이 켜젔습니다.");}
}
```
### 모듈과 패키지 개념, 자바 패키지 활용
패키지 개념과 필요성

  3명이 분담하여 자바 응용프로그램을 개발하는 경우, 동일한 이름의 클래스가 존재할 가능성 있음
  -> 합칠 때 오류 발생 가능성
  -> 개발자가 서로 다른 디랙터리로 코드 관리하여 해결
  자바의 패키지와 모듈이란?

패키지(package)

  서로 관련된 클래스와 인터페이스를 컴파일한 클래스 파일들을 묶어 놓은 디렉터리
  하나의 응용프로그램은 한 개 이상의 패키지로 작성
  패키지는 jar 파일로 압축할 수 있음
  
모듈(module)

  여러 패키지와 이미지 등의 자원을 모아 놓은 컨테이너
  하나의 모듈을 하나의 .jmod 파일에 저장
  Java 9부터 모듈화 도입

플랫폼의 모듈화: Java 9부터 자바 API의 모든 클래스들(자바 실행 환경)을 패키지 기반에서 모듈들로 완전히 재구성
응용프로그램의 모듈화: 클래스들은 패키지로 만들고, 다시 패키지를 모듈로 만듦. 모듈 프로그래밍은 복잡
자바 모듈화의 목적

모듈화의 목적

  Java 9부터 자바 API를 여러 모듈로 분할: Java 8까지는 rt.jar의 한 파일에 모든 API 저장 # 현재 70개로 정리됨
  응용프로그램이 실행할 때 꼭 필요한 모듈들로만 실행 환경 구축: 메모리 자원이 열악한 작은 소형 기기에 꼭 필요한 모듈로 구성된 작은 크기의 실행 이미지를 만들기 위함
  모듈의 현실

  Java 9부터 전면적으로 도입

  복잡한 개념

  큰 자바 응용프로그램에는 개발, 유지보수 등에 적합

  현실적으로 모듈로 나누어 자바 프로그램을 작성할 필요 없음

  모듈화 작업은 매우 중요한 개념이며, 소규모 프로젝트부터 적용해야 대형 프로젝트 쉽게 도입, 활용 가능

자바 API의 모듈 파일들

  자바 JDK에 제공되는 모듈 파일들
  자바가 설치된 jmods 디렉터리에 모듈 파일 존재: .jmod 확장자를 가진 파일. 모듈은 수 십개. 모듈 파일은 ZIP 포맷으로 압축된 파일 -> 포맷이 zip이며 확장자는 .jmod
  모듈 파일에는 자바 API의 패키지와 클래스들이 들어 있음
  java.base.jmod 파일을 풀어 놓은 사례

  java.base.jmod 파일을 풀면, 모듈에 있는 패키지와 클래스를 볼 수 있다
  패키지 사용하기, import문

  다른 패키지에 작성된 클래스 사용
  import를 이용하지 않는 겅우 -> 소스에 클래스 이름의 완전 경로명 사옹


디폴트 패키지

  package 선언문이 없는 자바 소스 파일의 경우
  컴파일러는 클래스나 인터페이스를 디폴트 패키지에 소속시킴
  디폴트 패키지 -> 현재 디렉터리
  VS Code에서 Java Package 생성하기 1

  Eclipse 보다도 간단히 만들 수 있음
  일반적으로 package는 com.foo.test와 같이 도메인의 역순으로 만드는 것이 일반적
  먼저 다음과 같은 디렉터리 구조 생성. 한 번에 com/foo/test로 입력해도 좋음

  클래스 파일에 package com.foo.test

  VS Code에서 Java Package 생성하기 2

  Explorer 아래쪽의 "JAVA PROECTS"를 클릭하면 package의 계층 구조를 볼 수 있음
  사용자 정의 package를 만든 후 사용하려면 import 키워드 사용
  // 파일: src/com/example/utils/HelloUtill.java
  // 파일: src/com/example/Main.java
  어떤 클래스 파일에서 package선언을 생략하면 default package에 속함
  같은 기본 패키지에 있는 다른 클래스에서는 import 없이 사용 가능 -> 5장까지 했던 방식
  default package에 속해 있으면 다른 package를 사용할 수 없음
  실제 프로젝트에서는 거의 모든 클래스가 명시적으로 package를 선언

package의 운영 방법

  패키지 이름은 도메인 기반으로 시작(일반 관례)형식: com.회사이름.프로젝트명.기능명 -> 충돌 방지(전 세계 어디서든 유일한 패키지명 확보 가능) / 모듈별 분리 가능
  기능/역할별로 하위 패키지를 구분: utils, controllerm service 등
  디렉토리 구조와 package 선언을 정확히 일치해야 함
  import는 필요한 만큼만 * 전체 import는 피하는 것이 좋음




## 4월 18일 (9주차)
## 클래스와 객체
static 메소드의 제약 조건 2

  static 메소드에서는 this 사용 불가
  static 메소드는 객체 없이도 사용 가능하므로, this 레퍼런스 사용할 수 없음
  
final 클래스와 메소드

final 클래스 - 더 이상 클래스 상속 불가능

```java
final class FinalClass{
  ....
}
class SubClass extends FinalClass{ // 컴파일 오류 발생
  .....
}
```
final 메소드 - 더 이상 오버라이딩 불가능
```java
public class SuperClass{
  protected final int finalMethod(){...}
}
class SubClass extends Superclass{ // SubClass가 SuperClass를 상속받음
  protected in finalMethod(){...} // 컴파일 오류. finalMethod() 오버라이딩 할 수 없음
}
```
final 필드

  final 필드: 상수를 선언할 때 사용
  상수 필드는 선언 시에 초기 값을 지정하여야 한다
  상수 필드는 실행중에 값을 변경할 수 없다

## 상속(inheritance)
상속(inheritance)의 필요성

클래스 사이의 멤버 중복 선언 불필요 - 클래스의 간결화
클래스들의 계층적 분류로 클래스 관리 용이
클래스 재사용과 확장을 통한 소프트웨어의 생산성 향상
클래스 상속과 객체

상속 선언: extends 키워드 사용
부모 클래스를 돌려받아 자식 클래스를 확장한다는 의미
부모 클래스 -> 슈퍼 클래스(super class)
자식 클래스 -> 서브 클래스(sub class)

```java
class Point{
  int x, y;
}
class ColorPoint extends Point{ //Point를 상속받는 ColorPoint 클래스 선언

}
```
ColorPoint는 Point를 물려 받으므로, Point에 선언된 필드나 메소드를 재 선언할 필요가 없음
  
  클래스 상속 - Point와 ColorPoint 클래스

(x,y)의 한 점을 표현하는 Point 클래스와 이를 상속받아 점에 색을 추가한 ColorPoint 클래스

```java
class Point {
    private int x, y; // 한 점을 구성하는 x, y 좌표
    public void set(int x, int y){
        this.x = x; this.y = y;
    }
    public void showPoint(){ // 점의 좌표 출력
        System.out.println("(" + x + "," + y + ")");
    }
}

class ColorPoint extends Point{ //Point를 상속받은 ColorPoint 선언
    private String color; // 점의 색
    public void setColor(String color){
        this.color = color;
    }
    public void showColorPoint(){ // 컬러 점의 좌표 출력
        System.out.print(color);
        showPoint(); // Point 클래스의 set() 호출
    }
}

public class ex5_1{
    public static void main(String[] args) {
        Point p = new Point(); // Point 객체  생성
        p.set(1,2); // Point 클래스의 set() 호출
        p.showPoint();

        ColorPoint cp = new ColorPoint(); // ColorPoint 객체 생성
        cp.set(3,4); // Point 클래스의 set() 호출
        cp.setColor("red"); // ColorPoint 클래스의 setColor() 호출
        cp.showColorPoint(); // 컬러와 좌표 출력
    }
}
결과: (1,2)
red(3,4)
```
### 서브 클래스 객체의 모양

  슈퍼 클래스 객체와 서브 클래스의 객체는 별개
  서브 클래스 객체는 슈퍼 클래스 멤버 포함

### 자바 상속의 특징

  클래스 다중 상속(multiple inheritance) 불허
  하나의 클래스가 둘 이상의 부모 클래스를 동시에 상속받는 것을 말한다

  C++는 다중 상속 가능
  C++는 다중 상속으로 멤버가 중복 생성되는 문제 있음(다이아몬드 상속)
  부모 클래스 간에 계층적 관계가 있을 경우, 중복된 멤버가 생성될 수 있음 모호성(Ambiguity)문제: 두 부모 클래스에 동일한 이름의 멤버(변수나 함수)가 존재할 경우, 어떤 부모의 멤버를 호출해  야 할 지 모호해짐

### 자바는 인터페이스(interface)의 다중 상속 허용
다중 상속과 유사한 기능을 제공

모든 자바 클래스는 묵시적으로 Object클래스 상속받음
java.lang.Object는 클래스는 모든 클래스의 슈퍼 클래스
슈퍼 클래스의 멤버에 대한 서브 클래스의 접근

슈퍼 클래스의 private 멤버: 서브 클래스에서 접근 할 수 없음
슈퍼 클래스의 디폴트 멤버: 서브 클래스가 동일한 패키지에 있을 때, 접근 가능
슈퍼 클래스의 public 멤버: 서브 클래스는 항상 접근 가능
슈퍼 클래스의 protected 멤버:
같은 패키지 내의 모든 클래스 접근 허용
패키지 여부와 상관없이 서브 클래스는 접근 가능

protected 멤버

슈퍼 클래스의 protected 멤버에 대한 접근: 같은 패키지의 모든 클래스에게 허용
상속되는 서브 클래스가 같은 패키지든 다른 패키지든 상관 없이 허용
서브 클래스/슈퍼 클래스의 생성자 호출과 실행

서브 클래스의 객체가 생성될 때: 슈퍼클래스 생성자와 서브 클래스 생성자 모두 실행
호출 순서: 서브 클래스의 생성자 먼저 호출 -> 슈퍼 클래스 생성자 호출
실행 순서: 슈퍼 클래스의 생성자가 먼저 실행 -> 서브 클래스의 생성자 실행
서브 클래스에서 슈퍼 클래스 생성자 선택

슈퍼 클래스와 서브 클래스: 각각 여러 개의 생성자 작성 가능
서브 클래스의 객체가 생성될 때: 슈퍼 클래스 생성자 1개와 서브 클래스 생성자 1개가 실행
서브 클래스의 생성자와 슈퍼 클래스의 생성자가 결정되는 방식
개발자의 병시적 선택
서브 클래스 개발자가 슈퍼 클래스의 생성자 명시적 선택
super() 키워드를 이용하여 선택
컴파일러가 기본 생성자 선택
서브 클래스 개발자가 슈퍼 클래스의 생성자를 선택하지 않는 경우
컴파일러가 자동으로 슈퍼 클래스의 개본 생성자 선택
컴파일러에 의해 슈퍼 클래스의 기본 생성자가 묵시적 선택

개발자가 서브 클래스의 생성자에 대해 슈퍼 클래스의 생성자를 명시적으로 선택하지 않은 경우
서브 클래스의 매개 변수를 가진 생성자에 대해서도 슈퍼 클래스의 기본 생성자가 자동 선택

개발자가 서브 클래스의 생성자에 대해 슈퍼 클래스의 생성자를 명시적으로 선택하지 않은 경우
super()로 슈퍼 클래스의 생성자 명시적 선택

super(): 서브 클래스에서 명시적으로 슈퍼 클래스의 생성자 선택 호출
사용방식
super(parameter);
인자를 이용하여 슈퍼 클래스의 적당한 생성자 호출
반드시 서브 클래스 생성자 코드의 제일 첫 라인에 와야 함
super()를 활용한 ColorPoint 작성

```java
class Point{
    private int x, y; //한 점을 구성하는 x, y 좌표
    public Point(){
        this.x = this.y = 0;
    }
    public Point(int x, int y){
        this.x = x; this.y = y;
    }
    public void showPoint() {// 점의 좌표 출력
        System.out.println("(" + x + "," + y + ")");
    }
}

class ColorPoint extends Point{ // Point를 상속받은 ColorPoint 선언
    private String color; // 점의 색
    public ColorPoint(int x, int y, String color){
        super(x, y); // Point의 생성자 Point(x, y) 호출
        this.color = color;
    }
    public void showColorPoint() { // 컬러 점의 좌표 출력
        System.out.print(color);
        showPoint(); // Point 클래스의 showPoint() 호출
    }
}

public class ex5_2 {
    public static void main(String[] args) {
        ColorPoint cp = new ColorPoint(5, 6, "blue");
        cp.showColorPoint();
    }
}
결과: blue(5,6)
```
### 업캐스팅(upcasting) 개념

하위 클래스의 레퍼런스는 상위 클래스를 가리킬 수 없지만, 상위 클래스의 레퍼런스는 하위 클래스를 가리킬수 있다
생물이 들어가는 밖스에 사람이나 코끼리를 넣어도 무방
사람이나 코끼리 모두 생물을 상속받았기 때문
업캐스팅(upcasting)이란?
서브 클래스의 레퍼런스를 슈퍼 클래스 레퍼런스에 대입
슈퍼 클래스 레퍼런스로 서브 클래스 객체를 가리키게 되는 현상

```java
class Person{
  String name;
  String id

  public Person(String name){
    this.name = name;
  }
}
class Student extends Person{
  String grade;
  String department;

  public Student(String name){
    super(name);
  }
}
public claass UpcastingEx{
  public static void main(String[] args){
    Person p;
    Student s = new Student("이재문");
    p = s; //업캐스팅

    system.out.println(p.name); // 오류 없음

    p.grade = "A"; // 컴파일 오류
    p.department = "Com"; // 컴파일 오류
  }
}
```
그렇다면 왜 p = s 로 업캐스팅을 한 걸까?

  이 사례는 업캐스팅의 제한 사항을 설명하기 위한 코드
  실제로는 이런 식으로 업새크싱을 사용하지 않음
  실제로는 여러 자식 클래스를 하나의 부모 타입으로 다루기 위해 사용

```java
Person[] people = new Person[3];
people[0] = new Student("홍길동");
people[1] = new Student("김영희");
people[2] = new Person("이순신");
```
이렇게 하면 공통된 타입(Person) 으로 여러 자식 클래스를 한 배열에 담을 수 있음
대신 접근은 Person 수준에서만 가능
다운캐스팅(downcasting)

슈퍼 클래스 레퍼런스를 서브 클래스 레퍼런스에 대입
업캐스팅 된 것을 다시 원래대로 되돌리는 것
반드시 명시적 타입 변환 지점
다운 캐스팅 사례

```java
public class DowncastingEX{
  public static void main(String[] args){
    Person p = new Student("이재문"); //업캐스팅 발생
    Student s;

    s = (Student)p; // 다운캐스팅

    System.out.println(s.name); //오류 없음
    s.grade = "A"; // 오류 없음
  }
}
```


## 최종 클래스와 메소드


```java
final class FinalClass{
  ....
}
class SubClass extends FinalClass{ // 컴파일 오류 발생
  .....
}
```



상속

클래스 사이의 선언문은 제외 - 클래스의 간결화
클래스의 위치를 ​​구분하여 클래스를 관리합니다.

문법과 사물
선포 선언:extends
상위 클래스를 응답받는다는 의미는 클래스를 축소한다는 의미입니다.
상위 클래스 -> 슈퍼 클래스(슈퍼 클래스)
클래스 -> 서브 클래스(sub class)

```java
class Point{
  int x, y;
}
class ColorPoint extends Point{ //Point를 상속받는 ColorPoint 클래스 선언

}
ColorPoint는 Point를 논의할 필요가 없습니다.
클래스 관련 - Point와 ColorPoint 클래스

(x,y)의 한 점을 표현하는 Point 클래스와 공유하는 사람을 받아 점에 색을 추가한 ColorPoint 클래스
```java
class Point {
    private int x, y; // 한 점을 구성하는 x, y 좌표
    public void set(int x, int y){
        this.x = x; this.y = y;
    }
    public void showPoint(){ // 점의 좌표 출력
        System.out.println("(" + x + "," + y + ")");
    }
}

class ColorPoint extends Point{ //Point를 상속받은 ColorPoint 선언
    private String color; // 점의 색
    public void setColor(String color){
        this.color = color;
    }
    public void showColorPoint(){ // 컬러 점의 좌표 출력
        System.out.print(color);
        showPoint(); // Point 클래스의 set() 호출
    }
}

public class ex5_1{
    public static void main(String[] args) {
        Point p = new Point(); // Point 객체  생성
        p.set(1,2); // Point 클래스의 set() 호출
        p.showPoint();

        ColorPoint cp = new ColorPoint(); // ColorPoint 객체 생성
        cp.set(3,4); // Point 클래스의 set() 호출
        cp.setColor("red"); // ColorPoint 클래스의 setColor() 호출
        cp.showColorPoint(); // 컬러와 좌표 출력
    }
}
```
결과: (1,2)
red(3,4)

서브클래스의 모양

슈퍼 클래스를 받는 것과 서브 클래스를 밝히는 것
서브 클래스는 슈퍼 클래스 기초를 포함합니다.

위세어의 특징

클래스 폴리(다중 상속) 불허
하나의 클래스가 유일하게 부모 클래스를 동시에 수신하는 것입니다.

C++는 상속 가능
C++는 질문으로 쿼리를 생성하는 것이 가능합니다(다이아몬드 쿼리)
부모 클래스에 관계적 관계가 있는 경우, 독립적인 라이브러리가 생성될 수 있는 모호성(Ambiguity)문제: 두부모 클래스에 대한 이름의 논쟁(변수나 함수)이 있는 경우, 어떤 부모의 멤버를 호출해야 할 지 모호해짐

현재는 인터페이스(interface)의 사용자에게 책임이 있습니다.
다중 사용자 기능을 제공합니다

모든 예외 클래스는 묵시적으로 Object클래스 클래스를 받음
java.lang.Object는 클래스는 모든 클래스의 훌륭한 클래스입니다.

슈퍼 클래스의 기초에 대한 서브 클래스의 접근

슈퍼 클래스의 개인 자료: 서브 클래스에서 접근할 수 없음
슈퍼 클래스의 마스터 기반: 서브 클래스가 동일한 클래스에 있을 때, 접근 가능
슈퍼 클래스의 공공 기반: 서브 클래스는 언제든지 접근 가능
슈퍼 클래스의 protected 기초:
같은 보호 장치는 모든 클래스 접근 권한에 속합니다.
가용성과 성공 여부 없이 서브 클래스에 접근 가능

## super()를 활용한 ColorPoint 작성

```java
class Point{
    private int x, y; //한 점을 구성하는 x, y 좌표
    public Point(){
        this.x = this.y = 0;
    }
    public Point(int x, int y){
        this.x = x; this.y = y;
    }
    public void showPoint() {// 점의 좌표 출력
        System.out.println("(" + x + "," + y + ")");
    }
}

class ColorPoint extends Point{ // Point를 상속받은 ColorPoint 선언
    private String color; // 점의 색
    public ColorPoint(int x, int y, String color){
        super(x, y); // Point의 생성자 Point(x, y) 호출
        this.color = color;
    }
    public void showColorPoint() { // 컬러 점의 좌표 출력
        System.out.print(color);
        showPoint(); // Point 클래스의 showPoint() 호출
    }
}

public class ex5_2 {
    public static void main(String[] args) {
        ColorPoint cp = new ColorPoint(5, 6, "blue");
        cp.showColorPoint();
    }
}
```
업캐스팅(upcasting) 컨셉
하위 계급의 분류는 상위 등급을 구분킬 수 있고, 상위 등급의 분류는 하위 등급을 분류할 수 있습니다


```java
class Person {
    String name;
    String id;

    public Person(String name) {
        this.name = name;
    }
}

class Student extends Person {
    String grade;
    String department;

    public Student(String name) {
        super(name);
    }
}

public class UpcastingEx {
    public static void main(String[] args) {
        Person p;
        Student s = new Student("이재문");
        p = s; // 업캐스팅

        System.out.println(p.name); // 오류 없음

        // 아래는 오류 발생: 업캐스팅된 참조 변수는 서브 클래스의 멤버에 직접 접근 불가
        // p.grade = "A"; // 컴파일 오류
        // p.department = "Com"; // 컴파일 오류
    }
}
```

## 4월 17일 (7주차)
## 생성자의 종류
변수 int a - 100; 는 int가 타입이지만
객체 circle pizza = new circle; 객체가 타입이 된다

기본 생성자가 자동 생성되지 않는 경우

* this 레퍼런스
객체 자신에 대한 레퍼런스
컴퍼일러에 의해 자동 관리
this.멤버 형태로 멤버에 접근할 때 사용

```java
```

* this()로 다른 생성자 호출
같은 클래스의 다른 생성자 호출
생성자 내에서만 사용 가능
생성자 코드의 제일 앞에 있어야 함

### 객체 배열
1. 배열 레퍼런스 변수 선언
2. 레퍼런스 배열 생성
3. 배열의 각 원소 객체 생성

### 메소드
메소드는 C/C++의 함수와 동일
자바의 모든 메소드는 반드시 클래스 안에 있어야 함(캡슐화 원칙)
접근 지정자 : 다른 클래스에서 메소드를 접근할 수 있는지 여부 선언
리턴 타입 : 메소드가 리턴하는 값의 데이터 타입












## 4월 10일 (6주차)
## 클래스와 사물  

---

## 실세계 사물의 특징

- 각자 고유한 짐(상태)과 행동(행동)을 가짐  
- 다른 것들과 정보를 끌어내는 등, 특수용접, 생체감  
- 컴퓨터 프로그램에 참여하는 존재  

예시:  
- 테트리스 게임의 각 블록들  
- 한글 프로그램의 메뉴나 버튼들  

---

## 캡슐화

- 패치를 패치로 공격서 내부를 볼 수 없는 것  
- 외부의 접근으로부터 보호  
- 자바의 캡슐화  
- 클래스(class): 하는 것을 선언하는 것(캡슐화하는 것)  
- 존재합니다: 인스턴스 내에 존재   

---

## 상속

- 상위의 속성이 하위로 이동하는 것에 대해 감지함  
- 하위가 자신의 재산을 모두 소유하고 있음을 나타냄

- 실세계 :  
  - 나무는 식물의 재산과 서명의 재산을 모두 가짐  
  - 사람은 군인의 재산은 있지만 식물의 재산은 가지고 있지 않음  

- 프로그램 :  
  - 상위 클래스의 구성원을 하위 클래스가 물려받음  
  - 상위 클래스: 최고급 클래스  
  - 하위 클래스: 하위 클래스  
  - 슈퍼 클래스 코드의 재사용 가능, 새로운 추가 가능  


---

## 다형성

- 동일한 이름이 클래스이거나 그에 따라 다르게 구현되는 것  
- 독립된 클래스: 내 클래스와 같은 이름이지만 다르게 작동  
- 슈퍼 클래스가 싫어하는 것과 동일한 이름으로 서브 클래스마다 독특한 특성  
- 사용하는 언어의 목적  

---

## 소프트웨어의 활동 개선

- 컴퓨터 산업 발전에 따른 소프트웨어의 수명주기(Life Cycle) 단축  
- 소프트웨어를 빠른 속도로 생산해야 하는지 여부  
- 객체 비전 언어  
- 필러, 다 찾아내는, 패치 등 소프트웨어를 다시 작동시킴  
- 소프트웨어와 부품 수정 빠름  
- 소프트웨어를 다시 만드는 책임감  
- 소프트웨어 생산성 향상  
- 실세계에 쉽게 보이는 모습  

---

## 초기 프로그래밍

- 수학 계산/통계 처리를 하는 등 처리 과정 중심  
- 처리 과정의 중요 요소  

---

## 현대 프로그래밍

- 컴퓨터가 산업에 활용  
- 실세계에서 발생하는 일을 프로그래밍  
- 실세계에서는 과정을 진행하는 자세(객체)의 복합체로 묘사  

---

## 객체 비전 언어

- 실세계의 일을 쉽게 이해하기  
- 절차를 진행하고 시작 

---

## 절차적 프로그래밍

- 활동을 표현하는 컴퓨터 집합  
- 사람들의 집합으로 프로그램 작성  

---

## 객체 비전 프로그래밍

- 컴퓨터가 활동하는 활동을 활동적으로 활용하는 효과로 표현  
- 클래스가 없거나 집합으로 프로그램 작성  

---

## 클래스와 사물

- 클래스: 존재의 속성(상태)과 의무(행동)를 선언하고, 이를 설계하거나 또는  
- 클래스의 실수로 인해 프로그램을 실행하고 생성하는 행위  
- 메모리 공간의 내부


예시:  
- 클래스: 소나타자동차, 나오다: 출고된 실제 소나타 100대  
- 클래스: 시계들  
- 클래스: 우리가 사용하는 실제 객체들  

---

## 이메일 구성

- 클래스 키워드 선언  
- 멤버: 클래스 구성 요소 (필드(멤버 변수)와 멤버 함수 포함)  
- 클래스에 대한 공개 접근 지시: 다른 모든 클래스에서 클래스 운용 가능  
- 학생에 대한 공개 접근권: 다른 모든 학급에게 학생 접근 권한  



## 4월 3일 (5주차)
## 반복문
* 자바 반복문 -
* for 문, while 문, do-whlie 문

* for 문
for 문을 이용하여 1부터 10까지 합 출력하기

```java
public class ex3_1 {
    public static void main(String[] args) {
        int i, sum = 0;

        for (i=1; i<=10; i++){
            sum += i;
            System.out.print(i);

            if (i <= 9)
                System.out.print("+");
            else {
                System.out.print("=");
                System.out.print(sum);
            }
        }
    }
}

결과: 1+2+3+4+5+6+7+8+9+10=55
```
* while 문

* while 문의 구성과 코드 사례: 조건식이 '참'인 동안 반복 실행
* for 문과 while 문의 차이: for문은 반복되는 수가 정확히 지정됨 그러나 while 문은 횟수가 정해지지 않은 반복문을 위해 만들어짐(예: 끝났다는 신호가 왔을 때)
* while 문을 이용하여 입력된 정수의 평균 구하기
```java
import java.util.Scanner;
public class ex3_2 {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int count=0, n=0;
        double sum=0;

        System.out.println("정수를 입력하고 마지막에 0을 입력하세요.");
        while((n=scanner.nextInt()) != 0){  //0이 입력되면 while 문 벗어남
            sum=sum+n;
            count++;
        }
        System.out.print("수의 개수는 " + count + "개이며 ");
        System.out.println("평균은 " + sum/count + "입니다.");
        scanner.close();
    }
}

결과: 정수를 입력하고 마지막에 0을 입력하세요.
10 30 -20 40 0
수의 개수는 4개이며 평균은 15.0 입니다.
```
* do-while 문

* do-while 문의 구성과 코드 사례: 조건식이 '참'인 동안 반복 실행. 작업문은 한 번 반드시 실행
* do-while 문을 이용하여 'a' 에서 'z' 가지 출력하기
```java
public class ex3_3 {
    public static void main(String[] args) {
        char a = 'a';

        do{
            System.out.print(a); // 문자 출력
            a = (char) (a+1);    // 알파벳의 경우 1을 더하면 다음 문자의 코드 값
        } while (a <= 'z');
    }
}

결과: abcdefghijklmnopqrstuvwxyz
```
중첩 반복

* 반복문이 다른 반복문을 내포하는 구조
* for 문안에 for 문이나 while 문을 둘 수도 있고, while 문 안에 for, while, do-while 문을 둘 수 도 있음
* 반복은 몇 번이고 중첩 가능하지만, 너무 많은 중첩 반복은 프로그램 구조를 복잡하게 하므로 2중 또는 3중 반복 정도가 적당함
* 2중 중첩을 이용한 구구단 출력하기
```java
public class ex3_4 {
    public static void main(String[] args) {
        for (int i=1; i<10; i++){  // 단에 대한 반복
            for (int j=1; j<10; j++) {  // 각 단의 곱셈
                System.out.print(j + "*" + i + "=" + j*i);  // 구구셈 출력
                System.out.print('\t');  // 하나씩 탭으로 띄기
            }
            System.out.println(); // 한 단이 끝나면 다음 줄로 커서 이동
        }
    }
}
```
* continue문과 break문
* continue 문

* 반복문을 빠져 나가지 않고, 다음 반복으로 제어 변경
* 반복문에서 continue; 문에 의한 분기한다
* continue 문을 이용하여 양수 합 구하기
```java
import java.util.Scanner;
public class ex3_5 {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        
        System.out.println("정수를 5개 입력하세요.");
        int sum=0;
        for(int i=0; i<5; i++){
            int n=scanner.nextInt();
            if(n<=0) continue;
            else sum += n;
        }
        System.out.println("양수의 합은 " + sum);

        scanner.close();
    }
}
결과: 정수를 5개 입력하세요.
5
-2
6
10
-4
양수의 합은 21
```
break 문

* 반복문 하나를 즉식 벗어날 때 사용. 하나의 반복문만 벗어남.
* 중첩 반복의 경우 안쪽 반복문의 break 문이 실행되면 안쪽 반복문만 벗어남.
* break 문을 이용하여 while 문 벗어나기

```java
import java.util.Scanner;
public class ex3_6 {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.println("exit을 입력하면 종료됩니다");
        while(true) {
            System.out.print(">>");
            String text = scanner.nextLine();
            if(text.equals("exit"))
                break;
        }
        System.out.println("종료합니다...");

        scanner.close();
    }
}
결과: exit을 입력하면 종료됩니다.
>> edit
>> exit
종료합니다...
```
# 자바의 배열  
## 자바 배열(array)

---

인덱스와 인덱스에 대응하는 데이터들로 이루어진 자료 구조로 한 번에 많은 메모리 공간 선언  
같은 타입의 데이터들이 순차적으로 저장되는 공간으로 인덱스를 이용하여 원소 데이터 접근  
반복문을 이용하여 처리하기에 적합한 자료구조  
배열 인덱스: 0 부터 시작  

---

## 배열 선언과 생성

- 배열에 대한 레퍼런스 변수 선언  
- 배열 타입-배열에 대한 레퍼런스 변수-배열 선언  
  `int intArray[];`  

- 배열 생성  
  배열에 대한 레퍼런스 변수 = 배열생성 - 타입 - 원소 개수  
  `intArray = new int[5];`

---

## 배열 선언 및 생성 디테일

- 배열은 선언과 생성의 두 단계 필요  
- 선언과 동시에 생성할 수 있음  

**배열 선언**: 배열의 이름 선언 (배열 레퍼런스 변수 선언)  
`int intArray[];` 또는 `int[] intArray;`  

**배열 생성**: 배열 공간 할당 받는 과정  
`intArray = new int[5];` 또는 `int intArray[] = new int[5];`  

---

## 배열 초기화

배열 생성과 값 초기화  
```java
int intArray[] = {4,3,2,1,0}; // 5개의 정수 배열 생성 및 값 초기화  
double doubleArray[] = {0.1, 0.2, 0.3, 0.4}; // 5개의 실수 배열 생성 및 값 초기화  

```java
import java.util.Scanner;
public class ex3_7 {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        int intArray[];
        intArray = new int[5];
        // 선언과 생성을 한 줄에 할 수 있다
        // int intArray[] = new int[5];

        int max = 0; //현재 가장 큰 수
        System.out.println("양수 5개를 입력하세요.");

        for (int i=0; i<5; i++) {
            intArray[i] = scanner.nextInt();
            if(intArray[i] > max)
                max = intArray[i];
        }
        System.out.print("가장 큰 수는 " + max + "입니다.");

        scanner.close();
    }
}
결과: 양수 5개를 입력하세요.
1 39 78 100 99
가장 큰 수는 100입니다.
```




## 3월 27일 (4주차)
## 자바의 특징

---

## 가비지 컬렉션

자바 언어는 메모리 할당 기능은 있어도 메모리 반환 기능 없음  
사용하지 않는 메모리는 JVM에 의해 자동 반환 - 가비지 컬렉션  
실시간 응용프로그램에 부적합  

- 실행 도중 예측할 수 없는 시점에 가비지 컬렉션 실행 때문  
- 응용프로그램의 일시적 중단 발생  

---

## 자바 프로그램은 안전

- 타임 체크 엄격  
- 물리적 주소 ???를 사용하는 포인터 개념 없음  

---

## 프로그램 작성 쉬움

- 포인터 개념이 없음  
- 동작 메모리 반환 하지 않음  
- 다양한 라이브러리 지원  

---

## 실행 속도 개선을 위한 JIT 컴파일러 사용

- 자바는 바이트 코드를 인터프리터 방식으로 실행  
- 기계어가 실행되는 것보다 느림  
- JIT컴파일 기법으로 실행 속도 개선  

> JIT 컴파일: 실행 중에 바이트 코드를 컴파일하여 기계어를 실행하는 기법

---

## 소스 코드, 바이트 코드, 기계어

### 소스코드 (source code)

- 우리가 작성하는 Java 코드 (.java 파일)  
- 사람이 읽을 수 있는 고수준 언어 (하이레벨랭귀지)  

### 바이트 코드 (.class 파일)

- Java 컴파일러(Javac)가 소스코드를 변환한 중간 코드  
- CPU가 직접 실행할 수 없음 → JVM이 실행  
- 기계어와 다르게 플랫폼 독립적  
- JVM이 해석(인터프리터)하거나, JIT 컴파일러가 기계어로 변환하여 실행  

### 기계어 (Machine Code)

- CPU가 직접 실행할 수 있는 0과 1의 이진 코드  
- 운영체제(OS)와 CPU 아키텍처(intel, ARM 등)에 따라 다름  
- 16진수 형태의 기계어  

### 바이트코드와 기계어의 차이점

- 바이트 코드는 JVM이 실행하는 중간 코드 → 운영체제와 CPU에 관계없이 사용 가능  
- 기계어는 CPU가 직접 실행하는 코드 → 특정 하드웨어에 종속됨  

---

## 자바 기본 프로그래밍

### 식별자(identifier) - 명명 규칙(Naming Convention)

- 식별자: 클래스, 변수, 상수, 메소드 등에 붙이는 이름  
- '@', '#', '!'와 같은 특수문자, 공백 또는 탭은 식별자로 사용 불가  
- '_', '$'는 사용 가능  
- 유니코드 문자 사용 가능, 한글 사용 가능 (but 한글은 권장하지 않음)  
- 자바 언어의 키워드는 식별자로 사용 불가  
- 식별자의 첫 번째 문자로 숫자 사용 불가  
- '_' 또는 '$'로 시작할 수는 있으나 일반적으로 사용하지 않음  
- 불린 리터럴 (true, false)와 널 리터럴 (null)은 식별자로 사용 불가  
- 길이 제한 없음  
- 대소문자 구별 (예: barChart 와 barchart 는 다른 식별자)  

---

## System.out.print의 종류

---

## System.out.print()

- 기본 출력문으로 줄 바꿈을 하지 않고 한 줄로 출력됨  
- 줄 바꿈을 하려면 개행 문자 `\n` (new line)을 넣어야 함  

## System.out.println()

- 출력 후 자동으로 줄 바꿈(개행)을 실행  

## System.out.printf()

- 서식(`%d`, `%o`, `%x`, `%f`, `%c` 등)을 사용하여 표현할 때 사용  

---

## 타입 변환

특정 데이터 타입의 값을 다른 데이터 타입의 값으로 변환  

## 자동 타입 변환

- 컴파일러에 의해 원래의 타입보다 큰 타입으로 자동 변환  
- 치환문(=)이나 수식 내에서 타입이 일치하지 않을 때  

## 강제 타입 변환

- 개발자의 의도적 타입 변환  
- `()` 안에 개발자가 명시적으로 타입 변환 지정  
- 강제 변환은 값 손실 우려  
- 큰 데이터 타입에서 작은 데이터 타입으로는 변환되지 않음  
- `int -> byte` 등은 오류가 발생  

---

## 자바의 키 입력: System.in VS Scanner

## System.in

- 키보드와 연결된 자바의 표준 입력 스트림  
- 입력되는 키를 바이트(문자 아님)로 리턴하는 저수준 스트림  
- `System.in`을 직접 사용하면 바이트를 문자나 숫자로 변환하는 많은 어려움 있음  

## Scanner 클래스

- 읽은 바이트를 문자, 정수, 실수, 불린, 문자열 등 다양한 타입으로 변환하여 리턴  
- 객체를 생성해서 사용  
- 키보드에 연결된 `System.in`에게 키를 읽게 하고, 원하는 타입으로 변환하여 리턴  
- 입력되는 키 값을 공백으로 구분되는 토큰 단위로 읽음  
- 공백 문자: `'\r'`, `'\n'`, `'\f'` (페이지 나누기, 폼 피드, 프린트에서 사용)  
- Scanner는 개발자가 원하는 타입 값으로 쉽게 읽을 수 있음  

---

## 연산자

연산: 주어진 식을 계산하여 결과를 알아내는 과정  

- **증감**: `++`, `--`  
- **산술**: `+`, `-`, `*`, `/`, `%`  
- **시프트**: `>>`, `<<`, `>>>`  
- **비교**: `>`, `<`, `>=`, `<=`, `==`, `!=`  
- **비트**: `&`, `|`, `^`, `~`  
- **논리**: `&&`, `||`, `!`, `^`  
- **조건**: `? :`  
- **대입**: `=`, `*=`, `/=`, `+=`, `-=`, `&=`, `^=`, `|=`, `<<=`, `>>=`, `>>>=`  

---

## 산술 연산자

산술연산자: 더하기(`+`), 빼기(`-`), 곱하기(`*`), 나누기(`/`), 나머지(`%`)  

---

## 증감 연산

- 1 증가 혹은 감소 시키는 연산: `++`, `--`  
- 변수의 앞에 붙으면 먼저 더해서 넣는 것(전위 연산자)  
- 변수의 뒤에 붙으면 넣은 후 더하는 것(후위 연산자)  

---

## 대입 연산

- 연산의 오른쪽 결과를 왼쪽 변수에 대입  

---

## 비교 연산, 논리 연산

- **비교연산자**: 두 개의 값을 비교하여 `true`/`false` 결과  
- **논리연산자**: 두 개의 논리 값에 논리 연산, 논리 결과  

---

## 조건 연산

- 3개의 피연산자로 구성된 삼항(ternary) 연산자  
- `opr1 ? opr2 : opr3` → opr1이 `true`면 opr2, `false`면 opr3  
- `if-else`를 조건연산자로 간결하게 표현 가능  

  

## 3월 20일 (3주차)
* 프로그래밍 언어의 진화 과정
  고급언어, 어셈블리어, 객체지향언어의 사용

* JVM : Java Varture Machine
  
* 사용자의 요구에 따라 java 9부터 모든 클래스를 모듈로 재구성했다.

* 자바 API
  자바 api를 사용하면서 자바 개발이 용이해졌다.

* 파스칼 케이스
  파일 이름을 생성할 때 첫 글자와 중간 글자를 대문자로 표기한다.

* 자바의 응용
  초기에는 거의 다 자바로 안드로이드 앱을 만들었다.

* 자바의 특징(1)
  1. 플랫폼 독립성
  2. 객체지향
  3. 클래스로 캡슐화
  4. 소스(.java)와 클래스(.class) 파일

* 자바의 특징(2)
  1. 다수 클래스 파일의 경우 jar 압축 파일로 실행 코드 배포
  2. 클래스를 패키지로 관리
  3. 자체 멀티스레드 지원
