# State & Props의 개념

<br>

## 💡 State(상태)

> React에서 State는 변수 대신 쓰는 데이터 저장공간

- useState() Hook을 이용해서 만들어야 한다.

  - 예시로 아래의 사진처럼 테마라는 상태가 Dark / Light 값에 따라 다른 동작을 해서 다른 화면을 볼 수 있다.
    <img src='https://user-images.githubusercontent.com/66936285/201866425-0b860b08-2b4f-43fa-95d2-8fd0acb80921.png'>

<br>

- 리액트에서는 어떤 컴포넌트가 가진 state가 바뀌면 그 컴포넌트가 재렌더링 되고,
  나에게 내려오는 props가 바뀔 때마다 재랜더링 되고,
  둘 다 아니어도 내 부모가 재랜더링 되면 나도 재랜더링 된다.

<br>
<br>

## 💡 Props

> React에서 계층 간 데이터를 전달하는 방법

<br>

#### 1. 부모에서 자식으로 데이터 전달하기 (Counter.js)

- 기존 방법 & 스프레드 연산자와 비구조화 할당을 활용한 방법

```jsx
/* App.js */
import './App.css';
import MyHeader from './MyHeader';
import MyFooter from './MyFooter';
import Counter from './Counter';

function App() {
  const counterProps = {
    a: 1,
    b: 2,
    c: 3,
    d: 4,
    e: 5,
    initialValue: 5,
  };

  return (
    <div className="App">
      <MyHeader />
      <header className="App-header">
        <h2>Hello React!</h2>
        <Counter {...counterProps} />
      </header>
      <MyFooter />
    </div>
  );
}

export default App;
```

> - 위와 같이 스프레드 연산자를 사용해서 전달할 수도 있음
> - 이전에는 전달할변수이름={변수명} 으로 작성해서
>   자식이 props.전달할변수이름 이러한 방식으로 전달했음

<br>
<br>

```jsx
/* Counter.js */
import React, { useState } from 'react';

const Counter = ({ initialValue }) => {
  const [count, setCount] = useState(initialValue);
  // 위와 같이 (props)가 아닌 비구조화 할당을 통해서 받을 수도 있다!
  // props에서 특정값만 꺼내서 넣을 수 있다는 것... 비구조화 할당 정리 필요 (자바스크립트 응용)

  const onIncrease = () => {
    setCount(count + 1);
  };

  const onDecrease = () => {
    setCount(count - 1);
  };

  return (
    <div>
      <h2>{count}</h2>
      <button onClick={onIncrease}>+</button>
      <button onClick={onDecrease}>-</button>
    </div>
  );
};

export default Counter;
```

<br>

#### 2. props로 컴포넌트 전달도 가능

- 컨테이너.js를 만들고 스타일을 적용하여 children이라는 특정 변수로 속성을 전달할 수 있음
- 받으려는 js에서 div를 컨테이너 컴포넌트로 감싸면 전달된 속성이 적용됨 (CSS)

```jsx
/* Container.js */
const Container = ({ children }) => {
  return <div style={{ margin: 20, padding: 20, border: '1px solid gray' }}>{children}</div>;
};

export default Container;
```

```jsx
/* App.js */

return (
  <Container>
    <div className="App">
      <MyHeader />
      <header className="App-header">
        <h2>Hello React!</h2>
        <Counter {...counterProps} />
      </header>
      <MyFooter />
    </div>
  </Container>
);
```

<br>
<br>

### 📚 Reference

&nbsp; https://www.inflearn.com/course/%ED%95%9C%EC%9E%85-%EB%A6%AC%EC%95%A1%ED%8A%B8

<br>
<br>
