# 브라우저 저장소 (Cookie & localStorage & sessionStorage)

<br>

## 💡 Cookie

> Cookie의 용량은 4KB로 다른 두 방식에 비해 굉장히 적다.
> 그리고 HTTP 요청으로 헤더에 담아 브라우저에서 서버로 송신되기 때문에 용량이 크면 성능에 영향이 미칠 수 있다.
>
> Cookie는 HTML4도 대응 가능하다. 즉, 구식 브라우저에서도 사용 가능하다.

<br>
<br>

## 💡 localStorage & sessionStorage

> LocalStorag와 SessionStorage의 사용은 저장기간이 길게 필요한가, 짧게 필요한가에 따라 나뉜다.
>
> localStorage는 데이터를 영구적으로 저장할 수 있으나,
> sessionStorage는 이름에서 알 수 있듯이 브라우저가 종료되면 데이터도 같이 지워지는 특성이 있다.

<br>
<br>

## 💡 브라우저 저장소 비교표

<img alt="cookie" src="https://user-images.githubusercontent.com/66936285/199433912-b2100978-3d67-4d58-a36e-576eac6fbaab.png">

<br>
<br>

### 📚 Reference

- https://www.youtube.com/watch?v=GihQAC1I39Q
- https://scotch.io/@PratyushB/local-storage-vs-session-storage-vs-cookie
- https://stackoverflow.com/questions/19867599/what-is-the-difference-between-localstorage-sessionstorage-session-and-cookies
