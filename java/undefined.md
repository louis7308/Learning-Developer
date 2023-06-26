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

{% code lineNumbers="true" %}
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
{% endcode %}

class에 선언된 변수들은 instance가 생성될 때 값이 초기화 된다.

따라서 변수의 선언부나 생성자를 통해서 초기화를 해주지 않는다면, 각 자료형의 default 값이 할당된다.

{% code lineNumbers="true" %}
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
{% endcode %}

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

{% code lineNumbers="true" %}
```java
class Animal{}
class Dog extends Animal{}
class Cat extends Animal{}
```
{% endcode %}

#### super, super() 메소드

부모 클래스로부터 상속받은 필드나 메소드 및 생성자를 자식 클래스에서 참조하여 사용하고 싶을 때 사용하는 키워드이다.



#### this, this() 메소드와 차이점

this는 현재 scope의 클래스를 지칭한다.

this() 메소드는 같은 클래스의 다른 생성자를 호출할 때 사용된다면, super() 메소드는 부모 클래스의 생성자를 호출할 때 사용된다. 따라서 super()의 매개변수 자리에는 부모 클래스 생성자의 매개변수와 동일하게 들어가야 한다.

예를 들어 부모 클래스에 다른 생성자가 있고, default 생성자가 없는 경우 자식 클래스에서 super(); 만을 선언하면 컴파일 에러가 발생한다. (매개변수 자리가 빈 default 생성자가 부모 클래스에 정의되어 있지 않기 때문이다.)



#### overloading과 overrideing

overloading은 한 클래스 내에 동일한 이름의 메소드를 여러개 정의하는 것입니다.

메소드 간 이름이 동일해야하며 단, 매개변수의 개수 및 타입이 전부 동일하다면 오버로딩이 아닙니다.

{% code lineNumbers="true" %}
```java
// 오버로딩의 조건에 부합하는 예제
int add(int x, int y, int z) {
    int result = x + y + z;
    return result;
}

long add(int a, int b, long c) {
    long result = a + b + c;
    return result;
}

int add(int a, int b) {
    int result = a + b;
    return result;
}
```
{% endcode %}

overridding은 부모 클래스로 부터 상속받은 메소드의 내용을 변경하는 것이다.

상속받은 메소드를 그대로 사용하기도 하지만, 필요에 의해 변경해야할 경우 오버라이딩을 한다.

부모 클래스의 메소드와 이름, 매개변수, 반환타입이 동일해야한

{% code lineNumbers="true" %}
```java
class Animal {
    String name;
    String color;

    public void cry() {
        System.out.println(name + " is crying.");
    }
}

class Dog extends Animal {
	//생성자
    Dog(String name) {
        this.name = name;
    }
	// 오버라이딩
    @Override
    public void cry() {
        System.out.println(name + " is barking!");
    }
    public void swim() {
        System.out.println(name + " is swimming.");
    }
}

public class Main {
    public static void main(String[] args) {
        Animal dog = new Dog("코코");
        // Animal 클래스인 dog는 자식 클래스 Dog의 swim() 사용 불가
        // 쉽게 말해 부모 클래스는 자식 클래스의 메소드를 사용하지 못한다.
        // 하지만 할당 시 오버라이딩한 cry()는 적용되어 is barking이 출력된다.
        dog.cry();
    }
}
```
{% endcode %}

자식(Dog) 객체는 자식(Dog) 타입으로 선언된 변수에도 할당할 수 있고, 부모(Animal) 타입으로 선언된 변수에도 할당할 수 있습니다.

단 부모(Animal) 타입의 변수로 사용할 때는, 실제 객체를 만들(new) 때 사용한 자식(Dog) 타입에 있는 메소드를 호출 할 수 없습니다. (swim() 함수 호출시 컴파일 에러)

**즉 오버로딩은 기존에 없는 새로운 메소드를 정의하는 것이며 오바라이딩은 상속받은 메소드의 내용을 변경하는 것이다.**



### 7) 접근 제어자 (access modifier)

접근 제어자는 멤버 변수거나 함수 혹은 클래스에 사용되며 외부에서의 접근을 제한하는 역활을 합니다.

\-> private : 같은 클래스 내에서만 접근이 가능합니다.

\-> default(nothing) : 같은 패키지 내에서만 접근이 가능합니다.

\-> protected : 같은 패키지 내에서, 그리고 다른 패키지의 자손클래스에서 접근이 가능합니다.

\-> public : 접근 제한이 전혀 없습니다.

접근 제어자로 제어하는 것을 캡슐화 라고 한다. (encapsulation)

객체지 프로그래밍이란 객체들 간의 상호작용을 코드로 표현하는 것입니다.

* 이때 객체들간의 관계에 따라서 접근 할 수 있는 것과 아닌 것, 권한을 구분할 필요가 생깁니다.
* 클래스 내부에 선언된 데이터의 부적한 사용으로부터 보호하기 위해서 ( 캡슐화 )
* 접근 제어자는 캡슐화가 가능할 수 있도록 돕는 도구입니다.



### 8) 추상 클래스

추상클래스는 추상메소드를 선언할 수 있는 클래스를 의미합니다.

추상클래스는 클래스와는 다르게 상속받는 클래스 없이 그 자체로 인스턴스를 생성할 수는 없습니다.

추상메소드는 설계만 되어있으며 수행되는 코드에 대해서는 작성이 안된 메소드입니다.

이처럼, 미완성으로 남겨두는 이유는 상속받는 클래스 마다 반드시 동작이 달라지는 경우에 상속받는 클래스 작성자가 반드시 작성하도록 하기 위함입니다. (자식 클래스에서 오버라이딩하여 작성됨) abstract 리턴타입 메소드이름();

```java
// 추상 클래스 Bird -> 그 자체로 인스턴스 생성 불가함.
abstract class Bird{
    private int x,y,z;

    void fly(int x, int y, int z){
        printLocation();
        System.out.println("이동합니다.");
        this.x = x;
        this.y = y;
        if(flyable(z)){
            this.z = z;
        }else{
            System.out.println("그 높이로는 날 수 없습니다.");
        }
        printLocation();
    }
	
    //추상 메서드 flyable() -> 자식 클래스에서 오버라이딩하여 사용
    abstract boolean flyable(int z);

    public void printLocation(){
        System.out.println("현재 위치 {" + x + "," + y + "," + z + ")");
    }
}

class Pigeon extends Bird{
	
    // 추상 메서드 오버라이딩
    @Override
    boolean flyable(int z) {
        return z < 10000;
    }
}

class Peacock extends Bird{
	
    // 추상 메서드 오버라이딩
    @Override
    boolean flyable(int z) {
        return false;
    }
}

public class Main {
    public static void main(String[] args) {
        Bird pigeon = new Pigeon();
        Bird peacock = new Peacock();
        System.out.println("---비둘기---");
        pigeon.fly(1, 2, 3);
        System.out.println("---공작새---");
        peacock.fly(1, 2, 3);
        System.out.println("---비둘기---");
        pigeon.fly(1, 2, 30000);
        
        
    }
}
// 실행결과
---비둘기---
현재 위치 {0,0,0)
이동합니다.
현재 위치 {1,2,3)
---공작새---
현재 위치 {0,0,0)
이동합니다.
그 높이로는 날 수 없습니다.
현재 위치 {1,2,0)
---비둘기---
현재 위치 {1,2,3)
이동합니다.
그 높이로는 날 수 없습니다.
현재 위치 {1,2,3)
```



### 9) 인터페이스

인터페이스는 객체의 특정 행동의 특징을 정의하는 간단한 문법입니다.

함수의 특징(method signature)인 접근제어자, 리턴타입, 메소드 이름만을 정의합니다. 함수의 내용 X

인터페이스를 구현하는 클래스는 인터페이스에 존재하는 함수의 내용을 반드시 구현해야 합니다.

interface 인터페이스명 { public abstract void 추상메서드명(); } -> 인ㅇ터페이스의 메소드는 추상메소드, static메소드, default 메소드 모두 허용됩니다.

{% code lineNumbers="true" %}
```java
interface Person {
    static final int a1 = 0;
    int  a = 0;
    abstract  String checkString1();
    default String checkString() {
        return "String";
    }
}

class Child implements Person {
    public String getMessage() {
        System.out.println("" + a);
    }

    @Override
    public String checkString() {
        return null;
    }

    @Override
    public String checkString1() {
        return null;
    }
}

class Mom {
    public String getMessage() {
        Person.a = 1; // Error a 라는 변수가 final을 컴파일 시 자동으로 생성해주기 때문
        System.out.println("" + Person.a);
    }
}
```
{% endcode %}

### +) 추상클래스와 인터페이스의 차이점

* 인터페이스

1. 모든 메서드는 추상 메소드 이다.
2. 구현하려는 객체의 동작을 명세하여 설계합니다.
3. 다중 상속 가능
4. implements를 이용하여 구현한다.
5. 메소드 시그니처(이름, 리턴타입, 파라미터)에 대한 선언만 가
6. 같은 이름의 메서드가 클래스에 따라 다르게 동작하도록 구현하는 것을 다형성을 지닌다고 말한다.



* 추상클래스

1. 클래스를 상속받아 이용 및 확장을 위함
2. 다중 상속 불가능 , 단일 상속 O
3. extends를 이용하여 구현
4. 추상메소드에 대한 구현 가능
5. 추상클래스의 기능을 재사용, 확장한다는 측면에서 상속성을 지님

추상클래스 사용 시기 : 상속 관계를 쭉 타고 올라갔을때 같은 조상클래스를 상속하는데 기능까지 완벽히 똑같은 기능이 필요한 경우

인터페이스 사용 시기 : 상속 관계를 쭉 타고 올라갔을때 다른 조상클래스를 상속하는데 같은 기능이 필요할 경우 인터페이스 사용



### 10) 예외 처리

예외리란(Exception, Error Handling)

* 예외처리의 목적

1. 예외의 발생으로 인한 실행 중인 프로그램의 비정상 종료를 막기 위해서
2. 개발자에게 알려서 코드를 보완할 수 있도록 하기 위해서

* Throwable 에는 크게 두 종류의 자식 클래스가 있다 (Error & Exception)
* 자바에 미리 정의 되어있는 예외 클래스 들이 있습니다. 기본적으로 이미 있는 것을 사용하시되, 필요한 것으로 표현할 수 없거나 구체적인 목적을 가진 예외를 가진 예외를 정의하고 싶다면, Throwable 또는 그 하위에 있는 예외 클래스를 상속받아서 자신만의 예외 클래스를 정의 할 수 있습니다.
* 메소드에서의 예외 선언\
  catch문을 이용해서 예외처리를 하지 않은 경우, 메소드에 throws로 예외가 발생할 수 있다는 것을 알려주어야 합니다. throws 키워드가 있는 함수를 호출한다면, caller 쪽에서 catch와 관련된 코드를 작성해주어야 합니다.

```java
void method() throws IndexOutOfBoundsException, IllegalArgumentException {
    //메소드의 내용
}
```

/ by zero와 arrayOutOfBoundException 출력하기.

```java
class ArrayCalculation {

    int[] arr = { 0, 1, 2, 3, 4 };

    public int divide(int denominatorIndex, int numeratorIndex) throws ArithmeticException, ArrayIndexOutOfBoundsException{
        return arr[denominatorIndex] / arr[numeratorIndex];
    }
}

public class Main {
    public static void main(String[] args) {
        ArrayCalculation arrayCalculation = new ArrayCalculation();
        System.out.println("2 / 1 = " + arrayCalculation.divide(2, 1));
        try{
            System.out.println("1 / 0 = " + arrayCalculation.divide(1, 0)); // java.lang.ArithmeticException: "/ by zero"
        }catch (ArithmeticException e){
            System.out.println("잘못된 계산 입니다. " + e.getMessage());
        }try{
            System.out.println("Try to divide using out of index element = "
                    + arrayCalculation.divide(5, 0)); // java.lang.ArrayIndexOutOfBoundsException: 5
        }catch (ArrayIndexOutOfBoundsException e){
            System.out.println("잘못된 인덱스 범위 입니다. 타당한 범위는 0부터 " + (arrayCalculation.arr.length -1) + "까지 입니다.");
        }
    }
}
```
