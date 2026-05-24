## data-* атрибуты

Любой HTML-атрибут начинающийся с data- считается кастомным и не валидирует страницу. Хранят в нём данные которые нужны JS, но не несут смысла для HTML.

```html
<button data-action="delete" data-id="42">удалить</button>
<li data-user-id="7" data-role="admin">Иван</li>
```

Из JS доступ через свойство dataset. Имена конвертируются из kebab-case в camelCase.

```js
const btn = document.querySelector('button');

btn.dataset.action;  // 'delete'
btn.dataset.id;      // '42'

const li = document.querySelector('li');
li.dataset.userId;   // '7' (из data-user-id)
li.dataset.role;     // 'admin'
```

Всегда строка. Если надо число - parseInt либо Number. Если объект - JSON.parse.

Записать и удалить тоже можно через dataset.

```js
btn.dataset.state = 'loading';   // добавит data-state="loading"
delete btn.dataset.state;        // уберёт атрибут
```

Идеально сочетается с делегированием - в обработчике на родителе смотришь dataset у event.target.closest и понимаешь что делать.

```js
table.addEventListener('click', (event) => {
  const trigger = event.target.closest('[data-action]');
  if (!trigger) return;
  const { action, id } = trigger.dataset;
  if (action === 'delete') deleteRow(id);
  if (action === 'edit') editRow(id);
});
```

Ссылки
- https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/data-*
- https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/dataset
