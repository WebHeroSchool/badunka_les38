###1.Избегайте глобальных переменных [##`1`](https://github.com/WebHeroSchool/badunka_les38/##`1`)

## 1.Избегайте глобальных переменных ##`1`

+ Глобальные переменные легко переписать в различных местах кода, потому что они везде доступны.
+ Глобальные переменные могут переписывать объект window, так как являются свойствами объекта window.

 :wink:  _Пример_ :
 ```
 const log = () => {
   console.log(x);
 }
 log(); // получим undefined
 let x = 1;
 log(); // получим 1
 ```


## 2.Всегда объявляйте локальные переменные.

+ Нужно всегда объявлять локальные переменные и постоянные также с помощью  let или const. В противном случае переменная будет объявлена как глобальная и как свойство объекта window.
😠  _Плохой ример_ :
```
x = 1;
```
:wink:  _Хороший пример_ :
```
let x = 1;
```
 *JavaScript strict mode (строгий режим) не позволяет необъявленные переменные, поэтому случайно создать глобальные переменные нельзя.*

## 3.Всегда инициализируйте переменные и константы наверху

+ Объявление переменных  вверху файла делает код чище.
+ Это помешает случайно ссылаться на переменные.
+ Уменьшает возможность нежелательных повторных объявлений.

😠  _Плохой ример_ :
```
let x, y;
x = 1;
y = 1;
console.log(x, y);
```
:wink:  _Хороший пример_ :
```
let x = 1;
let y = 1;
console.log(x, y);
```
## 4.Никогда не объявляйте числовые (number), строковые (string) или логические (boolean) объекты

+ Числа, строки, логические значения - это всё примитивные значения.
+ Объявление этих типов в качестве объектов замедляет скорость выполнения.
+ Может приводить к странным ошибкам.

😠  _Пример_ :
```
let x = "Андрей";             
let y = new String("Андрей");
(x === y) // false, потому что x - строка, а y - объект.
```
😠  _Пример_ :
```
var x = new String("1");             
var y = new String("1");
(x == y) // false, потому что нельзя сравнивать объекты
```
## 5.Не используйте new Object()

+ Используйте {} вместо new Object()
+ Используйте 0 вместо new Number()
+ Используйте false вместо new Boolean()
+ Используйте [] вместо new Array()
+ Используйте /()/ вместо new RegExp()
+ Используйте function (){} вместо new Function()

:wink:  _Пример_ :
```
let x1 = {};           // new object
let x2 = "";           // new primitive string
let x3 = 0;            // new primitive number
let x4 = false;        // new primitive boolean
let x5 = [];           // new array object
let x6 = /()/;         // new regexp object
let x7 = function(){}; // new function object
```
*Это сильно упрощает код и повышает читабельность.*

## 6.Остерегайтесь автоматических преобразований типов

+ Числа могут быть случайно преобразованы в строки или NaN.
+ Переменная может содержать разные типы данных, при этом в ходе кода может изменять свой тип данных:
+ При выполнении математических операций JavaScript может преобразовывать числа в строки.
+ Вычитание строки из строки не генерирует ошибку, но возвращает NaN.

:wink:  _Пример_ :
```
var x = 8 + 1;       // ответ: 9,  тип x является числом
var x = 8 + "1";     // ответ: 81,  тип x является строкой
var x = "8" + 1;     // ответ: 81,  тип x является строкой
var x = 8 - 1;       // ответ: 7,  тип x является числом
var x = 8 - "1";     // ответ: 7,  тип x является числом
var x = "8" - 1;     // ответ: 7,  тип x является числом
var x = 8 - "x";     // ответ: NaN, тип x является числом
```
## 7.Используйте === Сравнение
+ Оператор === вызывает сравнение значений и типа, в то время == преобразует в соответсвующие типы перед сранением.

:wink:  _Пример_ :
```
0 == "";        // true
12 == "12";     // true
1 == true;      // true

0 === "";       // false
12 === "12";    // false
1 === true;     // false
```
## 8.Используйте параметры по умолчанию
+ Если функция вызывается с _отсутствующими аргументами_ (меньше объявленного), отсутствующие значения устанавливаются в: _undefined_.

:wink:  _Пример_ :
```
function myFunction(x, y) {
  if (y === undefined) {
    y = 0;
  }
}

```
*Неопределенные значения могут нарушить ваш код, но если вы уверены в том, что это не помешает, то можно опускать явное присвоение _undefined_*

+ ECMAScript 2015 позволяет значения параметров по умолчанию в объявлении функции:

:wink:  _Пример_ :
```
function myFunction(x, y = 10) {
  // y равен 10 если не пройден или не определен
  return x + y;
}
myFunction(5); // вернёт 15

```
## 9.Всегда завершайте переключатели (switch) по умолчанию

+ Всегда завершайте операторы switch значением default. Даже если вы думаете, что в этом нет необходимости.

:wink:  _Пример_ :
```
switch (new Date().getMonth()) {
  case 0:
    month = "January";
    break;
  case 1:
    month = "February";
    break;
  case 2:
    month = "March";
    break;
  case 3:
    month = "April";
    break;
  case 4:
    month = "May";
    break;
  case 5:
    month = "June";
    break;
  case 6:
    month = "July";
    break;
  default:
    month = "Unknown";
}
```
*Блок кода после default будет выполняться, только если ни один case не совпал со значением переключателя.*

## 10.Избегайте использования eval ()
+ Функция eval() используется для запуска текста как кода.
+ eval() - опасная функция, которая выполняет код, проходящий со всеми привилегиями вызывателя. Если вы запускаете eval() со строкой, на которую могут влиять злоумышленники, то вы можете запустить вредоносный код на устройство пользователя с правами вашей веб-страницы/расширения.
+ Наиболее важно, код третьей стороны может видеть область видимости, в которой был вызван eval().
+ eval(),как правило, медленнее альтернатив, так как вызывает интерпретатор JS, тогда как многие другие конструкции оптимизированы современными JS движками.

😠  _Плохой ример_ :
```
let obj = { a: 20, b: 30 };
let propname = getPropName();  // возвращает "a" или "b"

eval( "let result = obj." + propname );
```
:wink:  _Хороший пример_ :
```
let obj = { a: 20, b: 30 };
let propname = getPropName();  // возвращает "a" или "b"
let result = obj[ propname ];  //  obj[ "a" ] то же, что и obj.a
```
