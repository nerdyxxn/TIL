# Immer

<br>

## ๐ก Immer ?

> ๋ฆฌ์กํธ์์๋ ๋ถ๋ณ์ฑ์ ์ ์งํ๋ฉฐ ์ํ๋ฅผ ์๋ฐ์ดํธ ํ๋ ๊ฒ์ด ์ค์ํ๋ค.

๋ถ๋ณ์ฑ์ ์ง์ผ์ผ ๊ฐ์ฒด ๋ด๋ถ์ ๊ฐ์ด ์๋ก ๋ณํ ๊ฒ์ ๋น๊ตํ์ฌ ๋ณํ๋ฅผ ๊ฐ์งํ๊ณ  ์ต์ ํ๋ฅผ ํ  ์ ์๋ค.
์ด๋ฌํ ๋ถ๋ณ์ฑ์ ์ ์งํ๊ธฐ ์ํด์ ์คํ๋ ๋ ๋ฌธ๋ฒ๊ณผ ๋ฐฐ์ด์ ๋ด์ฅํจ์๋ก ๋ฐฐ์ด, ๊ฐ์ฒด๋ฅผ ๋ณต์ฌํ๊ณ  ์๋ก์ด ๊ฐ์ ๋ง๋ ๋ค. ํ์ง๋ง ์ด๋ฌํ ๊ฐ์ฒด์ ๊ตฌ์กฐ๊ฐ ๋งค์ฐ ๊น์ด์ง๋ฉด ๋ถ๋ณ์ฑ์ ์ ์งํ๊ธฐ์ ์ ์ง๋ณด์๊ฐ ํ๋ค๋ค.

immer ๋ผ์ด๋ธ๋ฌ๋ฆฌ๋ฅผ ์ฌ์ฉํ๋ฉด ๊ตฌ์กฐ๊ฐ ๋ณต์กํ ๊ฐ์ฒด๋ ๋งค์ฐ ์ฝ๊ณ  ๊น๋ํ๊ฒ ๋ถ๋ณ์ฑ์ ์ ์งํ๋ฉฐ ์๋ฐ์ดํธ ํด์ค ์ ์๋ค.

<br>

#### ๐ Immer ์ค์น๋ฐฉ๋ฒ

```bash
npm i immer
```

<br>
<br>

## ๐ก ์ฌ์ฉ๋ฐฉ๋ฒ

- ๋ถ๋ณ์ฑ์ ์งํค๊ธฐ ์ํด ๋ณ๊ฒฝ์ํค๋ ค๊ณ  ํ๋ ๊ฐ์ ํ์ฌ๊ฐ์ ๋์ ํ๋ draftState์ ๋ชจ๋ ์ ์ฉ์์ผ๋๋ค.
- draftState์ ๋ณ๊ฒฝํ๋ ค๊ณ  ํ๋ ๊ฐ์ ๋ชจ๋ ์ ์ฉ์ํจ ํ์ nextState๋ฅผ ๋ง๋ ๋ค.

<img src="https://user-images.githubusercontent.com/66936285/207270188-a8efd750-cb17-40a6-840a-61e4dd5bd78c.png">

<br>

#### ๐ ์์ 

```jsx
import produce from 'immer';

const baseState = [
  {
    todo: 'Learn typescript',
    done: true,
  },
  {
    todo: 'Try immer',
    done: false,
  },
];

const nextState = produce(baseState, (draftState) => {
  draftState.push({ todo: 'Tweet about it' });
  draftState[1].done = true;
});
```

- ๊ธฐ์กด์ state๋ ๊ฑด๋๋ฆฌ์ง ์๊ณ  draftState๋ฅผ ์๋ก ๋ง๋ ๋ค. ์ด draftState๋ baseState์ ๊ฐ๊ณผ ๊ฐ๋ค.
- ์ด ๋ draftState์ ๊ฐ์ ๋ณ๊ฒฝ์ํค๋ ๋ฑ์ ๋ชจ๋  ์์์ด ์๋ฃ๋๋ฉด nextState๋ฅผ ๋ฐํํ๋ค.

<br>
<br>

#### ๐ Immer ์ฅ์ 

1. ๋ถ๋ณ์ฑ์ ์ํด ์ง์ผ์ผํ๋ ์คํ๋ ๋ ๋ฌธ๋ฒ๊ฐ์ ์์์ ํ์ง ์์๋ ๋๊ณ , ๊ธฐ์กด์ ๊ฐ์ ๋ณ๊ฒฝ์ํค๋ ์์์ ํด๋ ๋๋ค. ex) arr.push(1)....
2. ๋ง๋ค์ด์ง nextState ๊ฐ์ฒด๋ฅผ ๋ณ๊ฒฝ์ํฌ ์ ์๊ฒ ๋ง๋ค์ด ๋์๋ค.
3. ๊น์ ์๋ฐ์ดํธ๊ฐ ์ฝ๋ค.
4. Small: 3KB gzipped

<br>
<br>

## ๐ก Curried producers

> produce์ ์ฒซ๋ฒ์งธ ํ๋ผ๋ฏธํฐ๊ฐ์ผ๋ก ํจ์๋ฅผ ๋ฃ์ผ๋ฉด ๊ทธ ํ๋ผ๋ฏธํฐ์ ํจ์๊ฐ ์ํ๋ฅผ ๋ณ๊ฒฝ์ํค๋ ํจ์๋ฅผ ๋ฐํํ๋ค.

<br>

```jsx
// mapper will be of signature (state, index) => state
const mapper = produce((draft, index) => {
  draft.index = index;
});

// example usage
console.dir([{}, {}, {}].map(mapper));
//[{index: 0}, {index: 1}, {index: 2}])
```

- produce์ ํจ์๊ฐ์ ํ๋ผ๋ฏธํฐ๋ก ๋ฃ์์๋ ๊ทธ ํจ์๊ฐ ์ํ๋ฅผ ๋ณ๊ฒฝ์ํค๋ ์๋ฐ์ดํธ ํจ์๊ฐ ๋๋ค.
- ํจ์์ ์ฒซ๋ฒ์งธ ํ๋ผ๋ฏธํฐ์ธ draft๋ ์๋ก ๋ง๋  draft ๊ฐ์ฒด๊ฐ ๋๋ค.

<br>

#### ๐ React setState ์์ 

```jsx
onBirthDayClick1 = () => {
  this.setState((prevState) => ({
    user: {
      ...prevState.user,
      age: prevState.user.age + 1,
    },
  }));
};

/**
 * ...But, since setState accepts functions,
 * we can just create a curried producer and further simplify!
 */
onBirthDayClick2 = () => {
  this.setState(
    produce((draft) => {
      draft.user.age += 1;
    })
  );
};
```

- ์์ ๊ฐ์ด setState์ ๊ฐ์ด ์ผ์ ๋, ์ฒซ ๋ฒ์งธ ์์ ๋ setState์ ์ฒซ๋ฒ์งธ ํ๋ผ๋ฏธํฐ์ ํจ์๊ฐ ์์ ์ํ๋ฅผ ํ๋ผ๋ฏธํฐ๊ฐ์ผ๋ก ๋ฐ์ ๋ณ๊ฒฝ์์ผฐ๋ค.
  ๋ ๋ฒ์งธ ์์ ๋ Immer์ ์ฌ์ฉํ์ ๋ setState์ ์ฒซ๋ฒ์งธ ํ๋ผ๋ฏธํฐ๊ฐ์ผ๋ก proudce๊ฐ ์ค๊ฒ๋๋ค.

- produce์ ์ฒซ๋ฒ์งธ ํ๋ผ๋ฏธํฐ๊ฐ ํจ์๋ก ๋ค์ด์ค๊ฒ ๋๋ฉด ๊ทธ ํจ์๊ฐ ์๋ฐ์ดํธ ํจ์๋ก ๋ฐํ๋๋ฏ๋ก, setState์ produce๊ฐ ๋ค์ด๊ฐ๊ฒ ๋์์๋ ๋ฐํ๋๋ ์๋ฐ์ดํธ ํจ์๋ก setState๋ฅผ ์ฒ๋ฆฌํ๋ค.
  ๋๋ถ์ setState์ ์ธ์์ produce๋ฅผ ๋ฃ์ด ์๋ฐ์ดํธ ํจ์๋ฅผ ๋ง๋ค์ด์ฃผ๊ธฐ๋ง ํ๋ฉด๋๋ค.

<br>

#### ๐ Immer ์ฌ์ฉ ์ 

```jsx
import React, { useRef, useState } from 'react';
let id = 0;
const App = () => {
  const inputRef = useRef(null);
  const [value, setValue] = useState({ name: '', nickName: '' });
  const [list, setList] = useState([]);
  const onChange = ({ target }) => {
    setValue(() => ({ ...value, [target.name]: target.value }));
  };
  const onClick = (e) => {
    e.preventDefault();
    if (value.name === '' || value.nickName === '') return;
    setList(() => [{ id: id++, ...value }, ...list]);
    setValue(() => ({ name: '', nickName: '' }));
    inputRef.current.focus();
  };
  const onRemove = (id) => {
    setList(() => list.filter((list) => list.id !== id));
  };
  return (
    <>
      <form>
        <input value={value.name} ref={inputRef} name="name" onChange={onChange} />
        <input
          value={value.nickName}
          name="nickName"
          onChange={onChange}
          style={{ marginLeft: '10px' }}
        />
        <button type="submit" onClick={onClick} style={{ marginLeft: '10px' }}>
          ๋ฒํผ
        </button>
      </form>
      <ul>
        {list.map(({ id, name, nickName }) => (
          <li key={id} onDoubleClick={() => onRemove(id)}>
            {name}({nickName}) {id}
          </li>
        ))}
      </ul>
    </>
  );
};
export default App;
```

<br>

#### ๐ Immer ์ฌ์ฉ ํ

```jsx
import produce from 'immer';
import React, { useRef, useState } from 'react';
let id = 0;

const App = () => {
  const inputRef = useRef(null);
  const [value, setValue] = useState({ name: '', nickName: '' });
  const [list, setList] = useState([]);

  const onChange = ({ target }) => {
    setValue(
      produce((draft) => {
        draft[target.name] = target.value;
      })
    );
  };

  const onClick = (e) => {
    e.preventDefault();
    if (value.name === '' || value.nickName === '') return;
    setList(
      produce((draft) => {
        draft.push({ id: id++, name: value.name, nickName: value.nickName });
      })
    );
    setValue(
      produce((draft) => {
        draft.name = '';
        draft.nickName = '';
      })
    );
    inputRef.current.focus();
  };

  const onRemove = (id) => {
    setList(
      produce((draft) => {
        draft.splice(
          draft.findIndex((info) => info.id === id),
          1
        );
      })
    );
  };

  return (
    <>
      <form>
        <input value={value.name} ref={inputRef} name="name" onChange={onChange} />
        <input
          value={value.nickName}
          name="nickName"
          onChange={onChange}
          style={{ marginLeft: '10px' }}
        />
        <button type="submit" onClick={onClick} style={{ marginLeft: '10px' }}>
          ๋ฒํผ
        </button>
      </form>
      <ul>
        {list.map(({ id, name, nickName }) => (
          <li key={id} onDoubleClick={() => onRemove(id)}>
            {name}({nickName}) {id}
          </li>
        ))}
      </ul>
    </>
  );
};

export default App;
```

<br>
<br>

### ๐ Reference

&nbsp; https://immerjs.github.io/immer/docs/introduction
