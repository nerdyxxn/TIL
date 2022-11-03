# CSR(Client Side Rendering), SSR(Server Side Rendering)과 렌더링 방식의 차이

<br>

## 💡 렌더링 방식의 구분

> - 리퀘스트 시, 클라이언트 측에서 모든 렌더링을 한다. (Client Side Rendering)
> - 리퀘스트 시, 서버 측에서 최소한의 렌더링을 하고(퍼스트 뷰), 그 이후에는 클라이언트에서 렌더링한다. (SSR + CSR)
> - JS의 빌드 시에 서버 측에서 최소한의 렌더링을 하고 정적 파일을 생성한 후, 리퀘스트 시에는 정적 파일과 그 이후의 동작에 필요한 JS를 클라이언트 측에서 렌더링 한다. (프리 렌더링 + CSR)

<br>
<br>

## 💡 각 렌더링 방식의 특징

> 1. CSR(Client Side Rendering) : 초기 렌더링이 느리다.
> 2. SSR + CSR: 구현하기가 번거롭다.
> 3. 프리 렌더링 + CSR: 유저마다 표시내용이 다른 페이지에는 적용이 불가능하다.

<br>
<br>

## 💡 CSR, SSR의 주요 차이점

> **CSR(Client Side Rendering)**
>
> CSR은 SPA(Single Page Application)로, 클라이언트 사이드에서 HTML을 반환한 후에 JS가 동작하면서 데이터만을 주고 받아서 클라이언트에서 렌더링을 진행하는 것이다.
> 유저의 행동에 따라 필요한 부분만 다시 읽어들이기 때문에 SSR보다 빠른 인터랙션이 가능하다.
> 단, 페이지를 읽고 자바스크립트를 읽고나서 화면을 그리기 때문에 초기구동 속도가 느리다.

<br>

> **SSR(Server Side Rendering)**
>
> SSR은 사용자가 웹페이지에 접근할 때, 서버에 각각의 페이지에 대한 요청을 하여 HTML,JS 등을 다시 다운로드 하여 화면에 렌더링하는 방식이다.
> CSR과 비교하여 초기 구동속도가 빠르다는 장점이 있지만, 모든 요청에 관해 필요한 부분만 렌더링하는 것이 아니라 전체 페이지를 렌더링하기 때문에 불필요한 작업이 발생한다.

<br>
<br>

### 📚 Reference

- https://qrunch.net/@como/entries/wNz5sQ5ntxAX4Xi1
- https://velog.io/@zansol/%ED%99%95%EC%9D%B8%ED%95%98%EA%B8%B0-%EC%84%9C%EB%B2%84%EC%82%AC%EC%9D%B4%EB%93%9C%EB%A0%8C%EB%8D%94%EB%A7%81SSR-%ED%81%B4%EB%9D%BC%EC%9D%B4%EC%96%B8%ED%8A%B8%EC%82%AC%EC%9D%B4%EB%93%9C%EB%A0%8C%EB%8D%94%EB%A7%81CSR
