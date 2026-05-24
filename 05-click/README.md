## click

Срабатывает когда юзер кликнул по элементу. Под кликом понимается любое нажатие - мышью, тачем, либо нажатие Enter или Space на сфокусированной кнопке. Тип события PointerEvent, наследник MouseEvent.

```html
<button>жми</button>
```

```js
const btn = document.querySelector('button');

btn.addEventListener('click', (event) => {
  console.log('кликнули');
});
```

У event есть detail - счётчик подряд идущих кликов. Один клик это 1, двойной 2, тройной 3. Если пауза между кликами - сбрасывается.

```js
btn.addEventListener('click', (event) => {
  btn.textContent = `кликов: ${event.detail}`;
});
```

Сам click срабатывает после mousedown и mouseup. Если нужно реагировать раньше - используй их.

Координаты клика лежат в clientX/clientY относительно окна и pageX/pageY относительно документа.

```js
document.addEventListener('click', (event) => {
  console.log(event.clientX, event.clientY);
});
```

Ссылки
- https://developer.mozilla.org/en-US/docs/Web/API/Element/click_event
