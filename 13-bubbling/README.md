## Всплытие (bubbling)

Когда событие происходит на элементе, оно сначала срабатывает на нём, потом на его родителе, потом на родителе родителя и так до document и window. Этот путь называется фазой всплытия.

```html
<div id="a">
  <div id="b">
    <button id="c">клик</button>
  </div>
</div>
```

```js
document.getElementById('a').addEventListener('click', () => console.log('a'));
document.getElementById('b').addEventListener('click', () => console.log('b'));
document.getElementById('c').addEventListener('click', () => console.log('c'));
```

Клик по кнопке выведет c, потом b, потом a. event.target всё это время указывает на кнопку, а event.currentTarget меняется на текущий элемент.

Помимо всплытия есть ещё фаза погружения (capturing) - событие сначала идёт сверху вниз от window до целевого элемента, и только потом всплывает обратно. Чтоб поймать на погружении - передать { capture: true } в addEventListener. На практике используется редко.

Не все события всплывают. focus, blur, mouseenter, mouseleave, load - не всплывают. У каждого события свойство bubbles говорит как оно себя ведёт.

Остановить всплытие можно через event.stopPropagation().

Ссылки
- https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Building_blocks/Event_bubbling
