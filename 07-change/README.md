## change

Похож на input но срабатывает реже - только когда значение реально зафиксировано. Для текстовых полей это момент потери фокуса либо нажатия Enter. Для чекбоксов, радио и select - сразу при изменении.

```html
<input type="text" id="name">
<select id="lang">
  <option>js</option>
  <option>py</option>
  <option>go</option>
</select>
<input type="checkbox" id="agree">
```

```js
document.getElementById('name').addEventListener('change', (event) => {
  console.log('текст зафиксирован:', event.target.value);
});

document.getElementById('lang').addEventListener('change', (event) => {
  console.log('выбран:', event.target.value);
});

document.getElementById('agree').addEventListener('change', (event) => {
  console.log('чекбокс:', event.target.checked);
});
```

Когда использовать что - input если нужна реакция на каждое нажатие, change если нужна реакция только когда юзер закончил вводить или сделал выбор.

Ссылки
- https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/change_event
