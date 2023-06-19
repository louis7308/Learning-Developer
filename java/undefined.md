# 기초 문법

### Java 언어의 탄생

Java는 제임스 고슬링과 연구원들이 개발한 객체 지향적 프로그래밍 언어이다.



#### Write Once, Run Anywhere

직역을 하면, '한 번 작성하면 어디에서나 실행된다'는 의미로, 자바로 개발된 프로그램은 자바 실행 환경 JRE가 설치된 모든 환경에서 실행이 가능하다는 것을 의미한다.



### 1) 자료형

Java의 자료형은 크게 Primitive Type(기본 자료형)과 Reference Type(참조 자료형)으로 구분된다.



#### Primitive Type의 종류

#### byte, short, int, long, float, double, char, boolean, 등이 있다.

short, int, long은 숫자형이며, 이는 각 타입에 할당되는 메모리의 크기가 다르다.

순서대로 각 2byte, 4byte, 8byte가 할당 가능하다.

또한 아래의 코드로 최소 및 최대값을 찍어보며 실제 값을 볼 수 있다.

{% code lineNumbers="true" %}
```java
System.out.println(Integer.MAX_VALUE); // 2147483647
System.out.println(Integer.MIN_VALUE); // -2147483648
```
{% endcode %}



#### Reference Type의 종류

참조 자료형은 위의 기본 자료형을 제외한 모든 자료형을 말한다.

쉽게 말해 자바의 인스턴스를 가리킬 수 있는 자료형이다. \[String, 클래스, 배열, List, Enum, 인터페이스 등]



\+) 추가 팁

배열은 크기가 정적으로 설정되어 한번 밖에 설정하지 못하지만, List같은경우에는 크기가 동적으로 할당 되기 때문에 필요에 따라 크기를 자동으로 조정할 수 있습니다.



### 2) 조건문

#### switch 구조

switch의 소괄호에는 파라미터를 넣어주며 각각의 case에 맞는 기능을 구현하면 된다.\
default는 if문의 else와 비슷한 기능으로 생각하면 됩니다.\
단 주의해야할 점은 각 case마다 break가 없다면 조건을 충족한 case 이후에는 판별하지 않고 모두 실행시킨다.

{% code lineNumbers="true" %}
```java
        switch(score){
            case "A":
                System.out.println("A등급입니다.");
                break;
            case "B":
                System.out.println("B등급입니다.");
                break;
            case "C":
                System.out.println("C등급입니다.");
                break;
            default:
                System.out.println("D등급 이하 입니다.");
                break;
        }
```
{% endcode %}



#### 삼항 연산자

변수명 = (논리조건) ? true일시 실행되는 로직 : false일시 실행되는 로직

이러한 구조로 사용되어지고 있으며, 변수를 지정해주지 않으면 오류가 난다.

{% code lineNumbers="true" %}
```java
        int score = 10;

        String result = (score < 11) ? "11보다 작네요" : "11보다 큰 값을 가지고 계시네요.";
        System.out.println("결과는 ? " + result);
```
{% endcode %}



### 3) 반복문

```java
for( int i = 0 ; i < 100; i++){
	//이와 같은 형태로 사용한다.
}
```

#### forEach 반복문

배열, 리스트 등에서 하나 하나의 원소들을 iterate하며 사용하는 방식이다.

{% code lineNumbers="true" %}
```java
        String[] days = {"Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday", "Sunday"};

        for (String day : days){
            System.out.println(day);
        }
```
{% endcode %}

#### while 반복문 특정 조건이 충족될 때까지 반복하고, 중간에 break, continue 키워드를 줄 수 있다.

{% code lineNumbers="true" %}
```java
        int i = 0;
        int sum = 0;
        
        while (i<10){
            sum += (i+1);
            i++;
        }
        System.out.println(sum);
```
{% endcode %}

#### do - while 반복문

do블록의 마지막에 while문을 붙이는 구조이다.\
디버그를 돌려보니 do의 코드블록이 먼저 실행된 후 while에서 조건을 체크한 뒤 false면 반복, true면 벗어나는 구조였다.

{% code lineNumbers="true" %}
```java
        int i = 0;
        int sum = 0;
        
        do {
            sum += (i+1);
            i ++;
        } while (i<10);
        System.out.println(sum);
```
{% endcode %}

### 4) 클래스, 인스턴스, 메소드

#### Class ( 클래스 )

표현하고자 하는 대상의 공통 속성을 한 곳에 모아놓아 정의 해놓은 것 즉, 객체의 속성을 정의한 것이다.

객체의 속성에는 필드, 메소드, 생성자 가 존재한다.

필드(전역변수)는 클래스 내부 전역에서 사용 가능한 전역변수에 해당한다. 이는 멤버변수 라고도 불린다.

반면 Method와 Constructor에서 정의된 변수는 지역변수라고 한다.



#### Instance ( 인스턴스 )

어떠한 클래스로부터 만들어진 객체를 그 클래스의 인스턴스라고 부른다.

아래의 코드는 Phone은 클래스이고, 메인 함수의 galaxy, iphone은 인스턴스들이다.

{% code lineNumbers="true" %}
```java
class Phone {
    String model;
    String color;
    int price;
}

public class Main {
    public static void main(String[] args) {
        Phone galaxy = new Phone(); 
        galaxy.model = "Galaxy10";
        galaxy.color = "Black";
        galaxy.price = 100;
        
        Phone iphone =new Phone();
        iphone.model = "iPhoneX";
        iphone.color = "Black";
        iphone.price = 200;
        

        System.out.println("철수는 이번에 " + galaxy.model + galaxy.color + " + 색상을 " + galaxy.price + "만원에 샀다.");
        System.out.println("영희는 이번에 " + iphone.model + iphone.color + " + 색상을 " + iphone.price + "만원에 샀다.");
    }
}
```
{% endcode %}



#### Method

Method는(함수) 어떠한 작업을 수행하는 코드를 하나로 묶어 놓은 것이다.

Method 내의 변수는 지역변수로, Method 내부에서만 사용할 수 있다.

코드 컨벤션은 시작은 동사로 하면서 카멜케이스를 사용해야 한다.

{% code lineNumbers="true" %}
```java
//반환타입 메소드이름 (타입 변수명,타입 변수명, ...){ 
//    수행되어야 할 코드
//}

int add(int x, int y) {
    int result = x + y;
    return result;
}
```
{% endcode %}



### 5) 생성자

#### Constructor ( 생성자 )

인스턴스가 생성될 때 사용되는 인스턴스 초기화 메소드이다. ( 기본으로 매개변수 없는 default 생성자 생성됨 )

new와 같은 키워드로 해당 클래스의 인스턴스가 새로 생성될 때, 자동으로 호출 되는 메소드

생성자의 이름은 클래스 명과 같아야 하며, 리턴값이 없다는 특징을 지닌다.

```java
//클래스이름 (타입 변수명, 타입 변수명, ...){
//    인스턴스 생성 될 때에 수행하여할 코드
//    변수의 초기화 코드
//}

class Phone {
    String model;
    String color;
    int price;
	
    //생성자
    Phone(String model, String color, int price) {
        this.model = model;
        this.color = color;
        this.price = price;
    }
}
```

class에 선언된 변수들은 instance가 생성될 때 값이 초기화 된다.

따라서 변수의 선언부나 생성자를 통해서 초기화를 해주지 않는다면, 각 자료형의 default 값이 할당된다.

```java
class DefaultValueTest {
    byte byteDefaultValue;
    int intDefaultValue;
    short shortDefaultValue;
    long longDefaultValue;
    float floatDefaultValue;
    double doubleDefaultValue;
    boolean booleanDefaultValue;
    String referenceDefaultValue;
}

public class Main {
    public static void main(String[] args) {
        DefaultValueTest defaultValueTest = new DefaultValueTest();
        System.out.println("byte default: " + defaultValueTest.byteDefaultValue); // 0
        System.out.println("short default: " + defaultValueTest.shortDefaultValue); // 0
        System.out.println("int default: " + defaultValueTest.intDefaultValue); // 0
        System.out.println("long default: " + defaultValueTest.longDefaultValue); // 0
        System.out.println("float default: " + defaultValueTest.floatDefaultValue); // 0.0
        System.out.println("double default: " + defaultValueTest.doubleDefaultValue); // 0.0
        System.out.println("boolean default: " + defaultValueTest.booleanDefaultValue); // false
        System.out.println("reference default: " + defaultValueTest.referenceDefaultValue); // null
    }
}
```

단 필드의 마지막 참조 자료형은 default 값이 아닌 참조할 값이 없다는 null을 반환한다.



### 6) 상속

상속이란 기존의 클래스를 재사용하는 방식중의 하나이다.

한번 작성한 코드가 재사용이 필요하다면, 변경사항만 코드로 작성하면 되며 상대적으로 적은 양의 코드를 작성 할 수 있다.&#x20;

이렇게 코드를 재사용한다면, 코드와 클래스가 많아질수록 관리가 용이해진다.

상속을 하게되면 이루어지는 절차

1. 부모 class로부터 정의된 field와 method를 물려 받는다.
2. 새로운 필드와 메소드를 추가할 수 있다.
3. 부모 클래스에서 물려받은 메소드를 수정할 수 있다.

상속은 extends로 한다. (하나의 class만 상속 가능)

```java
class Animal{}
class Dog extends Animal{}
class Cat extends Animal{}
```

#### super, super() 메소드

부모 클래스로부터 상속받은 필드나 메소드 및 생성자를 자식 클래스에서 참조하여 사용하고 싶을 때 사용하는 키워드이다.

