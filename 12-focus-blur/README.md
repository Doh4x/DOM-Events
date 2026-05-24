## focus и blur

focus срабатывает когда элемент получил фокус. blur когда потерял. Оба не всплывают - это их главная особенность. Если нужен делегированный обработчик на родителе - бери focusin и focusout, они всплывают.

```html
<input id="name" placeholder="имя">
```

```js
const input = document.getElementById('name');

input.addEventListener('focus', () => {
  input.style.background = '#eef';
});

input.addEventListener('blur', () => {
  input.style.background = '';
});
```

В объекте события есть relatedTarget - куда фокус ушёл (для blur) или откуда пришёл (для focus). Может быть null если фокус ушёл с страницы.

```js
input.addEventListener('blur', (event) => {
  console.log('фокус ушёл на', event.relatedTarget);
});
```

Программно поставить фокус - element.focus(), снять - element.blur(). Получить активный элемент - document.activeElement.

По умолчанию фокус могут получать только интерактивные элементы (input, button, a, textarea и тд). Чтоб сделать фокусируемым любой элемент - tabindex="0" в HTML.

Ссылки
- https://developer.mozilla.org/en-US/docs/Web/API/Element/focus_event
- https://developer.mozilla.org/en-US/docs/Web/API/Element/blur_event
