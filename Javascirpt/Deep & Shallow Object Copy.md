# Deep/Shallow Object Copy

> 자바스크립트에서 객체 복사는 얕은 복사(Shallow Copy)와 깊은 복사(Deep Copy)로 나뉜다.

<br>

## 💡 얕은 복사(Shallow Copy)

> spread 방식이나 Object.assign 등으로 객체가 지닌 키, 밸류만을 얕게 복사하는 방법이다. 원본 객체와 다른 주소를 바라보기 때문에 값이 변동될 때 원본 객체에 영향을 끼치지 않는다.
> 하지만 최상위 레벨의 depth에만 적용이 되며, 그 이상으로 깊은 depth에서는 원본 객체가 변경되면 복사된 객체도 같이 변경되게 된다.(깊은 복사의 필요성!)

<br>

#### 얕은 복사하는 방법

```jsx
let obj = { a: 1, b: { b: 2 } };

let copiedObj = Object.assign({}, obj);
copiedObj; // {a: 1, b: {b: 2}}

// * 최상위 depth 이상의 깊은 depth의 경우
obj.b.b = '변경';

copiedObj.b.b; // 변경
```

<br>

#### Object.assign() 이란?

> Object.assign() 메소드는 열거할 수 있는 하나 이상의 출처 객체로부터 대상 객체로 속성을 복사할 때 사용합니다. 대상 객체를 반환합니다. (MDN)

<br>

아래 예제 코드는 MDN에 있는 예제 코드이며 이를 참고하도록 하겠다.

먼저 assing()을 하기 위해서는 타겟이 되는 객체와 타켓 객체에 속성을 복사할 1개 이상의 소스 객체가 필요하다.

첫 번째 매개변수에는 타켓 객체가 위치하게 되며 두 번째부터는 속성을 복사할 소스 객체들이 위치하게 된다.

특징으로는 타켓 객체에 key와 소스 객체의 key가 같은 경우에는 타겟 객체의 key/value 페어가 소스 객체의 key/value 페어로 대체된다는 점이다. 그리고 리턴되는 반환 값은 소스 코드의 속성이 복사된 타겟 객체가 된다. 따라서 target과 returnTarget은 같은 주소를 참조하게 된다.

```jsx
const target = { a: 1, b: 2 };
const source = { b: 4, c: 5 };

const returnedTarget = Object.assign(target, source);

console.log(target);
// { a: 1, b: 4, c: 5 }

console.log(returnedTarget);
// { a: 1, b: 4, c: 5 }

console.log(target === returnedTarget);
// true
```

<br>
<br>

## 💡 깊은 복사(Deep Copy)

> 원본 객체의 주소를 참조한다. 기본형 타입(primitive type)과 달리 참조형 타입(reference type)인 객체는 같은 주소를 참조하고 있기 때문에 값이 변동될 때 원본 객체에 영향을 끼치게 된다.

<br>

#### 깊은 복사하는 방법

> JSON.parse(JSON.stringify(object))를 이용해 JSON화 하고 다시 파싱하는 방식으로 객체를 복사한다.

```jsx
let obj = { a: 1, b: { b: 2 } };

let copiedObj = JSON.parse(JSON.stringify(obj));
copiedObj; // {a: 1, b: {b: 2}}

// * 최상위 depth 이상의 깊은 depth의 경우
obj.b.b = '변경';

// 원본 객체와 관계 없이 독자적인 값을 유지한다.(깊은 복사)
copiedObj.b.b; // 2
```

<br>
<br>

### 📚 Reference

- https://stackoverflow.com/questions/24512712/what-is-the-difference-between-a-shallow-copy-and-a-deep-copy-with-javascript-ar
- https://medium.com/@arunrajeevan/shallow-copy-vs-deep-copy-in-javascript-5ce718725a0
- https://medium.com/@han7096/shallow-copy-%EC%96%95%EC%9D%80-%EB%B3%B5%EC%A0%9C-%EC%99%80-deep-copy-%EA%B9%8A%EC%9D%80-%EB%B3%B5%EC%A0%9C-%EC%9D%98-%EC%B0%A8%EC%9D%B4-9d11458b4da1
