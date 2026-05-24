## removeEventListener

Снимает обработчик который раньше повесили через addEventListener. Чтоб снять обработчик надо передать ровно ту же функцию и тот же флаг capture.

```js
function handler(event) {
  console.log('клик');
}

btn.addEventListener('click', handler);
btn.removeEventListener('click', handler);
```

Анонимную функцию снять нельзя - на неё нет ссылки.

```js
btn.addEventListener('click', () => console.log('hi'));
btn.removeEventListener('click', () => console.log('hi'));  // не сработает - другая функция
```

Если повесили с capture: true - снимать тоже надо с capture: true. Остальные опции (once, passive) при снятии игнорируются, важен только capture.

Современная альтернатива - AbortController. Удобно когда надо снять сразу несколько листенеров одной командой.

```js
const ctrl = new AbortController();

btn.addEventListener('click', onClick, { signal: ctrl.signal });
window.addEventListener('resize', onResize, { signal: ctrl.signal });
document.addEventListener('keydown', onKey, { signal: ctrl.signal });

ctrl.abort();  // снимет все три
```

Снимать листенеры важно когда элемент удаляется из DOM а функция держит ссылку на что-то крупное - иначе утечка памяти. Если элемент удаляется и больше не появится - GC сам всё уберёт.

Ссылки
- https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/removeEventListener
- https://developer.mozilla.org/en-US/docs/Web/API/AbortController
