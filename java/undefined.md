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







