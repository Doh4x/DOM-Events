## DOMContentLoaded

Срабатывает на document когда HTML распарсен и отложенные скрипты (defer, type=module) выполнены. Картинки, стили, async-скрипты и iframe ждать не будет - для этого есть load.

Нужен когда скрипт в head без defer и хочет работать с DOM который ещё не дошёл до конца страницы.

```js
document.addEventListener('DOMContentLoaded', () => {
  const btn = document.querySelector('button');
  btn.addEventListener('click', handler);
});
```

Если скрипт подключён с defer либо стоит в конце body перед закрывающим тегом - DOMContentLoaded не нужен, к моменту выполнения скрипта DOM уже готов.

Тонкий момент. Если скрипт async или подгружается динамически - он может выполниться уже после DOMContentLoaded. Тогда обработчик никогда не сработает. Чтобы не упустить момент, проверяй readyState.

```js
function init() {
  // работа с DOM
}

if (document.readyState === 'loading') {
  document.addEventListener('DOMContentLoaded', init);
} else {
  init();
}
```

Ссылки
- https://developer.mozilla.org/en-US/docs/Web/API/Document/DOMContentLoaded_event
