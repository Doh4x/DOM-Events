## scroll

Срабатывает когда что-то проскроллили - document, window или конкретный элемент с overflow. Не всплывает с элементов на document. Не отменяется (event.cancelable === false), preventDefault внутри не сработает.

```js
window.addEventListener('scroll', () => {
  console.log(window.scrollY);
});
```

Событие стреляет очень часто - десятки раз в секунду при активном скролле. Тяжёлые операции внутри убьют производительность. Варианты борьбы.

Throttle через флаг и таймаут.

```js
let ticking = false;

window.addEventListener('scroll', () => {
  if (ticking) return;
  ticking = true;
  setTimeout(() => {
    doStuff(window.scrollY);
    ticking = false;
  }, 100);
});
```

Через requestAnimationFrame - откладывает работу до следующего кадра.

```js
let ticking = false;

window.addEventListener('scroll', () => {
  if (ticking) return;
  ticking = true;
  requestAnimationFrame(() => {
    doStuff(window.scrollY);
    ticking = false;
  });
});
```

Passive-флаг говорит браузеру что preventDefault точно не будет, и тогда он не блокирует скролл в ожидании JS. Для scroll это даёт прирост FPS особенно на мобильных.

```js
window.addEventListener('scroll', onScroll, { passive: true });
```

Если задача - узнать что элемент попал в зону видимости, скролл-обработчик это плохой инструмент. Лучше IntersectionObserver - он не дёргается на каждый пиксель, а зовёт колбэк только когда порог пересечён.

Ссылки
- https://developer.mozilla.org/en-US/docs/Web/API/Document/scroll_event
- https://developer.mozilla.org/en-US/docs/Web/API/IntersectionObserver
