# XSS(Cross-Site Scripting)

<br>

## 💡 XSS(Cross-Site Scripting)란?

> XSS는 '유저가 웹 페이지에 접속하는 것으로 올바르지 않은 스크립트가 실행되는 취약점 또는 공격방법' 을 말한다.
>
> 사이트 간 스크립팅으로 웹 앱에서 많이 나타나는 취약점의 하나이며, 웹 사이트의 관리자가 아닌 일반 유저가 웹 페이지에 악성 스크립트를 삽입할 수 있는 취약점이다.

<br>

<img src="https://user-images.githubusercontent.com/66936285/200252457-03c8d390-baf6-4194-868b-c84413d19938.png">

<br>
<br>

## 💡 XSS에 의한 피해 사례

> **공격자에 의해 올바르지 않은 로그인**
> 유저의 Cookie가 공격자에 손에 넘어가는 것으로 Cookie 내에 있는 유저의 세션 정보가 공격자에 의해 사용되는 것으로, 유저를 사칭하여 서비스를 이용할 수 있는 위험성이 있다.

<br>
<br>

## 💡 XXS를 방지하는 대표적인 방법

> 1.  유저가 입력한 값의 검증을 서버 측에서 수행
>
> 2.  유저가 입력한 값 중에 HTML 코드로 인식될 수 있는 특수문자를 일반문자로 바꿔서 처리
>     웹 페이지를 출력할 때, HTML 코드로 인식될 수 있는 문자열(예를 들면 '<', '&' 등)을 일반 문자열로 바꿔서 출력하도록 하며, 유저가 입력한 값 뿐만 아니라 외부 시스템에서 온 데이터 등도 웹 페이지에 출력 대상이 되는 것이라면 반드시 처리해주는 것이 중요하다.

<br>
<br>

### 📚 Reference

- https://www.nascenia.com/why-cross-site-scripting-is-detrimental-and-how-to-prevent/
- https://stupidsecurity.tistory.com/17
- https://4rgos.tistory.com/1
