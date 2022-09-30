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
<br>

### 📚 Reference

&nbsp; [requestAnimationFrame 사용법 - 1분코딩](https://youtu.be/9XnqDSabFjM)
&nbsp; [MDN WEB DOCS - windowrequestAnimationFrame()](https://developer.mozilla.org/ko/docs/Web/API/Window/requestAnimationFrame)
<br>
<br>
