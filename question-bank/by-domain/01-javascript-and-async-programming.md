# 1. JavaScript и асинхронное программирование — вопросы

> Статус: `частично готово — 1.1–1.3 одобрены; 1.4–1.12 остаются заглушками`
>
> Ответы: [в отдельном файле](../answers/by-domain/01-javascript-and-async-programming.md)
>
> Разделы 1.4–1.12 остаются заглушками.

## 1.1. Модель выполнения, объявления и области видимости

Используйте эти вопросы для активного воспроизведения знаний. Не открывайте файл с ответами до самостоятельной попытки.

### JS-SCOPE-Q01

**Сравните `var`, `let` и `const`.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.1. Модель выполнения, объявления и области видимости`
- Уровень: `Junior`
- Тип: `conceptual | compare`
- Приоритет/частота: `Core | F3`
- Связанные inventory IDs: `JS-01`
- Статус modern/legacy: `современная рекомендация + legacy-знание о var`
- Ответ: [JS-SCOPE-Q01](../answers/by-domain/01-javascript-and-async-programming.md#js-scope-q01)
- Источники / последняя проверка: `ECMAScript 2026, MDN | 2026-09-23`

#### Вопрос

Сравните три вида объявлений: где имя видно, что происходит до строки объявления, можно ли присвоить новое значение и можно ли объявить то же имя ещё раз. В конце сформулируйте правило выбора для современного рабочего кода.

### JS-SCOPE-Q02

**Назовите основные границы области видимости.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.1. Модель выполнения, объявления и области видимости`
- Уровень: `Junior`
- Тип: `conceptual | explain`
- Приоритет/частота: `Core | F3`
- Связанные inventory IDs: `JS-02`
- Статус modern/legacy: `современная основа`
- Ответ: [JS-SCOPE-Q02](../answers/by-domain/01-javascript-and-async-programming.md#js-scope-q02)
- Источники / последняя проверка: `ECMAScript 2026 | 2026-09-23`

#### Вопрос

Объясните глобальную область видимости, область видимости функции, блока и модуля. Затем объясните, почему лексическая область видимости (`lexical scope`) — это правило разрешения имён, а не ещё одна равноправная граница.

### JS-SCOPE-Q03

**Чем отличаются объявление, инициализация и присваивание?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.1. Модель выполнения, объявления и области видимости`
- Уровень: `Junior`
- Тип: `conceptual | why`
- Приоритет/частота: `Core | F3`
- Связанные inventory IDs: `JS-01`, `JS-03`
- Статус modern/legacy: `современная основа`
- Ответ: [JS-SCOPE-Q03](../answers/by-domain/01-javascript-and-async-programming.md#js-scope-q03)
- Источники / последняя проверка: `ECMAScript 2026 | 2026-09-23`

#### Вопрос

На примере `let count = 1; count = 2;` укажите объявление, создание привязки (`binding`), инициализацию и последующее присваивание. Почему это различие важно для временной мёртвой зоны (Temporal Dead Zone, TDZ) и `const`?

### JS-SCOPE-Q04

**Предскажите результат с учётом состояния привязки.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.1. Модель выполнения, объявления и области видимости`
- Уровень: `Junior`
- Тип: `output`
- Приоритет/частота: `Core | F3`
- Связанные inventory IDs: `JS-03`
- Статус modern/legacy: `современная основа + legacy-знание о var`
- Ответ: [JS-SCOPE-Q04](../answers/by-domain/01-javascript-and-async-programming.md#js-scope-q04)
- Источники / последняя проверка: `ECMAScript 2026, MDN: hoisting | 2026-09-23`

#### Вопрос

Считайте каждый фрагмент отдельным скриптом. Предскажите результат и назовите состояние привязки в момент чтения.

```js
console.log(a);
var a = 1;
```

```js
console.log(b);
let b = 1;
```

```js
console.log(typeof c);
const c = 1;
```

```js
console.log(typeof neverDeclared);
```

### JS-SCOPE-Q05

**Когда становятся доступны объявление функции (`function declaration`) и функциональное выражение (`function expression`)?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.1. Модель выполнения, объявления и области видимости`
- Уровень: `Junior`
- Тип: `compare | output`
- Приоритет/частота: `Core | F3`
- Связанные inventory IDs: `JS-03`
- Статус modern/legacy: `современная основа + legacy-знание о var`
- Ответ: [JS-SCOPE-Q05](../answers/by-domain/01-javascript-and-async-programming.md#js-scope-q05)
- Источники / последняя проверка: `ECMAScript 2026, MDN: объявления и выражения функций | 2026-09-23`

#### Вопрос

Для каждого независимого фрагмента определите, завершится ли вызов успешно или выбросит исключение. Если будет исключение, назовите класс ошибки и объясните причину.

```js
ready();
function ready() {}
```

```js
ready();
var ready = function () {};
```

```js
ready();
const ready = function () {};
```

### JS-SCOPE-Q06

**Сокрытие имени (`shadowing`) или повторное объявление?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.1. Модель выполнения, объявления и области видимости`
- Уровень: `Junior`
- Тип: `conceptual | why`
- Приоритет/частота: `Core | F2`
- Связанные inventory IDs: `JS-04`
- Статус modern/legacy: `современная основа + взаимодействие с legacy-var`
- Ответ: [JS-SCOPE-Q06](../answers/by-domain/01-javascript-and-async-programming.md#js-scope-q06)
- Источники / последняя проверка: `ECMAScript 2026, MDN: let/var | 2026-09-23`

#### Вопрос

Дайте определения shadowing и повторного объявления (`redeclaration`). Почему первый фрагмент допустим, а второй отклоняется?

```js
var mode = "outer";
{
  let mode = "inner";
}
```

```js
let mode = "outer";
{
  var mode = "inner";
}
```

### JS-SCOPE-Q07

**Найдите и исправьте случайную глобальную переменную.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.1. Модель выполнения, объявления и области видимости`
- Уровень: `Junior`
- Тип: `debugging`
- Приоритет/частота: `Core | F2`
- Связанные inventory IDs: `JS-22`
- Статус modern/legacy: `современная профилактика + legacy-поведение нестрогого скрипта`
- Ответ: [JS-SCOPE-Q07](../answers/by-domain/01-javascript-and-async-programming.md#js-scope-q07)
- Источники / последняя проверка: `ECMAScript 2026, MDN: strict mode | 2026-09-23`

#### Вопрос

Классический браузерный скрипт неожиданно создаёт `total` в `globalThis`:

```js
function update(items) {
  total = items.length;
}

update(["a", "b"]);
```

Объясните поведение нестрогого (`sloppy`) скрипта, предскажите результат в строгом режиме (`strict mode`), исправьте дефект и назовите два способа его предотвращения.

Затем ответьте:

- с чем работает `delete globalThis.total` после выполнения нестрогой версии и что он обычно возвращает?
- почему `delete` не может удалить локальную привязку, объявленную через `let`/`const`?
- что произойдёт, если строгий код содержит `delete total`?

### JS-SCOPE-Q08

**Контекст выполнения (`execution context`), запись окружения (`Environment Record`) и стек вызовов (`call stack`).**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.1. Модель выполнения, объявления и области видимости`
- Уровень: `Mid`
- Тип: `conceptual | explain`
- Приоритет/частота: `Core | F3`
- Связанные inventory IDs: `JS-02`, `JS-03`
- Статус modern/legacy: `современная основа`
- Ответ: [JS-SCOPE-Q08](../answers/by-domain/01-javascript-and-async-programming.md#js-scope-q08)
- Источники / последняя проверка: `ECMAScript 2026: execution contexts и environment records | 2026-09-23`

#### Вопрос

Разграничьте контекст выполнения, стек вызовов, область видимости и запись окружения. Проследите, что меняется, когда `outer()` вызывает `inner()`, и что меняется, когда `inner()` входит в блок `if`.

### JS-SCOPE-Q09

**Проследите лексическое разрешение имени.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.1. Модель выполнения, объявления и области видимости`
- Уровень: `Mid`
- Тип: `output | explain`
- Приоритет/частота: `Core | F3`
- Связанные inventory IDs: `JS-02`
- Статус modern/legacy: `современная основа`
- Ответ: [JS-SCOPE-Q09](../answers/by-domain/01-javascript-and-async-programming.md#js-scope-q09)
- Источники / последняя проверка: `ECMAScript 2026: разрешение идентификаторов | 2026-09-23`

#### Вопрос

Предскажите вывод, затем перечислите записи окружения, которые проверяются при чтении `name`.

```js
const name = "global";

function makeReader() {
  const name = "factory";
  return function () {
    return name;
  };
}

function run(reader) {
  const name = "caller";
  console.log(reader());
}

run(makeReader());
```

Почему локальная привязка вызывающей функции не получает приоритет?

### JS-SCOPE-Q10

**Почему блок не добавляет кадр в стек вызовов?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.1. Модель выполнения, объявления и области видимости`
- Уровень: `Mid`
- Тип: `why | compare`
- Приоритет/частота: `Professional | F2`
- Связанные inventory IDs: `JS-02`
- Статус modern/legacy: `современная основа`
- Ответ: [JS-SCOPE-Q10](../answers/by-domain/01-javascript-and-async-programming.md#js-scope-q10)
- Источники / последняя проверка: `ECMAScript 2026: execution contexts | 2026-09-23`

#### Вопрос

Сравните вход в `{ const value = 1; }` с вызовом `function f() { const value = 1; }`. Какое новое состояние спецификационной модели требуется в каждом случае и почему модель «одна область видимости равна одному кадру стека» неверна?

### JS-SCOPE-Q11

**Найдите все дефекты объявлений.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.1. Модель выполнения, объявления и области видимости`
- Уровень: `Mid`
- Тип: `find-the-bug | output`
- Приоритет/частота: `Core | F2`
- Связанные inventory IDs: `JS-01`, `JS-04`
- Статус modern/legacy: `современная основа + взаимодействие с legacy-var`
- Ответ: [JS-SCOPE-Q11](../answers/by-domain/01-javascript-and-async-programming.md#js-scope-q11)
- Источники / последняя проверка: `ECMAScript 2026: ранние ошибки объявлений | 2026-09-23`

#### Вопрос

Классифицируйте каждый независимый фрагмент как допустимый код или раннюю ошибку (`Early Error`). Для допустимого кода укажите, какая привязка читается.

```js
function first() {
  let id = 1;
  {
    var id = 2;
  }
}
```

```js
function second() {
  var id = 1;
  {
    let id = 2;
    console.log(id);
  }
}
```

```js
const id = 1;
const id = 2;
```

Если во фрагменте есть ранняя ошибка, выполнится ли предшествующий ей `console.log` в той же единице разбора?

### JS-SCOPE-Q12

**Глобальные объявления в классическом браузерном скрипте и модуле.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.1. Модель выполнения, объявления и области видимости`
- Уровень: `Mid`
- Тип: `compare | output`
- Приоритет/частота: `Professional | F2`
- Связанные inventory IDs: `JS-02`, `JS-22`
- Статус modern/legacy: `современные модули + совместимость с классическим скриптом`
- Ответ: [JS-SCOPE-Q12](../answers/by-domain/01-javascript-and-async-programming.md#js-scope-q12)
- Источники / последняя проверка: `ECMAScript 2026: global environment, HTML Living Standard | 2026-09-23`

#### Вопрос

Предскажите два логических результата сначала при загрузке как классического браузерного скрипта, затем как браузерного ES-модуля:

```js
var fromVar = 1;
let fromLet = 2;

console.log(globalThis.fromVar === 1);
console.log(globalThis.fromLet === 2);
```

Объясните глобальную запись окружения (`Global Environment Record`) на практическом уровне. Не используйте поведение консоли DevTools как доказательство.

### JS-SCOPE-Q13

**Одна привязка цикла или отдельная для каждой итерации?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.1. Модель выполнения, объявления и области видимости`
- Уровень: `Mid`
- Тип: `output | why`
- Приоритет/частота: `Core | F3`
- Связанные inventory IDs: `JS-01`, `JS-02`
- Статус modern/legacy: `современная рекомендация + legacy-знание о var`
- Ответ: [JS-SCOPE-Q13](../answers/by-domain/01-javascript-and-async-programming.md#js-scope-q13)
- Источники / последняя проверка: `ECMAScript 2026, MDN: for/closures | 2026-09-23`

#### Вопрос

Предскажите содержимое обоих массивов и объясните результат через **привязки**, а не через «магию таймингов».

```js
const withVar = [];
for (var i = 0; i < 3; i += 1) {
  withVar.push(() => i);
}

const withLet = [];
for (let j = 0; j < 3; j += 1) {
  withLet.push(() => j);
}

console.log(withVar.map((read) => read()));
console.log(withLet.map((read) => read()));
```

### JS-SCOPE-Q14

**Исправьте повторные объявления в `switch`.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.1. Модель выполнения, объявления и области видимости`
- Уровень: `Mid`
- Тип: `find-the-bug | debugging`
- Приоритет/частота: `Professional | F2`
- Связанные inventory IDs: `JS-01`, `JS-04`
- Статус modern/legacy: `современная основа`
- Ответ: [JS-SCOPE-Q14](../answers/by-domain/01-javascript-and-async-programming.md#js-scope-q14)
- Источники / последняя проверка: `ECMAScript 2026: block declarations, MDN: let | 2026-09-23`

#### Вопрос

Почему эта функция отклоняется из-за ранней ошибки, хотя выполняется только один `case`? Исправьте её, не вынося `message` за пределы ветвей.

```js
function label(status) {
  switch (status) {
    case "idle":
      const message = "Waiting";
      return message;
    case "done":
      const message = "Complete";
      return message;
    default:
      return "Unknown";
  }
}
```

### JS-SCOPE-Q15

**Проведите ревью устаревшего кода, чувствительного к области видимости.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.1. Модель выполнения, объявления и области видимости`
- Уровень: `Mid`
- Тип: `code-review | refactoring`
- Приоритет/частота: `Professional | F2`
- Связанные inventory IDs: `JS-01`, `JS-02`, `JS-22`
- Статус modern/legacy: `диагностика legacy-кода → современная рекомендация`
- Ответ: [JS-SCOPE-Q15](../answers/by-domain/01-javascript-and-async-programming.md#js-scope-q15)
- Источники / последняя проверка: `ECMAScript 2026, MDN: strict mode/closures | 2026-09-23`

#### Вопрос

Проведите ревью корректности, владения глобальным состоянием и сопровождаемости. Расставьте замечания по серьёзности; не ограничивайтесь механической заменой каждого `var`.

```js
function register(items) {
  handlers = {};

  for (var i = 0; i < items.length; i += 1) {
    handlers[i] = function () {
      return items[i];
    };
  }

  return handlers;
}
```

Предложите минимальное безопасное исправление и более чистый API, ориентированный на модули.

### JS-SCOPE-Q16

**Точно объясните поднятие объявлений (`hoisting`) без излишнего погружения в спецификацию.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.1. Модель выполнения, объявления и области видимости`
- Уровень: `Senior`
- Тип: `conceptual | interview-communication`
- Приоритет/частота: `Core | F3`
- Связанные inventory IDs: `JS-03`
- Статус modern/legacy: `современная основа + точная терминология`
- Ответ: [JS-SCOPE-Q16](../answers/by-domain/01-javascript-and-async-programming.md#js-scope-q16)
- Источники / последняя проверка: `ECMAScript 2026: declaration instantiation, MDN: hoisting | 2026-09-23`

#### Вопрос

Дайте ответ на 45–60 секунд, который:

1. отвергает модель физического перемещения исходного кода;
2. объясняет `var`, лексические объявления и объявления функций;
3. не перегружен ненужными деталями абстрактных операций (`abstract operations`);
4. остаётся достаточно точным для последующего Senior-вопроса.

### JS-SCOPE-Q17

**Объясните глобальную запись окружения браузера (`Global Environment Record`).**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.1. Модель выполнения, объявления и области видимости`
- Уровень: `Senior`
- Тип: `conceptual | explain`
- Приоритет/частота: `Professional | F2`
- Связанные inventory IDs: `JS-02`, `JS-22`
- Статус modern/legacy: `совместимость с классическим скриптом + сравнение с современными модулями`
- Ответ: [JS-SCOPE-Q17](../answers/by-domain/01-javascript-and-async-programming.md#js-scope-q17)
- Источники / последняя проверка: `ECMAScript 2026: global environment, HTML Living Standard | 2026-09-23`

#### Вопрос

Объясните объектную запись (`Object Record`) и декларативную запись (`Declarative Record`), не создавая впечатления, что движки буквально используют два JavaScript-объекта. Включите в ответ объявленные на верхнем уровне (`top-level`) `var`, объявления функций, `let`, `const`, модули и `globalThis`.

### JS-SCOPE-Q18

**Диагностируйте глобальный конфликт, возникающий только в рабочей среде.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.1. Модель выполнения, объявления и области видимости`
- Уровень: `Senior`
- Тип: `practical-scenario | debugging`
- Приоритет/частота: `Professional | F2`
- Связанные inventory IDs: `JS-02`, `JS-04`, `JS-22`
- Статус modern/legacy: `legacy-классические скрипты → современная граница модуля`
- Ответ: [JS-SCOPE-Q18](../answers/by-domain/01-javascript-and-async-programming.md#js-scope-q18)
- Источники / последняя проверка: `ECMAScript 2026: GlobalDeclarationInstantiation | 2026-09-23`

#### Вопрос

В среде разработки используются собранные модули, и всё работает. В рабочей среде эти независимые классические скрипты загружаются по порядку:

```html
<script src="app-config.js"></script>
<script src="vendor-widget.js"></script>
```

```js
// app-config.js
let config = { locale: "en" };
```

```js
// vendor-widget.js
console.log("vendor starts");
var config = { mode: "compact" };
```

Что произойдёт при инстанцировании второго скрипта? Выполнится ли его `console.log`? Предложите немедленную меру снижения риска и долговременное архитектурное исправление.

### JS-SCOPE-Q19

**Проверьте предположение о коде верхнего уровня в разных средах выполнения.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.1. Модель выполнения, объявления и области видимости`
- Уровень: `Senior`
- Тип: `code-review | trade-off`
- Приоритет/частота: `Professional | F2`
- Связанные inventory IDs: `JS-02`, `JS-22`
- Статус modern/legacy: `современное ревью переносимости`
- Ответ: [JS-SCOPE-Q19](../answers/by-domain/01-javascript-and-async-programming.md#js-scope-q19)
- Источники / последняя проверка: `ECMAScript 2026, Node.js: module wrapper | 2026-09-23`

#### Вопрос

Автор библиотеки ожидает, что этот код одинаково сработает в классическом браузерном скрипте, браузерном модуле, Node.js ESM и Node.js CommonJS:

```js
var registry = { enabled: true };
console.log(globalThis.registry.enabled);
```

Проведите ревью этого предположения. Если намеренная публикация глобального свойства действительно нужна, какой явный контракт вы используете? Если она не нужна, что модуль должен экспортировать вместо этого?

### JS-SCOPE-Q20

**Реализуйте явный мост к глобальному API устаревшей системы.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.1. Модель выполнения, объявления и области видимости`
- Уровень: `Senior`
- Тип: `implementation | practical-scenario`
- Приоритет/частота: `Professional | F2`
- Связанные inventory IDs: `JS-02`, `JS-22`
- Статус modern/legacy: `legacy-совместимость с явным современным владением`
- Ответ: [JS-SCOPE-Q20](../answers/by-domain/01-javascript-and-async-programming.md#js-scope-q20)
- Источники / последняя проверка: `ECMAScript 2026: per-iteration environments | 2026-09-23`

#### Вопрос

Обычно приложение использует ES-модули, но одному устаревшему потребителю требуется единственное свойство на переданном объекте, играющем роль глобального. Реализуйте:

```js
const uninstall = installLegacyApi(root, api);
```

Контракт:

- используйте имя свойства `frontendInterview`;
- отклоняйте установку, если у `root` уже есть собственное свойство с таким именем;
- публикуйте `api` через явную запись свойства — никогда через неразрешённый идентификатор;
- `uninstall()` удаляет свойство, только если в нём всё ещё находится тот же установленный `api`;
- возвращайте `true`, только если очистка действительно удалила свойство; иначе возвращайте `false`;
- используйте `root`, а не жёстко заданный `window`, чтобы мост можно было тестировать и чтобы он не зависел от окружения хоста (`host environment`).

Объясните, почему `delete root.frontendInterview` здесь уместен, почему `delete` не может удалить лексическую привязку и почему обычный экспорт из модуля остаётся предпочтительным API для рабочего кода.

## 1.2. Значения, типы, равенство и преобразование типов

Используйте вопросы для active recall. Модельные ответы находятся в отдельном файле и не должны открываться до собственной попытки.

### JS-VALUES-Q01

**Какие значения в JavaScript являются primitives, а какие — objects?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.2. Значения, типы, равенство и преобразование типов`
- Уровень: `Junior`
- Тип: `conceptual | explain`
- Приоритет/частота: `Core | F3`
- Связанные inventory IDs: `JS-05`, `JS-06`
- Статус modern/legacy: `современная основа`
- Ответ: [JS-VALUES-Q01](../answers/by-domain/01-javascript-and-async-programming.md#js-values-q01)
- Источники / последняя проверка: `ECMAScript 2026, MDN: data types | 2026-10-01`

#### Вопрос

Перечислите семь primitive types и объясните, почему функция одновременно даёт `typeof value === "function"`, но относится к object values. Затем разграничьте:

- type текущего value;
- возможность переназначить binding;
- mutability самого value.

Покажите различие на одном `let` с values разных типов и одном `const`-объекте.

### JS-VALUES-Q02

**Primitive immutability, object mutation или reassignment?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.2. Значения, типы, равенство и преобразование типов`
- Уровень: `Junior`
- Тип: `compare | output`
- Приоритет/частота: `Core | F3`
- Связанные inventory IDs: `JS-05`
- Статус modern/legacy: `современная основа`
- Ответ: [JS-VALUES-Q02](../answers/by-domain/01-javascript-and-async-programming.md#js-values-q02)
- Источники / последняя проверка: `ECMAScript 2026, MDN: primitives | 2026-10-01`

#### Вопрос

Предскажите вывод и для каждой строки назовите операцию: получение нового primitive, mutation или reassignment.

```js
let label = "draft";
label.toUpperCase();

const settings = { mode: "light" };
const alias = settings;
settings.mode = "dark";

console.log(label);
console.log(alias.mode);
console.log(settings === alias);
```

Почему `const` не делает `settings` immutable?

### JS-VALUES-Q03

**Докажите, что object argument передаётся по value.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.2. Значения, типы, равенство и преобразование типов`
- Уровень: `Junior`
- Тип: `conceptual | why | output`
- Приоритет/частота: `Core | F3`
- Связанные inventory IDs: `JS-05`, `JS-11`
- Статус modern/legacy: `современная основа`
- Ответ: [JS-VALUES-Q03](../answers/by-domain/01-javascript-and-async-programming.md#js-values-q03)
- Источники / последняя проверка: `ECMAScript 2026: function calls and bindings | 2026-10-01`

#### Вопрос

Предскажите результат и объясните его через два bindings и один object identity:

```js
function change(item) {
  item.enabled = true;
  item = { enabled: false };
}

const config = { enabled: false };
change(config);

console.log(config.enabled);
```

Почему mutation видна вызывающему коду, а reassignment параметра — нет? Почему формулировка «objects передаются by reference» неточна?

### JS-VALUES-Q04

**Что вернёт `typeof` и где появится ошибка?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.2. Значения, типы, равенство и преобразование типов`
- Уровень: `Junior`
- Тип: `output | explain`
- Приоритет/частота: `Core | F3`
- Связанные inventory IDs: `JS-06`
- Статус modern/legacy: `современная основа + historical oddity`
- Ответ: [JS-VALUES-Q04](../answers/by-domain/01-javascript-and-async-programming.md#js-values-q04)
- Источники / последняя проверка: `ECMAScript 2026, MDN: typeof | 2026-10-01`

#### Вопрос

Считайте фрагменты независимыми. Предскажите результат и объясните каждую строку:

```js
typeof null;
typeof NaN;
typeof 1n;
typeof Symbol("id");
typeof [];
typeof function () {};
```

```js
let declared;
console.log(typeof declared);
console.log(typeof neverDeclared);
```

```js
// Намеренно проверяется TDZ.
console.log(typeof later);
let later;
```

Почему `typeof value === "undefined"` не доказывает, что identifier необъявлен?

### JS-VALUES-Q05

**Сравните `Symbol` и `BigInt`.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.2. Значения, типы, равенство и преобразование типов`
- Уровень: `Junior`
- Тип: `conceptual | compare`
- Приоритет/частота: `Core | F2`
- Связанные inventory IDs: `JS-06`
- Статус modern/legacy: `современная основа`
- Ответ: [JS-VALUES-Q05](../answers/by-domain/01-javascript-and-async-programming.md#js-values-q05)
- Источники / последняя проверка: `ECMAScript 2026, MDN: Symbol/BigInt | 2026-10-01`

#### Вопрос

Объясните назначение, создание, `typeof` и ключевые ограничения обоих primitives. Обязательно разберите:

- `Symbol("id") === Symbol("id")`;
- Symbol как property key;
- `5n / 2n`;
- `1n + 1`;
- почему явный переход BigInt → Number может потерять точность;
- почему BigInt не является decimal type для денег.

### JS-VALUES-Q06

**Как проверять `NaN`, Infinity и signed zero?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.2. Значения, типы, равенство и преобразование типов`
- Уровень: `Junior`
- Тип: `conceptual | output`
- Приоритет/частота: `Core | F2`
- Связанные inventory IDs: `JS-07`, `JS-09`
- Статус modern/legacy: `современная основа`
- Ответ: [JS-VALUES-Q06](../answers/by-domain/01-javascript-and-async-programming.md#js-values-q06)
- Источники / последняя проверка: `ECMAScript 2026, MDN: Number/NaN | 2026-10-01`

#### Вопрос

Предскажите results и назовите подходящую production-проверку:

```js
NaN === NaN;
Number.isNaN(NaN);
Number.isNaN("hello");
isNaN("hello");
Number.isFinite(Infinity);
0 === -0;
Object.is(0, -0);
1 / -0;
```

Почему проверки `value !== NaN` и «не `NaN` значит finite» неверны?

### JS-VALUES-Q07

**Восстановите truthy/falsy и nullish по памяти.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.2. Значения, типы, равенство и преобразование типов`
- Уровень: `Junior`
- Тип: `recall | conceptual`
- Приоритет/частота: `Core | F3`
- Связанные inventory IDs: `JS-08`
- Статус modern/legacy: `современная основа`
- Ответ: [JS-VALUES-Q07](../answers/by-domain/01-javascript-and-async-programming.md#js-values-q07)
- Источники / последняя проверка: `ECMAScript 2026: ToBoolean | 2026-10-01`

#### Вопрос

Перечислите все практические falsy values, отдельно назовите nullish values и предскажите:

```js
Boolean("0");
Boolean([]);
Boolean({});
Boolean(0n);
Boolean(new Boolean(false));
```

Почему «empty object is falsy» — неверная mental model?

### JS-VALUES-Q08

**Выберите `||` или `??` для defaults.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.2. Значения, типы, равенство и преобразование типов`
- Уровень: `Junior`
- Тип: `compare | debugging`
- Приоритет/частота: `Core | F3`
- Связанные inventory IDs: `JS-08`, `JS-40`
- Статус modern/legacy: `современная рекомендация`
- Ответ: [JS-VALUES-Q08](../answers/by-domain/01-javascript-and-async-programming.md#js-values-q08)
- Источники / последняя проверка: `ECMAScript 2026, MDN: nullish coalescing | 2026-10-01`

#### Вопрос

Клиент может намеренно передать `0`, `false` и empty string:

```js
function options(input) {
  return {
    retries: input.retries || 3,
    visible: input.visible || true,
    label: input.label || "Untitled",
  };
}
```

Найдите bug, исправьте код и сформулируйте случай, когда исходный `||` был бы правильным выбором. Что возвращают `||` и `??`: boolean или operand value?

### JS-VALUES-Q09

**Проследите short-circuit и side effects.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.2. Значения, типы, равенство и преобразование типов`
- Уровень: `Mid`
- Тип: `output | why`
- Приоритет/частота: `Core | F3`
- Связанные inventory IDs: `JS-08`, `JS-40`
- Статус modern/legacy: `современная основа`
- Ответ: [JS-VALUES-Q09](../answers/by-domain/01-javascript-and-async-programming.md#js-values-q09)
- Источники / последняя проверка: `ECMAScript 2026: logical operators | 2026-10-01`

#### Вопрос

Предскажите итоговые `calls`, `first`, `second` и `third`:

```js
let calls = 0;
const build = () => {
  calls += 1;
  return "fallback";
};

const first = "ready" || build();
const second = 0 && build();
const third = null ?? build();
```

Почему higher-precedence expression справа может вообще не вычислиться? Когда side effects в short-circuit operand становятся проблемой для code review?

### JS-VALUES-Q10

**Найдите traps optional chaining.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.2. Значения, типы, равенство и преобразование типов`
- Уровень: `Mid`
- Тип: `find-the-bug | output`
- Приоритет/частота: `Core | F3`
- Связанные inventory IDs: `JS-40`
- Статус modern/legacy: `современная основа`
- Ответ: [JS-VALUES-Q10](../answers/by-domain/01-javascript-and-async-programming.md#js-values-q10)
- Источники / последняя проверка: `ECMAScript 2026, MDN: optional chaining | 2026-10-01`

#### Вопрос

Для каждого независимого выражения укажите value, exception или syntax failure и объясните, какое значение защищает `?.`:

```js
const data = null;
data?.user.name;
```

```js
const data = null;
(data?.user).name;
```

```js
const api = {};
api?.save();
api.save?.();
```

```js
const api = { save: "yes" };
api.save?.();
```

```js
// Намеренно недопустимо.
account?.name = "Ada";
```

Дополнительно: вычислится ли `index++` в `items?.[index++]`, если `items === null`?

### JS-VALUES-Q11

**Сравните `==`, `===`, `Object.is` и SameValueZero.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.2. Значения, типы, равенство и преобразование типов`
- Уровень: `Mid`
- Тип: `conceptual | compare`
- Приоритет/частота: `Core | F3`
- Связанные inventory IDs: `JS-09`
- Статус modern/legacy: `современная основа + interview knowledge о ==`
- Ответ: [JS-VALUES-Q11](../answers/by-domain/01-javascript-and-async-programming.md#js-values-q11)
- Источники / последняя проверка: `ECMAScript 2026, MDN: equality comparisons | 2026-10-01`

#### Вопрос

Постройте матрицу для четырёх semantics по осям: coercion, `NaN`, signed zero, object identity. Затем назовите реальные места использования SameValueZero и объясните, почему `Object.is()` не является «самым строгим `===`» или deep equality.

### JS-VALUES-Q12

**Почему shallow copy не устранил shared mutation?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.2. Значения, типы, равенство и преобразование типов`
- Уровень: `Mid`
- Тип: `output | debugging`
- Приоритет/частота: `Professional | F3`
- Связанные inventory IDs: `JS-05`, `JS-09`
- Статус modern/legacy: `современная production-модель`
- Ответ: [JS-VALUES-Q12](../answers/by-domain/01-javascript-and-async-programming.md#js-values-q12)
- Источники / последняя проверка: `ECMAScript 2026, MDN: object identity/spread | 2026-10-01`

#### Вопрос

Предскажите четыре результата и нарисуйте identities:

```js
const base = {
  theme: "light",
  network: { retries: 2 },
};

const copy = { ...base };
copy.theme = "dark";
copy.network.retries = 5;

console.log(base === copy);
console.log(base.network === copy.network);
console.log(base.theme);
console.log(base.network.retries);
```

Как исправить конкретный bug, не обещая universal deep clone? Где проходит граница темы 1.2 и full copying topic 1.5?

### JS-VALUES-Q13

**`Number.isNaN()` против глобального `isNaN()`.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.2. Значения, типы, равенство и преобразование типов`
- Уровень: `Mid`
- Тип: `compare | practical-scenario`
- Приоритет/частота: `Core | F2`
- Связанные inventory IDs: `JS-07`, `JS-10`
- Статус modern/legacy: `современная рекомендация + legacy global API`
- Ответ: [JS-VALUES-Q13](../answers/by-domain/01-javascript-and-async-programming.md#js-values-q13)
- Источники / последняя проверка: `ECMAScript 2026, MDN: isNaN | 2026-10-01`

#### Вопрос

API получает `""`, `"42"`, `"oops"`, `42`, `NaN` или `1n`. Для каждого значения предскажите глобальный `isNaN(value)` и `Number.isNaN(value)`; отметьте возможный exception. Какую последовательность parsing/validation вы выберете, если API принимает только non-empty decimal string или finite Number?

### JS-VALUES-Q14

**Отладьте floating-point и money bug.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.2. Значения, типы, равенство и преобразование типов`
- Уровень: `Mid`
- Тип: `debugging | production-scenario`
- Приоритет/частота: `Professional | F2`
- Связанные inventory IDs: `JS-07`
- Статус modern/legacy: `современная production-рекомендация`
- Ответ: [JS-VALUES-Q14](../answers/by-domain/01-javascript-and-async-programming.md#js-values-q14)
- Источники / последняя проверка: `ECMAScript 2026, MDN: Number.EPSILON/isSafeInteger | 2026-10-01`

#### Вопрос

Checkout сравнивает рассчитанную сумму с ожидаемой:

```js
const expected = 0.3;
const actual = 0.1 + 0.2;

if (actual !== expected) {
  throw new Error("Price mismatch");
}
```

Объясните причину, предложите:

1. domain-aware comparison для general measurements;
2. integer minor-unit model для fixed-scale money;
3. проверки range и rounding policy.

Почему `Math.abs(actual - expected) < Number.EPSILON` не является универсальным money solution?

### JS-VALUES-Q15

**Заполните таблицу explicit conversions.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.2. Значения, типы, равенство и преобразование типов`
- Уровень: `Mid`
- Тип: `output | conceptual`
- Приоритет/частота: `Core | F3`
- Связанные inventory IDs: `JS-08`, `JS-10`
- Статус modern/legacy: `современная основа`
- Ответ: [JS-VALUES-Q15](../answers/by-domain/01-javascript-and-async-programming.md#js-values-q15)
- Источники / последняя проверка: `ECMAScript 2026: ToBoolean/ToNumber/ToString | 2026-10-01`

#### Вопрос

Не выполняя код, заполните `Boolean`, `Number` и `String` для: `undefined`, `null`, `false`, `""`, `"  "`, `"42"`, `"42px"`, `0`, `1n`, `Symbol("x")`.

Отдельно укажите случаи, где возникает `NaN`, `TypeError` или возможная потеря точности. Сравните `Number(value)`, unary `+value`, `String(value)` и `"" + value` там, где они неэквивалентны.

### JS-VALUES-Q16

**Предскажите output operator `+`.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.2. Значения, типы, равенство и преобразование типов`
- Уровень: `Mid`
- Тип: `output | explain`
- Приоритет/частота: `Core | F3`
- Связанные inventory IDs: `JS-10`
- Статус modern/legacy: `современная основа + interview trap`
- Ответ: [JS-VALUES-Q16](../answers/by-domain/01-javascript-and-async-programming.md#js-values-q16)
- Источники / последняя проверка: `ECMAScript 2026: addition operator | 2026-10-01`

#### Вопрос

Предскажите value и type каждого независимого expression, показывая промежуточный `ToPrimitive`/conversion:

```js
1 + 2 + "3";
"1" + 2 + 3;
true + 1;
null + 1;
undefined + 1;
[1] + 2;
1n + 2n;
"1" + 2n;
```

Что произойдёт в намеренно ошибочном `1n + 2` и почему `"5" - 2` ведёт себя иначе, чем `"5" + 2`?

### JS-VALUES-Q17

**Сравните equality и relational coercion.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.2. Значения, типы, равенство и преобразование типов`
- Уровень: `Mid`
- Тип: `output | why`
- Приоритет/частота: `Professional | F2`
- Связанные inventory IDs: `JS-09`, `JS-10`
- Статус modern/legacy: `современная основа + interview trap`
- Ответ: [JS-VALUES-Q17](../answers/by-domain/01-javascript-and-async-programming.md#js-values-q17)
- Источники / последняя проверка: `ECMAScript 2026: comparison operations | 2026-10-01`

#### Вопрос

Предскажите и объясните разные conversion paths:

```js
"2" < "10";
"2" < 10;
null == 0;
null > 0;
null >= 0;
0n === 0;
0n == 0;
1n < 1.5;
```

Почему нельзя моделировать все comparison operators как «сначала Number() обеих сторон»?

### JS-VALUES-Q18

**Проследите `ToPrimitive`, `valueOf()` и `toString()`.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.2. Значения, типы, равенство и преобразование типов`
- Уровень: `Mid`
- Тип: `output | explain`
- Приоритет/частота: `Professional | F3`
- Связанные inventory IDs: `JS-10`
- Статус modern/legacy: `современная основа + specification precision`
- Ответ: [JS-VALUES-Q18](../answers/by-domain/01-javascript-and-async-programming.md#js-values-q18)
- Источники / последняя проверка: `ECMAScript 2026: ToPrimitive, MDN: Symbol.toPrimitive | 2026-10-01`

#### Вопрос

Предскажите call order и results:

```js
const amount = {
  valueOf() {
    console.log("valueOf");
    return 7;
  },
  toString() {
    console.log("toString");
    return "seven";
  },
};

Number(amount);
String(amount);
amount + 1;
```

Затем добавьте `[Symbol.toPrimitive](hint)` и объясните его приоритет, три hints и требование вернуть primitive. Почему `Date` — важное исключение для default hint, но не повод запоминать редкие puzzles?

### JS-VALUES-Q19

**Сформулируйте policy для `==` на code review.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.2. Значения, типы, равенство и преобразование типов`
- Уровень: `Senior`
- Тип: `code-review | trade-off`
- Приоритет/частота: `Professional | F3`
- Связанные inventory IDs: `JS-09`, `JS-10`
- Статус modern/legacy: `современная рекомендация + deliberate legacy-compatible operator knowledge`
- Ответ: [JS-VALUES-Q19](../answers/by-domain/01-javascript-and-async-programming.md#js-values-q19)
- Источники / последняя проверка: `ECMAScript 2026, MDN: loose equality | 2026-10-01`

#### Вопрос

Команда запрещает любой `==`, но в PR появляется:

```js
if (value == null) {
  return "missing";
}
```

Проведите review:

- объясните точную семантику expression;
- сравните с явным `value === null || value === undefined`;
- предложите team/linter policy;
- отделите correctness от readability;
- объясните, почему это не оправдывает `==` в произвольных сравнениях.

### JS-VALUES-Q20

**Выберите equality semantics для коллекции.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.2. Значения, типы, равенство и преобразование типов`
- Уровень: `Senior`
- Тип: `practical-scenario | architecture`
- Приоритет/частота: `Professional | F2`
- Связанные inventory IDs: `JS-07`, `JS-09`
- Статус modern/legacy: `современная основа`
- Ответ: [JS-VALUES-Q20](../answers/by-domain/01-javascript-and-async-programming.md#js-values-q20)
- Источники / последняя проверка: `ECMAScript 2026, MDN: SameValueZero/Set/Map | 2026-10-01`

#### Вопрос

Analytics pipeline должен дедуплицировать primitive readings, среди которых встречаются `NaN`, `0` и `-0`. Сравните:

- `Set`;
- `Array.prototype.includes()`;
- `indexOf()`;
- ручной поиск через `===`;
- ручной поиск через `Object.is()`.

Какие значения каждая стратегия объединит или различит? Что выбрать, если signed zero имеет domain meaning? Как изменится решение для object readings с одинаковым содержимым, но разной identity?

### JS-VALUES-Q21

**Проведите review shared mutation и shallow copy.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.2. Значения, типы, равенство и преобразование типов`
- Уровень: `Senior`
- Тип: `code-review | refactoring`
- Приоритет/частота: `Professional | F2`
- Связанные inventory IDs: `JS-05`, `JS-11`
- Статус modern/legacy: `современная production-модель`
- Ответ: [JS-VALUES-Q21](../answers/by-domain/01-javascript-and-async-programming.md#js-values-q21)
- Источники / последняя проверка: `ECMAScript 2026, MDN: object identity | 2026-10-01`

#### Вопрос

```js
const DEFAULTS = {
  retry: { count: 2 },
  headers: { accept: "application/json" },
};

export function buildOptions(overrides = {}) {
  const options = { ...DEFAULTS, ...overrides };
  options.retry.count += 1;
  return options;
}
```

Ранжируйте review findings по серьёзности. Нарисуйте shared identities, объясните изменение между вызовами и предложите минимальное исправление без универсального deep clone. Какие ownership/immutability expectations должен документировать API?

### JS-VALUES-Q22

**Спроектируйте numeric input boundary.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.2. Значения, типы, равенство и преобразование типов`
- Уровень: `Senior`
- Тип: `debugging | practical-scenario`
- Приоритет/частота: `Advanced | F2`
- Связанные inventory IDs: `JS-06`, `JS-07`, `JS-10`
- Статус modern/legacy: `современная production-рекомендация`
- Ответ: [JS-VALUES-Q22](../answers/by-domain/01-javascript-and-async-programming.md#js-values-q22)
- Источники / последняя проверка: `ECMAScript 2026, MDN: Number/isFinite/isSafeInteger | 2026-10-01`

#### Вопрос

Backend принимает quantity от UI и сейчас делает:

```js
function parseQuantity(input) {
  const value = Number(input);
  if (!Number.isNaN(value)) return value;
  throw new Error("invalid");
}
```

Найдите inputs, которые функция неожиданно принимает: empty/whitespace, infinities, fractions, negative zero, unsafe integers. Сформулируйте contract для positive safe integer quantity, реализуйте validation order и объясните, где явное coercion всё ещё недостаточно.

### JS-VALUES-Q23

**Реализуйте scale-aware `nearlyEqual`.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.2. Значения, типы, равенство и преобразование типов`
- Уровень: `Senior`
- Тип: `implementation | testing`
- Приоритет/частота: `Advanced | F2`
- Связанные inventory IDs: `JS-07`
- Статус modern/legacy: `современная production-рекомендация`
- Ответ: [JS-VALUES-Q23](../answers/by-domain/01-javascript-and-async-programming.md#js-values-q23)
- Источники / последняя проверка: `MDN: Number.EPSILON | 2026-10-01`

#### Вопрос

Реализуйте:

```js
nearlyEqual(left, right, {
  relativeTolerance,
  absoluteTolerance,
});
```

Контракт:

- exact equal values, включая одинаковые infinities, возвращают `true`;
- разные non-finite values и `NaN` возвращают `false`;
- finite values сравниваются через maximum из absolute и scale-aware relative tolerance;
- defaults должны быть явно документированы как пример, а не universal truth;
- добавьте tests для near zero, values около `1`, больших magnitudes, signed zero, infinities и `NaN`.

### JS-VALUES-Q24

**Интегрированный challenge: identity, equality и coercion.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.2. Значения, типы, равенство и преобразование типов`
- Уровень: `Senior`
- Тип: `output | debugging | interview-communication`
- Приоритет/частота: `Advanced | F3`
- Связанные inventory IDs: `JS-05`, `JS-07`, `JS-08`, `JS-09`, `JS-10`, `JS-11`, `JS-40`
- Статус modern/legacy: `современная production-модель + ограниченная puzzle practice`
- Ответ: [JS-VALUES-Q24](../answers/by-domain/01-javascript-and-async-programming.md#js-values-q24)
- Источники / последняя проверка: `ECMAScript 2026, MDN primary references | 2026-10-01`

#### Вопрос

Не запускайте код до полного прогноза:

```js
const source = {
  amount: "0",
  meta: { attempts: 0 },
};

const copy = { ...source };

function prepare(input) {
  input.meta.attempts += 1;

  return {
    amount: input.amount || 10,
    label: input.details?.label ?? "none",
    numeric: input.amount + 1,
  };
}

const result = prepare(copy);

console.log(source.meta.attempts);
console.log(source === copy);
console.log(source.meta === copy.meta);
console.log(result);
console.log([NaN].includes(NaN), [NaN].indexOf(NaN));
```

Задание:

1. предскажите каждый output;
2. назовите identity/equality/coercion rule на каждом шаге;
3. найдите ambiguous requirements вокруг string `"0"` и defaulting;
4. предложите typed normalization boundary и безопасную ownership model;
5. объясните анализ за три минуты без формулировки «objects передаются by reference».

## 1.3. Функции, замыкания и функциональные паттерны

Не открывайте отдельный файл ответов до собственной попытки. В задачах на результат сначала подпишите привязки, форму вызова и момент, когда вызывается колбэк.

### JS-FUNCTIONS-Q01

**Сравните основные формы функций.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.3. Функции, замыкания и функциональные паттерны`
- Уровень: `Junior`
- Тип: `conceptual | compare`
- Приоритет/частота: `Core | F3`
- Связанные inventory IDs: `JS-12`, `JS-13`, `JS-18`
- Статус modern/legacy: `современная основа`
- Ответ: [JS-FUNCTIONS-Q01](../answers/by-domain/01-javascript-and-async-programming.md#js-functions-q01)
- Источники / последняя проверка: `ECMAScript 2026, MDN: Functions, Arrow functions | 2026-10-06`

#### Вопрос

Сравните объявление функции, анонимное и именованное функциональные выражения и стрелочную функцию по моменту создания, доступности имени, собственным `this` и `arguments`, а также возможности вызова через `new`. Для каждой формы назовите один естественный сценарий применения.

### JS-FUNCTIONS-Q02

**Предскажите поведение объявления и выражения до их строки.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.3. Функции, замыкания и функциональные паттерны`
- Уровень: `Junior`
- Тип: `output | explain`
- Приоритет/частота: `Core | F3`
- Связанные inventory IDs: `JS-12`
- Статус modern/legacy: `современная основа + legacy-знание о var`
- Ответ: [JS-FUNCTIONS-Q02](../answers/by-domain/01-javascript-and-async-programming.md#js-functions-q02)
- Источники / последняя проверка: `ECMAScript 2026 | 2026-10-06`

#### Вопрос

Считайте фрагменты независимыми. Предскажите результат или ошибку и объясните жизненный цикл привязки.

```js
console.log(run());
function run() {
  return "declaration";
}
```

```js
console.log(run());
var run = function () {
  return "expression";
};
```

```js
console.log(run());
const run = () => "arrow";
```

### JS-FUNCTIONS-Q03

**Где видно имя именованного функционального выражения?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.3. Функции, замыкания и функциональные паттерны`
- Уровень: `Junior`
- Тип: `output | why`
- Приоритет/частота: `Core | F3`
- Связанные inventory IDs: `JS-12`
- Статус modern/legacy: `современная основа`
- Ответ: [JS-FUNCTIONS-Q03](../answers/by-domain/01-javascript-and-async-programming.md#js-functions-q03)
- Источники / последняя проверка: `ECMAScript 2026 | 2026-10-06`

#### Вопрос

Предскажите результат и объясните две разные привязки имени.

```js
const task = function internal(depth) {
  return depth === 0
    ? typeof internal
    : internal(depth - 1);
};

console.log(task(1));
console.log(task.name);
console.log(typeof internal);
```

### JS-FUNCTIONS-Q04

**Параметры, аргументы и значения по умолчанию.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.3. Функции, замыкания и функциональные паттерны`
- Уровень: `Junior`
- Тип: `conceptual | compare`
- Приоритет/частота: `Core | F3`
- Связанные inventory IDs: `JS-19`
- Статус modern/legacy: `современная основа`
- Ответ: [JS-FUNCTIONS-Q04](../answers/by-domain/01-javascript-and-async-programming.md#js-functions-q04)
- Источники / последняя проверка: `MDN: Default parameters | 2026-10-06`

#### Вопрос

Различите параметр и аргумент. Объясните, когда срабатывает значение по умолчанию для пропущенного аргумента, `undefined`, `null` и пустой строки. Зачем внешнее `= {}` нужно в `function connect({ timeout = 1000 } = {})`?

### JS-FUNCTIONS-Q05

**Остаточный параметр, `arguments` и граница стрелочной функции.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.3. Функции, замыкания и функциональные паттерны`
- Уровень: `Junior`
- Тип: `compare | output`
- Приоритет/частота: `Core | F3`
- Связанные inventory IDs: `JS-13`, `JS-19`
- Статус modern/legacy: `современная рекомендация + legacy-знание об arguments`
- Ответ: [JS-FUNCTIONS-Q05](../answers/by-domain/01-javascript-and-async-programming.md#js-functions-q05)
- Источники / последняя проверка: `MDN: Rest parameters, arguments | 2026-10-06`

#### Вопрос

Сравните остаточный параметр и `arguments` по типу, содержимому и доступности в стрелочной функции. Затем предскажите результат:

```js
function outer(first) {
  const read = (...rest) => [
    arguments[0],
    rest,
  ];

  return read("inner", "extra");
}

console.log(outer("outer"));
```

### JS-FUNCTIONS-Q06

**Функция первого класса, колбэк и функция высшего порядка.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.3. Функции, замыкания и функциональные паттерны`
- Уровень: `Junior`
- Тип: `conceptual | explain`
- Приоритет/частота: `Core | F3`
- Связанные inventory IDs: `JS-14`
- Статус modern/legacy: `современная основа`
- Ответ: [JS-FUNCTIONS-Q06](../answers/by-domain/01-javascript-and-async-programming.md#js-functions-q06)
- Источники / последняя проверка: `MDN: Functions | 2026-10-06`

#### Вопрос

Дайте определения трём терминам и покажите небольшой пример функции, которая принимает колбэк и возвращает новую функцию. Какие семь вопросов стоит задать о контракте колбэка?

### JS-FUNCTIONS-Q07

**Стрелочная или обычная функция?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.3. Функции, замыкания и функциональные паттерны`
- Уровень: `Junior`
- Тип: `compare | code-review`
- Приоритет/частота: `Core | F3`
- Связанные inventory IDs: `JS-13`, `JS-16`, `JS-18`
- Статус modern/legacy: `современная рекомендация для рабочего кода`
- Ответ: [JS-FUNCTIONS-Q07](../answers/by-domain/01-javascript-and-async-programming.md#js-functions-q07)
- Источники / последняя проверка: `MDN: Arrow functions, this | 2026-10-06`

#### Вопрос

Для метода, небольшого преобразования массива, конструктора, вложенного колбэка таймера и функции с переменным числом аргументов выберите стрелочную или обычную функцию. Обоснуйте выбор семантикой, а не длиной записи.

### JS-FUNCTIONS-Q08

**Замыкание: снимок или привязка?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.3. Функции, замыкания и функциональные паттерны`
- Уровень: `Junior`
- Тип: `output | explain`
- Приоритет/частота: `Core | F3`
- Связанные inventory IDs: `JS-15`
- Статус modern/legacy: `современная основа`
- Ответ: [JS-FUNCTIONS-Q08](../answers/by-domain/01-javascript-and-async-programming.md#js-functions-q08)
- Источники / последняя проверка: `MDN: Closures | 2026-10-06`

#### Вопрос

Предскажите результат. Что нужно изменить, чтобы функция чтения возвращала сохранённый снимок `"idle"`?

```js
let status = "idle";
const readStatus = () => status;

status = "ready";
console.log(readStatus());
```

### JS-FUNCTIONS-Q09

**Чистая функция, побочный эффект и практическая неизменяемость.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.3. Функции, замыкания и функциональные паттерны`
- Уровень: `Junior`
- Тип: `conceptual | code-review`
- Приоритет/частота: `Core | F2`
- Связанные inventory IDs: `JS-21`
- Статус modern/legacy: `современная рекомендация для рабочего кода`
- Ответ: [JS-FUNCTIONS-Q09](../answers/by-domain/01-javascript-and-async-programming.md#js-functions-q09)
- Источники / последняя проверка: `engineering analysis, 1.2 identity model | 2026-10-06`

#### Вопрос

Дайте практическое определение чистой функции. Является ли локальная мутация только что созданного объекта-результата побочным эффектом? Почему поверхностная spread-копия не гарантирует неизменяемость вложенного графа?

### JS-FUNCTIONS-Q10

**Проследите вычисление параметров по умолчанию.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.3. Функции, замыкания и функциональные паттерны`
- Уровень: `Mid`
- Тип: `output | why`
- Приоритет/частота: `Professional | F2`
- Связанные inventory IDs: `JS-19`
- Статус modern/legacy: `современная основа`
- Ответ: [JS-FUNCTIONS-Q10](../answers/by-domain/01-javascript-and-async-programming.md#js-functions-q10)
- Источники / последняя проверка: `ECMAScript 2026, MDN: Default parameters | 2026-10-06`

#### Вопрос

Не запускайте до прогноза:

```js
let seed = 0;

function build(
  id = ++seed,
  copy = id,
) {
  return [id, copy, seed];
}

console.log(build());
console.log(build(10));
console.log(build(undefined, 20));
```

Затем объясните, почему выражение по умолчанию не может вызвать функцию, объявленную в теле той же функции.

### JS-FUNCTIONS-Q11

**Предскажите значения, связанные с арностью.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.3. Функции, замыкания и функциональные паттерны`
- Уровень: `Mid`
- Тип: `output | compare`
- Приоритет/частота: `Professional | F2`
- Связанные inventory IDs: `JS-19`
- Статус modern/legacy: `современная основа`
- Ответ: [JS-FUNCTIONS-Q11](../answers/by-domain/01-javascript-and-async-programming.md#js-functions-q11)
- Источники / последняя проверка: `ECMAScript 2026: Function length | 2026-10-06`

#### Вопрос

Предскажите все значения и различите объявленную арность, фактическое число аргументов и число элементов в остаточном параметре.

```js
function inspect(a, b = 2, c, ...rest) {
  return [inspect.length, arguments.length, rest.length];
}

console.log(inspect("A", undefined, "C", "D", "E"));
console.log(inspect.bind(null, "A").length);
```

### JS-FUNCTIONS-Q12

**Почему `map(parseInt)` ломается?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.3. Функции, замыкания и функциональные паттерны`
- Уровень: `Mid`
- Тип: `find-the-bug | debugging`
- Приоритет/частота: `Professional | F3`
- Связанные inventory IDs: `JS-14`, `JS-19`
- Статус modern/legacy: `современная практика рабочего кода`
- Ответ: [JS-FUNCTIONS-Q12](../answers/by-domain/01-javascript-and-async-programming.md#js-functions-q12)
- Источники / последняя проверка: `MDN: Array.map, parseInt | 2026-10-06`

#### Вопрос

Объясните `["10", "20", "30"].map(parseInt)` через контракты обеих функций, исправьте код и назовите ещё одну типичную ошибку от передачи функции с несовместимой сигнатурой.

### JS-FUNCTIONS-Q13

**Диагностируйте потерю контекста метода.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.3. Функции, замыкания и функциональные паттерны`
- Уровень: `Mid`
- Тип: `debugging | output`
- Приоритет/частота: `Professional | F3`
- Связанные inventory IDs: `JS-16`, `JS-17`
- Статус modern/legacy: `современная основа`
- Ответ: [JS-FUNCTIONS-Q13](../answers/by-domain/01-javascript-and-async-programming.md#js-functions-q13)
- Источники / последняя проверка: `ECMAScript 2026, MDN: this | 2026-10-06`

#### Вопрос

```js
"use strict";

const account = {
  balance: 10,
  read(currency) {
    return currency + ":" + this.balance;
  },
};

const read = account.read;

console.log(account.read("USD"));
console.log(read("USD"));
```

Предскажите результат или ошибку, объясните форму вызова и предложите исправления через `call`, `bind` и функцию-адаптер. Сравните компромиссы жизненного цикла и идентичности функции.

### JS-FUNCTIONS-Q14

**Сравните `call` и `apply` глубже синтаксиса.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.3. Функции, замыкания и функциональные паттерны`
- Уровень: `Mid`
- Тип: `compare | practical-scenario`
- Приоритет/частота: `Professional | F3`
- Связанные inventory IDs: `JS-16`, `JS-17`
- Статус modern/legacy: `современная основа + legacy-знание о заимствовании методов`
- Ответ: [JS-FUNCTIONS-Q14](../answers/by-domain/01-javascript-and-async-programming.md#js-functions-q14)
- Источники / последняя проверка: `MDN: Function.call/apply | 2026-10-06`

#### Вопрос

Объясните немедленный вызов, разницу между списком аргументов и массивоподобным значением, а также различие между `apply` и spread для итерируемого значения. Как `thisArg` обрабатывается в строгом и нестрогом режимах? Когда `Object.hasOwn` яснее заимствования метода?

### JS-FUNCTIONS-Q15

**Разберите `bind`: контекст, аргументы и идентичность.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.3. Функции, замыкания и функциональные паттерны`
- Уровень: `Mid`
- Тип: `output | why`
- Приоритет/частота: `Professional | F3`
- Связанные inventory IDs: `JS-17`, `JS-19`
- Статус modern/legacy: `современная основа`
- Ответ: [JS-FUNCTIONS-Q15](../answers/by-domain/01-javascript-and-async-programming.md#js-functions-q15)
- Источники / последняя проверка: `ECMAScript 2026, MDN: Function.bind | 2026-10-06`

#### Вопрос

```js
function describe(a, b, c) {
  return [this.name, a, b, c];
}

const once = describe.bind({ name: "first" }, "A");
const twice = once.bind({ name: "second" }, "B");

console.log(twice("C"));
console.log(describe.length, once.length, twice.length);
console.log(once === twice, once === describe);
```

Предскажите результат. Почему второй `bind` не заменяет получателя вызова, но добавляет аргумент?

### JS-FUNCTIONS-Q16

**Могут ли `call`, `apply` или `bind` изменить `this` стрелочной функции?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.3. Функции, замыкания и функциональные паттерны`
- Уровень: `Mid`
- Тип: `output | explain`
- Приоритет/частота: `Professional | F3`
- Связанные inventory IDs: `JS-13`, `JS-16`, `JS-17`
- Статус modern/legacy: `современная основа`
- Ответ: [JS-FUNCTIONS-Q16](../answers/by-domain/01-javascript-and-async-programming.md#js-functions-q16)
- Источники / последняя проверка: `MDN: Arrow functions, this | 2026-10-06`

#### Вопрос

```js
function makeReader() {
  return (prefix) => [prefix, this.name];
}

const reader = makeReader.call({ name: "outer" });
const bound = reader.bind({ name: "bound" }, "fixed");

console.log(reader.call({ name: "called" }, "runtime"));
console.log(bound());
```

Отдельно объясните поведение получателя вызова и аргументов.

### JS-FUNCTIONS-Q17

**`new`, возвращаемое значение и стрелочная функция как не-конструктор.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.3. Функции, замыкания и функциональные паттерны`
- Уровень: `Mid`
- Тип: `output | conceptual`
- Приоритет/частота: `Professional | F2`
- Связанные inventory IDs: `JS-18`
- Статус modern/legacy: `современная граница + знание функций-конструкторов`
- Ответ: [JS-FUNCTIONS-Q17](../answers/by-domain/01-javascript-and-async-programming.md#js-functions-q17)
- Источники / последняя проверка: `ECMAScript 2026, MDN: new, bind | 2026-10-06`

#### Вопрос

Дайте пошаговую практическую модель `new`. Затем предскажите результат:

```js
function First(name) {
  this.name = name;
  return 10;
}

function Second(name) {
  this.name = name;
  return { name: "replacement" };
}

console.log(new First("Ada").name);
console.log(new Second("Ada").name);
```

Почему `new (() => {})` выбрасывает `TypeError`? Что произойдёт с заранее привязанным `this`, если привязанную функцию-конструктор вызвать через `new`?

### JS-FUNCTIONS-Q18

**Мутация захваченного объекта и переназначение привязки.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.3. Функции, замыкания и функциональные паттерны`
- Уровень: `Mid`
- Тип: `output | explain`
- Приоритет/частота: `Professional | F3`
- Связанные inventory IDs: `JS-15`, `JS-21`
- Статус modern/legacy: `современная основа`
- Ответ: [JS-FUNCTIONS-Q18](../answers/by-domain/01-javascript-and-async-programming.md#js-functions-q18)
- Источники / последняя проверка: `MDN: Closures; 1.2 identity model | 2026-10-06`

#### Вопрос

```js
function createState() {
  let state = { count: 0 };

  return {
    mutate() {
      state.count += 1;
    },
    replace() {
      state = { count: 100 };
    },
    read() {
      return state;
    },
  };
}

const box = createState();
const before = box.read();
box.mutate();
const afterMutation = box.read();
box.replace();
const afterReplacement = box.read();

console.log(before === afterMutation);
console.log(afterMutation.count);
console.log(afterMutation === afterReplacement);
console.log(afterReplacement.count);
```

Объясните результат через привязку и идентичность объектов.

### JS-FUNCTIONS-Q19

**Исправьте ошибку замыкания в цикле.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.3. Функции, замыкания и функциональные паттерны`
- Уровень: `Mid`
- Тип: `output | debugging`
- Приоритет/частота: `Professional | F3`
- Связанные inventory IDs: `JS-15`
- Статус modern/legacy: `современная рекомендация + legacy-знание об IIFE`
- Ответ: [JS-FUNCTIONS-Q19](../answers/by-domain/01-javascript-and-async-programming.md#js-functions-q19)
- Источники / последняя проверка: `ECMAScript 2026, MDN: Closures | 2026-10-06`

#### Вопрос

Почему `for (var i = 0; i < 3; i++) callbacks.push(() => i)` даёт `[3,3,3]`? Исправьте код с помощью отдельной привязки `let` для каждой итерации и с помощью старого приёма через фабрику или IIFE. Объясните привязки, а не только синтаксис.

### JS-FUNCTIONS-Q20

**Спроектируйте фабрику с общим закрытым состоянием.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.3. Функции, замыкания и функциональные паттерны`
- Уровень: `Mid`
- Тип: `implementation | explain`
- Приоритет/частота: `Professional | F3`
- Связанные inventory IDs: `JS-14`, `JS-15`
- Статус modern/legacy: `современная практика рабочего кода`
- Ответ: [JS-FUNCTIONS-Q20](../answers/by-domain/01-javascript-and-async-programming.md#js-functions-q20)
- Источники / последняя проверка: `MDN: Closures | 2026-10-06`

#### Вопрос

Реализуйте `createLimitedCounter({ initial, min, max })`, возвращающий `increment`, `decrement`, `read` и `reset`. Состояние должно быть закрыто; все методы должны разделять одну привязку; недопустимые настройки должны приводить к ошибке до создания API. Сравните фабрику на замыкании с приватным полем класса.

### JS-FUNCTIONS-Q21

**Каррирование или частичное применение?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.3. Функции, замыкания и функциональные паттерны`
- Уровень: `Mid`
- Тип: `compare | implementation`
- Приоритет/частота: `Professional | F2`
- Связанные inventory IDs: `JS-20`
- Статус modern/legacy: `необязательный современный паттерн`
- Ответ: [JS-FUNCTIONS-Q21](../answers/by-domain/01-javascript-and-async-programming.md#js-functions-q21)
- Источники / последняя проверка: `engineering analysis | 2026-10-06`

#### Вопрос

Различите `f(a,b,c) → f(a)(b)(c)` и фиксацию только `a`. Реализуйте `partial(operation, ...preset)` и назовите два случая, когда объект настроек яснее каррирования.

### JS-FUNCTIONS-Q22

**Предскажите порядок композиции.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.3. Функции, замыкания и функциональные паттерны`
- Уровень: `Mid`
- Тип: `output | compare`
- Приоритет/частота: `Professional | F2`
- Связанные inventory IDs: `JS-20`
- Статус modern/legacy: `необязательный современный паттерн`
- Ответ: [JS-FUNCTIONS-Q22](../answers/by-domain/01-javascript-and-async-programming.md#js-functions-q22)
- Источники / последняя проверка: `engineering analysis | 2026-10-06`

#### Вопрос

```js
const compose = (f, g) => (value) => f(g(value));
const pipe = (...operations) => (value) =>
  operations.reduce((current, operation) => operation(current), value);

const addOne = (value) => value + 1;
const double = (value) => value * 2;

console.log(compose(double, addOne)(3));
console.log(pipe(double, addOne)(3));
```

Предскажите результат и сформулируйте правило направления вычислений.

### JS-FUNCTIONS-Q23

**Проведите ревью функции высшего порядка и неизменяемости.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.3. Функции, замыкания и функциональные паттерны`
- Уровень: `Senior`
- Тип: `code-review | refactoring`
- Приоритет/частота: `Professional | F2`
- Связанные inventory IDs: `JS-14`, `JS-21`
- Статус modern/legacy: `современная рекомендация для рабочего кода`
- Ответ: [JS-FUNCTIONS-Q23](../answers/by-domain/01-javascript-and-async-programming.md#js-functions-q23)
- Источники / последняя проверка: `engineering analysis, 1.2 identity model | 2026-10-06`

#### Вопрос

```js
function withDiscount(rule) {
  return function applyDiscount(order) {
    order.total -= rule(order);
    audit.push(order);
    return order;
  };
}
```

Найдите мутацию общего объекта и скрытые побочные эффекты. Предложите чистое вычисление с явной границей эффектов. Какие вложенные ссылки останутся общими после spread-копии?

### JS-FUNCTIONS-Q24

**Найдите расхождение между ожидаемым и фактическим захватом значения.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.3. Функции, замыкания и функциональные паттерны`
- Уровень: `Senior`
- Тип: `debugging | practical-scenario`
- Приоритет/частота: `Professional | F2`
- Связанные inventory IDs: `JS-15`
- Статус modern/legacy: `современная практика рабочего кода`
- Ответ: [JS-FUNCTIONS-Q24](../answers/by-domain/01-javascript-and-async-programming.md#js-functions-q24)
- Источники / последняя проверка: `MDN: Closures | 2026-10-06`

#### Вопрос

```js
let config = { endpoint: "/v1" };

const capturedBinding = () => config.endpoint;
const currentConfig = config;
const capturedObject = () => currentConfig.endpoint;

config.endpoint = "/v2";
config = { endpoint: "/v3" };

console.log(capturedBinding());
console.log(capturedObject());
```

Предскажите результат и объясните мутацию старого объекта в сравнении с переназначением внешней привязки.

### JS-FUNCTIONS-Q25

**Диагностируйте удерживаемый граф объектов.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.3. Функции, замыкания и функциональные паттерны`
- Уровень: `Senior`
- Тип: `performance-diagnosis | debugging`
- Приоритет/частота: `Advanced | F3`
- Связанные inventory IDs: `JS-15`
- Статус modern/legacy: `современная практика рабочего кода`
- Ответ: [JS-FUNCTIONS-Q25](../answers/by-domain/01-javascript-and-async-programming.md#js-functions-q25)
- Источники / последняя проверка: `MDN: Closures; browser lifecycle analysis | 2026-10-06`

#### Вопрос

Модальное окно регистрирует обработчик, замыкание которого читает небольшое поле из большого ответа сервера. При закрытии окна DOM-узел удаляется, но обработчик остаётся в реестре приложения. Нарисуйте цепочку удержания, объясните, почему само наличие замыкания ещё не доказывает утечку, и предложите очистку с минимальным захватом данных. Опишите, как подтвердить исправление с помощью снимка кучи.

### JS-FUNCTIONS-Q26

**Проведите ревью жизненного цикла API с колбэками.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.3. Функции, замыкания и функциональные паттерны`
- Уровень: `Senior`
- Тип: `code-review | practical-production-scenario`
- Приоритет/частота: `Advanced | F3`
- Связанные inventory IDs: `JS-14`, `JS-15`, `JS-16`, `JS-17`
- Статус modern/legacy: `современная практика рабочего кода`
- Ответ: [JS-FUNCTIONS-Q26](../answers/by-domain/01-javascript-and-async-programming.md#js-functions-q26)
- Источники / последняя проверка: `ECMAScript 2026, MDN primary references | 2026-10-06`

#### Вопрос

```js
class Controller {
  start(button) {
    button.addEventListener("click", this.handle.bind(this));
    this.timer = setInterval(this.refresh.bind(this), 1000);
  }

  stop(button) {
    button.removeEventListener("click", this.handle.bind(this));
    clearInterval(this.timer);
  }
}
```

Найдите дефекты идентичности функций, контекста и жизненного цикла. Предложите решение со стабильными ссылками, идемпотентной очисткой и ясным владением ресурсами. Объектную модель класса подробно не разбирайте.

### JS-FUNCTIONS-Q27

**Спроектируйте безопасную политику мемоизации.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.3. Функции, замыкания и функциональные паттерны`
- Уровень: `Senior`
- Тип: `implementation | performance | architecture`
- Приоритет/частота: `Advanced | F3`
- Связанные inventory IDs: `JS-15`, `JS-21`
- Статус modern/legacy: `современная практика рабочего кода`
- Ответ: [JS-FUNCTIONS-Q27](../answers/by-domain/01-javascript-and-async-programming.md#js-functions-q27)
- Источники / последняя проверка: `engineering analysis | 2026-10-06`

#### Вопрос

Реализуйте `memoizeUnary(operation, { maxSize })` с ограниченным LRU-кешем и корректным сохранением результата `undefined`. Объясните сравнение ключей, ключи-объекты, обработку ошибок и промисов, устаревание данных, долю повторных попаданий и случаи, когда мемоизацию лучше удалить.

### JS-FUNCTIONS-Q28

**Итоговая задача по функциям в формате интервью.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.3. Функции, замыкания и функциональные паттерны`
- Уровень: `Senior`
- Тип: `output | debugging | code-review | interview-communication`
- Приоритет/частота: `Advanced | F3`
- Связанные inventory IDs: `JS-12`, `JS-13`, `JS-14`, `JS-15`, `JS-16`, `JS-17`, `JS-18`, `JS-19`, `JS-20`, `JS-21`
- Статус modern/legacy: `современная рабочая модель + интеграция тем интервью`
- Ответ: [JS-FUNCTIONS-Q28](../answers/by-domain/01-javascript-and-async-programming.md#js-functions-q28)
- Источники / последняя проверка: `ECMAScript 2026, MDN primary references | 2026-10-06`

#### Вопрос

```js
"use strict";

function createProcessor(config = { prefix: "ID" }) {
  const cache = new Map();

  return {
    process(value, transform = this.normalize) {
      if (cache.has(value)) return cache.get(value);
      const result = transform(config.prefix + ":" + value);
      cache.set(value, result);
      return result;
    },
    normalize(value) {
      return value.trim().toLowerCase();
    },
    size: () => cache.size,
  };
}

const processor = createProcessor();
const detached = processor.process;

console.log(processor.process(" 1 "));
console.log(processor.size());
console.log(detached(" 2 "));
```

До запуска:

1. предскажите результат до первой ошибки;
2. объясните вычисление значения по умолчанию, `this` метода, замыкание и кеш;
3. исправьте контракт вызова отделённого метода;
4. добавьте ограничение размера и правила сброса кеша;
5. отделите чистую нормализацию от кеширования с состоянием;
6. объясните решение за три минуты и обозначьте границу с объектной моделью из 1.4.
