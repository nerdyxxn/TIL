# React-Router

> SPA에서 한 개의 웹 페이지(html) 내에서 여러 개의 페이지를 보여주기 위해 react-router 라이브러리를 활용해서 Routing 구현
>
> - SPA(Single Page Application) : 페이지가 한 개인 애플리케이션
> - MPA(Multi Page Application) : 페이지가 여러 개인 애플리케이션

<br>

## 💡 Routing 이란?

> 사용자가 요청한 경로(URL 주소)에 따라 해당 URL에 맞는 다른 View(화면)를 보여주는 것이다.
> React 자체에는 이러한 기능이 내장되어 있지 않으며 react-router는 라우팅 기능을 위해 가장 많이 사용되는 라이브러리 중 하나이다.

<br>
<br>

## 💡 React-router 설치하기

```bash
// React Router Install
$ npm install react-router-dom

// 특정 버전 React-Router Install
$ npm install react-router-dom@6.3.0
```

<br>

- **package.json에서 설치 확인**
  <img src='https://user-images.githubusercontent.com/66936285/202854674-aefc7d21-2cc8-4358-8e92-19d7c8410bfb.png' width=500>

<br>
<br>

## 💡 Router Component 구현하기

```jsx
import React from 'react';
import { BrowserRouter, Routes, Route } from 'react-router-dom';
import Login from './pages/Login/Login.js';
import Main from './pages/Main/Main.js';

function Router() {
  return (
    <BrowserRouter>
      <Routes>
        <Route path="/" element={<Login />} />
        <Route path="/main" element={<Main />} />
      </Routes>
    </BrowserRouter>
  );
}

export default Router;
```

- 라우터를 통하여 사용자가 해당 주소를 입력하면 어떤 컴포넌트로 이동할지 지정할 수 있다.

<br>

```jsx
// index.js
import Router from './Router.js';

ReactDOM.render(<Router />, document.getElementById('root'));
```

- CRA로 만든 앱에 routing 기능을 적용하려면 index.js 파일을 수정하는데 기존 App 컴포넌트 대신에 routing을 설정한 컴포넌트 Router로 변경했다.

<br>
<br>

## 💡 React Router 주요 컴포넌트

#### 1) BrowserRouter

- 라우터 역할을 담당한다. 새로고침을 하지 않더라도 새로운 컴포넌트를 렌더링 해주는 기능을 담당한다.

#### 2) Routes, Route

- 경로를 매칭해주는 역할을 담당. 경로가 일치하는 컴포넌트를 렌더링하게 된다. Route에서는 구체적으로 어떤 컴포넌트를 렌더링할지 결정한다.

#### 3) Link

- 경로를 변경해주는 역할을 담당. 기존 HTML의 a 태그가 새로고침을 통해 처음부터 렌더링을 수행한다면 Link 컴포넌트는 페이지 전환을 방지하는 기능을 내장하고 있다.
  즉, 새로고침을 하지 않더라도 해당 페이지의 소스를 렌더링하게 된다.

<br>
<br>

## 💡 Route 이동하기

#### 1) Link

```jsx
import React from 'react';
import { Link } from 'react-router-dom';

function Login() {
  return (
    <div>
      <Link to="/login">로그인</Link>
    </div>
  );
}

export default Login;
```

- Router.js에서 설정한 path로 이동하는 첫 번째 방법은 Link 컴포넌트를 사용하는 것이다.
  react-router-dom에서 제공하는 Link 컴포넌트는 DOM에서 a 태그로 변환(compile)된다.
  a 태그와 마찬가지로 Link 컴포넌트도 지정한 경로로 바로 이동시켜주는 기능을 한다.

<br>

- **a 태그와 Link 컴포넌트의 차이점**
  - a 태그는 외부 사이트로 이동하는 경우에 사용하며, Link 컴포넌트 컴포넌트는 프로젝트 내에서 페이지를 전환하는 경우 사용한다.

<br>

#### 2) useNavigate

```jsx
import React form 'react';
import { useNavigate } from 'react-router-dom';

function Login() {
	const navigate = useNavigate();

    const goToMain = () => {
    	navigate("/main");
    }

    return (
    	<div>
        	<button className="loginBtn" onClick={goToMain}>
            	로그인
            </button>
        </div>
    );
}

export default Login;
```

- Link 컴포넌트를 사용하지 않고 함수 호출을 통해 페이지를 이동하는 방법은 useNavigate 훅을 사용하는 것이다.
  useNavigate 훅을 실행하면 페이지 이동을 할 수 있게 해주는 함수를 반환한다.
  해당 함수를 navigate라는 변수에 저장하고 navigate의 인자로 Router.js에서 설정한 path를 넘겨주면 해당 경로로 이동할 수 있다.

<br>

#### 🔖 Link와 useNavigate 두 방식의 활용방법

**Link**

- 클릭 시 바로 이동하는 로직 구현 시 사용한다.
- Nav Bar, Aside, Menu 등 아이템 리스트 페이지에서 아이템 클릭시 상세 페이지로 이동한다.

<br>

**useNavigate**

- 페이지 전환 시 추가로 처리해야 하는 로직이 있는 경우 훅을 활용하여 구현한다.
- ex) 로그인 버튼 클릭시
  - Backend API로 데이터 전송
  - User Data 인증/인가
  - response message
  - Case 1 : 회원가입 되어 있는 사용자는 Main page 이동
  - Case 2 : 회원가입이 되어 있지 않은 사용자는 Signup page 이동

<br>
<br>

### 📚 Reference

&nbsp; https://reactjs.org/
&nbsp; https://www.inflearn.com/course/%ED%95%9C%EC%9E%85-%EB%A6%AC%EC%95%A1%ED%8A%B8

<br>
<br>
