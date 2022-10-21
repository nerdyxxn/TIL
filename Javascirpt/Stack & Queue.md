# 자료구조 - Stack & Queue

## 💡 스택(stack)

> 스택(stack)은 자료의 입력과 출력이 한 곳에서만 이루어지는 형태의 자료구조

- 스택을 표현하는 대표적인 예로는 프링글스라고 할 수 있는데 위에 있는 과자를 먼저 먹어야만 아래의 있는 과자를 꺼낼 수 있음
- 이를 FILO(First In Last Out)이라고 하며 자바스크립트에서는 배열이지만 shift, unshift 없이 push와 pop만 가능한 것이라고 생각할 수 있음
- 자바스크립트에서 스택이 가지고 있는 Method는 다음과 같음

  - Array.prototype.push()
  - Array.prototype.pop()

  ```jsx
  let stack = [];

  stack.push(2); // stack is [2];
  stack.push(5); // stack is [2, 5];

  let poppedStack = stack.pop(); // stack is [2];
  console.log(poppedStack); // 5
  ```

<br>
<br>

## 💡 큐(Queue)

> 큐(Queue)는 자료의 입력과 출력이 한 방향으로만 이루어지는 형태의 자료구조

- 큐를 표현하는 대표적인 예로는 고속도로 톨게이트라고 볼 수 있는데, 톨게이트에 먼저 들어간 차량이 정산을 마치고 나가야만 뒤에서 기다리던 차량이 정산할 수 있음
- 이를 FIFO(First In First Out)이라고 하며 자바스크립트에서는 배열이지만 push와 shift만 가능한 것이라고 생각할 수 있음
- 자바스크립트에서 큐가 가지고 있는 Method는 다음과 같음

```jsx
let queue = [];

queue.push(2); // queue is [2];
queue.push(5); // queue is [2, 5];

let shiftedQueue = queue.shift(); // queue is [5];
console.log(shiftedQueue); // 2
```

<br>
<br>
<br>

### 📚 Reference

- https://medium.com/@songjaeyoung92/%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0-javascript-stack-%EC%9D%B4%EB%9E%80-31f9bbb84897
- https://www.zerocho.com/category/Algorithm/post/5800b79e1dfb250015c38db6
- https://stackoverflow.com/questions/1590247/how-do-you-implement-a-stack-and-a-queue-in-javascript

<br>
