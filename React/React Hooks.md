# React Hooks

<br>

## 💡 Hook 이란?

> Hook은 React 버전 16.8부터 React 요소로 새로 추가되었다. Hook을 이용하여 기존 Class 바탕의 코드를 작성할 필요 없이 상태 값과 여러 React의 기능을 사용할 수 있다.

- **이전 React의 문제점**
  1. 컴포넌트 간의 상태 로직을 재사용하기 어렵다.
  2. 복잡한 컴포넌트들의 이해가 어렵다.
     - render props나 HOC와 같은 패턴을 사용하며 난이도 상승
  3. Class 문법 자체의 어려움
     - Class 함수에서의 this 개념 등등

<br>

- **Hook을 사용하면?**
  1. 컴포넌트 간의 계층을 바꾸지 않고 상태 로직을 재사용할 수 있다.
  2. 하나의 컴포넌트를 생명주기가 아닌 기능을 기반으로 하여 작은 함수 단위로 나뉠 수 있게 해준다.
  3. Class 문법 없이도 React 기능을 사용할 수 있게끔 해준다.

<br>
<br>

## 💡 1. useState()

> useState()는 상태 유지 값과 그 값을 갱신하는 함수를 반환한다.

<br>

#### 🔖 문법

```jsx
const [state, setState] = useState(initialState);
```

> - state : 상태 값 저장 변수
> - setState 상태 값 갱신 함수
> - initialState : 상태 초기 값

<br>

#### 🔖 예제

```jsx
import React, { useState } from 'react';

function FormFunciton() {
  const [email, setEmail] = useState('');

  return (
    <>
      <label htmlFor="email">email:</label>
      <input
        value={email}
        id="email"
        onChange={() => {
          setEmail(e.target.value);
        }}
      />
    </>
  );
}
```

<br>
<br>

## 💡 2. useEffect()

> useEffect()는 컴포넌트가 렌더링 될 때마다 특정 작업을 실행해주는 Hook
> 컴포넌트가 mount / unmount / update 되었을 때 특정 작업을 실행시켜준다.

<br>

#### 🔖 문법

##### 1) mount / update

```jsx
useEffect(callback, dependencyArray);
```

> - callback : 컴포넌트가 렌더링 될 때 실행시킬 함수
> - dependencyArray : 여기는 배열 형태의 인수가 들어가는데, 배열 내의 값이 변경될 때마다 useEffect가 실행하라고 설정하는 것. 예를 들면,
>   - [count] : count의 값이 변경될 때마다 useEffect의 콜백함수가 실행된다.
>   - [ ] : 빈 배열인 경우, useEffect의 콜백함수는 컴포넌트가 렌더링 되는 시점에서 딱 한 번만 실행된다.
>   - 아무 것도 지정하지 않으면? 컴포넌트 렌더링 될 때마다 실행된다.

<br>

##### 2) unmount / update 직전

> dependencyArray의 인수가 빈 배열이라면, unmount 될 때 cleanup 함수가 실행이 되고, 특정 값을 넣어준다면 그 값이 update 될 때에 cleanup 함수를 실행시킬 수 있게 된다.

```jsx
useEffect(() => {
  // ...
  return () => {
    // cleanup...
  };
}, []);
```

<br>

#### 🔖 예제

##### 1. 버튼을 눌러 count의 값에 변화를 줄 때마다 alert창을 띄우게 한다.

```jsx
import React, { useState, useEffect } from 'react';

function CountFunciton() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    alert(`현재 count는 ${count}`);
  }, [count]);

  return (
    <>
      <button
        onClick={() => {
          setCount(count + 1);
        }}
      >
        +
      </button>
      <button
        onClick={() => {
          setCount(count - 1);
        }}
      >
        -
      </button>
    </>
  );
}
```

<br>

##### 2. 컴포넌트가 mount 될 때 "Hello"를 콘솔에 찍어 주고, unmount 될 때 "Bye"를 찍어 준다.

```jsx
useEffect(() => {
  console.log('Hello');
  return () => {
    console.log('Bye');
  };
}, []);
```

<br>
<br>

## 💡 3. useRef()

> useRef()는 .current 프로퍼티로 전달된 인자(initialValue)로 초기화된 변경 가능한 ref 객체를 반환한다. 반환된 객체는 컴포넌트의 전 생애주기를 통해 유지된다.

- 자바스크립트에서 DOM Selctor를 사용하여 특정 엘리먼트를 지정하듯, 리액트는 useRef()를 활용해 DOM에 접근할 수 있다.
- 또한, 컴포넌트 안에서 조회 및 수정할 수 있는 변수 관리의 기능도 한다.
- useRef()는 .current 프로퍼티에 변경 가능한 값을 담고 있는 상자와도 같다.
- useRef()안의 객체는 .current 프로퍼티를 통해 값을 변경하더라도 리렌더링을 유발하지 않으며 리렌더 되더라도 값을 유지한다.
  - useRef() 객체는 리액트 생명주기로부터 독립적이기 때문

<br>

#### 🔖 문법

```jsx
const refContainer = useRef(initialValue);
```

<br>

#### 🔖 예제

```jsx
// 1. DOM Selector
import React, { useRef } from 'react';

export const App = () => {
  const divRef = useRef(null);

  function clickHandler() {
    divRef.current.style.display = 'none'; // div 엘리먼트 클릭시, 사라지게 됨
  }

  return (
    <div>
      <div ref={divRef} onClick={clickHandler}>
        안녕하세요
      </div>
    </div>
  );
};
```

```jsx
// 2. 변수
import React, { useRef } from 'react';

export const App = () => {
  const count = useRef(0);

  function increaseCount() {
    count.current += 1;
    console.log(count.current); // 1, 2, 3 ...
  }

  return (
    <>
      <button onClick={increaseCount}>count</button>
    </>
  );
};
```

<br>
<br>

## 💡 4. useCallback()

> useCallback()은 콜백의 메모이제이션된 버전을 반환한다.
> 그 메모이제이션된 버전은 콜백의 의존성이 변경되었을 때에만 변경된다.
> 이것은, 불필요한 렌더링을 방지하기 위해 (예로 shouldComponentUpdate를 사용하여)
> 참조의 동일성에 의존적인 최적화된 자식 컴포넌트에 콜백을 전달할 때 유용하다.

**※ 메모이제이션(memoization)** : 계산된 값을 자료구조에 저장하고 이후 같은 계산을 반복하지 않고 자료구조에서 꺼내 재사용하는 것

<br>

React의 리렌더링 조건에는 4가지가 있다

- props 변경
- state 변경
- 부모 컴포넌트의 렌더링
- forceUpdate()의 실행

컴포넌트가 리렌더링 될 때마다 컴포넌트 내부에 있는 함수들도 재선언 되어지는데,
useCallback() 이러한 불필요한 재선언을 방지하기 위해 쓰인다.

<br>

#### 🔖 문법

```jsx
const memoizedCallback = useCallback(callback, dependencyArray);
```

- dependencyArray의 역할은 useEffect() 에서 설명한 것과 같다.

<br>

#### 🔖 예제

```jsx
import React, { useState, useCallback } from 'react';

function CountFunciton() {
  const [count, setCount] = useState(0);

  const increment = useCallback(() => {
    setCount(count + 1);
  }, [count]); // count 값이 변경될 때마다 재생성

  return (
    <>
      <button onClick={increment}>+</button>
    </>
  );
}
```

<br>
<br>

## 💡 5. useMemo()

> props가 바뀌지 않으면 리렌더링을 방지하는 Hook
> 컴포넌트에서 리렌더링이 필요한 상황에서만 리렌더링을 하도록 설정할 수 있다.

<br>

#### 🔖 문법

```jsx
const memoizedValue = useMemo(() => computeExpensiveValue(a, b), [a, b]);
```

- 우리가 최적화하고자 하는 함수를 useMemo() 로 감싸주면 된다.
- useEffect처럼 콜백함수, deps[의존성배열] 순으로 작성함
- 이 때 deps에 data.length를 넣어서 data.length가 변화할 때만 콜백함수가 다시 수행된다.
- **주의할 점**
  - is not a function 에러를 가장 많이 접하게 되는데
    useMemo가 결과값을 리턴하면 getDiaryAnalysis는 더이상 함수가 아니라, 결과값을 담은 상수가 되는 것

<br>

#### 🔖 예제

```jsx
const getDiaryAnalysis = useMemo(() => {
  console.log('일기 분석 시작');

  const goodCount = data.filter((it) => it.emotion >= 3).length;
  const badCount = data.length - goodCount;
  const goodRatio = (goodCount / data.length) * 100;
  return { goodCount, badCount, goodRatio };
});

const { goodCount, badCount, goodRatio } = getDiaryAnalysis;
// 결과값 가져올 때 getDiaryAnalysis를 함수로 적지 않도록 주의할 것!
```

<br>
<br>

### 📚 Reference

&nbsp; https://reactjs.org/
&nbsp; https://www.inflearn.com/course/%ED%95%9C%EC%9E%85-%EB%A6%AC%EC%95%A1%ED%8A%B8

<br>
<br>
