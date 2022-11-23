# Styled-components

> CSS in JS는 스타일 정의를 CSS 파일이 아닌 JavaScript로 작성된 컴포넌트에 바로 삽입하는 스타일 기법이다.
> 대표적인 CSS-in-JS 라이브러리인 Styled Components를 사용해서 React 컴포넌트를 스타일링하는 방법을 알아보자!

<br>

## 💡 Styled-components를 사용하는 이유

> - 스타일을 자바스크립트 파일에 내장시켜 사용할 수 있다.
> - 재사용이 쉬운 CSS 커스텀 컴포넌트를 만들 수 있다.

- 리액트에서 컴포넌트를 스타일링하는 방식은 다양한데, 그 중 스타일을 자바스크립트 파일에 내장시켜 사용하기 위해 사용한다. 스타일을 작성함과 동시에 해당 스타일이 적용된 컴포넌트를 만들 수 있도록 라이브러리를 제공해준다

<br>
<br>

## 💡 Styled-components 사용 환경 준비

```bash
npm install styled-components
yarn add styled-components
```

> 1. 프로젝트에 styled-components 설치
> 2. import styled from 'styled-components'; 를 추가하기
>    -> styled 객체를 이용할 것!

<br>

<br>
<br>

## 💡 Styled-componets 기본 문법

> - const 컴포넌트명 = styled.태그명스타일 넣기...문법으로 작성한다.
> - 만들고자하는 컴포넌트의 render 함수 밖에서 만든다.

```jsx
const 상수명 = styled.태그명`
    넣을 css 효과들
`;
```

```jsx
const Title = styled.h1`
  font-size: 1.5em;
  text-align: center;
  color: palevioletred;
`;

function App() {
  return <Title>Styled Components</Title>;
}
```

<br>
<br>

## 💡 Styled-componets 활용 방법

#### 🔖 고정 스타일링

```jsx
//App.js
import React from 'react';
import styled from 'styled-components';
import Button from './components/Button';
//Button테그는 재사용가능한 컴포넌트로부터 데려온다

//고정값을 가지고 스타일링 함
const AppBlock = styled.div`
  width: 512px;
  margin: 0 auto;
  margin-top: 4rem;
  border: 1px solid black;
  padding: 1rem;
`;

function App() {
  return (
    <AppBlock>
      <Button>Button</Button>
    </AppBlock>
  );
}

export default App;
```

<br>

#### 🔖 가변 스타일링 (props 사용)

> styled-component를 사용하는 장점 중 하나가 변수에 의해 스타일을 바꿀 수 있다는 점이다.
> 아래 예시를 보면 email이라는 state값에 따라 ExampleWrap에 prop으로 내려준 active라는 값이 true or false로 바뀌게 된다.
> styled-component는 내부적으로 props을 받을 수 있고, 그 props에 따라 스타일을 변경할 수 있다.

```jsx
import React, { useState } from 'react';
import styled from 'styled-components';

function Example() {
  const [email, setEmail] = useState('');

  return (
    <ExampleWrap active={email.length}>
      <Button>Hello</Button>
      <NewButton color="blue">Im new Button</NewButton>
    </ExampleWrap>
  );
}

const ExampleWrap = styled.div`
  background: ${({ active }) => {
    if (active) {
      return 'white';
    }
    return '#eee';
  }};
  color: black;
`;

const Button = styled.button`
  width: 200px;
  padding: 30px;
`;

// Button 컴포넌트 상속
// NewButton 컴포넌트에 color가는 props가 있으면 그 값 사용, 없으면 'red' 사용
const NewButton = styled.Button`
  color: ${(props) => props.color || 'red'};
`;

export default Example;
```

<br>

- 여러 줄의 css코드를 조건부로 넘겨줄 때에는 css를 불러와서 사용해야 한다.
  이때 import styled, { css } from "styled-components"; 를 잊지 말 것!!

```jsx
import React from 'react';
import styled, { css } from 'styled-components';

// div를 스타일링해서 Circle 컴포넌트에 넣음
// Circle 컴포넌트에 color라는 props를 줌
const Circle = styled.div`
  width: 5rem;
  height: 5rem;
  background: ${(props) => props.color || 'black'};
  border-radius: 50%;
  ${(props) =>
    props.huge &&
    css`
      width: 10rem;
      height: 10rem;
    `}
`;
// 여러 줄의 css코드를 조건 식으로 넘김

function App() {
  return <Circle color="blue" huge />;
}

export default App;
```

<br>

#### 🔖 props를 이용해 재사용 가능한 컴포넌트 생성하기

```jsx
// Button.js

import React from 'react';
import styled, { css } from 'styled-components';

// size를 제어
const sizeStyles = css`
  ${(props) =>
    props.size === 'large' &&
    css`
      height: 3rem;
      font-size: 1.25rem;
    `}

  ${(props) =>
    props.size === 'medium' &&
    css`
      height: 2.25rem;
      font-size: 1rem;
    `}

    ${(props) =>
    props.size === 'small' &&
    css`
      height: 1.75rem;
      font-size: 0.875rem;
    `}
`;

/* 공통 스타일 */
const StyleButton = styled.button`
  display: inline-flex;
  outline: none;
  border: none;
  border-radius: 4px;
  color: white;
  font-weight: bold;
  cursor: pointer;
  padding-left: 1rem;
  padding-right: 1rem;

  ${sizeStyles}
`;

function Button({ children, size, ...rest }) {
  return (
    <StyleButton size={size} {...rest}>
      {children}
    </StyleButton>
  );
}

export default Button;
```

```jsx
// App.js
import React from 'react';
import styled from 'styled-components';
import Button from './components/Button';
// Button 태그는 재사용 가능한 컴포넌트로부터 데려온다!

// 고정값을 가지고 스타일링
const AppBlock = styled.div`
  width: 512px;
  margin: 0 auto;
  margin-top: 4rem;
  border: 1px solid black;
  padding: 1rem;
`;

function App() {
  return (
    <AppBlock>
      <Button size="large">Button</Button>
      <Button size="small">Button</Button>
      <Button size="medium">Button</Button>
    </AppBlock>
  );
}

export default App;
```

- 이처럼 props값을 받아서 각각의 props값에 따라 다르게 스타일링 할 수 있다.

<br>

#### 🔖 다른 파일에서 컴포넌트 import

> 해당 파일에서 정의한 css를 export하여 다른 파일에서 import 할 수 있다.

```jsx
// Login.jsx
export const LoginContainer = styled.div`
  background: red;
`;

// Other.jsx
import { LoginContainer } from '.Login';

const Other = () => {
  return <LoginContainer>...</LoginContainer>;
};
```

<br>

#### 🔖 기존 스타일 확장시켜서 활용하기

> 기존에 만든 스타일과 비슷하지만 코드를 추가해 확장한 새로운 스타일을 만들고 싶다면 아래의 방법을 이용할 수 있다.

```jsx
const 확장스타일컴포넌트이름 = styled(상속받을스타일컴포넌트)`추가할 코드 작성`;
```

```jsx
const StyleButton = styled.button`
  /* 공통 스타일 */
  display: inline-flex;
  outline: none;
  border: none;
  border-radius: 4px;
  color: white;
  font-weight: bold;
  cursor: pointer;
  padding-left: 1rem;
  padding-right: 1rem;
`;

//StyleButton값은 자동으로 세팅이 되어 있는 상태에서 새로운 스타일을 추가할 수 있다!
const RedButton = styled(Stylebutton)`
  color: red;
`;
```

<br>
<br>

### 📚 Reference

&nbsp; https://reactjs.org/
&nbsp; https://www.inflearn.com/course/%ED%95%9C%EC%9E%85-%EB%A6%AC%EC%95%A1%ED%8A%B8
&nbsp; https://styled-components.com/

<br>
<br>
