# 쿼리 파라미터 로그 남기기

1. 설정파일(`properties` or `yml`)에 해당 속성 추가

{% code lineNumbers="true" %}
```yaml
logging:
    level:
        org.hibernate.SQL: debug
```
{% endcode %}

2. build.gradle에 라이브러리 추가

```gradle
implementation 'com.github.gavlyukovskiy:p6spy-spring-boot-starter:1.6.1'
```

<쿼리 예시>

{% code lineNumbers="true" %}
```sql
insert 
    into
        member
        (username, id) 
    values
        (?, ?)
        
insert into member (username, id) values (?, ?)
insert into member (username, id) values ('memberA', 1);
```
{% endcode %}

이렇게 깔끔하게 파라미터 값을 볼 수 있다.

\+) 참고 : 쿼리 파라미터를 로그로 남기는 외부 라이브러리는 시스템 자원을 사용하므로, 개발 단계에서는 편하게 사용해도 된다. 하지만 운영시스템에 적용하려면 꼭 성능테스트를 하고 사용하는 것이 좋다.
