# 이도영 202230123

## 4월 10일 (6주차)
## 클래스와 사물  
**세상 모든 것이 되다**

---

## 실세계 사물의 특징

- 각자 고유한 짐(상태)과 행동(행동)을 가짐  
- 다른 것들과 정보를 끌어내는 등, 특수용접 생체감  
- 컴퓨터 프로그램에 참여하는 존재  

예시:  
- 테트리스 게임의 각 블록들  
- 한글 프로그램의 메뉴나 버튼들  
- 좌회전: 좌회전  

---

## 캡슐화

- 패치를 패치로 공격서 내부를 볼 수 없는 것  
- 외부의 접근으로부터 보호  
- 자바의 캡슐화  
- 클래스(class): 하는 것을 선언하는 것(캡슐화하는 것)  
- 존재합니다: 인스턴스 내에 존재  
- 선택의 방향: 왼쪽  

---

## 유전

- 상위의 속성이 하위로 이동하는 것에 대해 감지함  
- 하위가 자신의 재산을 모두 소유하고 있음을 나타냄
- 실세계의 유산:  
  - 나무는 식물의 재산과 서명의 재산을 모두 가짐  
  - 사람은 군인의 재산은 있지만 식물의 재산은 가지고 있지 않음  

- 위스의 유산:  
  - 상위 클래스의 구성원을 하위 클래스가 물려받음  
  - 상위 클래스: 최고급 클래스  
  - 하위 클래스: 하위 클래스  
  - 슈퍼 클래스 코드의 재사용 가능, 새로운 추가 가능  
  - 좌회전: 좌회전  

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
- 메모리 공간을 안뜰  
- 반발(instance)을 두고  
- 섬  

예시:  
- 클래스: 소나타자동차, 나오다: 출고된 실제 소나타 100대  
- 클래스: 벽시계, 일하는: 우리집 벽에 벽시계들  
- 클래스: 존재, 존재: 우리가 사용하는 실제 객체들  

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
* 자바의 특징(3)
  1. 실시간 응용프로그램에 부적합

* 소스코드, 바이트 코드, 기계어의 차이점

* 식별자 : 클래스, 변수, 상수, 메소드 등에 붙이는 이름
* 식별자의 원칙
  1. @, #과 같은 특수문자 사용 X _, $는 사용 O
  2. 유니코드, 한글 사용 O
  3. 자바 키워드는 식별자로 사용 X
  4. 길이 제한 X

* JAVA 데이터 타입
  문자열 같은 경우 string 클래스로 표현
  리터럴 : 데이터 자체

* 참조 자료형
  JVM에서 포인터(주소) 안내를 해준다

* 참조 자료형 사용 이유
  1. 보안 강화(포인터를 사용하면 버퍼 오버플로우 같은 보안 취약점이 생기는데, java에서는 불가능함)
  2. 다중 플랫폼 지원
  3. 메모리 안정성
  4. 코드 단순화, 가속화 향상
  5. 다중 플랫폼 지원

* 메모리의 구조
  힙 (heap) : 프로그래머가 직접 공간을 할당, 해제하는 메모리
  스택 (stack) : 프로그램이 자동으로 사용하는 임시 메모리 
  각각 메모리가 침범하면 힙, 스택 오버플로우

* 변수 : 값을 임시로 저장하기 위한 메모리

* 비트 연산
  비트 논리 : AND, OR, XOR, NOT 연산
  시프트 : 비트를 오른쪽이나 왼쪽으로 이동시킴
  사용 이유 : 성능, 최적화가 중요한 경우 기본 연산자보다 비트 연산이 훨씬 빠르다
  

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
