# Jest & ESLint

## ๐ก Code Quality

> 1. ์๋ํ ๋๋ก ๋์ํ๋๊ฐ
> 2. ๊ฒฐํจ์ด๋ ๋ฌธ์ ๊ฐ ์๋๊ฐ
> 3. ์ฝ๊ธฐ ์ฝ๊ณ , ์ ์ง ๋ฐ ํ์ฅํ๊ธฐ ์ฉ์ดํ๊ฐ

- Testing Tool
  1. End to end test
  2. Integration test
  3. Unit test

<br>
<br>

## ๐ก Jest

> Jest๋ ์๋ฐ์คํฌ๋ฆฝํธ๋ก ์์ฑํ ์ฝ๋๋ฅผ ํ์คํธ ํ๊ธฐ ์ํ ํ๋ ์์ํฌ

```jsx
ํ์คํธํ  ์ฝ๋(sum.js)
function sum(a, b) {
    return a + b;
}

ํ์คํธํ  ์ผ์ด์ค(sum.test.js)
const num - require('./sum');

test('add 1 + 2 to equal 3', () => {
    expect(sum(1, 2).toBe(3));
});
```

- matcher function ์ค toBe์ toEqual์ ๊ธฐ๋ฅ์ ์ ์ฌํ์ง๋ง toBe๊ฐ ๋ ์๊ฒฉํ๊ฒ ์ฒดํฌํจ (like === operation)
- toEqual์ ๊ฐ์ ๋ชจ์, ๊ฐ์ ๊ฐ์ ๊ฐ์ก๋์ง ํ์ธ(===๊ณผ ๋ค๋ฆ)
- ๋ํ์ ์ธ global ํจ์์ ์ข๋ฅ
  <br>

```jsx
beforeEach(fn); // ๋ชจ๋  ํ์คํธ์ ์์ ์ ์ fn ์ ์คํ

describe(name, fn); // ํ์คํธ ๋ธ๋ก ํ์ฑ
describe.skip(name, fn); // ํ์คํธ ๋ธ๋ก์ ์ํ ๋ชจ๋  ํ์คํธ ๊ฒ์ฌํ์ง ์๊ณ  ๋์ด๊ฐ

test(name, fn, timeout); // ํ์คํธ ํญ๋ชฉ ๋ง๋ค๊ธฐ fn์ ๋์ค์ ์คํ๋จ
it(name, fn, timeout); // test์ ๋์ผ(alias)

test.skip(name, fn); // ํ์คํธ ํญ๋ชฉ ๊ฑด๋๋ฐ๊ธฐ
it.skip(name, fn); // test.skip๊ณผ ๋์ผ
xit(name, fn); // it.skip๊ณผ ๋์ผ
xtest(name, fn); // xit๊ณผ ๋์ผ
```

<br>
<br>

## ๐ก ESLint

> ESLint๋ ์ฝ๋์ ๋ฃฐ์ ์งํค๋์ง ์ฒดํฌํด ์ฃผ๋ ์ญํ ์ ํจ

- ๋ํ์ ์ผ๋ก ์์ด๋น์๋น, ๋ค์ด๋ฒ ๋ฑ์์ ์์ ๋ค์ ESLint ๋ฃฐ์ ๊ณต์ ํ๊ณ  ์์

<br>
<br>
<br>

### ๐ Reference

[ESLint ๊ณต์ ๋ฌธ์](https://eslint.org/)
