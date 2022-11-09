# Sass & Scss

<br>

## 💡 Sass란?

> Sass는 'Syntactically Awesome StyleSheet' 의 약자로, CSS를 보다 효율적으로 사용할 수 있도록 기능을 확장한 언어라고 할 수 있다.

<br>
<br>

## 💡 Sass의 특징

> Sass는 프로그래밍적으로 CSS를 적는다. 그렇기 때문에 때문에 코딩의 효율이나 소스코드의 유지보수가 수월해진다.
>
> Sass는 함수나 변수를 처리할 수 있어서 'CSS Preprocessor(전처리기)' 라고 불리기도 한다.
>
> CSS Preprocessor는 변수나 조합, 함수등으로 작성된 코드를 컴파일 하여 css로 변환하여 사용할 수 있게 하는 CSS 확장언어 이다.
> CSS Preprocessor 종류로는 Sass, LESS, Stylus 가 있다.

<br>
<br>

## 💡 Sass 사용법

> Sass를 사용하는 방법은 'SASS'와 'SCSS' 두 가지가 존재한다.

<br>

#### 1. SASS

```css
div
  background-color: black
  margin: 0 auto
  p
    padding: 10px
    span
      font-size: 1em
```

가장 오래 전부터 사용된 방법이다.
문법이 매우 간소화되어 있어 코딩을 컴팩트하고 간결하게 할 수 있다. 특징은 세미콜론을 적을 필요가 없다는 것이다.

<br>

#### 2. SCSS

```css
div {
  background-color: black;
  margin: 0 auto;
  p {
    padding: 10px;
    span {
      font-size: 1em;
    }
  }
}
```

SCSS는 SASS가 CSS와의 호환성이 부족한 부분이 있어 만들어진 방식이다.
SCSS의 가장 큰 장점은 CSS의 문법 그대로 사용할 수 있다는 점이다. SCSS를 처음 사용하더라도 CSS와 문법이 유사하기 때문에 적응하기 쉽다.

<br>
<br>

### 📚 Reference

&nbsp; http://study.zziraweb.com/less/less/?ckattempt=3
&nbsp; https://sass-lang.com/guide

<br>
<br>
