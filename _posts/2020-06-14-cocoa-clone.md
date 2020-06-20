---
title: "HTML & CSS - 코코아 클론코딩"
date: 2020-06-14 14:32:00 -0400
categories: html&css
---

코코아 클론 코딩 기록 - 1

## 사전작업

- vs code 설치
- prettier extention 설치 > editor.fomatOnSave = true

## HTML Basics

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="description" content="welcome to my website" />
    <title>Document</title>
  </head>
  <body>
    <sction>
      <header id="headerNumberOne" class="defaultHeader">
        <h1>Title of a section</h1>
      </header>
    </sction>
    <div>
      <header id="differHeader" class="dafaultHeader">
        Title of unknown container
      </header>
    </div>
  </body>
</html>
```

- header : 보이지 않는 부분
- body : 보이는 부분
- meta : header에 속함. 브라우저에 전달하는 추가정보
- semantic, non-semantic
  - semantic : 제목, 문단, 내비게이션 등등 뭔가 뜻이 있는 태그, 수많은 코드 속에서 헤메이고 있을 때, semantic 태그는 각 항목이 각각 무엇을 뜻하는지 알려준다. 예) section, header
  - non-semantic : 아무 지칭한 바 없는, 의미없는 태그들 예) div, span
- id, class
  - id : 여권번호같은 고유번호, 고유한 것들에 부여, 각 엘리먼트당 하나.
  - class : 수천만명이 가지고 있는 국적, 계속 반복되는 element들에 사용.

## CSS Basics

- selector
- property : 소문자, 공백없음, 마지막에 세미클론
  - property-name: value;

```html
<head>
  <link rel="stylesheet" href="style.css" />
</head>
```

```css
// style.css
body {
  background-color: aqua;
}

h1 {
  color: azure;
}
```

- css와 html을 연결하는 방법은 inline과 external 방식이 있는데 inline방식은 재활용하려면 html마다 중복되는 css를 사용하므로 추천하지 않는다.

- Box Model
  - content
  - border : padding, margin 가운데
  - padding : 안쪽 간격
  - margin : 바깥쪽 간격
- ![boxmodel](/images/cssboxmodel.png)

```css
.box {
  background-color: yellow;
  width: 50%;
  height: 50%;
  padding-top: 50px;
  padding-left: 50px;
  margin-top: 50px;
  margin-left: 50px;
  margin: 20px;
  margin: 20px 10px;
  margin: 20px 10px 5px 2px;
}
.inside-box {
  background-color: blue;
  width: 50%;
  height: 50%;
  border-width: 5px;
  border-color: red;
  border-style: dashed;
}
```
