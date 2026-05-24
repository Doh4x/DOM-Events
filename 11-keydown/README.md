## keydown

Срабатывает когда юзер нажал клавишу. Работает для любых клавиш - букв, цифр, модификаторов, стрелок, F1-F12. Бывает ещё keyup (отпустили) и устаревший keypress (не использовать).

Если клавишу держат - keydown повторяется. Распознать повтор можно по event.repeat.

```js
document.addEventListener('keydown', (event) => {
  console.log(event.key);   // 'a', 'Enter', 'ArrowLeft'
  console.log(event.code);  // 'KeyA', 'Enter', 'ArrowLeft'
});
```

key это что юзер ввёл с учётом раскладки и Shift. code это физическая клавиша вне зависимости от раскладки. Для горячих клавиш типа Ctrl+S обычно берут code, потому что на русской раскладке key будет 'ы' вместо 's'.

```js
document.addEventListener('keydown', (event) => {
  if (event.ctrlKey && event.code === 'KeyS') {
    event.preventDefault();
    save();
  }
});
```

Модификаторы лежат в event.ctrlKey, event.shiftKey, event.altKey, event.metaKey (Win/Cmd).

Для полей с поддержкой IME (китайский, японский) лучше игнорировать события во время композиции.

```js
input.addEventListener('keydown', (event) => {
  if (event.isComposing) return;
  // обработка
});
```

Ссылки
- https://developer.mozilla.org/en-US/docs/Web/API/Element/keydown_event
- https://developer.mozilla.org/en-US/docs/Web/API/KeyboardEvent
