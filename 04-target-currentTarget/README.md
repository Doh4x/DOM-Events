## target и currentTarget

Путаница между ними самая частая ошибка у новичков.

target это где событие реально произошло. Если кликнули по span внутри button - target это span.

currentTarget это где висит обработчик. Если обработчик повешен на button - currentTarget это button даже если кликнули по вложенному span.

Совпадают они когда обработчик висит прямо на том элементе по которому кликнули. Когда событие всплыло с дочернего элемента - target и currentTarget разные.

```html
<ul id="list">
  <li>один</li>
  <li>два</li>
  <li>три</li>
</ul>
```

```js
const list = document.getElementById('list');

list.addEventListener('click', (event) => {
  console.log(event.target);        // конкретный li по которому кликнули
  console.log(event.currentTarget); // всегда ul
});
```

После того как обработчик отработал, currentTarget становится null. Если нужно сохранить ссылку на текущий элемент - сохрани её в переменную сразу.

Ссылки
- https://developer.mozilla.org/en-US/docs/Web/API/Event/target
- https://developer.mozilla.org/en-US/docs/Web/API/Event/currentTarget
