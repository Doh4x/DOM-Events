## Делегирование событий

Идея в том чтобы вместо навешивания обработчика на каждый из десятков дочерних элементов повесить один обработчик на их общего родителя. Когда событие всплывёт - оно попадёт в родительский обработчик, а из event.target можно понять по какому именно дочернему элементу кликнули.

```html
<ul id="todos">
  <li data-id="1">купить хлеб</li>
  <li data-id="2">помыть посуду</li>
  <li data-id="3">выгулять кота</li>
</ul>
```

```js
const list = document.getElementById('todos');

list.addEventListener('click', (event) => {
  const li = event.target.closest('li');
  if (!li) return;
  console.log('кликнули по', li.dataset.id);
});
```

Плюсы - один обработчик вместо ста, работает для динамически добавленных элементов автоматически, меньше памяти, меньше кода.

Минусы - не работает для событий которые не всплывают (focus, blur, mouseenter). Для них надо использовать focusin/focusout или ставить capture: true.

Типичная связка - делегирование + closest + data-атрибуты. Кликнули по таблице - нашли через closest строку - прочитали data-id - сделали действие.

Ссылки
- https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Building_blocks/Event_bubbling
