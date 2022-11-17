# Custom Hooks

> login form, validation 등 비슷한 로직이 여러 컴포넌트에서 쓰이는 경우가 자주 발생한다.
> 이 때, 중복되는 로직을 유틸 함수와 같이 Custom Hook을 만들어 중복을 최소화 시킬 수 있다.
>
> **반복되는 로직들을 React Hooks API를 통해 하나의 함수로 분할 & 재사용할 수 있는 Hook이 바로 'Custom Hook' 이다.**
>
> 아래 예시를 통해 Custom Hook을 만드는 방법과 Custom Hook으로 만들기 전, Custom Hook으로 만든 후 코드의 차이에 대해 알아보자!

<br>

## 💡 예시 전제

> input form이 있고, 그 안에 데이터를 넣는 onChange함수가 있다.

<br>
<br>

## 💡 Custom Hook 쓰기 전 로직

> useState()는 상태 유지 값과 그 값을 갱신하는 함수를 반환한다.

<br>

```jsx
const [state, setState] = useState(initialState);
// Login.jsx
import React, { useState, useCallback } from 'react';

// state
const [text, setText] = useState({
  email: '',
  password: '',
});

// func
const onChange = useCallback(
  (e) => {
    const { value, name } = e.target;
    setText({ ...text, [name]: value });
  },
  [text]
);

return (
  <>
    <input id="email" value={text.email} onChange={onChange} />
    <input id="password" value={text.password} onChange={onChange} />
  </>
);
```

- 기본적인 입력 폼에 데이터를 넣는 함수 생성함
- 유사한 상황에서 위와 같은 로직이 계속 반복될 것을 예상할 수 있음
- 중복을 최소화 시키기 위해 대응 방안으로 Custom Hook을 만들고 반영시키기

<br>
<br>

## 💡 Custom Hook 만들기

> - src 폴더 > hooks 폴더 생성 후, Custom Hook 파일을 추가한다.
>   파일명(훅네임)은 통상 use +"키워드" 형태로 설정한다.
> - Hook 내에선, React Hooks API(useState, useEffect, useCallback, useRef 등) 를 사용하여 원하는 기능을 구현하고 컴포넌트에서 사용하고자 하는 값을 반환하면 된다.
> - Rules of Hooks 규칙들을 준수해야 한다.

<br>

#### 🔖 Rules of Hooks

> 위에서 언급했듯, React Hooks 의 사용 및 커스텀에 있어 몇 가지 규칙이 존재한다. 공식문서 소스를 참고해보자.

<br>

#### 1. 최상위(at the Top Level)에서만 Hook을 호출해야 합니다.

반복문, 조건문 혹은 중첩된 함수 내에서 Hook을 호출하지 마세요. 대신 early return이 실행되기 전에 항상 React 함수의 최상위(at the top level)에서 Hook을 호출해야 합니다.
이 규칙을 따르면 컴포넌트가 렌더링 될 때마다 항상 동일한 순서로 Hook이 호출되는 것이 보장됩니다. 이러한 점은 React가 useState 와 useEffect 가 여러 번 호출되는 중에도 Hook의 상태를 올바르게 유지할 수 있도록 해줍니다.

<br>

#### 2. 오직 React 함수 내에서 Hook을 호출해야 합니다.

Hook을 일반적인 JavaScript 함수에서 호출하지 마세요. 대신 아래와 같이 호출할 수 있습니다.

- ✅ React 함수 컴포넌트에서 Hook을 호출하세요.

- ✅ Custom Hook에서 Hook을 호출하세요.

출처 : React 공식문서 (ko.reactjs.org/docs/hooks-rules.html)

<br>

#### 🔖 Custom Hook 만들기

> 입력 폼의 데이터를 핸들링하기 위한 Custom Hook인 useInput 파일 생성

```jsx
// useInput
import { useState, useCallback } from 'react';

export default (initalValue = null) => {
  // state 정의
  const [data, setData] = useState(initalValue);

  // 함수 정의
  const handler = useCallback(
    (e) => {
      const { value, name } = e.target;
      setData({
        ...data,
        [name]: value,
      });
    },
    [data]
  );
  return [data, handler];
};
```

<br>

#### 🔖 Custom Hook 적용하기

```jsx
// Login.jsx
import React from 'react';
import useInput from 'useInput';

// state
const [text, setText] = useInput({
  email: '',
  password: '',
});

return (
  <>
    <input id="email" value={text.email} onChange={setText} />
    <input id="password" value={text.password} onChange={setText} />
  </>
);
```

- useInput 커스텀 훅 안에 useState, useCallback에 있는 로직을 미리 정의했기 때문에, 컴포넌트에서는 커스텀 훅을 사용하기만 하면 된다.

- 커스텀 훅을 활용해서 코드양도 적어지고, 다른 컴포넌트에서도 재사용 가능하기 때문에 동일한 로직을 수행하는 컴포넌트가 많을 경우 커스텀 훅을 더욱 유용히 사용할 수 있다.

<br>
<br>

### 📚 Reference

&nbsp; ko.reactjs.org/docs/hooks-custom.html  
&nbsp; https://www.inflearn.com/course/%ED%95%9C%EC%9E%85-%EB%A6%AC%EC%95%A1%ED%8A%B8
&nbsp; react.vlpt.us/basic/21-custom-hook.html  
&nbsp; medium.com/finda-tech/%ED%95%80%EB%8B%A4%EC%97%90%EC%84%9C-%EC%93%B0%EB%8A%94-react-custom-hooks-1a732ce949a5  
&nbsp; velog.io/@choidy180/React-Hook-1-useInput

<br>
<br>
