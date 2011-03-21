## `undefined` и `null`

В JavaScript есть два отдельных типа для представления `ничего`, при этом более полезным из них является `undefined`.

### Тип `undefined`

`undefined` — это тип с единственным возможным значением: `undefined`.

Кроме этого, в языке определена глобальная переменная со значением `undefined`, и эта переменная так и называется — `undefined`. Не являясь константой, она не является и ключевым словом. Из этого следует, что её значение можно с лёгкостью переопределить.

> **ES5 Замечание:** в ECMAScript 5 переменная `undefined` **больше не** *доступна на запись* в strict-режиме, однако она всё также может быть перегружена по имени, например - функцией с именем `undefined`.

Несколько случаев, когда возвращается `undefined`:

 - При попытке доступа к глобальной переменной `undefined` (если она не изменена).
 - Неявный возврат из функции при отсутствия в ней оператора `return`.
 - Из операторов `return`, которые ничего не возвращают.
 - В результате поиска несуществующего свойства у объекта (и доступа к нему).
 - Параметры, которые не были переданы в функцию явно.
 - При доступе ко всему, чьим значением является `undefined`.

### Обработка изменений значения `undefined`

Поскольку глобальная переменная `undefined` содержит копию настоящего *значения* `undefined`, присвоение этой переменной нового значения **не** изменяет значения *типа* `undefined`.

Но при этом, чтобы сравнить что-либо со *значением* `undefined` прежде нужно получить значение самой *переменной* `undefined`.

Чтобы защитить код от переопределения переменной `undefined`, часто используется техника [анонимной обёртки](#function.scopes), которая использует отсутствующий аргумент.

    var undefined = 123;
    (function(something, foo, undefined) {
        // в локальной области видимости `undefined`
        // снова ссылается на правильное значене.

    })('Hello World', 42);

Другой способ достичь того же эффекта — использовать определение внутри обёртки.

    var undefined = 123;
    (function(something, foo) {
        var undefined;
        ...

    })('Hello World', 42);

Единственная разница между этими вариантами в том, что последняя версия будет больше на 4 байта при минификации, а в первом случае внутри анонимной обёртки нет дополнительного оператора `var`.

### Использование `null`

Хотя `undefined` в контексте языка JavaScript чаще используется в качестве традиционного *null*, настоящий `null` (и тип и литерал) является в большей или меньшей степени просто другим типом данных.

Он используется во внутренних механизмах JavaScript (например для определения конца цепочки прототипов засчёт присваивания `Foo.prototype = null`). Но в большинстве случаев тип `null` может быть заменён на `undefined`.
