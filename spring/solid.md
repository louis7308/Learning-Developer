# SOLID

### SOLID <a href="#sould" id="sould"></a>

> 클린코드로 유명한 로버트 마틴이 "좋은 객체 지향 설계의 5가지 원칙" 을 정리

* SRP : 단일 책임 원칙 (Single Responsibility Principle)
* OCP : 개방-폐쇠 원칙 (Open/Closed Princple)
* LSP : 리스코프 치환 원칙 (Liskov Substitution Principle)
* ISP : 인터페이스 분리 원칙 (Interface Segregation Principle)
* DIP : 의존관계 역전 원칙 (Dependency Inversion Principle)



### SRP 단일 책임 원칙 <a href="#srp" id="srp"></a>

> 중요한 기준은 변경이다. 변경이 있을 때 파급 효과가 적으면 단일 책임 원칙을 잘 따른것

* 하나의 크래스는 하나의 책임만 가져야 한다.
* 하나의 책임이라는 것은 모호하다
  * 클 수 있고, 작을 수 있다
  * 문맥과 상황에 따라 다르다

EX)&#x20;
