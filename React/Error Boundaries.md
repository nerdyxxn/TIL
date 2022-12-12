# Error Boundaries

> 자바스립트의 에러가 React의 에러까지 이어지면서 애플리케이션이 정상적으로 동작하지 않게 되었다. 이렇게 자바스크립트 에러가 전체 애플리케이션을 중단시키면 안 되기에 Error Boundaries 라는 개념을 도입했다.

<br>

## 💡 Error Boundaries란?

> Error Boundaries 하위 컴포넌트 어디에서든 자바스크립트 에러를 기록하며 이렇게 에러가난 컴포넌트 대신 폴백 UI를 보여주는 React 컴포넌트이다.
> **즉, 에러가 발생한 컴포넌트 대신 들어가는 컴포넌트**

<br>

#### 🔖 Error Boundaries는 4가지의 경우 포착하지 않는다.

1. 이벤트 핸들러
2. 비동기적 코드
3. 서버 사이드 렌더링
4. error boudary 자체에서 에러

<br>
<br>

## 💡 Error Boundaries 사용방법

> `getDeribedStateFromError()` 와 `ComponentDidCatch()` 중 하나를 정의하면 해당 클래스 컴포넌트 자체가 error Boundaries가 된다.

<br>

#### 🔖 static getDerivedStateFromError()

> 하위 자손 컴포넌트에서 오류가 발생했을 때 호출된다. 이 메서드는 매개변수로 에러를 전달받고, 에러가 났는지 확인하는 state값을 반드시 반환해야한 다.

```jsx
class ErrorBoundary extends React.Component {
  constructor(props) {
    super(props);
    this.state = { hasError: false };
  }

  static getDerivedStateFromError(error) {
    // state를 갱신하여 다음 렌더링에서 대체 UI를 표시합니다.
    return { hasError: true };
  }

  render() {
    if (this.state.hasError) {
      // 별도로 작성한 대체 UI를 렌더링할 수도 있습니다.
      return <h1>Something went wrong.</h1>;
    }

    return this.props.children;
  }
}
```

<br>

#### 🔖 componentDidCatch()

> 자손 컴포넌트에서 에러가 발생했을때 호출되며, 2개의 매개변수를 전달받는다.

1. error 발생한 오류
2. info 어떤 컴포넌트가 오류를 발생했는지에 대한 정보

<br>

컴포넌트 생명주기중 'commit' 단계에서 호출되므로 DOM 트리가 이미 다 작성된 이후이므로 side Effect를 발생시켜도 된다. 에러 로그 기록등을 위해 사용된다.

```jsx
class ErrorBoundary extends React.Component {
  constructor(props) {
    super(props);
    this.state = { hasError: false };
  }

  static getDerivedStateFromError(error) {
    // state를 갱신하여 다음 렌더링에서 대체 UI를 표시합니다.
    return { hasError: true };
  }

  componentDidCatch(error, info) {
    // Example "componentStack":
    //   in ComponentThatThrows (created by App)
    //   in ErrorBoundary (created by App)
    //   in div (created by App)
    //   in App
    logComponentStackToMyService(info.componentStack);
  }

  render() {
    if (this.state.hasError) {
      // 별도로 작성한 대체 UI를 렌더링할 수도 있습니다.
      return <h1>Something went wrong.</h1>;
    }

    return this.props.children;
  }
}
```

<br>

#### 🔖 정리

- `getDerivedStateFromError`는 에러가 났는지에 대한 state값을 관리 하여 UI 렌더링
- `ComponentDidCatch` 는 에러 기록 및 에러가 났는지에 대한 state값을 관리 가능
- 에러 경계는 트리 내에서 하위에 존재하는 컴포넌트의 에러만을 포착
- react.docs에는 다음과 같은 구문이 있다.

  > Use static getDerivedStateFromError() to render a fallback UI after an error has been thrown. Use componentDidCatch() to log error information.

  - 따라서 에러 state를 관리할 땐 `getDerivedStateFromError` 사용
  - error infromation을 기록할땐 `ComponentDidCatch` 사용

<br>
<br>

### 📚 Reference

&nbsp; https://ko.reactjs.org/docs/react-component.html#static-getderivedstatefromerror
&nbsp; https://ko.reactjs.org/docs/error-boundaries.html
&nbsp; https://stackoverflow.com/questions/52962851/whats-the-difference-between-getderivedstatefromerror-and-componentdidcatch
&nbsp; https://stackoverflow.com/questions/1784664/what-is-the-difference-between-declarative-and-imperative-paradigm-in-programmin

<br>
<br>
