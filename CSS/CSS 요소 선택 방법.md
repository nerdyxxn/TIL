# CSS 요소 선택 방법

> first-child, last-child, nth-child, nth-of-type, nth-last-of-type

<br>

## 💡 :first-child, :last-child

> - first-child : 부모의 자식 엘리먼트 중 첫 번째 요소를 선택한다.
> - :last-child : 부모의 자식 엘리먼트 중 마지막 요소를 선택한다.

<br>

#### 🔖 적용 예제

```html
<div>
  <li>1</li>
  <li>2</li>
  <li>3</li>
  <li>4</li>
</div>
```

```css
div {
  li:first-child {
    color: red;
  }

  li:last-child {
    color: lime;
  }
}
```

<br>
<br>

## 💡 :nth-child(n)

> nth-child는 부모의 모든 자식 엘리먼트 중에서 n번째 인 것을 선택한다.

<br>

#### 🔖 적용 예제

```html
<div>
  <li>1</li>
  <li>2</li>
  <li>3</li>
  <li>4</li>
</div>
```

```css
div {
  li:nth-child(2) {
    color: lime;
  }
}
```

<br>
<br>

## 💡 :nth-of-type(n)

> nth-of-type은 같은 유형의 n번째 형제 요소를 선택한다.

<br>

#### 🔖 적용 예제

```html
<div>
  <li>1</li>
  <li>2</li>
  <li>3</li>
  <li>4</li>
</div>
```

```css
div {
  li:nth-of-type(1) {
    color: lime;
  }
}
```

<br>
<br>

## 💡 :nth-last-of-type(n)

> - nth-last-of-type은 마지막 순서의 n번째 형제 요소를 선택한다.
> - a:nth-last-of-type(1)
>   - 맨 마지막 부터 계산해서 a 태그의 첫 번째 요소를 선택하는 것!

```css
div p:nth-last-of-type(1) {
  color: #f00;
}
```

<br>
<br>

### 📚 Reference

&nbsp; https://reactjs.org/
&nbsp; https://developer.mozilla.org/en-US/docs/Web/CSS/:nth-last-of-type
&nbsp; https://developer.mozilla.org/ko/docs/Web/CSS/:nth-child

<br>
<br>
