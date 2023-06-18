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
