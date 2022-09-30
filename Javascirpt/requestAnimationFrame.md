# requestAnimationFrame()

> Canvas를 활용한 인터렉티브 웹 개발에서 많이 사용하는 메소드

<br>

## 💡 requestAnimationFrame()이란?

> 브라우저에게 수행하기를 원하는 애니메이션을 알리고 다음 리페인트가 진행되기 전에 해당 애니메이션을 업데이트하는 함수를 호출하게 한다. 이 메소드는 리페인트 이전에 실행할 콜백을 인자로 받는다.

- 브라우저가 매번 계속 화면을 그리는데, 변화된 화면을 그릴 준비가 완료됐을 때 딱 그려준다는 것!
  → 최적화를 해서 애니메이션을 부드럽게 처리하는 기술과 같은 의미
- 특히, Canvas를 활용한 인터렉티브 웹 개발에서 많이 사용하는 메소드

<br>
<br>

## 💡 구문

> window.requestAnimationFrame(callback);

- 파라미터 (callback) : 다음 리페인트를 위한 애니메이션을 업데이트할 때 호출할 함수
- 반환값 : 콜백 리스트의 항목을 정의하는 고유한 요청 id인 long 정수값. 0이 아니라는것 외에는 다른 추측을 할 수가 없는 값

<br>
<br>

## 💡 기본적인 사용법

> 반복시킬 함수 안에서 requestAnimationFrame() 메소드를 사용하는데, 인자로 반복시킬 함수를 넣어준다.

- 속도는 초당 60회를 목표로 함 (60frame) → PC 사양에 따라 차이 있을 수 있음!
- 화면에 새로운 애니메이션을 업데이트할 준비가 될때마다 이 메소드를 호출하는 것이 좋다.<br>브라우저가 다음 리페인트를 수행하기전에 호출된 애니메이션 함수를 요청한다.<br>콜백의 수는 보통 1초에 60회지만, 일반적으로 대부분의 브라우저에서는 W3C 권장사항에 따라 그 수가 디스플레이 주사율과 일치하게 된다. (MDN)

```jsx
const ilbuni = document.querySelector('.ilbuni');
const value = document.querySelector('.value');
let yPos = 0;

function render() {
  value.innerHTML = yPos;
  yPos++;

  requestAnimationFrame(render);
}

render();
```

<br>
<br>

## 💡 종료시키기

> cancelAnimationFrame() 메소드를 사용해서 종료시킬 수 있다!

- requestAnimationFrame()는 리턴값으로 콜백 리스트의 항목을 정의하는 고유한 요청 id인 long 정수값을 가짐
- 변수(rafId)를 하나 만들어서 requestAnimationFrame(render) 메소드를 담고, **_cancelAnimationFrame(rafId)_** 이벤트로 종료시킬 수 있다.

```jsx
const ilbuni = document.querySelector('.ilbuni');
const value = document.querySelector('.value');
let yPos = 0;
let rafId;

function render() {
  value.innerHTML = yPos;
  ilbuni.style.transform = `translateY(${-yPos}px)`;
  yPos += 10;

  rafId = requestAnimationFrame(render);
}

render();

window.addEventListener('click', () => {
  cancelAnimationFrame(rafId);
});
```

<br>
<br>

## 💡 부드러운 감속의 원리

> requestAnimationFrame()을 활용해 스크롤 애니메이션이 보다 더 부드럽게 동작하도록 적용하는 것

- 속도 감속 시킬 때 자주 사용하는 식
- 이동량이 점점 줄어들어서 0에 수렴하도록 식을 작성해서 부드러운 감속에 활용하는 것!
  <br>
  <br>

  > **_c + ( d - c ) x 0.1_** <br> [ c : 현재위치, d : 목표위치 ]

- 현재위치에 목표위치에서 현재위치를 뺀 값에 임의의 소수를 곱한 값을 더해줘서 이동시킴
- 현재위치가 점점 목표위치로 이동하기 때문에 곱한 값이 점점 작아짐 → 따라서 이동거리 줄어드는 것 → 0에 수렴하면서 자연스러운 감속 진행

```jsx
const box = document.querySelector('.box');
let acc = 0.1;
let delayedYOffset = 0;
let rafId;
let rafState;

window.addEventListener('scroll', () => {
  if (!rafState) {
    rafId = requestAnimationFrame(loop);
    rafState = true;
  }
});

function loop() {
  // pageYOffset : 현재 스크롤 위치
  delayedYOffset = delayedYOffset + (pageYOffset - delayedYOffset) * acc;
  box.style.width = `${delayedYOffset}`;
  console.log('loop');

  rafId = requestAnimationFrame(loop);

  if (Math.abs(pageYOffset - delayedYOffset) < 1) {
    cancelAnimationFrame(rafId);
    rafState = false;
  }
}

loop();
```

<br>
<br>

🤔 **애니메이션은 멈췄지만 loop 함수 계속 돌아가는 문제 발생!**

- 움직일 때만 반복되고 스크롤 멈추면 loop 함수도 멈추도록 로직 작성 필요
- 목표위치와 현재위치의 차이가 1px 이하이면 반복을 멈추도록 조건 추가하기
- **_requestAnimationFrame()_** 종료 시킬 땐 **_cancelAnimationFrame()_** 사용
- **pageYOffset - delayedYOffset** 값을 그대로 사용하면, 스크롤을 위로 올릴 때는 계속 음수여서 부드러운 감속이 제대로 동작하지 않음!
  우리가 필요한 건 거리이기 때문에 음수여도 상관이 없어야 함 ⇒ 따라서 절대값 처리 필요
  <br>
  <br>
  <br>

### 📚 Reference

&nbsp; [requestAnimationFrame 사용법 - 1분코딩](https://youtu.be/9XnqDSabFjM)
&nbsp; [MDN WEB DOCS - windowrequestAnimationFrame()](https://developer.mozilla.org/ko/docs/Web/API/Window/requestAnimationFrame)
<br>
<br>
