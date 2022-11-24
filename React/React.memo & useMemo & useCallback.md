# React 최적화 (React.memo, useMemo, useCallback)

> React는 컴포넌트를 렌더링 한 뒤, 이전 렌더된 결과와 비교하여 Dom 업데이트를 결정한다. 이 때 리렌더가 필요없는 컴포넌트의 렌더를 방지하여 업데이트 속도를 높일 수 있는 방법들이 있다.
> React.memo, useMemo, useCallback은 모두 불필요한 렌더링 또는 연산을 제어하는 용도로 성능 최적화에 그 목적이 있다.

<br>

## 💡 Memoization

> 동일한 문제에 대한 답을 기억해뒀다가, 같은 문제를 만나면 계산하지 않고 기억해둔 답을 반환시키는 방법

<img src="https://user-images.githubusercontent.com/66936285/203700996-9ede3ba8-b091-4ca6-8006-414f746410c8.png">

<br>
<br>

## 💡 React.memo

> React.memo는 Higher-Order Components(HOC)이다.
> (HOC란 컴포넌트를 인자로 받아서 새로운 컴포넌트를 return해주는 구조의 함수)

```jsx
// example
const MyComponent = React.memo((props) => {
	return (/*컴포넌트 렌더링 코드*/)}
);
```

- 하나의 컴포넌트가 똑같은 props를 넘겨 받았을 때, 같은 결과를 렌더링 하고 있다면 React.memo를 사용하여 불필요한 컴포넌트 렌더링을 방지 할 수 있다.
- `React.memo`는 props의 변경 여부만을 체크한다. `React.memo`로 감싸진 컴포넌트 내부에서 useState, useReducer, useContext Hook을 사용한다면, 여전히 state나 context가 변할 때 리렌더링 된다.

<br>

#### 🔖 React.memo 적용하기

- TextView를 React.memo로 감싸면 props인 text가 변할 때만 리렌더링 된다.

```jsx
import React, { useState, useEffect } from 'react';

const TextView = React.memo(({ text }) => {
  useEffect(() => {
    console.log(`Update :: text :: ${text}`);
  });
  return <div>{text}</div>;
});

const CountView = React.memo(({ count }) => {
  useEffect(() => {
    console.log(`Update :: count :: ${count}`);
  });
  return <div>{count}</div>;
});

const OptimizeTest = () => {
  const [count, setCount] = useState(1);
  const [text, setText] = useState('');
  return (
    <div style={{ padding: 50 }}>
      <div>
        <h2>count</h2>
        <CountView count={count} />
        <button onClick={() => setCount(count + 1)}>+</button>
      </div>
      <div>
        <h2>text</h2>
        <TextView text={text} />
        <input value={text} onChange={(e) => setText(e.target.value)} />
      </div>
    </div>
  );
};

export default OptimizeTest;
```

- 넘겨받은 props의 변경 여부는 shallow compare로 비교 되므로, object의 경우 같은 값을 참조 하고 있는지를 비교한다.

<br>
<br>

## 💡 useMemo

> 메모이제이션된 '값'을 반환하는 Hook
> 이전 값을 기억해두었다가 조건에 따라 재활용하여 성능을 최적화 하는 용도로 사용된다.

<br>

#### 🔖 useMemo 사용법

```jsx
useMemo(() => fn, deps);
```

- useMemo는 deps 가 변한다면, () => fn이라는 함수를 실행하고, 그 함수의 반환 값을 반환한다. deps는 dependency이며, useMemo가 이 deps라는 것에 '의존'한다는 뜻이다.
- 모든 함수를 useMemo로 감싸게 되면 이 또한 리소스 낭비가 될 수 있으므로, 퍼포먼스 최적화가 필요한 연상량이 많은 곳에 사용하는 것이 좋다.

<br>

#### 🔖 useMemo 예시

```jsx
const memoizedValue = useMemo(() => computeExpensiveValue(a, b), [a, b]);
```

- 인자로 함수와 Dependencies를 넘겨 받는다. 이 때, 2번째 인자로 넘겨준 의존 인자 중에 하나라도 값이 변경되면 1번째 인자의 함수를 재실행한다. 이를 통해 매 렌더링 할때마다 소요되는 불필요한 계산을 피할 수 있다. 만약 Dependencies 인자를 전달하지 않는다면 매번 새롭게 계산하여 return 한다.

<br>
<br>

## 💡 useCallback

> 메모이제이션된 '함수'를 반환하는 Hook
>
> 두 번째 인자로 전달한 deps(의존성 배열) 안에 들어있는 값이 변하지 않으면, 첫 번째 인자로 전달한 콜백함수를 계속 재사용할 수 있도록 도와주는 react hook

<br>

#### 🔖 useCallback 사용법

```jsx
useCallback(fn, deps);
```

- useCallback 은 deps가 변하면, fn이라는 새로운 함수를 반환한다.
- useCallback(fn, deps)은 useMemo(() => fn, deps)와 같다.
  - useCallback은 deps가 변하면 콜백함수가 반환되고,
    useMemo는 deps가 변하면 콜백함수의 값이 반환되므로 useMemo 첫번째인자로 콜백함수에 콜백함수를 넣으면 콜백함수가 반환되어 동일하게 된다.
- useMemo와 마찬가지로 1번째 인자로 함수, 2번째 인자로 Dependencies를 전달한다.
  전달된 의존성 인자가 바뀌지 않으면 이전에 생성한 함수가 재사용 된다.
- 자식 컴포넌트에 함수를 props으로 줄 때는 반드시 useCallback을 사용하여 불필요한 리렌더링을 줄일 것!

<br>

#### 🔖 useCallback 예시

```jsx
// useCallback 기본 구문
const memoizedCallback = useCallback(() => {
  doSomething(a, b);
}, [a, b]);

// 예시 함수
const onCreate = useCallback((author, content, emotion) => {
  const created_date = new Date().getTime();
  const newItem = {
    author,
    content,
    emotion,
    created_date,
    id: dataId.current,
  };
  dataId.current += 1;
  setData((data) => [newItem, ...data]);
}, []);
```

- deps로 빈 배열을 전달해서 App 컴포넌트가 처음 마운트될 때 한 번만 onCreate를 만들고, 그 다음부터는 처음에 만들어놓은 함수를 재사용할 수 있도록 작성함

<br>
<br>

### 📚 Reference

&nbsp; https://reactjs.org/
&nbsp; https://www.inflearn.com/course/%ED%95%9C%EC%9E%85-%EB%A6%AC%EC%95%A1%ED%8A%B8

<br>
<br>
