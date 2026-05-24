## submit

Срабатывает на форме когда её отправляют. Отправить можно тремя способами - нажать submit-кнопку, нажать Enter в поле формы, вызвать form.requestSubmit() из JS. Прямой вызов form.submit() событие не вызывает.

Событие висит на самой форме, не на кнопке.

```html
<form id="form">
  <input name="email" type="email" required>
  <button type="submit">отправить</button>
</form>
```

```js
const form = document.getElementById('form');

form.addEventListener('submit', (event) => {
  event.preventDefault();
  const data = new FormData(form);
  console.log(Object.fromEntries(data));
});
```

preventDefault нужен почти всегда - иначе браузер перезагрузит страницу либо перейдёт по action атрибуту.

В event.submitter лежит конкретная кнопка которой отправили форму. Удобно если у формы несколько кнопок типа Save и Save as draft.

```js
form.addEventListener('submit', (event) => {
  event.preventDefault();
  if (event.submitter.name === 'draft') saveDraft();
  else send();
});
```

Если форма не прошла встроенную валидацию (required, pattern и тд) - submit не сработает, вместо него полетит invalid.

Ссылки
- https://developer.mozilla.org/en-US/docs/Web/API/HTMLFormElement/submit_event
