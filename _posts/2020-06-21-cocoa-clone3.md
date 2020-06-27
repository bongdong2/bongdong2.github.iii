---
title: "HTML & CSS - CSS Advance"
date: 2020-06-14 18:05:00 -0400
categories: html&css
---

트랜지션 & 트랜스포메이션 & 애니메이션 & 미디어쿼리

## 트랜지션(transitions)

애니메이션을 적용하고 싶다.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Transitions</title>
    <style>
      .box {
        background-color: green;
        color: white;
        transition: background-color 0.5s ease-in-out;
        /* background-color 글자색에도 애니메이션 적용하고 싶다면 'background-color' 대신  'all' */
      }
      .box:hover {
        /* hover, active, focus, visited */
        background-color: red;
        color: blue;
      }
    </style>
  </head>
  <body>
    <span class="box">
      text
    </span>
  </body>
</html>
```

<br><br>

## 트랜스포메이션(transformations)

html 문서의 element들을 변경, 모습이 변하는 효과를 말한다.

가로 세로 500px 빨간 box에 hover하면 0.5초동안 5번 회전하면서 스케일이 절반으로 줄어든다.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>transformations</title>
    <style>
      .box {
        width: 500px;
        height: 500px;
        background-color: red;
        transition: transform 0.5s ease-in-out;
      }
      .box:hover {
        transform: rotate(5turn) scale(0.5, 0.5);
      }
    </style>
  </head>
  <body>
    <header class="box"></header>
  </body>
</html>
```

[다양한 transform 사용방법](https://developer.mozilla.org/en-US/docs/Web/CSS/transform)

<br><br>

## 애니메이션

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>transformations</title>
    <style>
      .box {
        width: 500px;
        height: 500px;
        background-color: red;
        animation: 1.5s scaleAndRotateSquare2 ease-in-out infinite;
      }
      @keyframes scaleAndRotateSquare {
        from {
          transform: none;
        }
        to {
          transform: rotate(1turn) scale(0.5, 0.5);
        }
      }
      @keyframes scaleAndRotateSquare2 {
        0% {
          transform: none;
        }
        50% {
          transform: rotate(1turn) scale(0.5, 0.5);
        }
        100% {
          transform: none;
        }
      }
    </style>
  </head>
  <body>
    <div class="box"></header>
  </body>
</html>

```

<br><br>

## 미디어쿼리
반응형웹
```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Media queries</title>
    <style>
      body {
        background-color: green;
      }
      @media screen and (min-width: 320px) and (max-width: 640px) {
        body {
          background-color: blue;
        }
      }
    </style>
  </head>
  <body></body>
</html>
```

<br><br>

## 요약
- 트랜지션 : 하나의 state에서 다른 state로 넘어갈 때 효과
  - hover하면 애니메이션 뜨는 거
- 트랜스포메이션 : element의 모양새를 바꾸는 것. 비틀거나 키우거나. 여러가지
- 트랜지션/트랜스포메이션 섞기
  - hover하면 순간에 모양새가 트랜스폼. 변신함. 회전하거나.
- 애니메이션 : 키프레임을 만들어서 from-to 지정하거나, 2개 이상의 스텝을 만들 수 있다. 0-20-47등
- 미디어쿼리 : 브라우저 사이즈를 잡는 것

