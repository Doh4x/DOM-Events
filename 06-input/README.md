## input

Срабатывает каждый раз когда значение input, textarea или select меняется по действию юзера. На каждом нажатии клавиши, на каждой вставке текста, на каждом изменении чекбокса. Программное изменение value через JS событие не вызывает.

```html
<input placeholder="введи что-нибудь">
<p id="out"></p>
```

```js
const input = document.querySelector('input');
const out = document.getElementById('out');

input.addEventListener('input', (event) => {
  out.textContent = event.target.value;
});
```

Для текстовых полей объект события это InputEvent. У него есть data - что именно вставили, и inputType - что произошло (insertText, deleteContentBackward и тд).

```js
input.addEventListener('input', (event) => {
  console.log(event.data);       // 'a' если ввели a
  console.log(event.inputType);  // 'insertText'
});
```

Хорошо подходит для живой валидации, поиска по мере ввода, счётчиков символов. Обычно в паре с debounce чтоб не дёргать обработчик на каждом символе.

Ссылки
- https://developer.mozilla.org/en-US/docs/Web/API/Element/input_event
