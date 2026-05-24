## this и стрелочные функции в обработчиках

В обычной function-обработчике this это элемент на котором висит обработчик. То же что и event.currentTarget.

```js
btn.addEventListener('click', function (event) {
  console.log(this);            // сам btn
  console.log(this === event.currentTarget);  // true
});
```

В стрелочной функции своего this нет - он берётся из внешней области видимости. Внутри обработчика-стрелки this будет тем же чем он был там где функция объявлена. Если объявлена в модуле верхнего уровня - undefined либо window.

```js
btn.addEventListener('click', (event) => {
  console.log(this);            // не btn, а внешний this
  console.log(event.currentTarget);  // btn - этим и пользуемся
});
```

Поэтому в обработчиках чаще пишут стрелку - проще, нет неожиданностей с this, доступ к элементу через event.currentTarget или замыкание.

Где стрелка стреляет в ногу - в классах если делать метод обработчиком.

```js
class Widget {
  constructor(el) {
    this.el = el;
    this.el.addEventListener('click', this.handle);  // плохо - this в handle будет el, а не Widget
    this.el.addEventListener('click', this.handle.bind(this));  // ок
    this.el.addEventListener('click', (e) => this.handle(e));   // ок
  }
  handle() {
    console.log(this.el);
  }
}
```

Либо объявить метод стрелкой как class field - тогда this всегда привязан к инстансу.

```js
class Widget {
  handle = (event) => {
    console.log(this);  // инстанс Widget
  }
}
```

Ссылки
- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/this
- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions
