# LifeCycle

> 리액트 컴포넌트는 LifeCycle (생명주기) 가 있다.

<br>

## 💡 Component의 LifeCycle

<img src="https://user-images.githubusercontent.com/66936285/206835599-1a47316f-08f5-4337-a9e3-85cb74be4d62.png">

<br>
<br>

#### 🔖 컴포넌트의 라이프 사이클은 크게 세가지로 구분된다.

1. 마운트 ⇒ 페이지에서 컴포넌트가 생김
2. 업데이트 ⇒ 컴포넌트 정보가 업데이트
3. 언마운트 ⇒ 페이지에서 사라짐

<br>
<br>

## 💡 마운트 (Mount)

> 웹 브라우저에서 컴포넌트가 나타났을 때를 마운트(mount)라고 한다.
> 마운트가 되면 메서드들이 호출된다.

<br>

#### 🔖 메서드가 호출되는 순서

1. constructor
   → 클래스 생성자 메서드가 컴포넌트만들때 사용된다.
2. getDerivedStateFromProps
   → props에 있는 값을 state에 동기화 시킬때 사용
3. render
   → 웹브라우저에 렌더링할 컴포넌트를 랜더해주는 함수
4. componentDidMount
   → 컴포넌트가 웹 브라우저에서 나타난후 호출

<br>

- componentDidMount에서는 DOM에 접근 가능하다.
  - DOM트리가 다 만들어진 이후이기 때문에 DOM에 접근이 가능하기 때문
  - 따라서 이 부분에서 주로 AJAX, setTImeout, setInterval과 같은 동작을 처리한다.

<br>
<br>

## 💡 업데이트

<br>

#### 🔖 업데이트가 되는 4가지 경우

1. props가 변경
2. state가 변경
3. 부모 컴포넌트가 리렌더링
4. this.forceUpdate 강제로 렌더링

<br>

#### 🔖 업데이트 될때 호출되는 메서드

1. getDerivedStateFromProps
   → 마운트에서 메서드와 같다. 업데이트가 되기 전에 호출
2. shouldComponentUpdate
   → 컴포넌트가 리렌더링 되어야할지 결정한다.
   → true이면 다음 라이플 사이클메서드를 실행, false이면 중단된다.
3. render
   → 컴포넌트를 렌더링한다.
4. getSnapshotBeforeUpdate
   → DOM 반영하기 직전에 호출된다.
5. componentDidUpdate
   → 브라우저에 반영된 후 호출된다.

<br>

- shouldComponentUpdate는 아직 render하기 이전이고 return문으로 boolean 값을 넣어 render를 취소할지 실행할지 결정할 수 있다. 이 때 주로 성능 최적화를 한다.
- componentDidUpdate는 첫번째 인자로 prevState를 두번째로 prevProps를 인자로 받는다.

<br>
<br>

## 💡 언마운트

> 컴포넌트가 DOM에서 제거된 것을 **언마운트** 라고 한다.

<br>

#### 🔖 언마운트될 때 호출되는 메서드

- componentWillUnmount
  → 컴포넌트가 브라우저에서 제거되기 전에 호출된다.
  <br>
- 주로 이벤트 리스너를 제거하고 이후 cleanUp 작업을 이곳에서 한다.

<br>
<br>

## 💡 ComponentDidCatch

> 라이프사이클과정에서 에러가 발생하면 ComponentDidCatch 메서드가 호출된다.

<br>

이 메서드는 this.state.error 값을 true로 업데이트해준다.

```jsx
import React, { Component } from 'react';

class MyComponent extends Component {
  state = {
    error: false,
  };
  componentDidCatch() {
    this.setState({
      error: true,
    });
  }
  render() {
    if (this.state.error) return <h1>에러가 발생했습니다.</h1>;
    return this.props.children;
  }
}

export default MyComponent;
```

<br>

에러를 위한 리액트 컴포넌트를 만들었으면 부모 컴포넌트에서 다른 컴포넌트들을 감싸주면 된다.

```jsx
import MyComponent from './MyComponent';
import Errorboundary from './Errorboundary';

function App() {
  return;
  <Errorboundary>
    <MyComponent />
  </Errorboundary>;
}

export default App;
```
