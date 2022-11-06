# CSRF(Cross-Site Request Forgery)

<br>

## 💡 CSRF(Cross-Site Request Forgery)란?

> CSRF는 크로스 사이트 리퀘스트 변조라고 하며, 한 문장으로 정리하면 '웹 어플리케이션 유저인 자신이 의도하지 않은 처리가 실행되는 취약성 또는 공격수법' 이라고 할 수 있다.
>
> 즉, 사용자가 자신의 의지와는 무관하게 공격자의 의도한 행위를 특정 웹사이트에 요청하게 하는 공격이라고 할 수 있다.

<br>

<img src="https://user-images.githubusercontent.com/66936285/200162217-a4a26caa-8574-40e6-9be2-c12b35ddc9df.png">

<br>
<br>

## 💡 CSRF에 의한 피해 사례

> 이용자가 의도하지 않은 처리 실행: 로그인한 이용자만 허가되어 있는 페이지의 처리 등

<br>
<br>

## 💡 CSRF를 방지하는 대표적인 방법

> - Form 페이지의 반환 시에 토큰을 부여
>
> 1.  예를 들어, 처음 게시판에 글을 쓰는 화면을 표시할 때 서버가 클라이언트에 대해 특정한 문자열인 토큰을 발급한다.
> 2.  실제로 글을 쓸 때, 요청이 있으면 서버는 전에 발급한 토큰과 같은 토큰이 요청에 포함되어 있는지는 확인한다.
>
> 이와 같이 공격자는 토큰을 알지 못하기 때문에 토큰을 확인하는 것으로 공격자로부터 올바르지 않는 요청을 방지하는 것이 가능해 진다.

<br>
<br>

### 📚 Reference

- https://rusyasoft.github.io/java/2019/02/15/spring-security-csrf-from-context/
- https://developer.mozilla.org/en-US/docs/Glossary/CSRF
- https://cheatsheetseries.owasp.org/cheatsheets/Cross-Site_Request_Forgery_Prevention_Cheat_Sheet.html
