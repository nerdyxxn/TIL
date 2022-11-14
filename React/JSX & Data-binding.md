# JSX & Data-binding

<br>

## 💡 JSX 란?

> - `JavaScript` 파일 안에서 `HTML`을 직관적으로 작성하기 위해 도와주는 `React` 기본 내장 문법
> - 공통적으로 써야되는 요소들을 리액트에서는 컴포넌트라는 이름으로 분할해서 재사용할 수 있음
> - JSX는 리액트 컴포넌트를 만드는데 아주 유용한 문법임

<img src='https://user-images.githubusercontent.com/66936285/201618450-dc56a8eb-5365-46f2-8528-74b9242b01c0.png'>

<br>
<br>

## 💡 JSX 문법

> - **닫힘 규칙**
>
>   - 태그는 반드시 닫는 태그가 있어야 함 (셀프 클로징 태그 포함)
>     <br>
>
> - **최상위 태그 규칙**
>
>   - JSX로 컴포넌트를 만들어서 리턴하려면 반드시 하나의 최상위 태그로 묶어줘야 함
>
>   1. App.js 처럼 App이라는 div로 감싼다.
>
>   2. import React from ‘react’; 를 시키고
>      <React.Fragment></React.Fragment> 태그로 감싼다.
>
>   3. <></>로 감싼다.
>      <br>
>
> - **className**
>   - JSX에서 클래스 이름을 지정하는 키워드 (class 대신 className을 사용해야 함)

<br>
<br>

## 💡 JSX에서 데이터바인딩하기

> 데이터바인딩은 JavaScript 데이터를 HTML에 넣는 작업을 뜻한다.

```jsx
function App() {
  let data = '안녕하세요';

  return (
    <div className="App">
      <div className="black-nav">
        <div>개발 blog</div>
        <div>{data}</div>
      </div>
    </div>
  );
}
```

위 코드를 구동시키면 div { data } 부분에 위에서 정의한 data 변수의 데이터가 출력된다.

- 변수명, HTML 속성, 함수 모두 가능
- `HTML` 중 `style`속성은 `{ 속성명: 속성값 }`를 사용하여 오브젝트로 바꿔서 넣어야 한다.
- 속성명에 `-(대쉬)` 기호를 사용할 수 없기 때문에, `camelCase`로 치환해줘야 한다. (되도록 css 파일 만들어서 사용)

```jsx
<div style={{ color: 'blue', fontSize: '30px' }}> 글씨 </div>
```

<br>
<br>

### 📚 Reference

&nbsp; https://codingapple.com/unit/react2-jsx-classname-html/?id=2305
&nbsp; https://www.inflearn.com/course/%ED%95%9C%EC%9E%85-%EB%A6%AC%EC%95%A1%ED%8A%B8

<br>
<br>
