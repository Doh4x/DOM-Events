## closest

Метод элемента. Ищет ближайшего предка (включая сам элемент) который подходит под CSS-селектор. Если ничего не нашёл - возвращает null.

```js
element.closest(selector)
```

```html
<article>
  <div class="card">
    <button>удалить</button>
  </div>
</article>
```

```js
const btn = document.querySelector('button');

btn.closest('.card');     // div.card
btn.closest('article');   // article
btn.closest('section');   // null
btn.closest('button');    // сам btn
```

Главное применение - в делегировании. Кликнули где-то внутри карточки, нужно достать саму карточку.

```js
document.addEventListener('click', (event) => {
  const card = event.target.closest('.card');
  if (!card) return;
  card.classList.toggle('selected');
});
```

Без closest пришлось бы вручную проверять event.target и его родителей циклом. С closest всё в одну строку.

Селектор может быть любым валидным CSS-селектором - комбинированным, с псевдоклассами, с атрибутами.

```js
event.target.closest('[data-action="delete"]');
event.target.closest('li:not(.disabled)');
```

Ссылки
- https://developer.mozilla.org/en-US/docs/Web/API/Element/closest
