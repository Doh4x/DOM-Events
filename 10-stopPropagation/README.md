## stopPropagation

Останавливает всплытие события дальше по дереву. Все обработчики на текущем элементе отработают, но родительские обработчики уже не сработают.

```html
<div id="outer">
  <button id="inner">кнопка</button>
</div>
```

```js
document.getElementById('outer').addEventListener('click', () => {
  console.log('outer');
});

document.getElementById('inner').addEventListener('click', (event) => {
  event.stopPropagation();
  console.log('inner');
});
```

При клике по кнопке в консоли будет только inner. Без stopPropagation было бы inner и outer.

Есть ещё stopImmediatePropagation - останавливает не только всплытие, но и остальные обработчики на том же элементе.

```js
btn.addEventListener('click', (event) => {
  event.stopImmediatePropagation();
  console.log('первый');
});

btn.addEventListener('click', () => {
  console.log('второй');  // не сработает
});
```

stopPropagation часто используют не по делу. Если кажется что он нужен - обычно лучше пересмотреть архитектуру обработчиков, потому что заглушенные события могут сломать сторонние библиотеки или аналитику которые слушают document.

Ссылки
- https://developer.mozilla.org/en-US/docs/Web/API/Event/stopPropagation
