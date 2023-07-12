# View 페이지 구동 원리

<figure><img src="../../.gitbook/assets/image (8) (1).png" alt=""><figcaption></figcaption></figure>

* 컨트롤러에서 리턴 값으로 문자(ex: `retrun "hello";`)를 반환하면 뷰 리졸버(`viewResolver`)가 화면을 찾아서 처리합니다.
  * 스프링 부트 템플릿 엔진 기본 viewName 매핑
  * `resources:templates/` + (ViewName) + `.html`
    * `yml` 에서 경로를 변경해줄 수도 있습니다.

```yaml
spring:
    thymeleaf:
        prefix: classpath:/templates/
        suffix: .html
```

참고 : `spring-boot-devtools` 라이브러리를 추가하면 `html` 파일을 컴파일만 하면 서버 재시작 없이 View 파일 변경이 가능합니다. IntelliJ : 메뉴 -> build -> Recompile



`hotswap` 기능을 사용하면 `Recompile` 도 자동으로 됩니다.

<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>
