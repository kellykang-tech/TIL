# 클래스 변수와 클래스 메소드

## 목차
1. [static 선언을 붙여서 선언하는 클래스 변수](#1-static-선언을-붙여서-선언하는-클래스-변수)  
  1.1 [클래스 변수는 언제 필요한가](#11-클래스-변수는-언제-필요한가)  
  1.2 [클래스 변수는 어디에 두어야 하는가](#12-클래스-변수는-어디에-두어야-하는가)  
  1.3 [어떻게 하면 클래스 변수가 되는가](#13-어떻게-하면-클래스-변수가-되는가)  
  1.4 [클래스 변수는 무엇인가](#14-클래스-변수는-무엇인가)  
  1.5 [선언된 클래스의 모든 인스턴스가 공유하는 클래스 변수](#15-선언된-클래스의-모든-인스턴스가-공유하는-클래스-변수)    
  1.6 [클래스 변수의 접근 방법](#16-클래스-변수의-접근-방법)    
  1.7 [클래스 변수 접근의 예](#17-클래스-변수-접근의-예)    
  1.8 [클래스 변수의 초기화 시점과 초기화 방법](#18-클래스-변수의-초기화-시점과-초기화-방법)   
  1.9 [클래스 변수 활용의 예](#19-클래스-변수-활용의-예)    

2. [static 선언을 붙여서 선언하는 클래스 메소드](#2-static-선언을-붙여서-선언하는-클래스-메소드)  
   2.1 [클래스 메소드의 정의와 호출](#21-클래스-메소드의-정의와-호출)  
   2.2 [클래스 메소드로 정의하는 것이 옳은 경우](#22-클래스-메소드로-정의하는-것이-옳은-경우)  
   2.3 [클래스 메소드에서 인스턴스 변수에 접근이 가능할까](#23-클래스-메소드에서-인스턴스-변수에-접근이-가능할까)
     
3. [System.out.println() 그리고 public static void main()](#3-systemoutprintln-그리고-public-static-void-main)  
   3.1 [System.out.println()에서 out과 println의 정체는?](#31-systemoutprintln에서-out과-println의-정체는)    
   3.2 [main 메소드가 public이고 static인 이유는?](#32-main-메소드가-public이고-static인-이유는)  
   3.3 [main 메소드를 어디에 위치시킬 것인가?](#33-main-메소드를-어디에-위치시킬-것인가)
   
4. [또 다른 용도의 static 선언](#4-또-다른-용도의-static-선언)
<br>

# 1. static 선언을 붙여서 선언하는 클래스 변수
## 1.1 클래스 변수는 언제 필요한가?
- 자바 프로그램은 클래스들로만 구성되어있다. 전부 다 클래스이다. 클래스가 아닌 것이 없다.
내가 변수, 메소드를 선언하려고 해도 클래스 안에 있어야 하고 메인 메소드까지도 클래스 안에 있어야 한다.

- 변수가 하나 필요한데, 우리가 알고있는 변수는 클래스 안에 있어야 했고 인스턴스 변수는 인스턴스를 생성할 때마다 만들어줬다.

```
class A     class B     class C     
┌────┐      ┌────┐      ┌────┐ 
│ A  │      │ B  │      │ C  │ 
└────┘      └────┘      └────┘ 
     ↓         ↓        ↓
            int num
```

- 전체 프로그램에서 하나의 변수로 선언하고, 이 변수를 전체 프로그램 모두에서 공유하고 싶을 때가 있는데, 자바는 모든 코드를 클래스로 감싸도록 되어있다.   
그렇다면 변수는 어디다가 두어야 하는가? 
<br>
<br>


## 1.2 클래스 변수는 어디에 두어야 하는가?
- 클래스 외부에 변수를 둘 수는 없다.   공유하고자 하는 int num이라는 변수도 class A, class B, class C 이 중에 한 클래스에 자리를 빌려서 들어가긴 해야한다.  

- A 클래스 진영에서만 쓸 것이라면 당연히 A에 들어가면 되지만, 공유하는 변수는 어디에 넣을 것인가?
  
- A, B, C 중에서 조금 더 연관이 깊은 클래스의 위치로 들어가면 된다.   
예를들어 A 클래스에 int num을 넣었다고 가정하자. 그렇다면 int num은 A, B, C클래스에서 공유하는 변수가 되는가?   
그렇지 않다. int num은 그냥 인스턴스 변수이다.
<br>
<br>

## 1.3 어떻게 하면 클래스 변수가 되는가?
- A 클래스에 넣어주되 **`static`** 이라는 선언을 앞에 붙여준다.  
  - **`static int num;`**

<br>
<br>

## 1.4 클래스 변수는 무엇인가?

- 코드 레벨에서 볼 때 A 클래스 안에 있으니 혼란스럽다.  
하지만 static 선언을 붙이면 인스턴스 생성과는 전혀 별개의, 하나만 존재하고 어디서나 접근이 가능한 변수의 성격을 지니게 된다. 이것이 **`클래스 변수`** 이다.
  - 인스턴스 변수는 인스턴스를 생성했을 때에 존재하게 되는 변수이다.

- 클래스 변수는, 위치는 클래스 안에 존재하지만 인스턴스 변수가 아니다. 
즉, '클래스에 종속, 위치 하는 변수다'라는 의미로써 클래스 변수라는 이름을 붙인다.   
하지만 흔히 static 변수라고 부른다.
<br>
<br>


## 1.5 선언된 클래스의 모든 인스턴스가 공유하는 클래스 변수
```java
class InstCnt {
    static int instNum = 0; // 클래스 변수(static 변수)

    InstCnt() {
        instNum++;
        System.out.println("인스턴스 생성: " + instNum);
    }
}

class CalssVar {

    public static void main(String[] args) {
        InstCnt cnt1 = new InstCnt();
        InstCnt cnt2 = new InstCnt();
        InstCnt cnt3 = new InstCnt();
    }
}
```
- static int instNum = 0;  
클래스 변수 instNum은 InstCnt 클래스랑 관련이 없다고 생각하자.   
월세를 내고 생활 하는 것처럼 뭔가 대가를 지불하고 자리를 빌려서 들어온 변수라고 이해하자.

- 그렇다면 대가는 어떤 것을 말하는가?   
월세를 내고 한 건물의 자리를 빌려 쓸 때도 그 건물에서 지켜야 하는 규칙을 준수해야 하는 것처럼, 클래스 변수도 그 클래스의 규칙을 지켜야 한다.
이 클래스에서 지시하는 접근 지시자의 규칙을 따라야한다. "뭐야 그럼 인스턴스 변수 아니야?" 라고 생각이 들수도 있지만 그렇지 않다.

- instNum++;  
생성자 안에서 클래스 변수에 이름만으로 접근 하고 있다.  
인스턴스 변수 instNum에 접근하는 것처럼 보이지만 실제로는 그렇지 않다.  
InstCnt는 자리를 빌려줬으니 직접 접근할 수 있는 권한을 획득한 것이라고 생각하자.

- InstCnt cnt1 = new InstCnt();  
메인메소드가 시행이 되면 InstCnt라는 클래스 정보가 자바가상머신에 로딩이 된다.  
로딩이 될 때 InstCnt를 자바 가상머신이 읽는데 static이 선언된 변수를 보면 인스턴스 생성을 하지 않더라도 인스턴스 생성과는 상관없이,  특정한 메모리 공간에 별도로 instNum을 저장하고
0으로 초기화를 시킨다. 

- 그리고 new InstCnt() 인스턴스를 생성하고, 인스턴스를 생성하는 과정에서 생성자가 실행이 되는데 생성자 내부에서 instNum++을 하고 있다.   
  - instNum = 0 -> 1;

- InstCnt cnt2 = new InstCnt();  
instNum = 1 -> 2

- InstCnt cnt3 = new InstCnt();  
instNum = 2 -> 3

- 세 개의 인스턴스를 생성하면서 각각의 인스턴스에서 instNum 값을 1씩 증가 시켰다.

- 자리를 빌려 들어왔기때문에 해당 클래스에서 정의하는 규칙을 따라야 한다.  
접근 수준 지시자 규칙을 지켜야 하는데, '이 클래스 내에서만 instNum 을 사용하겠다' 한다면 private으로 선언하고, '같은 패키지 범위 내에서는 접근을 허용하겠다' 한다면 default로 선언하고, '어디서든 다 접근을 하도록 하겠다' 한다면 public으로 선언한다.
<br>
<br>


## 1.6 클래스 변수의 접근 방법
- 클래스 내부 접근  
static 변수가 선언된 클래스 내에서는 이름만으로 직접 접근 가능하다.

- 클래스 외부 접근  
  - private으로 선언되지 않으면 클래스 외부에서도 접근이 가능하다.
  
  - 접근 수준 지시자가 허용하는 범위에서 접근이 가능하다.
  
  - 클래스 또는 인스턴스의 이름을 통해 접근한다.
<br>
<br>


## 1.7 클래스 변수 접근의 예
```java
class AccessWay {
    static int num = 0;

    AccessWay() {
        incrCnt();
    }

    void incrCnt() {
        num ++;   // 클래스 내부에서 이름을 통한 접근
    }
}

class ClassVarAccess {

    public static void main(String[] args) {
        AccessWay way = new AccessWay();
        way.num++;  // 외부에서 인스턴스의 이름을 통한 접근
        AccessWay.num++;  // 외부에서 클래스의 이름을 통한 접근
        System.out.println("num = " + AccessWay.num);
    }
}
```
- 두 클래스는 디폴트 패키지로 묶여있다. 같은 패키지로 묶여 있기 때문에 접근이 가능하다.

- AccessWay 클래스는 이름으로 바로 접근이  가능하다.   

- ClassVarAccess 클래스는 두 가지 방법으로 접근이 가능하다.  
인스턴스의 이름을 통해서 접근하거나 클래스의 이름을 통해 직접 접근하거나.

- 인스턴스의 이름을 통한 접근보다는 클래스의 이름을 통한 접근이 더 낫다.  
AccessWay는 클래스 이름이라는 것이 직관적으로 보이기때문에, 클래스 이름을 통해 접근하는 것을 보고 클래스 변수라는 것을 쉽게 알아차릴 수 있다.
<br>
<br>


## 1.8 클래스 변수의 초기화 시점과 초기화 방법
```java
class InstCnt {
    static int instNum = 100;  // 클래스 변수의 적절한 초기화 위치

    InstCnt() {
        instNum++;
        System.out.println("인스턴스 생성: " + instNum);
    }
}

class OnlyClassNoInstance {

    public static void main(String[] args) {
        InstCnt.instNum -= 15;  // 인스턴스 생성 없이 instNum에 접근
        System.out.println(InstCnt.instNum);
    }
}
```
### 1.8.1 초기화 방법
- 클래스 변수는 생성자 기반으로 초기화를 하면 안된다. 이 경우엔 인스턴스 생성 시마다 값이 리셋되기 때문이다. 

### 1.8.2 초기화 시점
*클래스 변수는 언제 메모리 공간에 올라가는가?*

- 자바 프로그램의 특징을 알아보자.  
프로그램을 구성하고 있는 클래스가 10개라고 가정하면, 자바 가상머신은 이 10개의 클래스 파일을 모두 한 번에 읽어들이는 것이 아니라 필요한 정보만 읽어들인다.

- 10개의 클래스로 이루어져있고, 이 중에 이번에 실행했을 때는 7개에 해당하는 클래스의  인스턴스만 생성을 했다고 한다면 필요한 시점에 7개의 클래스 정보만 읽어들인다.

- main 메소드를 실행하기 위해서는 OnlyClassNoInstance 클래스 정보를 읽어들여야한다.  
InstCnt.instNum 을 만나면 InstCnt라는 정보가 필요하다고 생각하고 그제서야 InstCnt의 정보를 읽어들인다.

- 이 때 static 으로 선언된 int instNum 이라는 변수가 있다는 사실을 캐치하고, 자바 가상머신이 관리하는 특정 메모리공간에 저 변수를 저장하고, 100으로 초기화 시킨다. 
<br>
<br>


## 1.9 클래스 변수 활용의 예
```java
class Circle {
    static final double PI = 3.1415;
    private double radius;

    Circle(double rad) {
        radius = rad;
    }

    void showPerimeter() {
        double peri = (radius * 2) * PI;
        System.out.println("둘레: " + peri);
    }

    void showArea() {
        double area = (radis * radius) * PI;
        System.out.println("넓이: " + area);
    }
}
```
- 원주율 값이라는 건 다른 영역에서도 필요하다.  
하지만 인스턴스를 생성하면 되기때문에 static 선언을 빼도 코드는 잘 돌아간다.  
하지만 인스턴스 별로 원주율 값을 가지고 있을 필요가 없다. PI값을 바꿀 필요가 없기 때문이다.

- 상황, 환경에따라 값을 바꿔야 된다고 가정해보자.  
날씨 정보가 실시간으로 업데이트 되고, 각 인스턴스들이 이 정보를 참조해야 된다면 인스턴스에서 변수를 각각 가지고 있는 것보다 하나에서만 참조 되는 값을 수정하고, 이 수정되는 값들을 가져가는 것이 더 효율적이다.

- 인스턴스 별로 가지고 있을 필요가 없는 변수
  - 값의 참조가 목적인 변수
  - 값의 공유가 목적인 변수
  
- 그리고 그 값이 외부에서도 참조하는 값이라면 public으로 선언한다.
<br>
<br>


# 2. static 선언을 붙여서 선언하는 클래스 메소드
## 2.1 클래스 메소드의 정의와 호출
```java
class NumberPrinter {
    
    private int myNum = 0;

    static void showInt(int n) {
        System.out.println(n);
    }
    
    static void showDouble(double n) {
        System.out.println(n);
    }

    void setMyNumber(int n) {
        myNum = n;
    }

    void showMyNumber() {
        showInt(myNum);     // 내부 접근
    }
}

class ClassMethod {
    public static void main(String[] args) {
        NumberPrinter.showInt(20);  // 외부 접근
        NumberPrinter np = new NumberPrinter();
        np.showDouble(3.15);    // 외부 접근
        np.setMyNumber(75);
        np.showMyNumber();
    }
}
```
- 클래스 메소드의 성격 및 접근 방법이 클래스 변수와 동일하다.

- NumberPrinter 인스턴스가 3개 있을 때, 각각의 인스턴스 안에 showInt, showDouble 메소드가 있는 게 아니라 static 메소드(클래스 메소드)는 다른 메모리 공간에 존재하고 있다.

- 외부에서는 클래스의 이름 또는 인스턴스의 참조 변수 이름을 통해서 접근한다.  
(클래스 이름을 통해서 접근하는 편이 좋다!)
<br>
<br>


## 2.2 클래스 메소드로 정의하는 것이 옳은 경우
```java
class SimpleCalculator {
    static final double PI = 3.1415;

    static double add(double n1, double n2) {
        return n1 + n2;
    }

    static double min(double n1, double n2) {
        return n1 - n2;
    }

    static double calCircleArea(double r) {
        return PI * r * r;
    }

    static double calCirclePeri(double r) {
        return PI * (r * 2);
    }
}
```
- **`단순 기능 제공이 목적인 메소드들, 인스턴스 변수와 관련 지을 이유가 없는 메소드들은 static으로 선언하는 것이 옳다.`**

- 인스턴스 메소드는 인스턴스 변수와 연관되어져야한다. 

- static 메소드는 인스턴스가 가질 필요도 없고, 여러 개가 있을 필요도 없고 하나만 존재하면 원할 때마다 가져다 쓸 수 있는 메소드이다.
<br>
<br>


## 2.3 클래스 메소드에서 인스턴스 변수에 접근이 가능할까?
```java
class AAA {
    int num = 0;
    static void addNum(int n){
        num += n;
    }
}
```
- num은 인스턴스화 되었을 때 존재하는 인스턴스 변수이고, addNum은 인스턴스 생성과 관련없이 존재하는 클래스 메소드이다. 
<br>

```
                  addNum
                ┌────────┐  
                │ Method │ 
                └────────┘ 

    AAA             AAA             AAA
┌──────────┐    ┌──────────┐    ┌──────────┐
│ Instance │    │ Instance │    │ Instance │ 
└──────────┘    └──────────┘    └──────────┘ 

```
<br>
<br>


# 3. System.out.println() 그리고 public static void main()

## 3.1 System.out.println()에서 out과 println의 정체는?
```java
java.lang.System.out.println(...);
```

### 3.1.1 System
- System은 java.lang 패키지에 묶여 있는 **`클래스의 이름`** 이다.
그러나 컴파일러가 `import java.lang.*;` 문장을 삽입해주므로 java.lang을 생략할 수 있다.

- import java.lang.*;  
패키지 전체를 import 하는 방식은 좋지 않다고 했는데 자바에서 이렇게 하고 있는 이유는 무엇인가?  
java.lang 패키지에는 시스템과 관련된 클래스들이 묶여 있다. 개발자가 이 클래스들의 이름과 중복된 이름을 실수로 만들 수도 있는데 이렇게 이름 충돌이 나버리면 문제가 생기므로 자바 컴파일러가 전부 import해버린다.  
우리가 중복된 이름을 만들려고 하면 컴파일 오류가 생기게 되는데, 이는 "제발 너희는 java.lang 패키지에 있는 클래스 이름 쓰지마" 라는 의미가 있다.
<br>

### 3.1.2 out
- out은 클래스 System의 이름을 통해 접근하므로, 이는 System 클래스의 **`클래스 변수 이름`** 임을 유추할 수 있다.
<br>

### 3.1.3 println
- println은 out이 참조하는 인스턴스의 메소드이다.
  - 이 부분은 이해가 안되므로 기본서를 찾아보자.
<br>
<br>


## 3.2 main 메소드가 public이고 static인 이유는?
**`public`** **`static`** void main(String[] args) {...} 

- static인 이유   
인스턴스 생성과 관계없이 제일 먼저 호출되는 메소드이다.

- public인 이유   
main 메소드의 호출 명령은 외부로부터 시작되는 명령이다.   
(단순히 일종의 약속으로 이해해도 괜찮다.) 

  - 자바와 우리의 합리적이고 타당성이 있는 약속이다.  
    궁극적으로 메인 메소드를 실행하는 명령을 내리는 위치는 외부이다.  
    명령 프롬프트에서 혹은 이클립스 같은 개발 툴을 사용한다면 이클립스라는 외부 툴에서 메인 메소드의 호출을 명령하는 것이다.  
    자바 런처에 의해서 모든 세팅이 되고 메인 메소드의 실행이 이루어진다. 즉 요청 자체가 클래스 외부에서 이루어진다.   
    이러한 상징적 의미로 public으로 둔다.
<br>
<br>


## 3.3 main 메소드를 어디에 위치시킬 것인가?
```java
class Car {
    void myCar() {
        System.out.println("This is my car.");
    }

    public static void main(String[] args) {
        Car c = new Car();
        c.myCar();

        Boat t = new Boat();
        t.myBoat();
    }
}

class Boat {
    void myBoat() {
        System.out.println("This is my boat.");
    }
}
```
- 어디에 두어도 상관없다. 넣어두면 실행하는 방법이 달라질 뿐이다.    
  -  java Car / java Boat

- main 메소드를 담기 위한 별도의 클래스를 만드는 것이 보편적인 방법이다.
<br>
<br>


# 4. 또 다른 용도의 static 선언

## 4.1 static 초기화 블록
```java
class DateOfExecution {
    static String date;
    
    static {
        LocalDate nDate = LocalDate.now();
        date = nDate.toString();
    }

    public static void main(String[] args) {
        System.out.println(date);
    }
}
```
- **`static {...}`** 문장을 실행 해주면, date 변수를 현재의 날짜를 저장한 static 변수로 만들어줄 수 있다.

- 현재의 날짜라는 것은 내가 코드에 직접 써줄 수가 없다. 오늘 실행할 때와 내일 실행할 때의 값이 달라지므로 날마다 바꿔줘야 한다. 
이처럼 내가 초기화 할 값을 메소드 호출을 통해서 얻어와야 하는 때가 있다. 

- date는 언제 초기화가 되느냐?   
DateOfExecution 클래스가 자바가상머신에 의해서 읽혀지는 순간에 특정 메모리 공간에 할당이 되고 초기화가 이루어진다.

- static 변수가 특정 메모리 공간에 할당이 되고, 할당 된 다음에 그냥 끝나는 것이 아니라 **`static 초기화 블록`** 이 그 시점에 실행이 된다.   
즉 메인 메소드에서 특별한 액션을 취하지 않아도 date가 메모리 공간에 올라가는 그 시점 직후에 자동으로 실행이 된다.
  - static {...}  
    인스턴스 생성과 관계 없이 static 변수가 메모리 공간에 할당될 때 실행이 된다.

- static 초기화 블록이 왜 필요한가?   
내가 static 변수에 값을 직접 찍어 넣는 것이 아니라 값을 얻어와서 static 변수를 초기화 해야 될 때 필요하다.
<br>
<br>


## 4.2 static import 선언
```java
import static java.lang.Math.PI;

System.out.println(Math.PI);

System.out.println(PI);
```
- import static java.lang.Math.PI;  
java.lang 패키지의 Math 클래스에 있는 static으로 선언된 PI 값을 import 하겠다.
  - import 이후 System.out.println(PI) 이렇게 PI를 바로 사용할 수 있다.

- vs 값의 출처는 코드 레벨에서 바로 보이는 게 좋다.
  - Math.PI vs PI