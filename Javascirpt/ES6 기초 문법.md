# ES6 기초 문법

## 💡 Hoisting

> var 키워드에서 가능
> let, const 키워드에 경우에는 'ReferenceError' 가 발생

```jsx
console.log(a); // undefined
var a = 1;
```

<br>
<br>

## 💡 Default Parameter

> 함수의 Prameter에 기본값을 줄 수 있음

```jsx
function testFunc(a = 'hello') {
  console.log(a);
}

testFunc(); // 'hello'
testFunc('world'); // 'world'
```

<br>
<br>

## 💡 Template Literal

> 내장된 표현식을 허용하는 문자열 리터럴

- 표현식/문자열 삽입, 여러 줄 문자열, 문자열 형식화, 문자열 태깅 등 다양한 기능을 제공
- 런타임 시점에 일반 자바스크립트 문자열로 처리/변환
- 프론트엔드에서는 HTML을 데이터와 결합해서 DOM을 다시 그려야 하는 일이 빈번하기 때문에, 템플릿을 좀 더 쉽게 편집하고 작성해야 할 필요가 있어서, 이러한 기능이 추가되었음

```jsx
let a = 'hello';
let b = 'world';

let c = `${a} + ${b} is 'hello world'`;
console.log(c); // hello + world is 'hello world'
```

<br>
<br>

## 💡 Arrow Function

> 화살표 함수는 기존 함수의 기능을 문법적으로 편하게 직관적으로 보여지기 위해 만들어진 이유보다 함수를 가볍게 하기 위해서 만들어진 목적이 더 크다.

<br>

**Arrow Function's detail info**

1. (매개변수) => { 본문 }
2. 매개변수가 하나뿐인 경우 괄호 생략 가능
3. 매개변수가 없을 경우에는 괄호 필수
4. 본문이  return [식 or 값] 뿐인 경우  { } 와  return 키워드 생략 가능
5. 위 4) 에서  return 할 값이  객체인 경우네는 괄호 필수
   <br>

```jsx
보통의 함수표현식 예시
let func = function(arg1, arg2, ...argN) {
  return expression;
};

화살표 함수를 이용한 함수표현식 예시
let double = n => n * 2;
// let double = function(n) { return n * 2 }과 거의 동일

alert( double(3) ); // 6

// 인수가 하나도 없을 땐 괄호를 비워두면 된다. (괄호는 생략할 수 없음)
let sayHi = () => alert("안녕하세요!");
```

<br>
<br>

## 💡 Rest Parameter

> Rest 파라미터(Rest Parameter, 나머지 매개변수)는 매개변수 이름 앞에 세개의 점 ...을 붙여서 정의한 매개변수를 의미한다. Rest 파라미터는 함수에 전달된 인수들의 목록을 배열로 전달받는다.

- Rest 파라미터는 이름 그대로 먼저 선언된 파라미터에 할당된 인수를 제외한 나머지 인수들이 모두 배열에 담겨 할당된다. 따라서 Rest 파라미터는 반드시 마지막 파라미터이어야 한다.
- Rest 파라미터는 함수 정의 시 선언한 매개변수 개수를 나타내는 함수 객체의 length 프로퍼티에 영향을 주지 않는다.
  <br>

```jsx
function foo(...rest) {
  console.log(Array.isArray(rest)); // true
  console.log(rest); // [ 1, 2, 3, 4, 5 ]
}

foo(1, 2, 3, 4, 5);

function foo(...rest) {}
console.log(foo.length); // 0

function bar(x, ...rest) {}
console.log(bar.length); // 1

function baz(x, y, ...rest) {}
console.log(baz.length); // 2
```

<br>
<br>

## 💡 Spead 문법

> Spread 문법(Spread Syntax, ...)는 대상을 개별 요소로 분리한다. Spread 문법의 대상은 이터러블이어야 한다.

```jsx
// ...[1, 2, 3]는 [1, 2, 3]을 개별 요소로 분리한다(→ 1, 2, 3)
console.log(...[1, 2, 3]); // 1, 2, 3

// 문자열은 이터러블이다.
console.log(...'Hello'); // H e l l o

// Map과 Set은 이터러블이다.
console.log(
  ...new Map([
    ['a', '1'],
    ['b', '2'],
  ])
); // [ 'a', '1' ] [ 'b', '2' ]
console.log(...new Set([1, 2, 3])); // 1 2 3

// 이터러블이 아닌 일반 객체는 Spread 문법의 대상이 될 수 없다.
console.log(...{ a: 1, b: 2 });
// TypeError: Found non-callable @@iterator
```

<br>
<br>
<br>

### 📚 Reference

[Javascript ES6+ 제대로 알아보기-초급](https://www.inflearn.com/course/ecmascript-6-flow)
