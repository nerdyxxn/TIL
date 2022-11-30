# Redux

<img src="https://user-images.githubusercontent.com/66936285/204738576-9ba97895-6269-48f7-8b0d-bbe442cc8e93.png">

<br>

## 💡 Redux 리덕스란?

> 리덕스는 가장 사용률이 높은 상태관리 라이브러리이다.
> 리덕스를 사용하면 우리가 만들게 될 컴포넌트들의 상태 관련 로직들을 다른 파일들로 분리시켜서 더욱 효율적으로 관리 할 수 있다.
> 또한, 컴포넌트끼리 상태를 공유하게 될 때 여러 컴포넌트를 거치지 않고도 손쉽게 상태 값을 전달할 수 있다.
>
> 추가적으로, 리덕스의 미들웨어라는 기능을 통하여 비동기 작업, 로깅 등의 확장적인 작업들을 더욱 쉽게 할 수도 있게 해준다.

<br>
<br>

## 💡 Redux 용어 및 개념

#### 1. 액션(Action)

- 상태에 어떠한 변화가 필요하게 될 때, 우리는 액션이란 것을 발생시킨다. 이는 하나의 객체로 표현되는데 액션 객체는 다음과 같은 형식으로 이루어져 있다.
  ```jsx
  {
    type: 'TOGGLE_VALUE';
  }
  ```
- 액션 객체는 type 필드를 필수적으로 가지고 있어야 하고, 그 외의 값들은 개발자 마음대로 넣어줄 수 있다.
  ```jsx
  {
  type: "ADD_TODO",
  data: {
    id: 0,
    text: "리덕스 배우기"
    }
  }
  ```

<br>

#### 2. 액션 생성함수 (Action Creator)

- 어떤 변화를 일으켜야 할 때마다 액션 객체를 만들어야 하는데 매번 액션 객체를 직접 작성하기 번거로울 수 있고, 만드는 과정에서 실수로 정보를 놓칠 수도 있다. 이러한 일을 방지하기 위해 이를 함수로 만들어서 관리한다.

  ```jsx
  function addTodo(data) {
    return {
      type: 'ADD_TODO',
      data,
    };
  }

  // 화살표 함수로도 만들 수 있음
  const changeInput = (text) => ({
    type: 'CHANGE_INPUT',
    text,
  });
  ```

<br>

#### 3. 리듀서 (Reducer)

- 리듀서(reducer)는 변화를 일으키는 함수
- 액션을 만들어서 발생시키면 리듀서가 현재 상태와 전달받은 액션 객체를 파라미터로 받아온다. 그리고 두 값을 참고하여 새로운 상태를 만들어서 반환해준다.
- 리듀서에서는 상태의 불변성을 유지하면서 데이터에 변화를 일으켜 주어야 한다. 이 작업을 할 때 spread 연산자(...)를 사용하면 편리하다.

  ```jsx
  const initialState = {
  toggle: false,
  counter: 1
  };

  // state가 undefined이면 initialState를 기본값으로 사용
  function reducer(state = initialState, action) {
    // action type에 따라 작업 처리
    switch(action.type) {
        case TOGGLE:
            return {
            // 불변성 유지
            ...state,
            toggle: !state.toggle;
        }
        case INCREMENT:
            return {
            ...state,
            counter: state.counter + 1
        }
        case DECREMENT:
            return {
            ...state,
            counter: state.counter - 1
        }
        default:
            return state;
    }
  ```

- Reducer에서 action.type에 따라 reducer가 실행될 때, state의 값을 변경할 때는 Spread Operator(...) 또는 Object.assign()으로 기존 state를 복사하여 사용해야 하는 이유는 다음과 같다.
- Redux는 reducer를 거친 state가 변경되었는지를 검사하기 위해 state 객체의 주소를 비교한다. state의 복제본을 만들어 반환하면 이전의 state와 다른 주소 값을 가리키기 때문에 state가 변경되었다고 판단한다. 반대로 State를 복제하는 것이 아닌 속성만 수정해서 반환하면 기존의 state와 가리키는 주소 값이 같기 때문에 변경 감지가 되지 않는다.

<br>

#### 4. 스토어 (Store)

- 프로젝트에 리덕스를 적용하기 위해 스토어(store)를 만든다. 한 개의 프로젝트는 단 하나의 스토어만 가질 수 있다.
- 스토어 안에는 현재 애플리케이션 상태와 리듀서가 들어가 있으며, 그 외에도 몇 가지 중요한 내장 함수를 지닌다.

  ```jsx
  import { createStore } from 'redux';

  (...)

  // 파라미터에는 리듀서 함수를 넣어주어야 함
  const store = createStore(reducer);
  ```

<br>

#### 5. 디스패치 (dispatch)

- 디스패치(dispatch)는 스토어의 내장 함수 중 하나로, '액션을 발생시키는 것'이라고 이해하시면 된다.
- 이 함수는 dispatch(action)과 같은 형태로 액션 객체를 파라미터로 넣어서 호출한다. 이 함수가 호출되면 스토어는 리듀서 함수를 실행시켜서 새로운 상태를 만들어준다.

  ```jsx
  import { createStore } from 'redux';

  (...)

  // 파라미터에는 리듀서 함수를 넣어주어야 함
  const store = createStore(reducer);

  button.onclick = () => {
  // dispatch 함수를 사용하여 액션을 스토어에게 전달
  store.dispatch(plus(1));
  }
  ```

<br>
<br>

## 💡 Redux의 3가지 원칙

#### 1. 애플리케이션의 모든 상태(state)는 하나의 저장소(store) 안에 하나의 객체 트리 구조로 저장된다.

- 하나의 저장소(store)가 존재하며, 이 저장소(store)에는 애플리케이션의 모든 상태들이 객체 트리 구조로 저장되어 있다.
  - 서버로부터 가져온 상태는 직렬화(serialized)되거나, 수화되어(hydrated) 전달되며 클라이언트에서 추가적인 코딩 없이도 사용할 수 있다. 하나의 상태 트리만을 가지고 있기 때문에 디버깅에도 용이하다.

<br>

#### 2. 상태(state)는 읽기 전용(read-only)이다.

- 상태(state)는 읽기 전용이다. 상태를 변화시키는 유일한 방법은 무신 일이 벌어지는 지를 묘사하는 액션 객체를 전달하는 방법뿐이다.
- 이를 통해서 뷰(view)나 네트워크 콜백에서 상태를 직접 바꾸지 못한다는 것을 보장 할 수 있다. 모든 상태 변화는 중앙에서 관리되며 모든 액션은 엄격한 순서에 의해 하나하나 실행되기 때문에 신경써 관리해야 할 경쟁 상태는 없다.

<br>

#### 3. 변화는 순수 함수로 작성되어야 한다.

- 변화를 일으키는 리듀서는 그저 이전 상태와 액션을 받아 다음 상태를 반환하는 순수 함수이다.
- 이전 상태를 변경하는 것이 아니라, 새로운 상태 객체를 생성해서 반환해야한다는 사실을 꼭 기억해야 한다.
- **순수 함수란?**
  - 동일한 인자가 주어졌을 때 항상 동일한 결과를 반환해야 하며, 외부의 상태를 변경하지 않는 함수
    즉, 함수 내 변수 외에 외부의 값을 참조, 의존하거나 변경하지 않는 함수

<br>
<br>

### 📚 Reference

&nbsp; https://reactjs.org/
&nbsp; https://www.inflearn.com/course/%ED%95%9C%EC%9E%85-%EB%A6%AC%EC%95%A1%ED%8A%B8
&nbsp; https://velog.io/@velopert/Redux-1-%EC%86%8C%EA%B0%9C-%EB%B0%8F-%EA%B0%9C%EB%85%90%EC%A0%95%EB%A6%AC-zxjlta8ywt
&nbsp; https://redux.js.org/understanding/thinking-in-redux/three-principles

<br>
<br>
