# 스프링부트는 어떻게 다중 유저 요청을 처리할까?

## 개요

스프링 부트는 웹서버 어플리케이션 구조에 대해 잘 몰라도, 뚝딱 웹서버 어플리케이션을 만들게 도와줍니다.

하지만 한번씩 궁금증이 들 때가 있습니다. 이게 왜 되지..??

<figure><img src="../../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

스프링부트의 flow를 찾아보면 흔히 나오는 MVC 흐름도 그림인데... **한 유저의 요청이 어떻게 처리되는지** 에 대한 내용은 많지만 **여러 유저의 요청이** 어떻게 처리되는지에 대한 내용은 잘 없습니다.

추측컨데, MVC는 스프링부트를 사용하는 개발자가 직접 구현해야하는 부분이고, 다중요청처리는 스프링부트가 알아서 해주고 있는 부분이니 상대적으로 관심도가 덜한 것이라 여겨집니다.

사실 스프링부트가 다중요청을 처리하는 것이 아니라, 스프링부트에 내장되어 있는 서블릿 컨테이너(Tomcat) 에서 다중요청을 처리해줍니다. 서블릿 컨테이너에 대해 잘 모르신다면 `서블릿 컨테이너` 키워드로 검색하시면 좋은 자료를 많이 찾을 수 있습니다.

핵심 키워드는 `Tomcat Thread Pool`, `NIO Connector`, `Embeded Tomcat` 입니다.



## 결론부터!

1. 스프링부트는 내장 서블릿 컨테이너인 Tomcat을 이용합니다.

> 스프링부트 2.5.4 기준으로 9.0.52 버전의 Tomcat을 내장하고 있습니다.

2. Tomcat은 다중 요청을 처리하기 위해서, 부팅할 때 스레드의 컬렉션인 Thread Pool을 생성합니다.
3. 유저 요청(HttpServletRequest)가 들어오면 Thread Pool 에서 하나씩 Thread를 할당합니다. 해당 Thread에서 스프링부트에서 작성한 Dispatcher Servlet을 거쳐 유저 요청을 처리합니다.
4. 작업을 모두 수행하고 나면 스레드는 스레드풀로 반환됩니다.

1번부터 차례대로 내용을 확인해보겠습니다.



### 스프링부트와 내장 톰캣

스프링과 스프링부트의 주요한 차이점 중 하나는, 스프링 부트에선 내장 서블릿 컨테이너(Tomcat)을 지원한다는 것입니다.

그럼으로써 `application.yml` 혹은 `application.properties` (Spring Environment)에 설정을 주는 것만으로 간편하게 Tomcat의 설정을 바꾸어줄 수 있습니다. 다음은 서버의 설정을 바꾸어주는 예시입니다.

```yaml
# application.yml ( 적어놓은 값은 default )
server:
    tomcat:
        threads:
            max: 200 # 생성할 수 있는 thread의 총 개수
            min-spare: 10 # 항상 활성화 되어있는(idle) thread의 개수
        max-connections: 8192 # 수립가능한 connection의 총 개수
        accept-count: 100 # 작업큐의 사이즈
        connection-timeout: 20000 # timeout 판단 기준 시간, 20초
    port: 8080 # 서버를 띄울 포트번호
```

이 밖에도 많은 옵션을 과거 xml방식의 복잡한 설정에서 벗어나 간단하게 옵션을 변경할 수 있습니다. 만약 설정을 주지 않는다면, SpringBoot AutoConfiguration에서 정의한 디폴트값을 주입하게 됩니다. 해당 디폴트 값은 `org.springframework.boot.autoconfigure.web.ServerPoperties` 클래스에서 확인할 수 있습니다.

<figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

### 스레드풀(Thread Pool) 설정

위에 예시로 들어둔 yml파일에 적어놓은 값들이, Tomcat `ThreadPoolExcutor` `Connector` 에 줄 수 있는 옵션들입니다.

#### 스레드풀이란?

Thread Pool은 프로그램 실행에 필요한 Thread들을 미리 생성해놓는다는 개념입니다.

(Thread는 cpu의 자원을 이용하여 코드를 실행하는 하나의 단위 입니다.)

Tomcat 3.2 이전 버전에서는, 유저의 요청이 들어올 때 마다 Servlet을 실행할 Thread를 하나씩 생성했습니다. 요청이 끝나면 destory 했고요. 이 방침은 두 가지 문제를 야기 했습니다.

> 1. 모든 요청에 대해 스레드를 생성하고 소멸하는 것은 OS와 JVM에 대해 많은 부담을 안겨준다
> 2. 동시에 일정 이상의 다수 요청이 들어올 경우 리소스(CPU와 메모리 자원) 소모에 대한 억제가 어렵다. 즉 순간적으로 서버가 다운되거나 동시다발적인 요청을 처리하지 못해서 생기는 문제가 야기 될 수 있다.

해당 문제를 해ㄹ결하기 위해, 톰캣은 스레드풀을 활용하기 시작합니다.

<figure><img src="../../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

스레드풀의 기본 flow는 다음과 같습니다.

1. 첫 작업이 들어오면, **core size만큼의 스레드를 생성합니다.**
2. 유저 요청(Connection, Server Socket에서 accept한 소캣 객체)이 들어올 때마다 작업 큐(queue)에 담아둡니다.
3. core size의 스레드 중, 유휴상태(idle)인 스레드가 있다면 작업 큐에서 작업을 꺼내 스레드에 작업을 할당하여 작업을 처리합니다.
   1. 만약 유휴상태인 스레드가 없다면, 작업은 작업 큐에서 대기합니다.
   2. 그 상태가 지속되어 작업 큐가 꽉 찬다면, 스레드를 새로 생성합니다.
   3. 3번 과정을 반복하다 스레드 최대 사이즈에 도달하고 작업큐도 꽉 차게 되면, 추가 요청에 대해선 connection-refused 오류를 반환합니다.
4. 태스크가 완료되면 스레드는 다시 유휴상태로 돌아갑니다.
   1. 작업큐가 비어있고 core size이상의 스레드가 생성되어있다면 destory합니다.

한줄요약 : 스레드를 미리 만들어놓고 필요한 작업에 할당했다가 돌려 받는다.

2번의 `Connection, Server Socket에서 accept한 소캣 객체` 가 이해 안 가신다면 `자바 소켓 프로그래밍` 으로 검색해보세요 구체적인 구현보다, 개념적으로 서버와 클라이언트가 어떻게 연결되는지에 대해 알아보세요.

스레드는 많으면 너무 많은 스레드가 cpu의 자원을 두고 경합하게 되므로 처리속도가 느려질 수 있고, 적으면 cpu 자원을 최적으로 활용하지 못하여 마찬가지로 처리속도가 느려질 수 있습니다. \`적절한&#x20;
