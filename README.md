# js-event
 

 ## Events개념
이벤트는 프로그래밍중인 시스템에서 발생하는 동작 또는 발생으로, 원하는 경우 어떤 방식 으로든 대응할 수 있도록 시스템에서 알려줍니다.

### Events
https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Building_blocks/Events

### Events 종류
https://developer.mozilla.org/en-US/docs/Web/Events

### Bubbling and Capturing
이벤트 버블 링 및 캡처는 동일한 이벤트 유형의 두 처리기가 한 요소에서 활성화 될 때 발생하는 상황을 설명하는 두 가지 메커니즘입니다.

https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Building_blocks/Events#Event_bubbling_and_capture


~~~HTML
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <style>
      .outer {
        width: 500px;
        height: 500px;
        background-color: yellow;
      }

      .middle {
        width: 50%;
        height: 50%;
        margin: auto;
        background-color: thistle;
        transform: translateY(50%);
      }

      button {
        position: relative;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
      }
    </style>
  </head>
  <body>
    <div class="outer">
      <div class="middle">
        <button>Click Me</button>
      </div>
    </div>
    <script>
      const outer = document.querySelector('.outer');
      const middle = document.querySelector('.middle');
      const button = document.querySelector('button');

      outer.addEventListener('click', event => {
      //bubble up(x)  
      	if (event.target !== event.currentTarget) {
          return;
        }
        console.log(`outer: ${event.currentTarget}, ${event.target}`);
      });
      middle.addEventListener('click', event => {
      //bubble up(x)
        if (event.target !== event.currentTarget) {
          return;
        }
        console.log(`middle ${event.currentTarget}, ${event.target}`);
      });
      button.addEventListener('click', event => {
        console.log(`button1 ${event.currentTarget}, ${event.target}`);
      });
      button.addEventListener('click', event => {
        console.log(`button2 ${event.currentTarget}, ${event.target}`);
      });
    </script>
  </body>
</html>
~~~

### 이벤트 위임

```Html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <style>
      .selected {
        background-color: yellow;
      }
    </style>
  </head>
  <body>
    <ul>
      <li>1</li>
      <li>2</li>
      <li>3</li>
      <li>4</li>
      <li>5</li>
      <li>6</li>
      <li>7</li>
      <li>8</li>
      <li>9</li>
      <li>10</li>
    </ul>
    <script>
      // Bad
      // const lis = document.querySelectorAll('li');
      // lis.forEach(li => {
      //   li.addEventListener('click', () => {
      //     li.classList.add('selected');
      //   });
      // });

      // Coooooooool 🙌
      const ul = document.querySelector('ul');
      ul.addEventListener('click', event => {
        if (event.target.tagName == 'LI') {
          event.target.classList.add('selected');
        }
      });
    </script>
  </body>
</html>
```







