## Обработка динамически созданных элементов

Если элемент создаётся позже (через innerHTML, appendChild, рендер из данных) - обработчик который повесили раньше на конкретный элемент на него не попадёт. Элемента ещё не было в момент addEventListener.

Два варианта.

Первый - вешать обработчик каждый раз когда создаём элемент.

```js
function addRow(text) {
  const li = document.createElement('li');
  li.textContent = text;
  li.addEventListener('click', () => li.remove());
  list.appendChild(li);
}
```

Работает, но если элементов сотни - сотни обработчиков. И при перерисовке списка их надо снимать.

Второй и обычно правильный - делегирование. Один обработчик на родителе ловит события от любых дочерних, в том числе будущих.

```html
<ul id="list"></ul>
```

```js
const list = document.getElementById('list');

list.addEventListener('click', (event) => {
  const li = event.target.closest('li');
  if (li) li.remove();
});

function addRow(text) {
  const li = document.createElement('li');
  li.textContent = text;
  list.appendChild(li);
}
```

Теперь добавлять можно сколько угодно элементов и обработчик заработает на каждом без дополнительных действий.

Ссылки
- https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Building_blocks/Event_bubbling
- https://developer.mozilla.org/en-US/docs/Web/API/Document/createElement
