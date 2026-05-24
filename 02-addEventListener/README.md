## addEventListener

Стандартный способ повесить обработчик на элемент. Главное преимущество перед onclick - можно вешать сколько угодно обработчиков на одно и то же событие, они не перетирают друг друга.

```js
target.addEventListener(type, listener)
target.addEventListener(type, listener, options)
```

Тип это строка типа click, input, submit. Листенер это функция. Опции это объект с настройками либо булево значение useCapture для совсем старого кода.

```js
const btn = document.querySelector('button');

btn.addEventListener('click', (event) => {
  console.log('кликнули');
});
```

Полезные опции

once - сработает один раз и сам отвалится.

```js
btn.addEventListener('click', () => console.log('один раз'), { once: true });
```

passive - обещаешь что не будешь вызывать preventDefault. Браузер от этого не тормозит скролл и тач-события.

```js
window.addEventListener('scroll', onScroll, { passive: true });
```

capture - ловить событие на фазе погружения, а не всплытия. Нужно редко.

signal - современная замена removeEventListener через AbortController.

```js
const ctrl = new AbortController();
btn.addEventListener('click', handler, { signal: ctrl.signal });
ctrl.abort();
```

Ссылки
- https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/addEventListener
