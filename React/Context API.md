# Context API

> 하위 컴포넌트들이 부모의 값을 사용 가능하게 하는 react 내장 문법

<br>

## 💡 Context 란?

> Context는 리액트 컴포넌트간에 어떠한 값을 공유할수 있게 해주는 기능이다.
> 주로 Context는 전역적(global)으로 필요한 값을 다룰 때 사용하는데, 꼭 전역적일 필요는 없다. Context를 단순히 "리액트 컴포넌트에서 Props가 아닌 또 다른 방식으로 컴포넌트간에 값을 전달하는 방법이다" 라고 접근을 하는 것이 좋다.

<br>

#### 🔖 Props로만 데이터를 전달하면 발생할 수 있는 문제

- 리액트 애플리케이션에서는 일반적으로 컴포넌트에게 데이터를 전달해야 할 때 Props를 통해 전달한다.
- 그런데 깊숙히 위치한 컴포넌트에 데이터를 전달해야 하는 경우에는 여러 컴포넌트를 거쳐 연달아서 Props를 설정해주어야 하기 때문에 그 과정이 불편하고 실수할 가능성이 높아진다.

```jsx
function App() {
  return <GrandParent value="Hello World!" />;
}

function GrandParent({ value }) {
  return <Parent value={value} />;
}

function Parent({ value }) {
  return <Child value={value} />;
}

function Child({ value }) {
  return <GrandChild value={value} />;
}

function GrandChild({ value }) {
  return <Message value={value} />;
}

function Message({ value }) {
  return <div>Received: {value}</div>;
}
```

- 이러한 코드를 Props Drilling 이라고 부른다. 컴포넌트를 한 두개정도 거쳐서 Props를 전달하는거라면 괜찮지만 이렇게 4개정도를 거쳐서 전달하게 된다면 너무 불편하고 비효율적이다.
- 예를 들어서 Message 컴포넌트를 열어서, 이 value 값이 어디서 오는건지 파악하려고 한다면 그 상위 컴포넌트로 타고 또 타고 거슬러 올라가야 하기 때문에 매우 불편하다.
- 또는, value 라는 네이밍을 message 로 변경을 하고 싶어진다면, 통일성을 맞추기 위해서 또 여러 컴포넌트들을 수정해야 하니까 그것도 그것대로 불편하다.
- 이러한 문제들은 Context API를 사용하면 깔끔하게 해결할 수 있다.

<br>
<br>

## 💡 Context 사용법

> 1. React.createContext() 함수로 범위 생성
> 2. 같은 값을 공유할 HTML을 범위로 감싸고, value = { 공유원하는state } 집어넣기
> 3. 해당 컴포넌트 내에서 useContext(범위이름) 훅을 이용해 공유된 값 사용하기

- Context 는 리액트 패키지에서 createContext 라는 함수를 불러와서 만들 수 있다.
- Context 객체 안에는 Provider라는 컴포넌트가 들어있다. 컴포넌트 간에 공유하고자 하는 값을 value 라는 Props로 설정하면 자식 컴포넌트들에서 해당 값에 바로 접근을 할 수 있다.

```jsx
import { createContext } from 'react';
const MyContext = createContext();
```

```jsx
function App() {
  return (
    <MyContext.Provider value="Hello World">
      <GrandParent />
    </MyContext.Provider>
  );
}
```

- 이렇게 하면, 원하는 컴포넌트에서 useContext 라는 Hook을 사용하여 Context에 넣은 값에 바로 접근할 수 있다. 해당 Hook의 인자에는 createContext로 만든 MyContext를 넣는다.

```jsx
import { createContext, useContext } from 'react';

function Message() {
  const value = useContext(MyContext);
  return <div>Received: {value}</div>;
}
```

<br>
<br>

## 💡 Context 에서 상태 관리가 필요한 경우

```jsx
import { createContext } from 'react';

const CounterContext = createContext();

function CounterProvider({ children }) {
  return <CounterContext.Provider>{children}</CounterContext.Provider>;
}

function App() {
  return (
    <CounterProvider>
      <div>
        <Value />
        <Buttons />
      </div>
    </CounterProvider>
  );
}

// (...)
```

- Context 에서 유동적인 값을 관리하는 경우엔 Provider를 새로 만들어주는 것이 좋다.
- 위와 같이 children Props를 받아와서 CounterContext.Provider 태그 사이에 넣어주면 된다. 그 다음에 필요한 기능들을 CounterProvider 컴포넌트 안에서 구현하면 된다.

```jsx
import { createContext, useState } from 'react';

const CounterContext = createContext();

function CounterProvider({ children }) {
  const counterState = useState(1);
  return <CounterContext.Provider value={counterState}>{children}</CounterContext.Provider>;
}

// (...)
```

```jsx
import { createContext, useContext, useState } from 'react';

// (...)

function useCounterState() {
  const value = useContext(CounterContext);
  if (value === undefined) {
    throw new Error('useCounterState should be used within CounterProvider');
  }
  return value;
}
```

```jsx
// (...)

function Value() {
  const [counter] = useCounterState();
  return <h1>{counter}</h1>;
}
function Buttons() {
  const [, setCounter] = useCounterState();
  const increase = () => setCounter((prev) => prev + 1);
  const decrease = () => setCounter((prev) => prev - 1);

  return (
    <div>
      <button onClick={increase}>+</button>
      <button onClick={decrease}>-</button>
    </div>
  );
}

export default App;
```

- 지금과 같이 하나의 상태만 있는 경우라면, useState를 사용하여 만들어진 값과 함수가 들어있는 배열을 통째로 value 로 넣는다.
- 위와 같이 useCounterState 라는 커스텀 Hook을 만들면, CounterProvider 의 자식 컴포넌트 어디서든지 useCoutnerState 를 사용하여 값을 조회하거나 변경할 수 있다.

<br>
<br>

## 💡 값과 업데이트 함수를 두개의 Context로 분리하기

- Context에서 관리하는 상태가 빈번하게 업데이트 되지 않는다면 방금 작성한 코드만으로도 충분하다. 하지만 상태가 빈번하게 업데이트 된다면 성능적으로 좋지 않다. 실제로 변화가 반영되는 곳은 Value 컴포넌트뿐인데, Buttons 컴포넌트도 리렌더링되기 때문이다.
- value를 만드는 과정에서 useMemo로 감싸주었긴 하지만, 어쨌든 counter가 바뀔 때 마다 새로운 배열을 만들어서 반환하고 있고 useContext에선 이를 감지하여 리렌더링을 하기 때문임.
- 이를 고치는 방법은 간단하다. Context를 하나 더 만들어서 분리하기!

```jsx
import { createContext, useContext, useMemo, useState } from 'react';

const CounterValueContext = createContext();
const CounterActionsContext = createContext();

function CounterProvider({ children }) {
  const [counter, setCounter] = useState(1);
  const actions = useMemo(
    () => ({
      increase() {
        setCounter((prev) => prev + 1);
      },
      decrease() {
        setCounter((prev) => prev - 1);
      },
    }),
    []
  );

  return (
    <CounterActionsContext.Provider value={actions}>
      <CounterValueContext.Provider value={counter}>{children}</CounterValueContext.Provider>
    </CounterActionsContext.Provider>
  );
}

function useCounterValue() {
  const value = useContext(CounterValueContext);
  if (value === undefined) {
    throw new Error('useCounterValue should be used within CounterProvider');
  }
  return value;
}

function useCounterActions() {
  const value = useContext(CounterActionsContext);
  if (value === undefined) {
    throw new Error('useCounterActions should be used within CounterProvider');
  }
  return value;
}

function App() {
  return (
    <CounterProvider>
      <div>
        <Value />
        <Buttons />
      </div>
    </CounterProvider>
  );
}

function Value() {
  console.log('Value');
  const counter = useCounterValue();
  return <h1>{counter}</h1>;
}
function Buttons() {
  console.log('Buttons');
  const actions = useCounterActions();

  return (
    <div>
      <button onClick={actions.increase}>+</button>
      <button onClick={actions.decrease}>-</button>
    </div>
  );
}

export default App;
```

- 기존의 CounterContext 를 CounterValueContext와 CounterActionsContext로 분리해준다.
- 두 Provider를 모두 사용하면서 커스텀 Hook 또한 두 개로 분리한다.
- 이제 버튼을 눌러서 상태에 변화가 일어날 때, Value 컴포넌트에서만 리렌더링이 발생한다.

<br>
<br>

### 📚 Reference

&nbsp; https://reactjs.org/
&nbsp; https://www.inflearn.com/course/%ED%95%9C%EC%9E%85-%EB%A6%AC%EC%95%A1%ED%8A%B8
&nbsp; https://velog.io/@velopert/react-context-tutorial#context-%EB%9E%80

<br>
<br>
