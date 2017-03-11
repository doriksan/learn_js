# learn_js

## Видео 1. Замыкания, область видимости. Глобальный объект

### Глобальный объект

Для программиста, использующего в работе javascript, очень важно понимание [области видимости](d) и замыканий,
так как механизм работы функций и переменных в JavaScript очень отличается от большинства языков.

В этом видео я расскажу про переменные и функции в глобальной области. В браузере глобальная область представлена объектом window. 

Важно! Переменные и функции, которые не находятся внутри какой-то функции, называются глобальными. Они являются свойствами объекта window.

Давайте напишем код, который объявляет переменную, присваивает ей какое-то значение, а потом выводит ее через алерт, обращаясь к ней, как к свойству глобального объекта window:

```javascript
var a = 5;
alert( window.a );
```

Теперь напишем код, который создает переменную с явным присваиванием в window:
```javascript
window.a = 5;
alert( a );
```

###  Порядок инициализации

Выполнение скрипта происходит в две фазы:

1. Первая фаза - инициализация, во время которой скрипт сканируется на предмет объявления функций вида Function Declaration, а затем на предмет объявления переменных var. Каждое такое объявление добавляется в window. Важно! Функции, объявленные как Function Declaration, создаются сразу работающими, а переменные – равными undefined.

2. Вторая фаза - выполнение. Присваивание значений переменных происходит, когда поток выполнения доходит до соответствующей строчки кода, до этого они undefined.

Тот факт, что к началу выполнения кода переменные и функции уже содержатся в window, можно легко проверить, выведя их:

```javascript
alert("a" in window); // true,  т.к. есть свойство window.a
alert(a); // равно undefined,  присваивание будет выполнено далее
alert(f); // function ...,  готовая к выполнению функция
alert(g); // undefined, т.к. это переменная, а не Function Declaration

var a = 5;
function f() { /*...*/ }
var g = function() { /*...*/ };
```
Итак, мы говорим про глобальный объект window, в который попадают переменные и функции, которые не находятся внутри какой-то функции. При этом важно понимать, что конструкции for, if, в которых также, как и в функциях, используются фигурные скобки, не влияют на область видимости.

### Объявление переменной

Не важно, где и сколько раз объявлена переменная. Объявлений var может быть сколько угодно:

```javascript
var i = 10;

for (var i = 0; i < 20; i++) {
  ...
}

var i = 5;
```

Все var будут обработаны один раз, на фазе инициализации. На фазе исполнения объявления var будут проигнорированы: они уже были обработаны. Зато будут выполнены присваивания.

### Задачи 
Задача 1: Что выведет алерт в этой и следующих задачах?
```javascript
if ("a" in window) {
  var a = 1;
}
alert( a );
```
Задача 2:
```javascript
if ("a" in window) {
  a = 1;
}
alert( a );
```
Задача 3:
```javascript
if ("a" in window) {
  a = 1;
}
var a;

alert( a );
```





