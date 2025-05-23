# 이도영 202230123
## 4월 18일 (8주차)
## 클래스와 사물  
## 정적 영향의 비교 2

static에서는 사용이 불가능합니다.  

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
