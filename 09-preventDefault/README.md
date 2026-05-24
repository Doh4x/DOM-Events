## preventDefault

Метод на объекте события. Отменяет действие которое браузер сделал бы по умолчанию. На submit форма не отправится, на клике по ссылке не будет перехода, на правом клике не появится контекстное меню, на нажатии Enter в input не сработает дефолтное поведение.

```js
form.addEventListener('submit', (event) => {
  event.preventDefault();
});

link.addEventListener('click', (event) => {
  event.preventDefault();
});

document.addEventListener('contextmenu', (event) => {
  event.preventDefault();
});
```

Сам обработчик при этом отрабатывает до конца. preventDefault не останавливает выполнение функции и не останавливает всплытие - для этого есть stopPropagation.

Работает только на событиях у которых cancelable равен true. У scroll, например, отменить нельзя.

```js
element.addEventListener('click', (event) => {
  if (!event.cancelable) return;
  event.preventDefault();
});
```

В passive листенере preventDefault не сработает и в консоль прилетит варнинг. Это сделано чтоб браузер мог не блокировать скролл в ожидании ответа от JS.

Ссылки
- https://developer.mozilla.org/en-US/docs/Web/API/Event/preventDefault
