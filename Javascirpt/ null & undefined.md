# JavaScript의 null, undefined 차이

> null, undefined는 둘 다 변수에 값이 없는 것을 나타내지만, 둘의 의미는 꽤 다르다.

<br>

## 💡 null

> null은 의도를 가지고 변수에 null을 할당하여 값이 없다는 것을 나타낸다. null이 할당된 변수의 타입을 확인해 보면 object인걸 확인할 수 있다.

```jsx
let a = null;
console.log(a); // null

console.log(typeof a); // object
```

<br>
<br>

## 💡 undefined

> 변수를 선언하고 값을 할당하기 전의 형태(값)라고 볼 수 있다. (\*변수에 값이 할당되어 있지 않음.)

```jsx
let b;
console.log(b); // undefined
```

<br>

#### undefined가 나오는 경우의 예시

1. 존재하지 않는 객체의 프로퍼티를 읽을려고 할 때

   ```jsx
   let obj = {};
   console.log(obj.a); // undefined
   ```

2. 존재하지 않는 배열에 엘리먼트를 읽을려고 할 때

   ```jsx
   let arr = [1, 2, 3];
   console.log(arr[10]); // undefined
   ```

<br>
<br>

## 💡 정리

> **undefined** : 접근 가능한 스코프에 변수가 선언되었으나 현재 아무런 값도 할당되지 않은 상태이다. 타입을 확인해 보면 'undefined' 이다.

> **null** : 변수를 선언하고 'null'이라는 빈 값을 할당한 경우이다. 타입을 확인해 보면 'object' 이다.

> **undeclared** : 접근 가능한 스코프에 변수 선언조차 되어있지 않은 상태이다. 타입을 확인해 보면 'undefined' 이다.

<br>
<br>

### 📚 Reference

- https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/null
- https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/undefined
- https://sudo-heedongdev.tistory.com/6profile
