# CSS의 font-size 단위

> CSS에서 폰트 사이즈를 설정하는 방법은 두 가지가 존재한다.
>
> 1. 절대치: 10px이라면 무조건 10px
> 2. 상대치: 부모 요소의 사이즈에 의해 가변

<br>

## 💡 px

> px는 폰트 사이즈의 절대치를 설정하는 단위이다.

```css
body {
  font-size: 64px;
}

h1 {
  font-size: 32px;
}

h2 {
  font-size: 16px;
}
```

<br>
<br>

## 💡 em

> em은 부모 요소의 폰트 사이즈를 기반으로 크기를 설정한다.

```css
body {
  font-size: 32px;
}

h1 {
  font-size: 2em; /* -> 64px; */
}

h2 {
  font-size: 0.5em; /* -> 32px; */
}
```

<br>
<br>

## 💡 %

> em과 같이 부모 요소의 폰트 사이즈를 기반으로 크기를 설정한다.

```css
body {
  font-size: 32px;
}

h1 {
  font-size: 200%; /* -> 64px; */
}

h2 {
  font-size: 50%; /* -> 32px; */
}
```

<br>
<br>

## 💡 rem (root em)

> rem은 html 문서의 루트인 html 태그를 기준으로 폰트 사이즈를 설정한다.

```css
html {
  font-size: 32px;
}

h1 {
  font-size: 2rem; /* -> 64px; */
}

h2 {
  font-size: 0.5rem; /* -> 16px; */
}
```

<br>
<br>

### 📚 Reference

&nbsp; https://www.sitepoint.com/understanding-and-using-rem-units-in-css/
&nbsp; https://qiita.com/masarufuruya/items/bb40d7e39f56e6c25f0d

<br>
<br>
