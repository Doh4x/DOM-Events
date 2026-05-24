## async/await в обработчиках

Обработчик можно объявить как async и внутри использовать await. Браузер ждать его не будет - сам обработчик вернёт promise, который никто не читает.

```js
form.addEventListener('submit', async (event) => {
  event.preventDefault();
  const data = new FormData(form);
  const response = await fetch('/api/save', { method: 'POST', body: data });
  const result = await response.json();
  render(result);
});
```

Важно вызвать preventDefault до первого await. После await текущий цикл событий закончится и preventDefault уже не отменит дефолт - браузер успеет отправить форму.

```js
form.addEventListener('submit', async (event) => {
  event.preventDefault();         // до await
  const data = await loadData();
  // ...
});
```

Ошибки внутри async-обработчика не ловятся try/catch снаружи. Либо try/catch внутри, либо глобальный unhandledrejection.

```js
btn.addEventListener('click', async () => {
  try {
    const data = await fetch('/api');
    // ...
  } catch (e) {
    showError(e);
  }
});
```

Часто нужно блокировать кнопку пока запрос летит - иначе юзер накликает десять раз.

```js
btn.addEventListener('click', async () => {
  btn.disabled = true;
  try {
    await send();
  } finally {
    btn.disabled = false;
  }
});
```

Ссылки
- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/async_function
- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/await
