# CSS Flex (Flexible Box)

> container와 items 기준으로 설명함

<br>

## 💡 수평 레이아웃

> items 따로 조정하지 않아도 수평 정렬된다.
> flex는 수평 정렬이 기본값

<br>

#### 🔖 적용 예제

```css
.container {
  display: flex;
}
```

<br>

## 💡 수직 레이아웃

> flex의 기본값인 수평 정렬이 수직 정렬로 전환된다.

<br>

#### 🔖 적용 예제

```css
.container {
  display: flex;
  flex-direction: column;
}
```

<br>

## 💡 x,y축 정렬

> 수직 레이아웃을 다시 수평으로 만들려면 flex-direction을 row로 바꾸면 된다.
> justify-content를 center로 하면 중심축(수평)의 중앙에 정렬된다. align-items를 center로 하면 교차축(수직)의 중앙에 정렬된다.

<br>

#### 🔖 적용 예제

```css
.container {
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
}
```

<br>

- **justify-content**

  - flex-start(default)
  - flex-end
  - center
  - space-between
  - space-around

- **align-items**
  - flex-start(default)
  - flex-end
  - center
  - baseline
  - stretch

<br>

## 💡 Items

> 축에 따른 전체적 정렬 말고도, 각각의 아이템을 정렬할 수 있다.

<br>

#### 🔖 적용 예제

```css
.item1 {
  align-self: flex-end;
}
```

- item1 요소만 하단을 기준으로 정렬된다.

<br>
<br>

### 📚 Reference

&nbsp; https://reactjs.org/
&nbsp; https://developer.mozilla.org/en-US/docs/Web/CSS/:nth-last-of-type
&nbsp; https://joshuajangblog.wordpress.com/2016/09/19/learn-css-flexbox-in-3mins/

<br>
<br>
