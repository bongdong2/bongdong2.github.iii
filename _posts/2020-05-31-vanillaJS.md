---
title: "Vanilla JS - study 1"
date: 2020-05-31 12:12:00 -0400
categories: javascript
---
바닐라 자바스크립트 공부


### JS 파일은 항상 body 아래에 둘 것

### 변수 
- 변수 사용은 const로, 진짜 필요한 경우에만 let을 사용한다.
- boolean true(1), false(0)
- String, Number, float, boolean ...

### 배열, 객체
```javascript
const array = ["Mon", "Tue", "Wed", true, 1, "hello"];
console.log(array[0]); // "Mon"

const mike = {
    name : "mike",
    age : 30,
    isHandsome = true
};
console.log(mike.isHansome); // true
```
- arr내부의 obj, ojb내의의 arr 가능하다.

### 함수
console.log ==> log는 console 객체 내부의 함수이다.

```javascript
const cal = {
    plus : function(a, b) {
        return a + b;
    },
    sub : function(a, b) {
        return a - b;
    } ...
}

console.log(cal.plus(5, 5)); // 10
```

### JS DOM Functions 
- DOM(Document Object Module)
- js는 html에 있는 모든 요소를 가져와서 객체로 바꾼다.

```javascript
const title = document.getElementById("title");
title.innerHTML = "HelloWorld";

console.dir(document); // DOM 내부를 살펴볼 수 있다.

documnet.querySelector("#id"); // .class
// querySelector는 첫 번째 자식의 노드를 반환한다.
```
textContent, innerText, innerHTML 중에 textContext가 가장 성능 높다.

## 이벤트
```javascript
function handleResize() {
    console.log("I have been resized");
}

window.addEventListener("resize", handleResize);

// 윈도우 크기를 조절하면 콘솔로그가 출력된다.
// handleResize() 를 사용하면 즉시 호출되므로 ()는 뺀댜.
// handleResize에 매개변수로 이벤트가 넘어오는데 console.log로 찍어볼 수 있다.
```

```javascript
const title = document.querySelector("#title");
const BASE_COLOR = "rgb(52, 73, 94)";
const OTHER_COLOR = "#e74c3c";

function handleClick() {
    const currentColor = title.style.color;

    console.log(currentColor);
    console.log(BASE_COLOR);

    title.style.color = OTHER_COLOR;

    if(currentColor === BASE_COLOR) {
        title.style.color = OTHER_COLOR;
    } else {
        title.style.color = BASE_COLOR;
    }
};

function init() {
    title.style.color = BASE_COLOR;
    title.addEventListener("mouseover", handleClick);
}

init();


function handleOffline() {
    console.log("offline");
}

function handleOnline() {
    console.log("online");
}

window.addEventListener("offline", handleOffline);
window.addEventListener("online", handleOnline);
```
- MDN을 참고하자



js로는 직접 css를 변경하는 것이 아닌 로직을 구현하고 싶다.
```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width">
    <title>javascript Test</title>
    <link href="index.css" rel="stylesheet" type="text/css" />
  </head>
  <body>
    <h1 id="title" class="btn">this is javascript test</h1>
    <script src="index.js"></script>
  </body>
</html>
```

```css
/* body{
    background-color: yellow;
  } */
  
h1{
    color: #34495e;
    transition: color 0.5s ease-in-out;
}

.clicked {
    color: #7f8c8d;
}
```


```javascript
const title = document.querySelector("#title");

const CLICKED_CLASS = "clicked";

function handleClick() {
    /*
    const hasClass = title.classList.contains(CLICKED_CLASS);

    if(!hasClass) { 
        title.classList.add(CLICKED_CLASS);
    } else {
        title.classList.remove(CLICKED_CLASS);
    }
    */

    title.classList.toggle(CLICKED_CLASS);
    // 위의 내용을 toggle 함수로 한 번에 구현
}

function init() {
    title.addEventListener("click", handleClick);
}

init();
```