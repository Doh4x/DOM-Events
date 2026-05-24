## debounce для input

input стреляет на каждый символ. Если на каждом символе делать запрос на сервер или тяжёлые вычисления - всё ляжет. Debounce задерживает вызов и сбрасывает таймер при каждом новом вызове, так что функция выполнится только после паузы.

```js
function debounce(fn, delay) {
  let timer;
  return function (...args) {
    clearTimeout(timer);
    timer = setTimeout(() => fn.apply(this, args), delay);
  };
}
```

Применение к поиску.

```html
<input id="search" placeholder="поиск">
```

```js
const search = document.getElementById('search');

const onSearch = debounce((event) => {
  fetch('/api/search?q=' + encodeURIComponent(event.target.value))
    .then(r => r.json())
    .then(render);
}, 300);

search.addEventListener('input', onSearch);
```

Если юзер печатает быстро - запрос уйдёт только через 300мс после последнего нажатия.

Похожая штука throttle - вызывает функцию не чаще раз в N мс. Для поиска подходит debounce, для scroll или resize обычно throttle. Готовые реализации есть в lodash (\_.debounce, \_.throttle).

Ссылки
- https://developer.mozilla.org/en-US/docs/Web/API/Element/input_event
- https://developer.mozilla.org/en-US/docs/Web/API/Window/setTimeout
