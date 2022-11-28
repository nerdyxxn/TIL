# useReducer - 복잡한 상태 관리 로직 분리하기

> 리액트의 컴포넌트에서 상태를 업데이트 하기 위해서는 useState를 사용해서 상태(state)를 관리했다.
> useState 말고도 상태를 관리할 수 있는 방법이 있는데 그게 바로 useReducer이다.

<br>

## 💡 useState와 useReducer의 차이?

> useReducer를 사용하면 컴포넌트 상태 업데이트 로직을 컴포넌트에서 분리시킬 수 있다.
> 상태 업데이트 로직을 컴포넌트 바깥에 작성할 수 있을 뿐만 아니라 심지어는 아예 다른 파일에 작성한 후 불러와서 사용할 수도 있다.

<br>
<br>

## 💡 useReducer 기본 문법

```jsx
const [state, dispatch] = useReducer(reducer, initialState);
```

- state : 우리가 앞으로 컴포넌트에서 사용할 수 있는 상태를 가리킴

- dispatch : 액션을 발생시키는 함수, dispatch는 dispatch({type : 'INCREMENT' }) 이런 식으로 사용함

- useReducer의 첫 번째 파라미터 : reducer 함수

- useReducer의 두 번째 파라미터 : state의 초기 값

```jsx
const reducer = (state, action) => {
  switch (action.type) {
    case 'INCREMENT':
      return state + 1;
    case 'DECREMENT':
      return state - 1;
    default:
      return state;
  }
};
```

<br>
<br>

## 💡 useReducer를 사용해 컴포넌트에서 복잡한 상태 관리 로직을 분리하기

- 가장 복합하고 많은 상태 변화 로직을 가진 **App 컴포넌트**
- onCreate, onEdit, onRemove 등 이와 같은 상태 변화 함수들은 컴포넌트 내에만 존재했어야 함
- 상태를 업데이트 하기 위해서 기존 상태를 참조해야하기 때문!
  but, 컴포넌트 코드가 복잡해지고 무거워지는 것은 좋은 현상이 아님
  <img src="https://user-images.githubusercontent.com/66936285/204231528-7f9dadc2-b61d-41ac-b729-8b91bf889bce.png">

<br>

#### 🔖 상태 변화 로직

<img src="https://user-images.githubusercontent.com/66936285/204231541-592132d6-277e-4be0-91f4-10562a3680ba.png">

- dispatch 함수를 호출하면서 Action 개체를 전달 { type : ? } (상태변화 객체)
- 상태변화에 대한 처리는 reducer가 수행함
- reducer 함수는 첫번째 인자로 최신의 state를 받고 두번째 인자로는 dispatch를 호출할 때 전달해줬던 Action 객체를 전달받음
- dispatch는 함수형 업데이트 같은 거 필요없이 호출하면 **현재 state를 reducer 함수가 알아서 참조함**
  - 따라서 useCallback 사용하면서 의존성 배열과 함수형 업데이트 신경 안 써도 된다.

<br>

#### 🔖 소스 코드 적용하기

1. App 컴포넌트에서 기존에 작성했었던 useState를 주석처리 → useReducer로 만들어야 함

- **기존 코드**

  ```jsx
  /* eslint-disable */
  import { useCallback, useEffect, useMemo, useRef, useState } from 'react';
  import axios from 'axios';
  import './App.css';
  import DiaryEditor from './DiaryEditor';
  import DiaryList from './DiaryList';

  function App() {
    // 1. 일기 데이터를 관리할 state 생성
    const [data, setData] = useState([]);
    // 2. onCreate 함수 생성 -> 데이터 추가 기능 구현
    // id는 useRef를 활용해 현재값 current + 1 형태로 구현
    const dataId = useRef(0);

    // const getData = async () => {
    //   const res = await fetch(
    //     "https://jsonplaceholder.typicode.com/comments"
    //   ).then(res => res.json());
    //   console.log(res);
    // };
    const getData = () => {
      axios
        .get('https://jsonplaceholder.typicode.com/comments')
        .then((res) => {
          //결과값 : res.data
          const initData = res.data.slice(0, 20).map((it) => {
            return {
              author: it.email,
              content: it.body,
              emotion: Math.floor(Math.random() * 5) + 1,
              created_date: new Date().getTime(),
              id: dataId.current++,
            };
          });
          setData(initData);
        })
        .catch(() => {
          console.log('데이터 호출 실패!');
        });
    };

    useEffect(() => {
      getData();
    }, []);

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

    const onRemove = useCallback((targetId) => {
      setData((data) => data.filter((it) => it.id !== targetId));
    }, []);

    const onEdit = useCallback((targetId, newContent) => {
      setData((data) =>
        data.map((list) => (list.id === targetId ? { ...list, content: newContent } : list))
      );
    }, []);

    const getDiaryAnalysis = useMemo(() => {
      const goodCount = data.filter((it) => it.emotion >= 3).length;
      const badCount = data.length - goodCount;
      const goodRatio = (goodCount / data.length) * 100;
      return { goodCount, badCount, goodRatio };
    }, [data.length]);

    const { goodCount, badCount, goodRatio } = getDiaryAnalysis;

    // 3. onCreate() 함수를 DiaryList에 props으로 전달
    return (
      <div className="App">
        <DiaryEditor onCreate={onCreate} />
        <div>전체 일기 : {data.length}</div>
        <div>기분 좋은 일기 개수 : {goodCount}</div>
        <div>기분 나쁜 일기 개수 : {badCount}</div>
        <div>기분 좋은 일기 비율 : {goodRatio}</div>
        <DiaryList onEdit={onEdit} onRemove={onRemove} diaryList={data} />
      </div>
    );
  }

  export default App;
  ```

<br>

2. App 컴포넌트 상단에(밖에서) 상태변화를 처리할 함수인 reducer를 정의
3. 이제 switch문을 쓰는데 상태변화 일으킬 case를 생각해보자 → setData 썼던 부분 전부 확인
   - INIT : getData (API의 데이터 가지고와서 한 번에 넣는)
   - CREATE : onCreate (기존의 created_date는 reducer에서 만들어줄거야)
   - REMOVE : onRemove
   - EDIT : onEdit
4. dispatch는 함수형 업데이트 같은 거 필요없이 그냥 호출을 하면 현재 state를 reducer 함수가 참조함!
   따라서 useCallback 사용하면서 deps 걱정 안 해도 된다!

- **상태 관리 로직 분리 후 코드**

  ```jsx
  import { useCallback, useEffect, useMemo, useReducer, useRef } from 'react';
  import axios from 'axios';
  import './App.css';
  import DiaryEditor from './DiaryEditor';
  import DiaryList from './DiaryList';

  const reducer = (state, action) => {
    switch (action.type) {
      case 'INIT': {
        return action.data;
      }
      case 'CREATE': {
        const created_date = new Date().getTime();
        const newItem = {
          ...action.data,
          created_date,
        };
        return [newItem, ...state];
      }
      case 'REMOVE': {
        return state.filter((it) => it.id !== action.targetId);
      }
      case 'EDIT': {
        return state.map((it) =>
          it.id === action.targetId ? { ...it, content: action.newContent } : it
        );
      }
      default:
        return state;
    }
  };

  function App() {
    //const [data, setData] = useState([]);
    const [data, dispatch] = useReducer(reducer, []);

    const dataId = useRef(0);

    const getData = () => {
      axios
        .get('https://jsonplaceholder.typicode.com/comments')
        .then((res) => {
          //결과값 : res.data
          const initData = res.data.slice(0, 20).map((it) => {
            return {
              author: it.email,
              content: it.body,
              emotion: Math.floor(Math.random() * 5) + 1,
              created_date: new Date().getTime(),
              id: dataId.current++,
            };
          });
          //setData(initData);
          dispatch({ type: 'INIT', data: initData });
        })
        .catch(() => {
          console.log('데이터 호출 실패!');
        });
    };

    useEffect(() => {
      getData();
    }, []);

    const onCreate = useCallback((author, content, emotion) => {
      dispatch({
        type: 'CREATE',
        //created_date는 reducer 함수에서 만들 것임
        data: { author, content, emotion, id: dataId.current },
      });
      dataId.current += 1;
    }, []);

    const onRemove = useCallback((targetId) => {
      dispatch({ type: 'REMOVE', targetId });
      //setData(data => data.filter(it => it.id !== targetId));
    }, []);

    const onEdit = useCallback((targetId, newContent) => {
      dispatch({ type: 'EDIT', targetId, newContent });
      // setData(data =>
      //   data.map(list =>
      //     list.id === targetId ? { ...list, content: newContent } : list
      //   )
      // );
    }, []);

    const getDiaryAnalysis = useMemo(() => {
      const goodCount = data.filter((it) => it.emotion >= 3).length;
      const badCount = data.length - goodCount;
      const goodRatio = (goodCount / data.length) * 100;
      return { goodCount, badCount, goodRatio };
    }, [data.length]);

    const { goodCount, badCount, goodRatio } = getDiaryAnalysis;

    return (
      <div className="App">
        <DiaryEditor onCreate={onCreate} />
        <div>전체 일기 : {data.length}</div>
        <div>기분 좋은 일기 개수 : {goodCount}</div>
        <div>기분 나쁜 일기 개수 : {badCount}</div>
        <div>기분 좋은 일기 비율 : {goodRatio}</div>
        <DiaryList onEdit={onEdit} onRemove={onRemove} diaryList={data} />
      </div>
    );
  }

  export default App;
  ```

  <br>
  <br>

### 📚 Reference

&nbsp; https://reactjs.org/
&nbsp; https://www.inflearn.com/course/

<br>
<br>
