## Объект Event

Когда событие срабатывает, в обработчик приходит объект Event. У разных типов событий он немного разный - у клика это PointerEvent, у клавиатуры KeyboardEvent, у формы SubmitEvent, но общая база одна.

Что обычно нужно

- type - имя события, например click
- target - элемент на котором событие изначально произошло
- currentTarget - элемент на котором висит текущий обработчик
- bubbles - всплывает ли событие
- cancelable - можно ли отменить дефолт
- timeStamp - момент когда событие произошло
- preventDefault() - отменить стандартное поведение
- stopPropagation() - остановить всплытие

```js
button.addEventListener('click', (event) => {
  console.log(event.type);
  console.log(event.target);
  console.log(event.currentTarget);
  event.preventDefault();
});
```

У специфичных событий есть свои свойства. У клавиатурных event.key и event.code, у мышиных event.clientX и event.clientY, у input event.data, у submit event.submitter.

```js
input.addEventListener('keydown', (event) => {
  if (event.key === 'Enter') submit();
});
```

Ссылки
- https://developer.mozilla.org/en-US/docs/Web/API/Event
