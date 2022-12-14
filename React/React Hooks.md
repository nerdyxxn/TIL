# React Hooks

<br>

## π‘ Hook μ΄λ?

> Hookμ React λ²μ  16.8λΆν° React μμλ‘ μλ‘ μΆκ°λμλ€. Hookμ μ΄μ©νμ¬ κΈ°μ‘΄ Class λ°νμ μ½λλ₯Ό μμ±ν  νμ μμ΄ μν κ°κ³Ό μ¬λ¬ Reactμ κΈ°λ₯μ μ¬μ©ν  μ μλ€.

- **μ΄μ  Reactμ λ¬Έμ μ **
  1. μ»΄ν¬λνΈ κ°μ μν λ‘μ§μ μ¬μ¬μ©νκΈ° μ΄λ ΅λ€.
  2. λ³΅μ‘ν μ»΄ν¬λνΈλ€μ μ΄ν΄κ° μ΄λ ΅λ€.
     - render propsλ HOCμ κ°μ ν¨ν΄μ μ¬μ©νλ©° λμ΄λ μμΉ
  3. Class λ¬Έλ² μμ²΄μ μ΄λ €μ
     - Class ν¨μμμμ this κ°λ λ±λ±

<br>

- **Hookμ μ¬μ©νλ©΄?**
  1. μ»΄ν¬λνΈ κ°μ κ³μΈ΅μ λ°κΎΈμ§ μκ³  μν λ‘μ§μ μ¬μ¬μ©ν  μ μλ€.
  2. νλμ μ»΄ν¬λνΈλ₯Ό μλͺμ£ΌκΈ°κ° μλ κΈ°λ₯μ κΈ°λ°μΌλ‘ νμ¬ μμ ν¨μ λ¨μλ‘ λλ  μ μκ² ν΄μ€λ€.
  3. Class λ¬Έλ² μμ΄λ React κΈ°λ₯μ μ¬μ©ν  μ μκ²λ ν΄μ€λ€.

<br>
<br>

## π‘ 1. useState()

> useState()λ μν μ μ§ κ°κ³Ό κ·Έ κ°μ κ°±μ νλ ν¨μλ₯Ό λ°ννλ€.

<br>

#### π λ¬Έλ²

```jsx
const [state, setState] = useState(initialState);
```

> - state : μν κ° μ μ₯ λ³μ
> - setState μν κ° κ°±μ  ν¨μ
> - initialState : μν μ΄κΈ° κ°

<br>

#### π μμ 

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

## π‘ 2. useEffect()

> useEffect()λ μ»΄ν¬λνΈκ° λ λλ§ λ  λλ§λ€ νΉμ  μμμ μ€νν΄μ£Όλ Hook
> μ»΄ν¬λνΈκ° mount / unmount / update λμμ λ νΉμ  μμμ μ€νμμΌμ€λ€.

<br>

#### π λ¬Έλ²

##### 1) mount / update

```jsx
useEffect(callback, dependencyArray);
```

> - callback : μ»΄ν¬λνΈκ° λ λλ§ λ  λ μ€νμν¬ ν¨μ
> - dependencyArray : μ¬κΈ°λ λ°°μ΄ ννμ μΈμκ° λ€μ΄κ°λλ°, λ°°μ΄ λ΄μ κ°μ΄ λ³κ²½λ  λλ§λ€ useEffectκ° μ€ννλΌκ³  μ€μ νλ κ². μλ₯Ό λ€λ©΄,
>   - [count] : countμ κ°μ΄ λ³κ²½λ  λλ§λ€ useEffectμ μ½λ°±ν¨μκ° μ€νλλ€.
>   - [ ] : λΉ λ°°μ΄μΈ κ²½μ°, useEffectμ μ½λ°±ν¨μλ μ»΄ν¬λνΈκ° λ λλ§ λλ μμ μμ λ± ν λ²λ§ μ€νλλ€.
>   - μλ¬΄ κ²λ μ§μ νμ§ μμΌλ©΄? μ»΄ν¬λνΈ λ λλ§ λ  λλ§λ€ μ€νλλ€.

<br>

##### 2) unmount / update μ§μ 

> dependencyArrayμ μΈμκ° λΉ λ°°μ΄μ΄λΌλ©΄, unmount λ  λ cleanup ν¨μκ° μ€νμ΄ λκ³ , νΉμ  κ°μ λ£μ΄μ€λ€λ©΄ κ·Έ κ°μ΄ update λ  λμ cleanup ν¨μλ₯Ό μ€νμν¬ μ μκ² λλ€.

```jsx
useEffect(() => {
  // ...
  return () => {
    // cleanup...
  };
}, []);
```

<br>

#### π μμ 

##### 1. λ²νΌμ λλ¬ countμ κ°μ λ³νλ₯Ό μ€ λλ§λ€ alertμ°½μ λμ°κ² νλ€.

```jsx
import React, { useState, useEffect } from 'react';

function CountFunciton() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    alert(`νμ¬ countλ ${count}`);
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

##### 2. μ»΄ν¬λνΈκ° mount λ  λ "Hello"λ₯Ό μ½μμ μ°μ΄ μ£Όκ³ , unmount λ  λ "Bye"λ₯Ό μ°μ΄ μ€λ€.

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

## π‘ 3. useRef()

> useRef()λ .current νλ‘νΌν°λ‘ μ λ¬λ μΈμ(initialValue)λ‘ μ΄κΈ°νλ λ³κ²½ κ°λ₯ν ref κ°μ²΄λ₯Ό λ°ννλ€. λ°νλ κ°μ²΄λ μ»΄ν¬λνΈμ μ  μμ μ£ΌκΈ°λ₯Ό ν΅ν΄ μ μ§λλ€.

- μλ°μ€ν¬λ¦½νΈμμ DOM Selctorλ₯Ό μ¬μ©νμ¬ νΉμ  μλ¦¬λ¨ΌνΈλ₯Ό μ§μ νλ―, λ¦¬μ‘νΈλ useRef()λ₯Ό νμ©ν΄ DOMμ μ κ·Όν  μ μλ€.
- λν, μ»΄ν¬λνΈ μμμ μ‘°ν λ° μμ ν  μ μλ λ³μ κ΄λ¦¬μ κΈ°λ₯λ νλ€.
- useRef()λ .current νλ‘νΌν°μ λ³κ²½ κ°λ₯ν κ°μ λ΄κ³  μλ μμμλ κ°λ€.
- useRef()μμ κ°μ²΄λ .current νλ‘νΌν°λ₯Ό ν΅ν΄ κ°μ λ³κ²½νλλΌλ λ¦¬λ λλ§μ μ λ°νμ§ μμΌλ©° λ¦¬λ λ λλλΌλ κ°μ μ μ§νλ€.
  - useRef() κ°μ²΄λ λ¦¬μ‘νΈ μλͺμ£ΌκΈ°λ‘λΆν° λλ¦½μ μ΄κΈ° λλ¬Έ

<br>

#### π λ¬Έλ²

```jsx
const refContainer = useRef(initialValue);
```

<br>

#### π μμ 

```jsx
// 1. DOM Selector
import React, { useRef } from 'react';

export const App = () => {
  const divRef = useRef(null);

  function clickHandler() {
    divRef.current.style.display = 'none'; // div μλ¦¬λ¨ΌνΈ ν΄λ¦­μ, μ¬λΌμ§κ² λ¨
  }

  return (
    <div>
      <div ref={divRef} onClick={clickHandler}>
        μλνμΈμ
      </div>
    </div>
  );
};
```

```jsx
// 2. λ³μ
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

## π‘ 4. useCallback()

> useCallback()μ μ½λ°±μ λ©λͺ¨μ΄μ μ΄μλ λ²μ μ λ°ννλ€.
> κ·Έ λ©λͺ¨μ΄μ μ΄μλ λ²μ μ μ½λ°±μ μμ‘΄μ±μ΄ λ³κ²½λμμ λμλ§ λ³κ²½λλ€.
> μ΄κ²μ, λΆνμν λ λλ§μ λ°©μ§νκΈ° μν΄ (μλ‘ shouldComponentUpdateλ₯Ό μ¬μ©νμ¬)
> μ°Έμ‘°μ λμΌμ±μ μμ‘΄μ μΈ μ΅μ νλ μμ μ»΄ν¬λνΈμ μ½λ°±μ μ λ¬ν  λ μ μ©νλ€.

**β» λ©λͺ¨μ΄μ μ΄μ(memoization)** : κ³μ°λ κ°μ μλ£κ΅¬μ‘°μ μ μ₯νκ³  μ΄ν κ°μ κ³μ°μ λ°λ³΅νμ§ μκ³  μλ£κ΅¬μ‘°μμ κΊΌλ΄ μ¬μ¬μ©νλ κ²

<br>

Reactμ λ¦¬λ λλ§ μ‘°κ±΄μλ 4κ°μ§κ° μλ€

- props λ³κ²½
- state λ³κ²½
- λΆλͺ¨ μ»΄ν¬λνΈμ λ λλ§
- forceUpdate()μ μ€ν

μ»΄ν¬λνΈκ° λ¦¬λ λλ§ λ  λλ§λ€ μ»΄ν¬λνΈ λ΄λΆμ μλ ν¨μλ€λ μ¬μ μΈ λμ΄μ§λλ°,
useCallback() μ΄λ¬ν λΆνμν μ¬μ μΈμ λ°©μ§νκΈ° μν΄ μ°μΈλ€.

<br>

#### π λ¬Έλ²

```jsx
const memoizedCallback = useCallback(callback, dependencyArray);
```

- dependencyArrayμ μ­ν μ useEffect() μμ μ€λͺν κ²κ³Ό κ°λ€.

<br>

#### π μμ 

```jsx
import React, { useState, useCallback } from 'react';

function CountFunciton() {
  const [count, setCount] = useState(0);

  const increment = useCallback(() => {
    setCount(count + 1);
  }, [count]); // count κ°μ΄ λ³κ²½λ  λλ§λ€ μ¬μμ±

  return (
    <>
      <button onClick={increment}>+</button>
    </>
  );
}
```

<br>
<br>

## π‘ 5. useMemo()

> propsκ° λ°λμ§ μμΌλ©΄ λ¦¬λ λλ§μ λ°©μ§νλ Hook
> μ»΄ν¬λνΈμμ λ¦¬λ λλ§μ΄ νμν μν©μμλ§ λ¦¬λ λλ§μ νλλ‘ μ€μ ν  μ μλ€.

<br>

#### π λ¬Έλ²

```jsx
const memoizedValue = useMemo(() => computeExpensiveValue(a, b), [a, b]);
```

- μ°λ¦¬κ° μ΅μ ννκ³ μ νλ ν¨μλ₯Ό useMemo() λ‘ κ°μΈμ£Όλ©΄ λλ€.
- useEffectμ²λΌ μ½λ°±ν¨μ, deps[μμ‘΄μ±λ°°μ΄] μμΌλ‘ μμ±ν¨
- μ΄ λ depsμ data.lengthλ₯Ό λ£μ΄μ data.lengthκ° λ³νν  λλ§ μ½λ°±ν¨μκ° λ€μ μνλλ€.
- **μ£Όμν  μ **
  - is not a function μλ¬λ₯Ό κ°μ₯ λ§μ΄ μ νκ² λλλ°
    useMemoκ° κ²°κ³Όκ°μ λ¦¬ν΄νλ©΄ getDiaryAnalysisλ λμ΄μ ν¨μκ° μλλΌ, κ²°κ³Όκ°μ λ΄μ μμκ° λλ κ²

<br>

#### π μμ 

```jsx
const getDiaryAnalysis = useMemo(() => {
  console.log('μΌκΈ° λΆμ μμ');

  const goodCount = data.filter((it) => it.emotion >= 3).length;
  const badCount = data.length - goodCount;
  const goodRatio = (goodCount / data.length) * 100;
  return { goodCount, badCount, goodRatio };
});

const { goodCount, badCount, goodRatio } = getDiaryAnalysis;
// κ²°κ³Όκ° κ°μ Έμ¬ λ getDiaryAnalysisλ₯Ό ν¨μλ‘ μ μ§ μλλ‘ μ£Όμν  κ²!
```

<br>
<br>

### π Reference

&nbsp; https://reactjs.org/
&nbsp; https://www.inflearn.com/course/%ED%95%9C%EC%9E%85-%EB%A6%AC%EC%95%A1%ED%8A%B8

<br>
<br>
