# μλ£κ΅¬μ‘° - Stack & Queue

## π‘ μ€ν(stack)

> μ€ν(stack)μ μλ£μ μλ ₯κ³Ό μΆλ ₯μ΄ ν κ³³μμλ§ μ΄λ£¨μ΄μ§λ ννμ μλ£κ΅¬μ‘°

- μ€νμ νννλ λνμ μΈ μλ‘λ νλ§κΈμ€λΌκ³  ν  μ μλλ° μμ μλ κ³Όμλ₯Ό λ¨Όμ  λ¨Ήμ΄μΌλ§ μλμ μλ κ³Όμλ₯Ό κΊΌλΌ μ μμ
- μ΄λ₯Ό FILO(First In Last Out)μ΄λΌκ³  νλ©° μλ°μ€ν¬λ¦½νΈμμλ λ°°μ΄μ΄μ§λ§ shift, unshift μμ΄ pushμ popλ§ κ°λ₯ν κ²μ΄λΌκ³  μκ°ν  μ μμ
- μλ°μ€ν¬λ¦½νΈμμ μ€νμ΄ κ°μ§κ³  μλ Methodλ λ€μκ³Ό κ°μ

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

## π‘ ν(Queue)

> ν(Queue)λ μλ£μ μλ ₯κ³Ό μΆλ ₯μ΄ ν λ°©ν₯μΌλ‘λ§ μ΄λ£¨μ΄μ§λ ννμ μλ£κ΅¬μ‘°

- νλ₯Ό νννλ λνμ μΈ μλ‘λ κ³ μλλ‘ ν¨κ²μ΄νΈλΌκ³  λ³Ό μ μλλ°, ν¨κ²μ΄νΈμ λ¨Όμ  λ€μ΄κ° μ°¨λμ΄ μ μ°μ λ§μΉκ³  λκ°μΌλ§ λ€μμ κΈ°λ€λ¦¬λ μ°¨λμ΄ μ μ°ν  μ μμ
- μ΄λ₯Ό FIFO(First In First Out)μ΄λΌκ³  νλ©° μλ°μ€ν¬λ¦½νΈμμλ λ°°μ΄μ΄μ§λ§ pushμ shiftλ§ κ°λ₯ν κ²μ΄λΌκ³  μκ°ν  μ μμ
- μλ°μ€ν¬λ¦½νΈμμ νκ° κ°μ§κ³  μλ Methodλ λ€μκ³Ό κ°μ

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

### π Reference

- https://medium.com/@songjaeyoung92/%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0-javascript-stack-%EC%9D%B4%EB%9E%80-31f9bbb84897
- https://www.zerocho.com/category/Algorithm/post/5800b79e1dfb250015c38db6
- https://stackoverflow.com/questions/1590247/how-do-you-implement-a-stack-and-a-queue-in-javascript

<br>
