# 1. JavaScript и асинхронное программирование — ответы

> Статус: `частично готово — ответы 1.1 и 1.2 одобрены; ответы 1.3 готовы к пользовательскому review; 1.4–1.12 остаются placeholders`
>
> Вопросы: [отдельный файл с условиями](../../by-domain/01-javascript-and-async-programming.md)
>
> Разделы 1.3–1.12 остаются заглушками.

## 1.1. Модель выполнения, объявления и область видимости (Execution Model, Declarations & Scope)

Это эталонные ответы и критерии оценки, а не тексты, которые нужно повторять дословно.

### JS-SCOPE-Q01

[Вернуться к вопросу](../../by-domain/01-javascript-and-async-programming.md#js-scope-q01)

Короткое сравнение:

- `var` ограничен ближайшей функцией, но не обычным блоком. Новая привязка заранее получает `undefined`. Её можно переназначать и обычно можно ещё раз объявить через `var` в той же области.
- `let` обычно ограничен блоком. До инициализации он находится в **временной мёртвой зоне (Temporal Dead Zone, TDZ)**. Его можно переназначать, но нельзя повторно объявить в той же области.
- `const` ведёт себя как `let` по scope и TDZ, но требует инициализатор и запрещает переназначение. Сам объект при этом не замораживается.

Точная деталь: совместимое повторное объявление `var` использует уже существующую привязку и не сбрасывает её значение обратно в `undefined`.

Практическое правило для рабочего кода (**production code**): по умолчанию использовать `const`, а при намеренном повторном присваивании — `let`. Новый код с `var` лучше не писать, но его нужно понимать для поддержки устаревшего кода (**legacy code**), отладки и интервью.

Признаки сильного ответа:

- кандидат различает инициализацию и последующее присваивание;
- не говорит, что `let` и `const` «не поднимаются»;
- отличает неизменяемую привязку от неизменяемого объекта;
- формулирует современное правило для рабочего кода.

### JS-SCOPE-Q02

[Вернуться к вопросу](../../by-domain/01-javascript-and-async-programming.md#js-scope-q02)

- **Глобальная область (global scope)** — внешний уровень скрипта и его среды. Точные правила зависят от способа запуска кода.
- **Функциональная область (function scope)** содержит параметры и локальные объявления функции. Каждый вызов получает свой набор таких привязок; `var` ограничен ближайшей функцией.
- **Блочная область (block scope)** ограничивает `let`, `const` и `class` в блоках, циклах, `catch` и общем `CaseBlock` у `switch`.
- **Модульная область (module scope)** принадлежит конкретному ES module. Его объявления верхнего уровня не становятся свойствами глобального объекта.

**Лексическая область видимости (lexical scope)** — не пятый вид границы. Это правило: функция ищет внешние имена по месту, где она написана, а не по месту вызова. В точной модели поиск начинается в текущей **Environment Record** и идёт наружу по `[[OuterEnv]]`.

### JS-SCOPE-Q03

[Вернуться к вопросу](../../by-domain/01-javascript-and-async-programming.md#js-scope-q03)

В `let count = 1; count = 2;` происходят разные события:

1. объявление сообщает, что в этой области есть имя `count`;
2. до выполнения строки JavaScript создаёт неинициализированную привязку `count`;
3. `let count = 1` впервые делает её доступной со значением `1` — это initialization;
4. `count = 2` меняет значение уже работающей привязки — это assignment.

Это различие и объясняет TDZ: привязка уже существует, но читать её до initialization нельзя. `const` разрешает одну обязательную инициализацию; запрещено только последующее assignment.

### JS-SCOPE-Q04

[Вернуться к вопросу](../../by-domain/01-javascript-and-async-programming.md#js-scope-q04)

1. `console.log(a)` выводит `undefined`. Привязка `var` уже создана и инициализирована, но присваивание из инициализатора ещё не выполнилось.
2. Чтение `b` выбрасывает `ReferenceError`. Лексическая привязка существует, но находится в TDZ и ещё не инициализирована.
3. `typeof c` тоже выбрасывает `ReferenceError`: оператор `typeof` не обходит TDZ существующей привязки.
4. `typeof neverDeclared` возвращает строку `"undefined"`. Здесь идентификатор вообще не разрешается, а не ссылается на существующую неинициализированную привязку.

Каждый фрагмент нужно рассматривать как независимый скрипт. В одном скрипте первое необработанное исключение остановило бы дальнейшее выполнение.

### JS-SCOPE-Q05

[Вернуться к вопросу](../../by-domain/01-javascript-and-async-programming.md#js-scope-q05)

1. Вызов объявления функции выполняется успешно. Его привязка получает объект функции ещё при обработке объявлений.
2. Вариант с `var` выбрасывает `TypeError`. Имя `ready` успешно разрешается, но в этот момент содержит `undefined`, а это значение нельзя вызвать.
3. Вариант с `const` выбрасывает `ReferenceError`. Чтение `ready` происходит в TDZ.

Сам объект **функционального выражения (function expression)** создаётся только при вычислении выражения. Поэтому поведение до этой строки определяется объявлением, в котором хранится выражение: `var`, `let` или `const`.

### JS-SCOPE-Q06

[Вернуться к вопросу](../../by-domain/01-javascript-and-async-programming.md#js-scope-q06)

**Затенение (shadowing)** возникает, когда во вложенных областях есть разные привязки с одинаковым именем. **Повторное объявление (redeclaration)** пытается объявить имя ещё раз в той же эффективной области.

Первый фрагмент корректен: `var mode` принадлежит внешней области `var`, а внутри блока создаётся отдельная лексическая привязка `mode`.

Во втором фрагменте возникает ранний `SyntaxError` — **ранняя статическая ошибка (Early Error)**. Объявление `var` не ограничено блоком и должно было бы попасть во внешнюю область `var`, где оно конфликтует с лексическим `mode`. На интервью это часто называют «недопустимым затенением (illegal shadowing)», но точнее говорить о конфликте объявлений из-за того, что `var` выходит за границу блока.

### JS-SCOPE-Q07

[Вернуться к вопросу](../../by-domain/01-javascript-and-async-programming.md#js-scope-q07)

В нестрогом классическом скрипте (**sloppy classic script**) присваивание неразрешимому имени `total` может создать свойство глобального объекта. В строгом режиме (**strict mode**) то же присваивание выбрасывает `ReferenceError`. Код ES-модулей всегда строгий.

Минимальное исправление:

```js
function update(items) {
  const total = items.length;
  return total;
}
```

Если значение нужно другому владельцу, его лучше вернуть из функции или записать в явно переданный объект состояния. Скрытая запись в глобальное состояние для этого не нужна.

Предотвратить дефект помогают ES-модули или строгий режим, правило линтера `no-undef`, проверка типов и тест, который убеждается, что лишнее глобальное свойство не появилось.

Если имя прежде не существовало, а глобальный объект — обычный и расширяемый, первое нестрогое присваивание создаёт на нём настраиваемое свойство. Поэтому `delete globalThis.total` явно удаляет свойство и обычно возвращает `true`. Существующее свойство или особое поведение объекта, предоставленного средой выполнения, может изменить детали записи.

`delete` работает со свойствами объектов, а не с лексическими привязками. Локальную привязку `let` или `const` удалить нельзя. В строгом коде выражение `delete total` является ранней синтаксической ошибкой.

### JS-SCOPE-Q08

[Вернуться к вопросу](../../by-domain/01-javascript-and-async-programming.md#js-scope-q08)

- **Контекст выполнения (execution context)** хранит состояние, необходимое для выполнения кода.
- **Стек вызовов (call stack)** задаёт порядок активных контекстов.
- **Область видимости (scope)** описывает, где в исходном коде имя может разрешиться в конкретную привязку.
- **Запись окружения (Environment Record)** хранит и разрешает привязки во время выполнения и ссылается наружу через `[[OuterEnv]]`.

Вызов `outer()` создаёт контекст выполнения функции и её запись окружения; этот контекст становится активным. Вызов `inner()` делает то же для `inner`, но её внешняя связь определяется местом объявления функции, а не местом вызова.

В спецификационной модели вход в непустой блок `if` создаёт блочную запись окружения и временно меняет ссылку `LexicalEnvironment`. При этом новая функция не вызывается, поэтому новый контекст выполнения функции в стек не добавляется. Движок может оптимизировать внутреннее представление, если поведение программы от этого не меняется.

### JS-SCOPE-Q09

[Вернуться к вопросу](../../by-domain/01-javascript-and-async-programming.md#js-scope-q09)

Результат:

```text
factory
```

При чтении `name` внутри возвращённой функции поиск проходит так:

1. запись окружения текущего вызова возвращённой функции;
2. сохранённое окружение вызова `makeReader`, где находится значение `"factory"`;
3. после найденной привязки поиск прекращается и до глобального `name` не доходит.

Локальное окружение `run` не входит в эту лексическую цепочку. `run` — активный вызывающий контекст, но **лексическое разрешение (lexical resolution)** следует месту определения функции, а не месту её вызова.

### JS-SCOPE-Q10

[Вернуться к вопросу](../../by-domain/01-javascript-and-async-programming.md#js-scope-q10)

В спецификационной модели при выполнении непустого блока создаётся новая **декларативная запись окружения (Declarative Environment Record)**. На время блока ссылка `LexicalEnvironment` указывает на неё. Вызова функции при этом нет. Это не означает, что движок обязан создавать отдельный JavaScript-объект: ненаблюдаемые детали можно оптимизировать.

Вызов `f()` создаёт контекст выполнения функции, состояние аргументов и параметров и функциональную запись окружения. Затем этот контекст становится текущим в стеке вызовов. Каждый рекурсивный вызов получает новый контекст.

Поэтому области видимости и кадры стека не соответствуют друг другу один к одному. Внутри одного вызова может быть несколько вложенных блочных областей, а одно определение функции может породить много контекстов при разных вызовах.

### JS-SCOPE-Q11

[Вернуться к вопросу](../../by-domain/01-javascript-and-async-programming.md#js-scope-q11)

- `first` содержит ранний `SyntaxError` — **Early Error**. Вложенное объявление `var id` принадлежит области `var` всей функции и конфликтует с лексическим `id` в её теле.
- Фрагмент `second` корректен. Если вызвать `second()`, блочный `let id` затенит функциональный `var id`, и функция выведет `2`. В приведённом виде код только объявляет функцию и ничего не выводит.
- Два объявления `const id` верхнего уровня создают ранний `SyntaxError`.

Если одна разобранная единица — скрипт, модуль или тело функции — содержит Early Error, её обычное выполнение не начинается. Поэтому предыдущий `console.log` внутри той же единицы тоже не выполнится.

### JS-SCOPE-Q12

[Вернуться к вопросу](../../by-domain/01-javascript-and-async-programming.md#js-scope-q12)

Предположим, что код запускается в новой изолированной браузерной среде (**realm**), где ещё нет одноимённых глобальных свойств:

| Среда | Первое значение | Второе значение |
|---|---:|---:|
| Классический скрипт | `true` | `false` |
| ES-модуль | `false` | `false` |

В классическом скрипте **глобальная запись окружения (Global Environment Record)** состоит из двух частей. Подходящие объявления `var` и функций обслуживает объектная часть (**Object Environment Record**), связанная с глобальным объектом. Лексические объявления хранит декларативная часть (**Declarative Environment Record**). Поэтому `fromVar` отражается как свойство глобального объекта, а `fromLet` остаётся глобальной лексической привязкой без свойства на `globalThis`.

В модуле оба объявления, включая `var`, имеют модульную область видимости. Ни одно из них не создаёт свойство `globalThis`. Если одноимённое свойство уже предоставила среда выполнения, прямое сравнение могло бы дать другой результат — поэтому условие о чистой изолированной среде важно.

### JS-SCOPE-Q13

[Вернуться к вопросу](../../by-domain/01-javascript-and-async-programming.md#js-scope-q13)

Результат:

```text
[3, 3, 3]
[0, 1, 2]
```

Первые три функции используют одну общую привязку `i` с областью `var`: функциональную внутри функции, глобальную для классического скрипта или модульную на верхнем уровне модуля. Функции вызываются после завершения цикла, когда в этой привязке уже находится `3`.

Семантика `for (let ...)` создаёт новую привязку `j` для каждой итерации. Каждая функция замыкается на привязку своей итерации. **Замыкание (closure)** сохраняет доступ к привязке, а не получает «замороженную копию» благодаря таймеру или другой магии времени.

### JS-SCOPE-Q14

[Вернуться к вопросу](../../by-domain/01-javascript-and-async-programming.md#js-scope-q14)

Все ветки принадлежат одному блоку `switch` (`CaseBlock`). Поэтому два объявления `const message` конфликтуют, хотя во время выполнения выбирается только одна ветка.

Исправление:

```js
function label(status) {
  switch (status) {
    case "idle": {
      const message = "Waiting";
      return message;
    }
    case "done": {
      const message = "Complete";
      return message;
    }
    default:
      return "Unknown";
  }
}
```

Фигурные скобки создают для каждой ветки отдельную лексическую область.

### JS-SCOPE-Q15

[Вернуться к вопросу](../../by-domain/01-javascript-and-async-programming.md#js-scope-q15)

Проблемы в порядке серьёзности:

1. **Корректность:** все обработчики замыкаются на одной привязке `var i`. После цикла `i === items.length`, поэтому каждый обработчик возвращает `items[items.length]`, обычно `undefined`.
2. **Корректность и владение состоянием:** `handlers = {}` создаёт случайное свойство глобального объекта в нестрогом коде и выбрасывает `ReferenceError` в строгом или модульном коде.
3. **Сопровождаемость:** скрытое глобальное состояние заставляет повторные вызовы и потребителей неявно делить один объект.
4. **Читаемость:** объявления не показывают, какие значения действительно должны изменяться.

Минимальное безопасное исправление:

```js
function register(items) {
  const handlers = {};

  for (let i = 0; i < items.length; i += 1) {
    handlers[i] = function () {
      return items[i];
    };
  }

  return handlers;
}
```

Если обработчик должен сохранить именно текущее значение элемента даже после изменения массива, внутри итерации нужно захватить `const item = items[i]` и возвращать `item`. Это решение о контракте функции, а не просто предпочтение синтаксиса.

Более чистый модульный API экспортирует `register` и возвращает коллекцию обработчиков. Глобальное имя тогда вообще не требуется.

### JS-SCOPE-Q16

[Вернуться к вопросу](../../by-domain/01-javascript-and-async-programming.md#js-scope-q16)

Эталонный ответ:

> **Hoisting** — неформальное название наблюдаемого поведения, которое возникает из-за обработки объявлений до обычного выполнения инструкций. Исходные строки физически никуда не перемещаются. Для нового имени привязка `var` создаётся и инициализируется значением `undefined`, поэтому раннее чтение разрешается. Совместимое повторное объявление `var` не сбрасывает существующую привязку. Привязки `let`, `const` и `class` тоже создаются заранее, но остаются неинициализированными в TDZ, поэтому раннее чтение выбрасывает `ReferenceError`. Объявление функции обычно сразу получает объект функции. Функциональное выражение создаётся только при выполнении своей строки и следует жизненному циклу содержащего его `var`, `let` или `const`.

Уточнение для Senior-ответа: названия конкретных алгоритмов обработки объявлений стоит приводить только когда они помогают рассуждению. Не нужно утверждать, что движок обязан создать определённый объект или выполнить одну универсальную «фазу создания» для любого кода.

### JS-SCOPE-Q17

[Вернуться к вопросу](../../by-domain/01-javascript-and-async-programming.md#js-scope-q17)

**Глобальная запись окружения (Global Environment Record)** — спецификационная модель, которая объединяет две части:

- **Object Environment Record** связан с глобальным объектом и обслуживает подходящие объявления `var` и функций из классических скриптов;
- **Declarative Environment Record** хранит глобальные лексические объявления `let`, `const` и `class` из классических скриптов.

Поэтому лексическое объявление верхнего уровня может быть глобальным, но не быть свойством `globalThis`. Сам `globalThis` даёт переносимую ссылку на глобальное `this`-значение. В браузере технические детали связаны с `WindowProxy`, но для базового ответа они не нужны.

ES-модули используют модульные окружения. Их объявления верхнего уровня не становятся свойствами глобального объекта, а код модулей автоматически выполняется в строгом режиме. Эта модель не означает, что движок обязан реализовать две части как два обычных JavaScript-объекта.

### JS-SCOPE-Q18

[Вернуться к вопросу](../../by-domain/01-javascript-and-async-programming.md#js-scope-q18)

Во время обработки глобальных объявлений второго классического скрипта его `var config` конфликтует с глобальной лексической привязкой `config`, которую уже создал первый скрипт. Второй скрипт завершается с `SyntaxError` до обычного выполнения, поэтому строка `"vendor starts"` не выводится.

Точное уточнение: межскриптовый конфликт обнаруживается во время `GlobalDeclarationInstantiation`. Формально это не **Early Error**, потому что ранние статические ошибки проверяются внутри одной разобранной единицы кода.

Быстрая мера — переименовать или изолировать глобальное имя библиотеки либо загрузить её через оболочку, которая не объявляет `config` глобально. Изменение имени в приложении требует изменить исходный код и открыть новую страницу или создать новую изолированную среду: уже созданную глобальную привязку `let` удалить во время выполнения нельзя. Простая перестановка скриптов может изменить, какой из них завершится ошибкой, но не решит конфликт владения именем.

Долговременное решение — модули или явный контракт интеграции с отдельным пространством имён. Каждый компонент должен владеть своими привязками и намеренно публиковать только публичный API. Проверять нужно реальный режим загрузки рабочей среды, а не только модульный граф сборщика в режиме разработки.

### JS-SCOPE-Q19

[Вернуться к вопросу](../../by-domain/01-javascript-and-async-programming.md#js-scope-q19)

Предположение кода работает только в подходящем классическом браузерном скрипте: объявление `var registry` верхнего уровня создаёт или использует свойство глобального объекта.

В браузерном ES-модуле и Node.js ESM эта привязка имеет модульную область. В Node.js CommonJS файл обёрнут функцией, поэтому `var` тоже остаётся локальным для модуля. В этих средах `globalThis.registry` обычно равен `undefined`, и чтение `.enabled` выбрасывает `TypeError`.

Если межскриптовый API действительно нужен, его следует публиковать явно:

```js
globalThis.myLibrary = {
  registry: { enabled: true },
};
```

Для такого API нужно документировать имя, порядок инициализации, правила коллизий и версий, а также очистку. Если глобальный контракт не нужен, значение лучше экспортировать:

```js
export const registry = { enabled: true };
```

### JS-SCOPE-Q20

[Вернуться к вопросу](../../by-domain/01-javascript-and-async-programming.md#js-scope-q20)

```js
function installLegacyApi(root, api) {
  const key = "frontendInterview";

  if (Object.hasOwn(root, key)) {
    throw new Error(`${key} is already installed`);
  }

  root[key] = api;

  return function uninstall() {
    if (root[key] !== api) {
      return false;
    }

    return delete root[key];
  };
}
```

Корневой объект передаётся явно, поэтому неразрешимое присваивание не создаст случайное глобальное свойство, а вспомогательная функция не зависит от браузерного `window`. Проверка `Object.hasOwn` защищает уже существующий контракт собственного свойства. При очистке дополнительно сравнивается ссылка на `api`: функция не удалит замену, которую после установки записал другой владелец.

`delete root[key]` работает со свойством объекта, а результат зависит от его дескриптора. Настраиваемое свойство можно удалить. Попытка удалить ненастраиваемое свойство возвращает `false` в нестрогом коде и выбрасывает `TypeError` в строгом. Оператор не может удалить привязку `let`, `const`, параметр или локальную переменную; синтаксис `delete identifier` недопустим в строгом коде.

Сложность — `O(1)` по времени и `O(1)` по сохраняемому состоянию. Такой адаптер оправдан только для намеренной совместимости с устаревшим кодом. В обычном случае модуль должен экспортировать API, а потребители — импортировать его, не создавая общее глобальное имя и отдельный жизненный цикл для него.

## 1.2. Значения, типы, равенство и преобразование типов

Это модельные ответы и критерии сильного рассуждения, а не тексты для дословного заучивания.

### JS-VALUES-Q01

[Вернуться к вопросу](../../by-domain/01-javascript-and-async-programming.md#js-values-q01)

Primitive types: `undefined`, `null`, `boolean`, `number`, `bigint`, `string`, `symbol`. Все остальные ECMAScript language values относятся к Object type. Функция — object с внутренней возможностью `[[Call]]`; `typeof` исторически возвращает для callable object специальную строку `"function"`.

Runtime type принадлежит текущему value. Binding, объявленный через `let`, может последовательно хранить number и string. Возможность reassignment определяет declaration (`const` против `let`), а mutability — семантика самого value. Поэтому `const user = {}` нельзя переназначить, но object может мутировать.

Сильный ответ не называет `null` object из-за `typeof null` и не смешивает TypeScript static type с JavaScript runtime value.

### JS-VALUES-Q02

[Вернуться к вопросу](../../by-domain/01-javascript-and-async-programming.md#js-values-q02)

Вывод:

```text
draft
dark
true
```

`toUpperCase()` возвращает новый immutable string value, но binding `label` не переназначается, поэтому остаётся `"draft"`. `settings.mode = "dark"` мутирует существующий object. `alias` и `settings` содержат copied object value, обозначающий одну identity; изменение видно через оба, а strict equality даёт `true`.

`const` запрещает только assignment нового value в binding `settings`. Он не выполняет `Object.freeze()` и не копирует object.

### JS-VALUES-Q03

[Вернуться к вопросу](../../by-domain/01-javascript-and-async-programming.md#js-values-q03)

Вывод: `true`.

Вызов создаёт parameter binding `item` и копирует в него object value из `config`. Оба bindings обозначают один object identity, поэтому mutation `item.enabled = true` видна через `config`. Следующая строка переназначает только локальный binding `item` новым object value. Binding `config` вызывающего кода остаётся связан с первым object.

Это pass-by-value. При pass-by-reference функция получила бы возможность переназначить сам binding `config`, чего здесь не происходит.

### JS-VALUES-Q04

[Вернуться к вопросу](../../by-domain/01-javascript-and-async-programming.md#js-values-q04)

Первый фрагмент возвращает по порядку:

```text
"object"
"number"
"bigint"
"symbol"
"object"
"function"
```

`typeof null === "object"` — historical compatibility bug; `null` остаётся primitive. `NaN` и infinities принадлежат Number type. Arrays — objects. Callable objects получают результат `"function"`.

Во втором фрагменте оба `console.log` выводят `"undefined"`: один identifier объявлен и хранит `undefined`, второй вообще не разрешается. Поэтому результат `typeof` не различает эти ситуации.

Третий фрагмент бросает `ReferenceError`: lexical binding `later` существует в TDZ, а специальное безопасное поведение `typeof` относится только к действительно undeclared identifier.

### JS-VALUES-Q05

[Вернуться к вопросу](../../by-domain/01-javascript-and-async-programming.md#js-values-q05)

`Symbol` — уникальный primitive, обычно используемый как collision-resistant property key или language hook. `Symbol("id") !== Symbol("id")`: description не является identity. `typeof` возвращает `"symbol"`.

`BigInt` — primitive для integer values произвольной величины: `typeof 1n === "bigint"`. `5n / 2n` даёт `2n`, поскольку дробь представить нельзя. Arithmetic между `1n` и `1` бросает `TypeError`; нужно явно выбрать BigInt или Number model. Конвертация большого BigInt в Number может потерять точность.

BigInt не хранит decimal fractions и сам по себе не задаёт currency scale или rounding policy. Для money его можно использовать только как integer minor-unit representation с отдельным контрактом.

### JS-VALUES-Q06

[Вернуться к вопросу](../../by-domain/01-javascript-and-async-programming.md#js-values-q06)

```text
NaN === NaN                 → false
Number.isNaN(NaN)           → true
Number.isNaN("hello")       → false
isNaN("hello")              → true
Number.isFinite(Infinity)    → false
0 === -0                    → true
Object.is(0, -0)            → false
1 / -0                      → -Infinity
```

`value !== NaN` всегда `true`, включая само `NaN`, поэтому так проверять нельзя. `Number.isNaN` проверяет exact NaN без coercion; global `isNaN` сначала делает number coercion. Для finite numeric input используйте `typeof value === "number"` по контракту и `Number.isFinite(value)`: Infinity не NaN, но для обычной величины часто недопустима.

### JS-VALUES-Q07

[Вернуться к вопросу](../../by-domain/01-javascript-and-async-programming.md#js-values-q07)

Практический полный набор falsy: `false`, `0`, `-0`, `0n`, `NaN`, `""`, `null`, `undefined`. Nullish — только `null` и `undefined`.

```text
Boolean("0")                 → true
Boolean([])                  → true
Boolean({})                  → true
Boolean(0n)                  → false
Boolean(new Boolean(false))  → true
```

Boolean coercion не проверяет «пустоту» object и не вызывает его `valueOf`/`toString`; обычные objects truthy. Wrapper `new Boolean(false)` — object, поэтому тоже truthy.

### JS-VALUES-Q08

[Вернуться к вопросу](../../by-domain/01-javascript-and-async-programming.md#js-values-q08)

Исправление:

```js
function options(input) {
  return {
    retries: input.retries ?? 3,
    visible: input.visible ?? true,
    label: input.label ?? "Untitled",
  };
}
```

`||` выбирает right operand для любого falsy left value и поэтому заменял valid `0`, `false` и `""`. `??` выбирает fallback только для `null`/`undefined`.

Исходный `||` уместен, если продукт действительно считает любое falsy значение отсутствующим, например выбирает первый non-empty display label и сознательно отвергает empty string. Оба оператора возвращают operand value, а не обязательно boolean.

### JS-VALUES-Q09

[Вернуться к вопросу](../../by-domain/01-javascript-and-async-programming.md#js-values-q09)

Результат:

```text
first  = "ready"
second = 0
third  = "fallback"
calls  = 1
```

`||` не вычисляет `build`, потому что `"ready"` truthy. `&&` не вычисляет right operand, потому что `0` falsy, и возвращает `0`. `??` вычисляет `build`, потому что `null` nullish.

Short-circuit условно пропускает весь right operand независимо от его внутреннего precedence. Side effects в таком operand допустимы семантически, но ухудшают review: вызов становится зависимым от truthiness/nullishness и его легко не заметить. Явный `if` часто лучше, если side effect является основной целью.

### JS-VALUES-Q10

[Вернуться к вопросу](../../by-domain/01-javascript-and-async-programming.md#js-values-q10)

- `data?.user.name` → `undefined`: nullish base останавливает continuous chain.
- `(data?.user).name` → `TypeError`: grouped expression сначала даёт `undefined`, затем отдельный `.name` выполняется обычно.
- `api?.save()` при `api = {}` → `TypeError`: защищён `api`, но отсутствующий `save` всё равно вызывается.
- `api.save?.()` при `api = {}` → `undefined`: защищён method value.
- `api.save?.()` при string `save` → `TypeError`: value существует, но не callable.
- `account?.name = "Ada"` → ранний `SyntaxError`: optional chain не может быть assignment target.
- при `items === null` expression `items?.[index++]` возвращает `undefined`, а `index` не увеличивается.

Optional chaining не ловит errors getter-а или реально вызванной функции и не разрешает undeclared root identifier.

### JS-VALUES-Q11

[Вернуться к вопросу](../../by-domain/01-javascript-and-async-programming.md#js-values-q11)

| Семантика | Coercion | `NaN` | signed zero | Objects |
|---|---:|---:|---:|---|
| `==` | да | не равен себе | равны | identity после возможного object-to-primitive |
| `===` | нет | не равен себе | равны | identity |
| `Object.is` / SameValue | нет | равен себе | различаются | identity |
| SameValueZero | нет | равен себе | равны | identity |

SameValueZero используют `includes`, `Set` values и `Map` keys. `Object.is` не лежит на одной шкале «строже/мягче»: он одновременно объединяет `NaN`, но различает zeros. Ни один алгоритм не выполняет general deep equality objects.

### JS-VALUES-Q12

[Вернуться к вопросу](../../by-domain/01-javascript-and-async-programming.md#js-values-q12)

```text
false
true
"light"
5
```

Spread создаёт новую outer identity для `copy`, поэтому `base === copy` false и изменение `copy.theme` не затрагивает `base.theme`. Но значение property `network` скопировано shallowly; оно обозначает один nested object, поэтому equality true и mutation retries видна через `base`.

Точечное исправление при изменении `network`:

```js
const copy = {
  ...base,
  network: { ...base.network },
};
```

Нужно копировать уровни, которыми новый owner будет независимо владеть. Universal deep clone, cycles и `structuredClone` относятся к 1.5 и требуют отдельного contract.

### JS-VALUES-Q13

[Вернуться к вопросу](../../by-domain/01-javascript-and-async-programming.md#js-values-q13)

| value | `isNaN(value)` | `Number.isNaN(value)` |
|---|---:|---:|
| `""` | false (`→ 0`) | false |
| `"42"` | false (`→ 42`) | false |
| `"oops"` | true (`→ NaN`) | false |
| `42` | false | false |
| `NaN` | true | true |
| `1n` | `TypeError` | false |

Для boundary «non-empty decimal string или finite Number» сначала проверяется исходный type и string grammar. Empty/whitespace отклоняются до conversion. После `Number(text)` требуется `Number.isFinite(result)`. Number input тоже проходит `Number.isFinite`. Такая схема отделяет parsing от validation; `Number.isNaN` сам по себе не подтверждает допустимый range или format.

### JS-VALUES-Q14

[Вернуться к вопросу](../../by-domain/01-javascript-and-async-programming.md#js-values-q14)

`0.1`, `0.2` и `0.3` не все представимы точно в binary floating point; actual становится `0.30000000000000004`.

Для measurements выбирают domain tolerances и сравнивают difference с maximum из absolute tolerance и relative tolerance, умноженного на scale. Это обрабатывает значения около zero и большие magnitudes, но сами tolerances должны прийти из requirements.

Для fixed-scale money практичнее integer minor units:

```js
const totalCents = priceCents * quantity;
```

Нужно валидировать `Number.isSafeInteger`, currency scale, sign/range и определить rounding points для taxes/discounts. BigInt пригоден для больших integer minor units, но не для decimal fractions.

`Number.EPSILON` описывает spacing около `1`; один абсолютный threshold не универсален для больших magnitudes и тем более не задаёт финансовую rounding policy.

### JS-VALUES-Q15

[Вернуться к вопросу](../../by-domain/01-javascript-and-async-programming.md#js-values-q15)

| Input | `Boolean` | `Number` | `String` |
|---|---:|---:|---|
| `undefined` | false | `NaN` | `"undefined"` |
| `null` | false | `0` | `"null"` |
| `false` | false | `0` | `"false"` |
| `""` | false | `0` | `""` |
| `"  "` | true | `0` | `"  "` |
| `"42"` | true | `42` | `"42"` |
| `"42px"` | true | `NaN` | `"42px"` |
| `0` | false | `0` | `"0"` |
| `1n` | true | `1` с риском потери точности для больших BigInt | `"1"` |
| `Symbol("x")` | true | `TypeError` | `"Symbol(x)"` |

Unary `+` почти повторяет number coercion, но `+1n` бросает `TypeError`, тогда как explicit `Number(1n)` разрешён. `String(Symbol("x"))` специально поддержан, но ordinary implicit string coercion через template literal или `"" + symbol` бросает `TypeError`. Поэтому `"" + value` не является general replacement для `String(value)`.

### JS-VALUES-Q16

[Вернуться к вопросу](../../by-domain/01-javascript-and-async-programming.md#js-values-q16)

```text
1 + 2 + "3"   → 3 + "3"   → "33"   (string)
"1" + 2 + 3   → "12" + 3  → "123"  (string)
true + 1      → 1 + 1      → 2      (number)
null + 1      → 0 + 1      → 1      (number)
undefined + 1 → NaN + 1    → NaN    (number)
[1] + 2       → "1" + 2    → "12"   (string)
1n + 2n                       → 3n     (bigint)
"1" + 2n                      → "12"   (string)
```

`1n + 2` бросает `TypeError`: numeric branch не смешивает Number и BigInt. Binary `+` сначала допускает string branch, тогда как `-` всегда идёт в numeric coercion: `"5" + 2` → `"52"`, но `"5" - 2` → `3`.

### JS-VALUES-Q17

[Вернуться к вопросу](../../by-domain/01-javascript-and-async-programming.md#js-values-q17)

```text
"2" < "10"  → false (string lexicographic comparison)
"2" < 10    → true  (numeric comparison)
null == 0   → false (special loose-nullish rule)
null > 0    → false (null → 0; 0 > 0)
null >= 0   → true  (ordering path treats null as 0)
0n === 0    → false (different types)
0n == 0     → true  (same mathematical integer value)
1n < 1.5    → true
```

Equality and relational comparison use different abstract algorithms. String-string ordering is lexicographic, loose equality has dedicated nullish/boolean/object branches, and Number/BigInt comparison avoids blindly converting every operand to one Number.

### JS-VALUES-Q18

[Вернуться к вопросу](../../by-domain/01-javascript-and-async-programming.md#js-values-q18)

Observed calls/results:

```text
Number(amount) → logs "valueOf" → 7
String(amount) → logs "toString" → "seven"
amount + 1     → logs "valueOf" → 8
```

Number hint tries `valueOf` then `toString`; string hint reverses the order. Binary `+` uses default hint, which ordinary objects handle like number.

`[Symbol.toPrimitive](hint)`, if present, runs first with `"number"`, `"string"` or `"default"` and must return a primitive or throw `TypeError`. `Date` treats default like string, unlike ordinary objects. Это стоит знать для точного объяснения, но production code не должен зависеть от surprising implicit Date concatenation.

### JS-VALUES-Q19

[Вернуться к вопросу](../../by-domain/01-javascript-and-async-programming.md#js-values-q19)

`value == null` — узкий deliberate use абстрактного равенства: для обычных JavaScript values expression истинно только для `null` и `undefined`. Эквивалент без loose equality:

```js
value === null || value === undefined
```

С точки зрения correctness короткая форма подходит, если контракт действительно означает «любое nullish value». С точки зрения readability явная форма легче для команды, которая не держит алгоритм `==` в active recall. Поэтому разумны обе team policies:

- полностью запрещать `==` и писать два strict comparisons;
- разрешать только документированное `value == null`, например точечным lint exception.

Важно соблюдать выбранное правило последовательно. Этот special case не делает безопасными произвольные `==`: в сравнениях boolean, string, number и object включаются другие ветви coercion, которые заметно труднее читать и review.

### JS-VALUES-Q20

[Вернуться к вопросу](../../by-domain/01-javascript-and-async-programming.md#js-values-q20)

Для primitive readings стратегии ведут себя так:

| Стратегия | `NaN` совпадает с `NaN` | `0` совпадает с `-0` | Семантика |
|---|---:|---:|---|
| `Set` | да | да | SameValueZero |
| `includes()` | да | да | SameValueZero |
| `indexOf()` | нет | да | strict equality |
| ручной `===` | нет | да | strict equality |
| ручной `Object.is()` | да | нет | SameValue |

Обычная дедупликация readings естественно выражается через `Set`: нечисловое показание `NaN` дедуплицируется, а signed zero считается одним числом. Если знак zero имеет domain meaning, это требование не выражается стандартным `Set`; нужен ручной поиск через `Object.is()` или явный canonical key вроде `"number:-0"`.

Для objects все перечисленные механизмы сравнивают identity, а не поля. Два `{ value: 1 }` останутся разными. Если domain требует structural equality, сначала строят стабильный key из проверенных полей или применяют domain comparator; случайный `JSON.stringify` без контракта на порядок, допустимые типы и cycles — хрупкая замена.

### JS-VALUES-Q21

[Вернуться к вопросу](../../by-domain/01-javascript-and-async-programming.md#js-values-q21)

Критическая проблема: spread создаёт только новый outer object. Без соответствующего override `options.retry === DEFAULTS.retry`, поэтому первый вызов меняет default count с `2` на `3`, следующий — с `3` на `4`. Аналогично `headers` остаётся shared reference. Если caller передаст собственный `overrides.retry`, функция мутирует уже caller-owned object.

Минимальное исправление — создать новые nested values именно на границах, которыми функция собирается владеть или которые может менять:

```js
export function buildOptions(overrides = {}) {
  const options = {
    ...DEFAULTS,
    ...overrides,
    retry: {
      ...DEFAULTS.retry,
      ...overrides.retry,
    },
    headers: {
      ...DEFAULTS.headers,
      ...overrides.headers,
    },
  };

  options.retry.count += 1;
  return options;
}
```

Ещё чище — вычислить final count без последующей mutation. API должен документировать, мутирует ли inputs, кто владеет returned nested objects и можно ли безопасно менять result. Universal deep clone здесь не нужен: он имеет отдельные semantics для prototypes, accessors, functions и host objects и относится к полной теме copying из 1.5.

### JS-VALUES-Q22

[Вернуться к вопросу](../../by-domain/01-javascript-and-async-programming.md#js-values-q22)

Исходная функция принимает `""`, whitespace и `null` как `0`; `"Infinity"` как `Infinity`; `"1.5"` как fraction; `"-0"` как negative zero; `"9007199254740993"` с потерей точности. Проверка только `NaN` отвечает на вопрос «получился ли специальный NaN», а не на business contract.

Если контракт принимает только canonical positive decimal string без знака и ведущих нулей:

```js
function parseQuantity(input) {
  if (typeof input !== "string" || !/^[1-9]\d*$/.test(input)) {
    throw new TypeError("quantity must be a positive decimal integer string");
  }

  const value = Number(input);

  if (!Number.isSafeInteger(value) || value <= 0) {
    throw new RangeError("quantity is outside the safe integer range");
  }

  return value;
}
```

Regex сначала фиксирует grammar и поэтому исключает whitespace, fractions, exponent notation, signs, `-0` и infinities. Затем `Number.isSafeInteger` проверяет representable range. Если API должно принимать также Number, для него нужна отдельная ветвь с `Number.isSafeInteger(input) && input > 0`; не стоит прогонять разные input types через одно широкое coercion.

### JS-VALUES-Q23

[Вернуться к вопросу](../../by-domain/01-javascript-and-async-programming.md#js-values-q23)

Один возможный implementation с примерными defaults:

```js
function nearlyEqual(
  left,
  right,
  {
    relativeTolerance = 1e-12,
    absoluteTolerance = 1e-12,
  } = {},
) {
  if (
    !Number.isFinite(relativeTolerance) ||
    !Number.isFinite(absoluteTolerance) ||
    relativeTolerance < 0 ||
    absoluteTolerance < 0
  ) {
    throw new RangeError("tolerances must be finite non-negative numbers");
  }

  if (left === right) return true;
  if (!Number.isFinite(left) || !Number.isFinite(right)) return false;

  const difference = Math.abs(left - right);
  const scale = Math.max(Math.abs(left), Math.abs(right));
  const allowed = Math.max(
    absoluteTolerance,
    relativeTolerance * scale,
  );

  return difference <= allowed;
}
```

Representative tests:

```js
console.assert(nearlyEqual(0, 5e-13));
console.assert(nearlyEqual(0.1 + 0.2, 0.3));
console.assert(nearlyEqual(1e12, 1e12 + 0.5));
console.assert(nearlyEqual(0, -0));
console.assert(nearlyEqual(Infinity, Infinity));
console.assert(!nearlyEqual(Infinity, -Infinity));
console.assert(!nearlyEqual(NaN, NaN));
```

`left === right` намеренно расположен первым: он принимает одинаковые infinities и оба zero. Defaults здесь демонстрационные; sensor readings, geometry и scientific data требуют tolerances из domain requirements. Для money обычно нужна другая model — integer minor units и явная rounding policy.

### JS-VALUES-Q24

[Вернуться к вопросу](../../by-domain/01-javascript-and-async-programming.md#js-values-q24)

Вывод:

```text
1
false
true
{ amount: "0", label: "none", numeric: "01" }
true -1
```

Outer spread создаёт новую identity, поэтому `source !== copy`, но nested `meta` остаётся общим: mutation через параметр видна как `source.meta.attempts === 1`. Параметр получает копию reference value; он не является alias самого binding `copy`.

String `"0"` truthy, поэтому `input.amount || 10` сохраняет строку. Continuous optional chain возвращает `undefined`, а `??` подставляет `"none"`. Binary `+` после `ToPrimitive` видит string operand и конкатенирует: `"0" + 1` → `"01"`. `includes()` применяет SameValueZero и находит `NaN`, тогда как `indexOf()` применяет strict equality и возвращает `-1`.

Production boundary должна решить, что такое `amount`: например, принять string, проверить grammar, один раз преобразовать в finite/safe Number и дальше хранить normalized type. Default выбирают по требованиям: `??` для отсутствующего значения, а не `||`, если `0` допустим. Ownership безопаснее сделать явным: функция либо не мутирует input и возвращает новый nested `meta`, либо документированно получает owned object. Объяснение на интервью: bindings содержат values, object value даёт доступ к identity; function получает копию этого reference value, поэтому shared mutation видна, а reassignment параметра — нет.

## 1.3. Функции, замыкания и функциональные паттерны

### JS-FUNCTIONS-Q01

[Вернуться к вопросу](../../by-domain/01-javascript-and-async-programming.md#js-functions-q01)

- Объявление функции подготавливается вместе с остальными объявлениями и имеет имя во внешней области.
- Функциональное выражение создаёт функцию при вычислении выражения; внешнее имя даёт окружающая привязка.
- Именованное выражение дополнительно получает внутреннее имя, видимое только в теле функции.
- Стрелочная функция тоже создаётся выражением, но не имеет собственных `this`, `arguments` и `new.target`, и её нельзя вызвать через `new`.

Объявление естественно для именованной операции уровня модуля, выражение — для функции как обычного значения или настроенного колбэка, стрелочная функция — для лексического колбэка или преобразования. Обычная функция-конструктор в основном нужна для поддержки старого кода и вопросов на интервью.

### JS-FUNCTIONS-Q02

[Вернуться к вопросу](../../by-domain/01-javascript-and-async-programming.md#js-functions-q02)

1. Объявление функции печатает `"declaration"`: привязка уже содержит готовую функцию.
2. `var run` до присваивания содержит `undefined`; попытка вызова даёт `TypeError`, поэтому `console.log` ничего не успевает напечатать.
3. `const run` находится в TDZ; чтение имени для вызова даёт `ReferenceError`.

Нельзя просто сказать, что выражение «не поднимается». Окружающее объявление обрабатывается по правилам `var` или `const`, но объект-функция появляется только при вычислении правой части.

### JS-FUNCTIONS-Q03

[Вернуться к вопросу](../../by-domain/01-javascript-and-async-programming.md#js-functions-q03)

Результат:

```text
function
internal
undefined
```

`task` — внешняя привязка, в которой хранится функция. `internal` — внутренняя привязка имени самого именованного выражения: рекурсивный вызов её видит, внешний код — нет. Свойство `task.name` получает явно указанное внутреннее имя.

### JS-FUNCTIONS-Q04

[Вернуться к вопросу](../../by-domain/01-javascript-and-async-programming.md#js-functions-q04)

Параметр — привязка в определении функции; аргумент — значение конкретного вызова. Значение по умолчанию применяется, когда аргумент пропущен или явно равен `undefined`, но не заменяет `null` и `""`. В `connect({ timeout = 1000 } = {})` внешнее `= {}` даёт объект для деструктуризации, когда весь аргумент отсутствует; внутреннее значение по умолчанию работает, когда свойство отсутствует или равно `undefined`.

### JS-FUNCTIONS-Q05

[Вернуться к вопросу](../../by-domain/01-javascript-and-async-programming.md#js-functions-q05)

Результат:

```js
["outer", ["inner", "extra"]]
```

Стрелочная функция не создаёт собственный `arguments`, поэтому читает объект внешней функции `outer`. Остаточный параметр принадлежит самой стрелочной функции и создаёт массив из аргументов её вызова. `arguments` содержит все фактические аргументы обычной функции и не является массивом; остаточный параметр содержит только аргументы после именованных параметров и является массивом.

### JS-FUNCTIONS-Q06

[Вернуться к вопросу](../../by-domain/01-javascript-and-async-programming.md#js-functions-q06)

«Функция первого класса» означает, что функция является обычным значением: её можно сохранять, передавать и возвращать. Колбэк — это роль функции, которую другой код вызывает по согласованному контракту. Функция высшего порядка принимает или возвращает функцию.

```js
function withFallback(operation, fallback) {
  return (...args) => {
    const result = operation(...args);
    return result ?? fallback;
  };
}
```

Контракт колбэка описывает: кто его вызывает, сколько раз и когда; какие аргументы и `this` передаёт; как использует результат; как сообщает об ошибках; как выполняются отмена и очистка; кто хранит ссылку на функцию.

### JS-FUNCTIONS-Q07

[Вернуться к вопросу](../../by-domain/01-javascript-and-async-programming.md#js-functions-q07)

- Метод с получателем, определяемым при вызове, → краткая запись метода или обычная функция.
- Небольшое преобразование массива без собственного получателя → стрелочная функция.
- Конструктор → обычная функция или класс; стрелочную функцию нельзя вызвать через `new`.
- Вложенный колбэк таймера, которому нужен `this` внешнего метода, → стрелочная функция.
- Функция с переменным числом аргументов → подходят обе формы, но лучше явно объявить остаточный параметр; стрелочная функция подходит, если получатель не нужен.

Критерий — семантика вызова, а не число символов.

### JS-FUNCTIONS-Q08

[Вернуться к вопросу](../../by-domain/01-javascript-and-async-programming.md#js-functions-q08)

Результат — `"ready"`: замыкание читает текущее значение привязки `status`. Снимок создаётся отдельно:

```js
let status = "idle";
const snapshot = status;
const readStatus = () => snapshot;
status = "ready";
```

Теперь замыкание читает отдельную привязку `snapshot`, значение которой не переназначалось.

### JS-FUNCTIONS-Q09

[Вернуться к вопросу](../../by-domain/01-javascript-and-async-programming.md#js-functions-q09)

Чистая функция при одинаковых входных данных даёт одинаковый наблюдаемый результат и не создаёт внешних наблюдаемых эффектов. Локальная мутация нового объекта-результата, который ещё не используется совместно, может оставаться ненаблюдаемой снаружи. Spread создаёт новый внешний объект, но вложенные объекты сохраняют прежнюю идентичность; их мутация по-прежнему видна через другие ссылки.

### JS-FUNCTIONS-Q10

[Вернуться к вопросу](../../by-domain/01-javascript-and-async-programming.md#js-functions-q10)

Результат:

```text
[1, 1, 1]
[10, 10, 1]
[2, 20, 2]
```

Значения по умолчанию вычисляются при каждом вызове слева направо и только для отсутствующего аргумента или `undefined`. Второй вызов не меняет `seed`. В третьем вызове первое значение по умолчанию увеличивает `seed` до 2, а явный аргумент `20` отключает вычисление второго.

При сложном списке параметров выражения по умолчанию выполняются в отдельном окружении параметров, которое находится снаружи окружения тела функции. Объявление из тела там не видно, поэтому попытка вызвать его из значения по умолчанию даёт `ReferenceError` во время вызова.

### JS-FUNCTIONS-Q11

[Вернуться к вопросу](../../by-domain/01-javascript-and-async-programming.md#js-functions-q11)

`inspect.length === 1`: подсчёт заканчивается перед `b = 2`. При вызове передано пять аргументов, а остаточный параметр собирает позиции после `c` — `["D","E"]`, то есть два значения.

```text
[1, 5, 2]
0
```

Один заранее привязанный аргумент уменьшает `length` исходной функции с 1 до 0. `arguments.length` отражает фактический вызов, а `rest.length` — только собранный остаток.

### JS-FUNCTIONS-Q12

[Вернуться к вопросу](../../by-domain/01-javascript-and-async-programming.md#js-functions-q12)

`map` передаёт `(value, index, array)`. `parseInt` принимает `(string, radix)`, поэтому индекс становится основанием системы счисления: результат равен `[10, NaN, NaN]`. Явный адаптер:

```js
["10", "20", "30"].map(
  (value) => Number.parseInt(value, 10),
);
```

Похожая ошибка возникает, если передать обработчик события в API с другим набором аргументов или передать метод без получателя вызова. Контракты нужно согласовывать явно.

### JS-FUNCTIONS-Q13

[Вернуться к вопросу](../../by-domain/01-javascript-and-async-programming.md#js-functions-q13)

Первый вызов печатает `"USD:10"`. Второй является обычным вызовом в строгом режиме: `this === undefined`, поэтому чтение `this.balance` даёт `TypeError`.

```js
account.read.call(account, "USD");
const bound = account.read.bind(account);
const adapter = (currency) => account.read(currency);
```

`call` подходит для разового вызова. `bind` создаёт новую функцию с закреплённым получателем. Адаптер замыкается над привязкой `account` и при каждом вызове читает её текущее значение. Если привязанная функция или адаптер регистрируется на будущее, ссылку нужно сохранить для последующей очистки.

### JS-FUNCTIONS-Q14

[Вернуться к вопросу](../../by-domain/01-javascript-and-async-programming.md#js-functions-q14)

`call(thisArg, a, b)` и `apply(thisArg, argsLike)` вызывают функцию немедленно. `apply` принимает массивоподобное значение, а spread в `call(thisArg, ...iterable)` требует итерируемое. Функция в строгом режиме получает `thisArg` без преобразований; в нестрогом режиме `null` и `undefined` заменяются глобальным объектом, а примитивы оборачиваются. Для обычной проверки собственного свойства `Object.hasOwn(obj, key)` яснее и безопаснее ручного `hasOwnProperty.call`.

### JS-FUNCTIONS-Q15

[Вернуться к вопросу](../../by-domain/01-javascript-and-async-programming.md#js-functions-q15)

Результат:

```text
["first", "A", "B", "C"]
3 2 1
false false
```

Первый `bind` фиксирует получателя и аргумент `"A"`. Второй `bind` оборачивает уже привязанную функцию: получатель `"second"` не заменяет `"first"`, но `"B"` добавляется после аргументов, привязанных раньше. Каждый вызов `bind` создаёт новую функцию. Свойство `length` уменьшается на число новых заранее привязанных позиционных аргументов, но не становится меньше нуля.

### JS-FUNCTIONS-Q16

[Вернуться к вопросу](../../by-domain/01-javascript-and-async-programming.md#js-functions-q16)

Результат:

```text
["runtime", "outer"]
["fixed", "outer"]
```

Стрелочная функция захватывает `this` из вызова `makeReader.call(...)`. Получатель, позже переданный в `call` или `bind`, игнорируется. Аргументы при этом работают как обычно: `call` передаёт `"runtime"`, а `bind` заранее сохраняет `"fixed"`.

### JS-FUNCTIONS-Q17

[Вернуться к вопросу](../../by-domain/01-javascript-and-async-programming.md#js-functions-q17)

Результат:

```text
Ada
replacement
```

`new` создаёт экземпляр, связывает его с прототипом конструктора, вызывает конструктор с новым экземпляром в `this` и возвращает либо явно возвращённый объект, либо созданный экземпляр. Примитив `10` игнорируется; объект из `Second` заменяет экземпляр. У стрелочной функции нет внутреннего метода `[[Construct]]`. Если исходную функцию можно вызвать как конструктор, то у привязанной функции сохранённый `thisArg` при `new` игнорируется, а заранее привязанные аргументы используются.

### JS-FUNCTIONS-Q18

[Вернуться к вопросу](../../by-domain/01-javascript-and-async-programming.md#js-functions-q18)

Результат:

```text
true
1
false
100
```

`mutate` меняет объект, на который указывает `state`; `before` и `afterMutation` — две ссылки на один объект. `replace` перенаправляет живую привязку `state` на новый объект, который возвращает последующий `read`. Старые переменные по-прежнему ведут к прежнему объекту со значением `count === 1`.

### JS-FUNCTIONS-Q19

[Вернуться к вопросу](../../by-domain/01-javascript-and-async-programming.md#js-functions-q19)

`var` создаёт одну привязку на уровне функции; колбэки вызываются после цикла и читают итоговое значение `3`. `let` создаёт отдельную привязку для каждой итерации:

```js
for (let i = 0; i < 3; i += 1) {
  callbacks.push(() => i);
}
```

Старый вариант через фабрику:

```js
for (var i = 0; i < 3; i += 1) {
  callbacks.push(
    ((snapshot) => () => snapshot)(i),
  );
}
```

Параметр `snapshot` получает новую привязку при каждом вызове фабрики.

### JS-FUNCTIONS-Q20

[Вернуться к вопросу](../../by-domain/01-javascript-and-async-programming.md#js-functions-q20)

```js
function createLimitedCounter({
  initial = 0,
  min = -Infinity,
  max = Infinity,
} = {}) {
  if (
    !Number.isFinite(initial) ||
    typeof min !== "number" ||
    typeof max !== "number" ||
    min > max ||
    initial < min ||
    initial > max
  ) {
    throw new RangeError("invalid counter bounds");
  }

  let value = initial;

  const set = (next) => {
    value = Math.min(max, Math.max(min, next));
    return value;
  };

  return {
    increment: (step = 1) => set(value + step),
    decrement: (step = 1) => set(value - step),
    read: () => value,
    reset: () => set(initial),
  };
}
```

Замыкание даёт закрытую привязку и отдельные функции для каждого экземпляра. Приватное поле класса может подойти лучше, если нужны общие методы в прототипе, явная модель экземпляров и более привычная поддержка объектов в отладчике и инструментах.

### JS-FUNCTIONS-Q21

[Вернуться к вопросу](../../by-domain/01-javascript-and-async-programming.md#js-functions-q21)

Каррирование превращает всю форму вызова в цепочку одноаргументных функций. Частичное применение фиксирует часть первых аргументов и оставляет функцию для остальных:

```js
function partial(operation, ...preset) {
  return (...later) => operation(...preset, ...later);
}
```

Объект настроек обычно яснее при множестве необязательных флагов, развивающемся API и в случаях, когда аргументы не образуют естественную последовательность этапов.

### JS-FUNCTIONS-Q22

[Вернуться к вопросу](../../by-domain/01-javascript-and-async-programming.md#js-functions-q22)

`compose(double, addOne)(3)`: сначала прибавить один → 4, затем удвоить → `8`. `pipe(double, addOne)(3)`: функции перечислены слева направо, поэтому сначала удвоить → 6, затем прибавить один → `7`.

```text
compose(f, g)(x) = f(g(x))  // справа налево
pipe(g, f)(x)    = f(g(x))  // в порядке слева направо
```

### JS-FUNCTIONS-Q23

[Вернуться к вопросу](../../by-domain/01-javascript-and-async-programming.md#js-functions-q23)

Исходный код мутирует объект `order`, принадлежащий вызывающему коду, и скрыто меняет глобальный `audit`. Разделение вычисления и эффекта:

```js
function calculateDiscountedOrder(order, rule) {
  const discount = rule(order);
  return {
    ...order,
    total: order.total - discount,
  };
}

function applyDiscount(order, rule, recordAudit) {
  const result = calculateDiscountedOrder(order, rule);
  recordAudit(result);
  return result;
}
```

Spread сохраняет идентичность вложенных объектов. Если правило или результат меняет вложенные данные, нужно копировать изменяемые уровни либо явно описать владение объектом и допустимую мутацию.

### JS-FUNCTIONS-Q24

[Вернуться к вопросу](../../by-domain/01-javascript-and-async-programming.md#js-functions-q24)

Результат:

```text
/v3
/v2
```

`capturedBinding` читает текущее значение внешней привязки `config`, которая теперь ведёт к новому объекту `/v3`. `currentConfig` сохранил прежний объект; его свойство было изменено до `/v2`, а последующее переназначение `config` уже не влияет на этот объект.

### JS-FUNCTIONS-Q25

[Вернуться к вопросу](../../by-domain/01-javascript-and-async-programming.md#js-functions-q25)

Возможная цепочка: реестр приложения → функция-обработчик → лексическое окружение → ответ сервера → вложенный граф. Удаление DOM-узла само по себе не разрывает ссылку из реестра. Замыкание — нормальный механизм; утечку доказывает сохранение объекта после ожидаемой очистки и повторяющийся рост памяти.

Решение:

- извлечь только нужный примитив или небольшую неизменяемую выжимку;
- сохранить ссылку на обработчик;
- снимать регистрацию при закрытии окна, желательно идемпотентно;
- удалять запись из реестра или подписки;
- сравнить снимки кучи после нескольких циклов открытия и закрытия и проверить цепочку удержания.

### JS-FUNCTIONS-Q26

[Вернуться к вопросу](../../by-domain/01-javascript-and-async-programming.md#js-functions-q26)

Каждый `bind` создаёт новую функцию, поэтому `removeEventListener` получает не ту ссылку. Ссылка на таймер очищается, но повторный `start` может потерять предыдущий идентификатор таймера и обработчик. Один из вариантов решения на уровне функций:

```js
class Controller {
  constructor() {
    this.onClick = this.handle.bind(this);
    this.onRefresh = this.refresh.bind(this);
    this.button = null;
    this.timer = null;
  }

  start(button) {
    this.stop();
    this.button = button;
    button.addEventListener("click", this.onClick);
    this.timer = setInterval(this.onRefresh, 1000);
  }

  stop() {
    this.button?.removeEventListener("click", this.onClick);
    if (this.timer !== null) clearInterval(this.timer);
    this.button = null;
    this.timer = null;
  }
}
```

Ссылки стабильны, очистку можно безопасно повторить, а владелец хранит сведения о регистрациях. Полный дизайн класса и прототипа остаётся в 1.4.

### JS-FUNCTIONS-Q27

[Вернуться к вопросу](../../by-domain/01-javascript-and-async-programming.md#js-functions-q27)

```js
function memoizeUnary(operation, { maxSize = 100 } = {}) {
  if (!Number.isInteger(maxSize) || maxSize < 1) {
    throw new RangeError("maxSize must be a positive integer");
  }

  const cache = new Map();

  return function memoized(key) {
    if (cache.has(key)) {
      const value = cache.get(key);
      cache.delete(key);
      cache.set(key, value);
      return value;
    }

    const value = operation(key);
    cache.set(key, value);

    if (cache.size > maxSize) {
      const oldestKey = cache.keys().next().value;
      cache.delete(oldestKey);
    }

    return value;
  };
}
```

Проверка через `has` корректно отличает сохранённый `undefined` от отсутствующей записи. Ключи `Map` сравниваются по SameValueZero, а объекты — по идентичности. Для рабочего кода нужно отдельно решить, удалять ли отклонённые промисы и ошибки, как учитывать TTL и устаревание, допустимы ли изменяемые ключи, как наблюдать работу кеша и какова реальная доля повторных попаданий. Если операция дешева или входные данные почти всегда уникальны, кеш лучше убрать.

### JS-FUNCTIONS-Q28

[Вернуться к вопросу](../../by-domain/01-javascript-and-async-programming.md#js-functions-q28)

Первый вызов метода получает `this = processor`. Значение по умолчанию `transform = this.normalize` вычисляется во время вызова и получает функцию метода. Затем она вызывается в обычной форме `transform(...)`, но `normalize` не использует `this`. Результат `"id: 1"` сохраняется в кеше, а `size` печатает `1`.

Отделённый вызов входит в `process` с `this === undefined`. Выражение по умолчанию пытается прочитать `this.normalize` и выбрасывает `TypeError` до выполнения тела функции.

Исправление — убрать зависимость значения по умолчанию от получателя вызова:

```js
const normalize = (value) => value.trim().toLowerCase();

function createProcessor(
  { prefix = "ID", maxSize = 100 } = {},
) {
  const cache = new Map();

  function process(value, transform = normalize) {
    if (cache.has(value)) return cache.get(value);
    const result = transform(prefix + ":" + value);
    cache.set(value, result);
    if (cache.size > maxSize) {
      cache.delete(cache.keys().next().value);
    }
    return result;
  }

  return {
    process,
    normalize,
    size: () => cache.size,
    clear: () => cache.clear(),
  };
}
```

Нормализация становится чистой явной зависимостью, замыкание управляет ограниченным кешем и его очисткой, а отделённый `process` работает. В 1.3 достаточно анализа вызова и замыкания; связи классов и прототипов относятся к 1.4.
