## Валидация форм через события

В HTML есть встроенная валидация - атрибуты required, minlength, maxlength, pattern, type=email и тд. Если поле не прошло проверку - submit не сработает, вместо него браузер покажет дефолтный тултип.

Перехватить и кастомизировать можно через события invalid и submit.

```html
<form id="form" novalidate>
  <input name="email" type="email" required>
  <span class="err"></span>
  <button>отправить</button>
</form>
```

novalidate отключает дефолтные браузерные тултипы. Валидация при этом не пропадает - просто отображение остаётся на нас.

```js
const form = document.getElementById('form');
const input = form.querySelector('input');
const err = form.querySelector('.err');

input.addEventListener('input', () => {
  if (input.validity.valid) {
    err.textContent = '';
  }
});

form.addEventListener('submit', (event) => {
  if (!form.checkValidity()) {
    event.preventDefault();
    if (input.validity.valueMissing) err.textContent = 'обязательное поле';
    else if (input.validity.typeMismatch) err.textContent = 'неправильный email';
    return;
  }
});
```

У каждого input есть validity - объект с булевыми флагами для каждого типа ошибки (valueMissing, typeMismatch, tooShort, patternMismatch и тд). И validationMessage - текст ошибки от браузера.

Для своих правил - setCustomValidity.

```js
input.addEventListener('input', () => {
  if (input.value.includes(' ')) {
    input.setCustomValidity('пробелы нельзя');
  } else {
    input.setCustomValidity('');
  }
});
```

Ссылки
- https://developer.mozilla.org/en-US/docs/Learn/Forms/Form_validation
- https://developer.mozilla.org/en-US/docs/Web/API/ValidityState
