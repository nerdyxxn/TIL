# State & Propsμ κ°λ

<br>

## π‘ State(μν)

> Reactμμ Stateλ λ³μ λμ  μ°λ λ°μ΄ν° μ μ₯κ³΅κ°

- useState() Hookμ μ΄μ©ν΄μ λ§λ€μ΄μΌ νλ€.

  - μμλ‘ μλμ μ¬μ§μ²λΌ νλ§λΌλ μνκ° Dark / Light κ°μ λ°λΌ λ€λ₯Έ λμμ ν΄μ λ€λ₯Έ νλ©΄μ λ³Ό μ μλ€.
    <img src='https://user-images.githubusercontent.com/66936285/201866425-0b860b08-2b4f-43fa-95d2-8fd0acb80921.png'>

<br>

- λ¦¬μ‘νΈμμλ μ΄λ€ μ»΄ν¬λνΈκ° κ°μ§ stateκ° λ°λλ©΄ κ·Έ μ»΄ν¬λνΈκ° μ¬λ λλ§ λκ³ ,
  λμκ² λ΄λ €μ€λ propsκ° λ°λ λλ§λ€ μ¬λλλ§ λκ³ ,
  λ λ€ μλμ΄λ λ΄ λΆλͺ¨κ° μ¬λλλ§ λλ©΄ λλ μ¬λλλ§ λλ€.

<br>
<br>

## π‘ Props

> Reactμμ κ³μΈ΅ κ° λ°μ΄ν°λ₯Ό μ λ¬νλ λ°©λ²

<br>

#### 1. λΆλͺ¨μμ μμμΌλ‘ λ°μ΄ν° μ λ¬νκΈ° (Counter.js)

- κΈ°μ‘΄ λ°©λ² & μ€νλ λ μ°μ°μμ λΉκ΅¬μ‘°ν ν λΉμ νμ©ν λ°©λ²

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

> - μμ κ°μ΄ μ€νλ λ μ°μ°μλ₯Ό μ¬μ©ν΄μ μ λ¬ν  μλ μμ
> - μ΄μ μλ μ λ¬ν λ³μμ΄λ¦={λ³μλͺ} μΌλ‘ μμ±ν΄μ
>   μμμ΄ props.μ λ¬ν λ³μμ΄λ¦ μ΄λ¬ν λ°©μμΌλ‘ μ λ¬νμ

<br>
<br>

```jsx
/* Counter.js */
import React, { useState } from 'react';

const Counter = ({ initialValue }) => {
  const [count, setCount] = useState(initialValue);
  // μμ κ°μ΄ (props)κ° μλ λΉκ΅¬μ‘°ν ν λΉμ ν΅ν΄μ λ°μ μλ μλ€!
  // propsμμ νΉμ κ°λ§ κΊΌλ΄μ λ£μ μ μλ€λ κ²... λΉκ΅¬μ‘°ν ν λΉ μ λ¦¬ νμ (μλ°μ€ν¬λ¦½νΈ μμ©)

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

#### 2. propsλ‘ μ»΄ν¬λνΈ μ λ¬λ κ°λ₯

- μ»¨νμ΄λ.jsλ₯Ό λ§λ€κ³  μ€νμΌμ μ μ©νμ¬ childrenμ΄λΌλ νΉμ  λ³μλ‘ μμ±μ μ λ¬ν  μ μμ
- λ°μΌλ €λ jsμμ divλ₯Ό μ»¨νμ΄λ μ»΄ν¬λνΈλ‘ κ°μΈλ©΄ μ λ¬λ μμ±μ΄ μ μ©λ¨ (CSS)

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

### π Reference

&nbsp; https://www.inflearn.com/course/%ED%95%9C%EC%9E%85-%EB%A6%AC%EC%95%A1%ED%8A%B8

<br>
<br>
