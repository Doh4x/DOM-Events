## mouseenter и mouseleave

mouseenter срабатывает когда курсор вошёл в границы элемента. mouseleave когда вышел. Не всплывают и не срабатывают при движении между родителем и его дочерними элементами - это их главное отличие от mouseover и mouseout.

```html
<div id="box">наведи</div>
```

```js
const box = document.getElementById('box');

box.addEventListener('mouseenter', () => {
  box.style.background = '#eef';
});

box.addEventListener('mouseleave', () => {
  box.style.background = '';
});
```

В чём разница с mouseover/mouseout. Если у тебя div и внутри него span, то на mouseover при наведении на span событие сработает на span, всплывёт до div и сработает на нём ещё раз. При уходе со span на div сработает mouseout на span и mouseover на div. Дёрганина.

mouseenter и mouseleave срабатывают ровно один раз когда курсор зашёл в div и один раз когда вышел из всей его области, как бы он внутри ни двигался.

Поскольку не всплывают - для делегирования не подходят. Если нужно отслеживать наведение на много элементов, либо вешать на каждый, либо использовать mouseover/mouseout с проверкой relatedTarget, либо capture: true.

На тач-устройствах не срабатывает - там нет курсора. Для тач-эффектов нужны touch- или pointer-события.

Ссылки
- https://developer.mozilla.org/en-US/docs/Web/API/Element/mouseenter_event
- https://developer.mozilla.org/en-US/docs/Web/API/Element/mouseleave_event
