# 1. JavaScript и асинхронное программирование — вопросы

> Статус: `частично готово — 1.1–1.11 одобрены; 1.12 остаётся заглушкой`
>
> Ответы: [в отдельном файле](../answers/by-domain/01-javascript-and-async-programming.md)
>
> Разделы 1.1–1.11 одобрены. Раздел 1.12 остаётся заглушкой.

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

Используйте вопросы для активного воспроизведения по памяти. Модельные ответы находятся в отдельном файле и не должны открываться до собственной попытки.

### JS-VALUES-Q01

**Какие значения в JavaScript являются примитивами, а какие — объектами?**

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

Перечислите семь примитивных типов и объясните, почему функция одновременно даёт `typeof value === "function"`, но относится к значениям-объектам. Затем разграничьте:

- тип текущего значения;
- возможность переназначить привязку;
- изменяемость самого значения.

Покажите различие на одном `let` со значениями разных типов и одном `const`-объекте.

### JS-VALUES-Q02

**Неизменяемость примитива, мутация объекта или переназначение?**

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

Предскажите вывод и для каждой строки назовите операцию: получение нового примитива, мутация или переназначение.

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

Почему `const` не делает `settings` неизменяемым?

### JS-VALUES-Q03

**Докажите, что аргумент-объект передаётся по значению.**

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

Предскажите результат и объясните его через две привязки и одну идентичность объекта:

```js
function change(item) {
  item.enabled = true;
  item = { enabled: false };
}

const config = { enabled: false };
change(config);

console.log(config.enabled);
```

Почему мутация видна вызывающему коду, а переназначение параметра — нет? Почему формулировка «объекты передаются по ссылке» неточна?

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

Почему `typeof value === "undefined"` не доказывает, что идентификатор необъявлен?

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

Объясните назначение, создание, `typeof` и ключевые ограничения обоих примитивов. Обязательно разберите:

- `Symbol("id") === Symbol("id")`;
- символ как ключ свойства;
- `5n / 2n`;
- `1n + 1`;
- почему явный переход `BigInt` → `Number` может потерять точность;
- почему `BigInt` не является десятичным типом для денег.

### JS-VALUES-Q06

**Как проверять `NaN`, `Infinity` и знаки нуля?**

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

Предскажите результаты и назовите подходящую проверку для рабочего кода:

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

Почему проверки `value !== NaN` и «не `NaN` значит конечное число» неверны?

### JS-VALUES-Q07

**Восстановите истинные, ложные и nullish-значения по памяти.**

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

Перечислите все практические ложные значения, отдельно назовите nullish-значения (`null`/`undefined`) и предскажите:

```js
Boolean("0");
Boolean([]);
Boolean({});
Boolean(0n);
Boolean(new Boolean(false));
```

Почему «пустой объект ложен в логическом контексте» — неверная ментальная модель?

### JS-VALUES-Q08

**Выберите `||` или `??` для значений по умолчанию.**

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

Клиент может намеренно передать `0`, `false` и пустую строку:

```js
function options(input) {
  return {
    retries: input.retries || 3,
    visible: input.visible || true,
    label: input.label || "Untitled",
  };
}
```

Найдите ошибку, исправьте код и сформулируйте случай, когда исходный `||` был бы правильным выбором. Что возвращают `||` и `??`: логическое значение или значение операнда?

### JS-VALUES-Q09

**Проследите короткое замыкание и побочные эффекты.**

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

Почему выражение справа с более высоким приоритетом может вообще не вычислиться? Когда побочные эффекты в операнде с коротким замыканием становятся проблемой для ревью кода?

### JS-VALUES-Q10

**Найдите ловушки опциональных цепочек.**

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

Для каждого независимого выражения укажите значение, исключение или синтаксическую ошибку и объясните, какое значение защищает `?.`:

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

Постройте матрицу для четырёх семантик по осям: преобразование типов, `NaN`, знаки нуля, идентичность объектов. Затем назовите реальные места использования SameValueZero и объясните, почему `Object.is()` не является «самым строгим `===`» или глубоким равенством.

### JS-VALUES-Q12

**Почему поверхностное копирование не устранило общую мутацию?**

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

Предскажите четыре результата и нарисуйте идентичности объектов:

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

Как исправить конкретную ошибку, не обещая универсального глубокого клонирования? Где проходит граница темы 1.2 и полной темы копирования 1.5?

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

API получает `""`, `"42"`, `"oops"`, `42`, `NaN` или `1n`. Для каждого значения предскажите глобальный `isNaN(value)` и `Number.isNaN(value)`; отметьте возможное исключение. Какую последовательность разбора и валидации вы выберете, если API принимает только непустую десятичную строку или конечное значение `Number`?

### JS-VALUES-Q14

**Отладьте ошибку вычислений с плавающей точкой и денежных расчётов.**

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

При оформлении заказа рассчитанная сумма сравнивается с ожидаемой:

```js
const expected = 0.3;
const actual = 0.1 + 0.2;

if (actual !== expected) {
  throw new Error("Price mismatch");
}
```

Объясните причину, предложите:

1. сравнение с учётом домена для обычных измерений;
2. целочисленную модель в минимальных денежных единицах для сумм с фиксированным масштабом;
3. проверки диапазона и правила округления.

Почему `Math.abs(actual - expected) < Number.EPSILON` не является универсальным решением для денег?

### JS-VALUES-Q15

**Заполните таблицу явных преобразований.**

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

Отдельно укажите случаи, где возникает `NaN`, `TypeError` или возможная потеря точности. Сравните `Number(value)`, унарный `+value`, `String(value)` и `"" + value` там, где они неэквивалентны.

### JS-VALUES-Q16

**Предскажите результат оператора `+`.**

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

Предскажите значение и тип каждого независимого выражения, показывая промежуточный `ToPrimitive` и дальнейшее преобразование:

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

**Сравните преобразования при проверке равенства и порядка.**

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

Предскажите и объясните разные пути преобразования:

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

Почему нельзя моделировать все операторы сравнения как «сначала `Number()` обеих сторон»?

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

Предскажите порядок вызовов и результаты:

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

Затем добавьте `[Symbol.toPrimitive](hint)` и объясните его приоритет, три подсказки и требование вернуть примитив. Почему `Date` — важное исключение для подсказки `"default"`, но не повод запоминать редкие головоломки?

### JS-VALUES-Q19

**Сформулируйте правила для `==` при ревью кода.**

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

Проведите ревью:

- объясните точную семантику выражения;
- сравните с явным `value === null || value === undefined`;
- предложите правила для команды и линтера;
- отделите корректность от читаемости;
- объясните, почему это не оправдывает `==` в произвольных сравнениях.

### JS-VALUES-Q20

**Выберите правила равенства для коллекции.**

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

Последовательность аналитической обработки должна дедуплицировать примитивные показания, среди которых встречаются `NaN`, `0` и `-0`. Сравните:

- `Set`;
- `Array.prototype.includes()`;
- `indexOf()`;
- ручной поиск через `===`;
- ручной поиск через `Object.is()`.

Какие значения каждая стратегия объединит или различит? Что выбрать, если знак нуля имеет доменный смысл? Как изменится решение для показаний-объектов с одинаковым содержимым, но разной идентичностью?

### JS-VALUES-Q21

**Проведите ревью общей мутации и поверхностного копирования.**

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

Ранжируйте замечания ревью по серьёзности. Нарисуйте общие идентичности объектов, объясните изменение между вызовами и предложите минимальное исправление без универсального глубокого клонирования. Какие ожидания о владении и неизменяемости должен документировать API?

### JS-VALUES-Q22

**Спроектируйте обработку числового ввода на границе системы.**

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

Сервер принимает `quantity` от интерфейса и сейчас делает:

```js
function parseQuantity(input) {
  const value = Number(input);
  if (!Number.isNaN(value)) return value;
  throw new Error("invalid");
}
```

Найдите входные данные, которые функция неожиданно принимает: пустую строку и пробельные символы, бесконечности, дроби, отрицательный ноль, целые за безопасным диапазоном. Сформулируйте контракт для положительного безопасного целого количества, реализуйте порядок валидации и объясните, где явного преобразования типов всё ещё недостаточно.

### JS-VALUES-Q23

**Реализуйте `nearlyEqual` с учётом масштаба.**

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

- точно равные значения, включая одинаковые бесконечности, возвращают `true`;
- разные неконечные значения и `NaN` возвращают `false`;
- конечные значения сравниваются через максимум из абсолютного допуска и относительного допуска с учётом масштаба;
- значения по умолчанию должны быть явно документированы как пример, а не универсальная истина;
- добавьте тесты для значений около нуля, около `1`, больших величин, знаков нуля, бесконечностей и `NaN`.

### JS-VALUES-Q24

**Комплексный челлендж: идентичность, равенство и преобразование типов.**

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

1. предскажите каждый результат;
2. назовите правило идентичности, равенства или преобразования типов на каждом шаге;
3. найдите неоднозначные требования вокруг строки `"0"` и выбора значений по умолчанию;
4. предложите нормализацию с проверкой типов на границе системы и безопасную модель владения;
5. объясните анализ за три минуты без формулировки «объекты передаются по ссылке».

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

## 1.4. `this`, вызов функции и объектная модель

Не открывайте отдельный файл ответов до собственной попытки. В задачах на результат сначала подпишите форму вызова, получателя, место хранения свойства и флаги его дескриптора.

### JS-OBJECTS-Q01

**Сравните пять способов создания объектов.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.4. this, вызов функции и объектная модель`
- Уровень: `Junior`
- Тип: `conceptual | compare`
- Приоритет/частота: `Core | F3`
- Связанные inventory IDs: `JS-23`
- Статус modern/legacy: `современная основа + знание constructor functions`
- Ответ: [JS-OBJECTS-Q01](../answers/by-domain/01-javascript-and-async-programming.md#js-objects-q01)
- Источники / последняя проверка: `ECMAScript 2026, MDN: Working with objects, Object.create, Classes | 2026-10-08`

#### Вопрос

Сравните объектный литерал (object literal), фабричную функцию (factory function), функцию-конструктор (constructor function), `Object.create` и класс (`class`): как создаётся объект, где хранится состояние экземпляра, где обычно находятся методы, как организуется общее поведение и требуется ли `new`. Для каждого подхода назовите один естественный сценарий и один компромисс.

### JS-OBJECTS-Q02

**Определите `this` по форме вызова.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.4. this, вызов функции и объектная модель`
- Уровень: `Junior`
- Тип: `output | explain`
- Приоритет/частота: `Core | F3`
- Связанные inventory IDs: `JS-24`
- Статус modern/legacy: `современная основа`
- Ответ: [JS-OBJECTS-Q02](../answers/by-domain/01-javascript-and-async-programming.md#js-objects-q02)
- Источники / последняя проверка: `ECMAScript 2026, MDN: this, Function.call, Function.bind | 2026-10-08`

#### Вопрос

Предскажите результат и для каждой строки назовите применившееся правило определения `this`:

```js
"use strict";

function readName() {
  return this?.name ?? "none";
}

const first = { name: "first", readName };
const second = { name: "second" };
const detached = first.readName;
const bound = detached.bind(first);

console.log(first.readName());
console.log(detached());
console.log(detached.call(second));
console.log(bound.call(second));
```

### JS-OBJECTS-Q03

**Найдите ошибочную модель стрелочной функции как метода.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.4. this, вызов функции и объектная модель`
- Уровень: `Junior`
- Тип: `output | debugging | why`
- Приоритет/частота: `Core | F3`
- Связанные inventory IDs: `JS-23`, `JS-24`
- Статус modern/legacy: `современная основа`
- Ответ: [JS-OBJECTS-Q03](../answers/by-domain/01-javascript-and-async-programming.md#js-objects-q03)
- Источники / последняя проверка: `ECMAScript 2026, MDN: Arrow functions, this | 2026-10-08`

#### Вопрос

```js
"use strict";

function createRecord(label) {
  return {
    label,
    regular() {
      return this.label;
    },
    arrow: () => this.label,
  };
}

const record = createRecord.call({ label: "outer" }, "inner");
const other = {
  label: "other",
  regular: record.regular,
  arrow: record.arrow,
};

console.log(record.regular());
console.log(other.regular());
console.log(record.arrow());
console.log(other.arrow.call({ label: "called" }));
```

Предскажите результат. Почему свойство со стрелочной функцией (arrow function) не получает `this` от объекта? Когда стрелочная функция внутри настоящего метода, наоборот, помогает сохранить контекст?

### JS-OBJECTS-Q04

**Проследите алгоритм `new`.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.4. this, вызов функции и объектная модель`
- Уровень: `Junior`
- Тип: `output | conceptual`
- Приоритет/частота: `Core | F3`
- Связанные inventory IDs: `JS-23`, `JS-24`
- Статус modern/legacy: `современная основа + знание constructor functions`
- Ответ: [JS-OBJECTS-Q04](../answers/by-domain/01-javascript-and-async-programming.md#js-objects-q04)
- Источники / последняя проверка: `ECMAScript 2026, MDN: new, new.target | 2026-10-08`

#### Вопрос

```js
function First(name) {
  this.name = name;
  return 42;
}

function Second(name) {
  this.name = name;
  return { name: "replacement" };
}

const BoundFirst = First.bind({ name: "ignored" }, "bound");

const first = new First("Ada");
const second = new Second("Grace");
const bound = new BoundFirst();

console.log(first.name);
console.log(second.name);
console.log(bound.name);
console.log(Object.getPrototypeOf(bound) === First.prototype);
```

Предскажите результат и восстановите шаги `new`. Что изменится при возврате функции вместо обычного объекта? Почему стрелочную функцию (arrow function) нельзя вызвать через `new`, и какую задачу решает `new.target`?

### JS-OBJECTS-Q05

**Различите `[[Prototype]]` объекта и `.prototype` функции.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.4. this, вызов функции и объектная модель`
- Уровень: `Junior`
- Тип: `conceptual | explain`
- Приоритет/частота: `Core | F3`
- Связанные inventory IDs: `JS-24`
- Статус modern/legacy: `современная основа`
- Ответ: [JS-OBJECTS-Q05](../answers/by-domain/01-javascript-and-async-programming.md#js-objects-q05)
- Источники / последняя проверка: `ECMAScript 2026, MDN: Inheritance and the prototype chain | 2026-10-08`

#### Вопрос

Нарисуйте связи между `Person`, `Person.prototype`, `new Person("Ada")`, `Function.prototype` и `Object.prototype`. Объясните, что означает внутренний `[[Prototype]]`, зачем функции-конструктору свойство `.prototype` и почему выражения `Person.prototype` и `Object.getPrototypeOf(Person)` указывают на разные объекты.

### JS-OBJECTS-Q06

**Отделите собственность свойства от перечисляемости.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.4. this, вызов функции и объектная модель`
- Уровень: `Junior`
- Тип: `output | compare`
- Приоритет/частота: `Core | F3`
- Связанные inventory IDs: `JS-26`
- Статус modern/legacy: `современная основа`
- Ответ: [JS-OBJECTS-Q06](../answers/by-domain/01-javascript-and-async-programming.md#js-objects-q06)
- Источники / последняя проверка: `ECMAScript 2026, MDN: Enumerability and ownership of properties | 2026-10-08`

#### Вопрос

```js
const base = { role: "member" };
Object.defineProperty(base, "hidden", {
  value: "base-secret",
  enumerable: false,
});

const user = Object.create(base);
user.name = "Ada";
Object.defineProperty(user, "token", {
  value: "abc",
  enumerable: false,
});

console.log(Object.hasOwn(user, "name"));
console.log(Object.hasOwn(user, "role"));
console.log("role" in user);
console.log("hidden" in user);
console.log(Object.keys(user));
console.log([...function* () {
  for (const key in user) yield key;
}()]);
```

Предскажите результат. Затем сформулируйте две независимые оси: собственные/унаследованные (own/inherited) и перечислимые/неперечислимые (enumerable/non-enumerable) свойства.

### JS-OBJECTS-Q07

**Где класс хранит методы, поля и статические члены?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.4. this, вызов функции и объектная модель`
- Уровень: `Junior`
- Тип: `conceptual | compare`
- Приоритет/частота: `Core | F3`
- Связанные inventory IDs: `JS-25`
- Статус modern/legacy: `современная основа`
- Ответ: [JS-OBJECTS-Q07](../answers/by-domain/01-javascript-and-async-programming.md#js-objects-q07)
- Источники / последняя проверка: `ECMAScript 2026, MDN: Classes, Public class fields, Private elements, static | 2026-10-08`

#### Вопрос

Для обычного метода класса, открытого поля экземпляра (public instance field), закрытого поля (private field) `#value`, статического метода и статического поля объясните, где находится соответствующее свойство и как к нему обращаться. Какие из них создаются отдельно для каждого экземпляра? Почему класс нужно вызывать через `new`, а код тела класса работает в строгом режиме (strict mode)?

### JS-OBJECTS-Q08

**Сравните уровни целостности объекта.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.4. this, вызов функции и объектная модель`
- Уровень: `Junior`
- Тип: `conceptual | compare`
- Приоритет/частота: `Core | F2`
- Связанные inventory IDs: `JS-28`
- Статус modern/legacy: `современная основа`
- Ответ: [JS-OBJECTS-Q08](../answers/by-domain/01-javascript-and-async-programming.md#js-objects-q08)
- Источники / последняя проверка: `ECMAScript 2026, MDN: Object.preventExtensions, Object.seal, Object.freeze | 2026-10-08`

#### Вопрос

Сравните `Object.preventExtensions`, `Object.seal` и `Object.freeze` по добавлению, удалению, изменению флагов дескриптора и изменению значения существующего свойства данных (data property). Чем `Object.freeze` отличается от `const`, и какую гарантию каждое средство даёт вложенным объектам?

### JS-OBJECTS-Q09

**Разберите пересечение `bind` и `new`.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.4. this, вызов функции и объектная модель`
- Уровень: `Mid`
- Тип: `output | why`
- Приоритет/частота: `Professional | F2`
- Связанные inventory IDs: `JS-23`, `JS-24`
- Статус modern/legacy: `современная основа + знание constructor functions`
- Ответ: [JS-OBJECTS-Q09](../answers/by-domain/01-javascript-and-async-programming.md#js-objects-q09)
- Источники / последняя проверка: `ECMAScript 2026, MDN: Function.bind, new | 2026-10-08`

#### Вопрос

```js
function Pair(first, second) {
  this.values = [first, second];
}

const BoundOnce = Pair.bind({ values: ["ignored"] }, "A");
const BoundTwice = BoundOnce.bind({ values: ["rebound"] }, "B");
const pair = new BoundTwice("C");

console.log(pair.values);
console.log(pair instanceof Pair);
console.log(pair instanceof BoundOnce);
console.log(pair instanceof BoundTwice);
console.log(BoundOnce === BoundTwice);
```

Предскажите результат. Почему повторный `bind` добавляет аргументы, но не заменяет уже связанный `this`, а вызов через `new` игнорирует оба связанных значения `this`?

### JS-OBJECTS-Q10

**Выберите модель создания объектов для трёх рабочих задач.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.4. this, вызов функции и объектная модель`
- Уровень: `Mid`
- Тип: `compare | practical-production-scenario`
- Приоритет/частота: `Professional | F3`
- Связанные inventory IDs: `JS-23`, `JS-25`
- Статус modern/legacy: `современная практика рабочего кода`
- Ответ: [JS-OBJECTS-Q10](../answers/by-domain/01-javascript-and-async-programming.md#js-objects-q10)
- Источники / последняя проверка: `MDN primary references, engineering analysis | 2026-10-08`

#### Вопрос

Выберите и обоснуйте модель для трёх случаев: одноразовый объект конфигурации; тысячи однотипных объектов с общими методами; сервис с закрытым состоянием, который создаётся редко и передаёт наружу небольшой API. Сравните объектный литерал, фабричную функцию, функцию-конструктор, `Object.create` и класс. Где композиция поведения даст более простой контракт, чем наследование?

### JS-OBJECTS-Q11

**Проследите чтение и присваивание по цепочке прототипов.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.4. this, вызов функции и объектная модель`
- Уровень: `Mid`
- Тип: `output | explain`
- Приоритет/частота: `Professional | F3`
- Связанные inventory IDs: `JS-24`, `JS-27`
- Статус modern/legacy: `современная основа`
- Ответ: [JS-OBJECTS-Q11](../answers/by-domain/01-javascript-and-async-programming.md#js-objects-q11)
- Источники / последняя проверка: `ECMAScript 2026, MDN: Inheritance and the prototype chain, Property setters | 2026-10-08`

#### Вопрос

```js
"use strict";

const base = { kind: "base" };

Object.defineProperty(base, "fixed", {
  value: 1,
  writable: false,
  enumerable: true,
  configurable: true,
});

Object.defineProperty(base, "score", {
  get() {
    return this._score ?? 0;
  },
  set(value) {
    this._score = value * 2;
  },
  enumerable: true,
  configurable: true,
});

const child = Object.create(base);
child.kind = "child";
child.score = 3;

try {
  child.fixed = 2;
} catch (error) {
  console.log(error.name);
}

console.log(child.kind, base.kind);
console.log(child.score, child._score);
console.log(Object.hasOwn(child, "kind"));
console.log(Object.hasOwn(child, "score"));
console.log(Object.hasOwn(child, "_score"));
```

Предскажите результат и различите поиск при чтении, создание затеняющего собственного свойства при присваивании и вызов унаследованного setter с исходным получателем (receiver).

### JS-OBJECTS-Q12

**Исследуйте объекты с заданным и с отсутствующим прототипом.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.4. this, вызов функции и объектная модель`
- Уровень: `Mid`
- Тип: `output | compare`
- Приоритет/частота: `Professional | F2`
- Связанные inventory IDs: `JS-24`, `JS-26`
- Статус modern/legacy: `современная основа`
- Ответ: [JS-OBJECTS-Q12](../answers/by-domain/01-javascript-and-async-programming.md#js-objects-q12)
- Источники / последняя проверка: `ECMAScript 2026, MDN: Object.create, Object.getPrototypeOf, instanceof | 2026-10-08`

#### Вопрос

```js
function Model() {}

const instance = Object.create(Model.prototype);
const dictionary = Object.create(null);
dictionary.toString = "stored-value";

console.log(Object.getPrototypeOf(instance) === Model.prototype);
console.log(Model.prototype.isPrototypeOf(instance));
console.log(instance instanceof Model);
console.log(Object.getPrototypeOf(dictionary));
console.log("hasOwnProperty" in dictionary);
console.log(Object.hasOwn(dictionary, "toString"));
```

Предскажите результат. Какие удобства и риски даёт `Object.create(null)`? Когда применять `Object.getPrototypeOf`, `isPrototypeOf` и `instanceof`?

### JS-OBJECTS-Q13

**Проведите ревью динамического изменения прототипа.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.4. this, вызов функции и объектная модель`
- Уровень: `Mid`
- Тип: `code-review | why | legacy`
- Приоритет/частота: `Professional | F2`
- Связанные inventory IDs: `JS-24`
- Статус modern/legacy: `современная рекомендация + legacy-знание о __proto__`
- Ответ: [JS-OBJECTS-Q13](../answers/by-domain/01-javascript-and-async-programming.md#js-objects-q13)
- Источники / последняя проверка: `ECMAScript 2026, MDN: Object.prototype.__proto__, Object.setPrototypeOf | 2026-10-08`

#### Вопрос

```js
function attachBehavior(record, behavior) {
  record.__proto__ = behavior;
  return record;
}

function isOrder(value) {
  return value.constructor === Order;
}
```

Объясните разницу между историческим accessor `__proto__` и внутренним `[[Prototype]]`. Найдите проблемы производительности, поддержки и проверки типа. Предложите создание правильной цепочки заранее и более подходящие способы чтения прототипа и проверки ожидаемого объекта.

### JS-OBJECTS-Q14

**Проследите инициализацию производного класса.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.4. this, вызов функции и объектная модель`
- Уровень: `Mid`
- Тип: `output | explain`
- Приоритет/частота: `Professional | F3`
- Связанные inventory IDs: `JS-25`
- Статус modern/legacy: `современная основа`
- Ответ: [JS-OBJECTS-Q14](../answers/by-domain/01-javascript-and-async-programming.md#js-objects-q14)
- Источники / последняя проверка: `ECMAScript 2026, MDN: extends, super, Public class fields, static | 2026-10-08`

#### Вопрос

```js
class Base {
  static kind = "base";
  label = "base-field";

  constructor(name) {
    this.name = name;
  }

  describe() {
    return `${this.name}:${this.label}`;
  }

  static readKind() {
    return this.kind;
  }
}

class Child extends Base {
  static kind = "child";
  label = "child-field";

  constructor(name) {
    super(name);
    this.afterSuper = super.describe();
  }

  describe() {
    return `${super.describe()}:child`;
  }
}

const item = new Child("Ada");

console.log(item.describe());
console.log(item.afterSuper);
console.log(Child.readKind(), Base.readKind());
console.log(Object.hasOwn(item, "describe"));
console.log(Object.hasOwn(item, "label"));
```

Предскажите результат. В каком порядке инициализируются поля базового и производного классов? Почему конструктор производного класса не может использовать `this` до `super()`?

### JS-OBJECTS-Q15

**Сравните метод в прототипе и поле со стрелочной функцией.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.4. this, вызов функции и объектная модель`
- Уровень: `Mid`
- Тип: `output | code-review | practical-production-scenario`
- Приоритет/частота: `Professional | F3`
- Связанные inventory IDs: `JS-25`
- Статус modern/legacy: `современная практика рабочего кода`
- Ответ: [JS-OBJECTS-Q15](../answers/by-domain/01-javascript-and-async-programming.md#js-objects-q15)
- Источники / последняя проверка: `ECMAScript 2026, MDN: Method definitions, Public class fields, Arrow functions | 2026-10-08`

#### Вопрос

```js
class Controller {
  constructor(id) {
    this.id = id;
  }

  method() {
    return this.id;
  }

  arrow = () => this.id;
}

const first = new Controller("first");
const second = new Controller("second");
const detachedMethod = first.method;
const detachedArrow = first.arrow;

console.log(first.method === second.method);
console.log(first.arrow === second.arrow);
console.log(detachedArrow());
console.log(detachedMethod());
```

Предскажите результат до первой ошибки. Сравните размещение, идентичность, сохранение `this`, расход памяти и удобство регистрации/снятия обработчиков. Какой вариант должен быть обычным выбором, а какой требует конкретной причины?

### JS-OBJECTS-Q16

**Диагностируйте проверку закрытого поля через Proxy.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.4. this, вызов функции и объектная модель`
- Уровень: `Mid`
- Тип: `output | debugging`
- Приоритет/частота: `Professional | F2`
- Связанные inventory IDs: `JS-25`, `JS-39`
- Статус modern/legacy: `современная основа`
- Ответ: [JS-OBJECTS-Q16](../answers/by-domain/01-javascript-and-async-programming.md#js-objects-q16)
- Источники / последняя проверка: `ECMAScript 2026, MDN: Private elements, Proxy | 2026-10-08`

#### Вопрос

```js
class Counter {
  #value = 1;

  read() {
    return this.#value;
  }
}

const counter = new Counter();
const proxy = new Proxy(counter, {});

console.log(counter.read());
console.log(proxy.read());
```

Предскажите результат. Почему proxy с пустым обработчиком (handler) не получает закрытый маркер экземпляра (private-field brand)? Как `#value in object` отличается от проверки строкового свойства? Обсудите возможный адаптер и его цену для идентичности методов.

### JS-OBJECTS-Q17

**Составьте матрицу API перечисления свойств.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.4. this, вызов функции и объектная модель`
- Уровень: `Mid`
- Тип: `output | compare`
- Приоритет/частота: `Professional | F3`
- Связанные inventory IDs: `JS-26`
- Статус modern/legacy: `современная основа`
- Ответ: [JS-OBJECTS-Q17](../answers/by-domain/01-javascript-and-async-programming.md#js-objects-q17)
- Источники / последняя проверка: `ECMAScript 2026, MDN: Enumerability and ownership of properties, Reflect.ownKeys | 2026-10-08`

#### Вопрос

```js
const inheritedSymbol = Symbol("inherited");
const ownSymbol = Symbol("own");
const base = {
  inherited: 1,
  [inheritedSymbol]: 2,
};

Object.defineProperty(base, "hiddenInherited", { value: 3 });

const object = Object.create(base);
object.own = 4;
object[ownSymbol] = 5;
Object.defineProperty(object, "hiddenOwn", { value: 6 });
```

Перечислите ключи, которые увидят `Object.keys`, `Object.values`, `Object.entries`, `for...in`, `Object.getOwnPropertyNames`, `Object.getOwnPropertySymbols` и `Reflect.ownKeys`. Почему перечисляемость и symbol key не дают приватности?

### JS-OBJECTS-Q18

**Восстановите значения флагов дескриптора по умолчанию.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.4. this, вызов функции и объектная модель`
- Уровень: `Mid`
- Тип: `output | conceptual`
- Приоритет/частота: `Professional | F3`
- Связанные inventory IDs: `JS-27`
- Статус modern/legacy: `современная основа`
- Ответ: [JS-OBJECTS-Q18](../answers/by-domain/01-javascript-and-async-programming.md#js-objects-q18)
- Источники / последняя проверка: `ECMAScript 2026, MDN: Object.defineProperty, Property descriptors | 2026-10-08`

#### Вопрос

```js
"use strict";

const object = { visible: 1 };
Object.defineProperty(object, "count", { value: 1 });

console.log(Object.getOwnPropertyDescriptor(object, "visible"));
console.log(Object.getOwnPropertyDescriptor(object, "count"));

object.count = 2;
```

Предскажите значения флагов обоих дескрипторов и результат последней строки. Почему нельзя смешать `value` с `get` или `set` в одном дескрипторе? Когда нужны `Object.getOwnPropertyDescriptors` и `Object.defineProperties`?

### JS-OBJECTS-Q19

**Определите получателя у getter и setter.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.4. this, вызов функции и объектная модель`
- Уровень: `Mid`
- Тип: `output | why`
- Приоритет/частота: `Professional | F2`
- Связанные inventory IDs: `JS-24`, `JS-27`
- Статус modern/legacy: `современная основа`
- Ответ: [JS-OBJECTS-Q19](../answers/by-domain/01-javascript-and-async-programming.md#js-objects-q19)
- Источники / последняя проверка: `ECMAScript 2026, MDN: get, set, Reflect.get | 2026-10-08`

#### Вопрос

```js
const proto = {
  get name() {
    return this._name ?? "unknown";
  },
  set name(value) {
    this._name = value.trim();
  },
};

const child = Object.create(proto);
child.name = " Ada ";

const grandchild = Object.create(child);
console.log(child.name);
console.log(grandchild.name);
console.log(Object.hasOwn(child, "name"));
console.log(Object.hasOwn(child, "_name"));
console.log(Reflect.get(proto, "name", { _name: "Guest" }));
```

Предскажите результат. Где найден accessor и какой объект становится `this`? Почему getter с неожиданными побочными эффектами усложняет чтение и отладку?

### JS-OBJECTS-Q20

**Найдите границу `Object.freeze`.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.4. this, вызов функции и объектная модель`
- Уровень: `Mid`
- Тип: `output | debugging`
- Приоритет/частота: `Professional | F3`
- Связанные inventory IDs: `JS-28`
- Статус modern/legacy: `современная основа`
- Ответ: [JS-OBJECTS-Q20](../answers/by-domain/01-javascript-and-async-programming.md#js-objects-q20)
- Источники / последняя проверка: `ECMAScript 2026, MDN: Object.freeze | 2026-10-08`

#### Вопрос

```js
"use strict";

const profile = { name: "Ada" };
const state = Object.freeze({
  profile,
  status: "idle",
});

profile.name = "Grace";

try {
  state.status = "ready";
} catch (error) {
  console.log(error.name);
}

console.log(state.profile.name);
console.log(Object.isFrozen(state));
console.log(Object.isFrozen(state.profile));
```

Предскажите результат и объясните его через идентичность объекта, общую ссылку и поверхностную гарантию `freeze`. Что понадобилось бы для глубокой неизменяемости, и какие ограничения есть у рекурсивной вспомогательной функции глубокой заморозки?

### JS-OBJECTS-Q21

**Реализуйте проверяемое свойство через дескриптор.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.4. this, вызов функции и объектная модель`
- Уровень: `Mid`
- Тип: `implementation | API-design`
- Приоритет/частота: `Professional | F2`
- Связанные inventory IDs: `JS-27`
- Статус modern/legacy: `современная практика рабочего кода`
- Ответ: [JS-OBJECTS-Q21](../answers/by-domain/01-javascript-and-async-programming.md#js-objects-q21)
- Источники / последняя проверка: `ECMAScript 2026, MDN: Object.defineProperty | 2026-10-08`

#### Вопрос

Реализуйте `defineValidatedProperty(target, key, { initial, validate, enumerable })`. Чтение должно возвращать сохранённое значение, присваивание — проверять новое значение и бросать `TypeError` при отказе валидатора. Явно выберите `configurable`, не используйте Proxy и проверьте исходное значение до установки свойства. Объясните цену скрытого состояния и случаи, когда обычная функция обновления яснее accessor.

### JS-OBJECTS-Q22

**Исправьте проверку наличия собственного свойства.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.4. this, вызов функции и объектная модель`
- Уровень: `Mid`
- Тип: `find-the-bug | debugging`
- Приоритет/частота: `Professional | F3`
- Связанные inventory IDs: `JS-26`
- Статус modern/legacy: `современная практика рабочего кода`
- Ответ: [JS-OBJECTS-Q22](../answers/by-domain/01-javascript-and-async-programming.md#js-objects-q22)
- Источники / последняя проверка: `ECMAScript 2026, MDN: Object.hasOwn, in | 2026-10-08`

#### Вопрос

```js
function readOwnOption(options, key, fallback) {
  if (options[key]) return options[key];
  if (options.hasOwnProperty(key)) return options[key];
  return fallback;
}

const options = Object.create(null);
options.enabled = false;
options.retries = 0;
options.hasOwnProperty = "data";
```

Найдите все проблемы при контракте «вернуть собственное значение, включая `false`, `0`, пустую строку и `undefined`; fallback использовать только при отсутствии собственного ключа». Исправьте функцию и объясните, когда вместо этого нужен оператор `in`.

### JS-OBJECTS-Q23

**Оцените надёжность `instanceof` и `.constructor`.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.4. this, вызов функции и объектная модель`
- Уровень: `Senior`
- Тип: `compare | why | interview-communication`
- Приоритет/частота: `Advanced | F2`
- Связанные inventory IDs: `JS-24`
- Статус modern/legacy: `современная точность интервью`
- Ответ: [JS-OBJECTS-Q23](../answers/by-domain/01-javascript-and-async-programming.md#js-objects-q23)
- Источники / последняя проверка: `ECMAScript 2026, MDN: instanceof, Symbol.hasInstance, Array.isArray | 2026-10-08`

#### Вопрос

Значение пришло из iframe, а часть объектов могла получить новый прототип после создания. Сравните `value instanceof Type`, `Type.prototype.isPrototypeOf(value)` и `value.constructor === Type`. Объясните влияние разных сред выполнения (realms) и пользовательского `Symbol.hasInstance`. Как проверять массивы и как выбирать проверку структуры, маркера экземпляра или доступной возможности для прикладного API?

### JS-OBJECTS-Q24

**Выберите композицию или наследование для расширяемого сервиса.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.4. this, вызов функции и объектная модель`
- Уровень: `Senior`
- Тип: `architecture | code-review | practical-production-scenario`
- Приоритет/частота: `Advanced | F2`
- Связанные inventory IDs: `JS-23`, `JS-25`
- Статус modern/legacy: `современная практика рабочего кода`
- Ответ: [JS-OBJECTS-Q24](../answers/by-domain/01-javascript-and-async-programming.md#js-objects-q24)
- Источники / последняя проверка: `MDN primary references, engineering analysis | 2026-10-08`

#### Вопрос

Система уведомлений поддерживает email, push и SMS. Для каждого канала нужны разные отправка и нормализация, а retry, logging и rate limiting должны независимо заменяться в тестах. Команда предлагает глубокую иерархию `BaseNotifier -> RetryingNotifier -> LoggedNotifier -> EmailNotifier`. Проведите ревью и предложите модель создания объектов и композиции зависимостей. Где класс и наследование всё же остаются уместными?

### JS-OBJECTS-Q25

**Проведите ревью API с дескрипторами и `freeze`.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.4. this, вызов функции и объектная модель`
- Уровень: `Senior`
- Тип: `code-review | debugging | API-design`
- Приоритет/частота: `Advanced | F2`
- Связанные inventory IDs: `JS-27`, `JS-28`
- Статус modern/legacy: `современная практика рабочего кода`
- Ответ: [JS-OBJECTS-Q25](../answers/by-domain/01-javascript-and-async-programming.md#js-objects-q25)
- Источники / последняя проверка: `ECMAScript 2026, MDN: Property descriptors, Object.freeze | 2026-10-08`

#### Вопрос

Библиотека принимает объект настроек, вызывает `Object.freeze(settings)` и обещает полную неизменяемость. Затем она добавляет через `Object.defineProperty` кеш без явных флагов, а getter `status` при каждом чтении выполняет сетевой запрос. Найдите ошибки контракта, значения флагов дескриптора по умолчанию и проблемы наблюдаемости. Предложите более явный API владения, проверки и кеширования.

### JS-OBJECTS-Q26

**Объясните получателя и инвариант Proxy в перехватчике `get`.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.4. this, вызов функции и объектная модель`
- Уровень: `Senior`
- Тип: `output | debugging | why`
- Приоритет/частота: `Advanced | F2`
- Связанные inventory IDs: `JS-27`, `JS-39`
- Статус modern/legacy: `современная точность интервью`
- Ответ: [JS-OBJECTS-Q26](../answers/by-domain/01-javascript-and-async-programming.md#js-objects-q26)
- Источники / последняя проверка: `ECMAScript 2026, MDN: Proxy.get, Reflect.get | 2026-10-08`

#### Вопрос

```js
const target = {
  _name: "target",
  get name() {
    return this._name;
  },
};

const wrong = new Proxy(target, {
  get(currentTarget, key) {
    return currentTarget[key];
  },
});

const correct = new Proxy(target, {
  get(currentTarget, key, receiver) {
    return Reflect.get(currentTarget, key, receiver);
  },
});

const wrongChild = Object.create(wrong);
wrongChild._name = "wrong-child";

const correctChild = Object.create(correct);
correctChild._name = "correct-child";

console.log(wrongChild.name);
console.log(correctChild.name);
```

Предскажите результат и объясните роль получателя (`receiver`). Затем объясните, почему перехватчик, который возвращает другое значение для собственного неконфигурируемого и неизменяемого свойства данных исходного объекта, приводит к `TypeError`.

### JS-OBJECTS-Q27

**Разберите контракт перехватчика `set` и строгий режим.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.4. this, вызов функции и объектная модель`
- Уровень: `Senior`
- Тип: `output | debugging`
- Приоритет/частота: `Advanced | F1`
- Связанные inventory IDs: `JS-27`, `JS-39`
- Статус modern/legacy: `современная точность интервью`
- Ответ: [JS-OBJECTS-Q27](../answers/by-domain/01-javascript-and-async-programming.md#js-objects-q27)
- Источники / последняя проверка: `ECMAScript 2026, MDN: Proxy.set, Reflect.set | 2026-10-08`

#### Вопрос

```js
"use strict";

const target = {};
const validated = new Proxy(target, {
  set(currentTarget, key, value, receiver) {
    if (key === "age" && (!Number.isInteger(value) || value < 0)) {
      return false;
    }

    return Reflect.set(currentTarget, key, value, receiver);
  },
});

validated.age = 42;
console.log(target.age);
validated.age = -1;
```

Предскажите результат до ошибки. Что означает логический результат перехватчика, чем `Reflect.set` полезнее ручного `target[key] = value` и какие ограничения исходного объекта нельзя нарушать даже при собственной валидации?

### JS-OBJECTS-Q28

**Оцените Proxy как границу доступа.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.4. this, вызов функции и объектная модель`
- Уровень: `Senior`
- Тип: `practical-production-scenario | architecture | code-review`
- Приоритет/частота: `Advanced | F1`
- Связанные inventory IDs: `JS-39`
- Статус modern/legacy: `современная обзорная глубина`
- Ответ: [JS-OBJECTS-Q28](../answers/by-domain/01-javascript-and-async-programming.md#js-objects-q28)
- Источники / последняя проверка: `ECMAScript 2026, MDN: Proxy, Proxy.revocable, Reflect | 2026-10-08`

#### Вопрос

Плагин получает временный доступ к объекту модели только на время транзакции. Оцените `Proxy.revocable` как механизм: что происходит после `revoke`, как различаются идентичности proxy и target, как это влияет на `===`, `Map`/`WeakMap`, логирование и отладку? Назовите реальные случаи для Proxy и случаи, где явная оболочка, обычная функция или дескриптор проще.

### JS-OBJECTS-Q29

**Реализуйте валидируемое представление через Proxy.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.4. this, вызов функции и объектная модель`
- Уровень: `Senior`
- Тип: `implementation | debugging | API-design`
- Приоритет/частота: `Advanced | F2`
- Связанные inventory IDs: `JS-26`, `JS-27`, `JS-39`
- Статус modern/legacy: `современная обзорная глубина`
- Ответ: [JS-OBJECTS-Q29](../answers/by-domain/01-javascript-and-async-programming.md#js-objects-q29)
- Источники / последняя проверка: `ECMAScript 2026, MDN: Proxy, Reflect | 2026-10-08`

#### Вопрос

Реализуйте `createValidatedView(target, validators, requiredKeys)`. Запись ключа с валидатором должна пройти проверку, удаление обязательного ключа должно быть запрещено, остальные операции следует прозрачно передать через `Reflect`. Сохраните корректного получателя. Объясните поверхностную границу проверки, поведение при ошибке, идентичность, закрытые поля, инварианты Proxy и тесты, необходимые перед использованием такого API.

### JS-OBJECTS-Q30

**Объясните выбор объектной модели как на Senior-интервью.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.4. this, вызов функции и объектная модель`
- Уровень: `Senior`
- Тип: `practical-production-scenario | architecture | interview-communication`
- Приоритет/частота: `Advanced | F2`
- Связанные inventory IDs: `JS-23`, `JS-24`, `JS-25`, `JS-26`, `JS-27`, `JS-28`, `JS-39`
- Статус modern/legacy: `современная рабочая модель + интеграция тем интервью`
- Ответ: [JS-OBJECTS-Q30](../answers/by-domain/01-javascript-and-async-programming.md#js-objects-q30)
- Источники / последняя проверка: `ECMAScript 2026, MDN primary references, engineering analysis | 2026-10-08`

#### Вопрос

Вы проектируете модель строк большой таблицы: объектов будут десятки тысяч, общее поведение должно быть расширяемым, сериализуемые данные — предсказуемыми, несколько вычисляемых полей — доступными для чтения, а режим разработки должен обнаруживать запрещённые изменения. За три минуты предложите объектную модель и объясните:

1. способ создания объектов и размещение методов;
2. правила `this` и передачи методов как callbacks;
3. роль цепочки прототипов и классов;
4. политику собственных и перечислимых свойств, а также дескрипторов;
5. границы `freeze`;
6. нужен ли Proxy в рабочей версии или только при разработке;
7. как вы проверите корректность, производительность и удобство отладки.

## 1.5. Arrays, Transformations & Copying

Не открывайте отдельный файл ответов до собственной попытки. В задачах на результат сначала подпишите существующие индексы, `length`, мутацию входа, возвращаемое значение и общие идентичности объектов.

### JS-ARRAYS-Q01

**Как отличить настоящий массив и почему `instanceof Array` недостаточно?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.5. Arrays, Transformations & Copying`
- Уровень: `Junior`
- Тип: `conceptual | compare | why`
- Приоритет/частота: `Core | F3`
- Связанные inventory IDs: `JS-29`, `JS-31`
- Статус modern/legacy: `современная основа + узнавание legacy-проверки`
- Ответ: [JS-ARRAYS-Q01](../answers/by-domain/01-javascript-and-async-programming.md#js-arrays-q01)
- Источники / последняя проверка: `ECMAScript 2026, MDN: Array.isArray | 2026-10-08`

#### Вопрос

Сравните `Array.isArray(value)`, `value instanceof Array`, проверку прототипа и `typeof value`. Объясните поведение для массива из другого `iframe`, `Uint8Array` и объекта `{ __proto__: Array.prototype }`. Какой API использовать на прикладной границе и почему?

### JS-ARRAYS-Q02

**Предскажите `length` и наличие индексных свойств.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.5. Arrays, Transformations & Copying`
- Уровень: `Junior`
- Тип: `output | explain`
- Приоритет/частота: `Core | F3`
- Связанные inventory IDs: `JS-29`, `JS-31`
- Статус modern/legacy: `современная основа`
- Ответ: [JS-ARRAYS-Q02](../answers/by-domain/01-javascript-and-async-programming.md#js-arrays-q02)
- Источники / последняя проверка: `ECMAScript 2026: Array exotic objects | 2026-10-08`

#### Вопрос

```js
const values = [];
values[2] = "c";
values.label = "draft";
values[-1] = "left";

console.log(values.length);
console.log(0 in values, 2 in values);
console.log(Object.keys(values));

values.length = 1;

console.log(values.length);
console.log(2 in values);
console.log(values.label, values[-1]);
```

Предскажите результат и объясните, какие ключи являются индексами массива (array indices). Почему увеличение `length` и его сокращение имеют несимметричную семантику?

### JS-ARRAYS-Q03

**Различите пустой слот (hole) и явный `undefined`.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.5. Arrays, Transformations & Copying`
- Уровень: `Junior`
- Тип: `output | conceptual`
- Приоритет/частота: `Core | F3`
- Связанные inventory IDs: `JS-31`
- Статус modern/legacy: `современная основа`
- Ответ: [JS-ARRAYS-Q03](../answers/by-domain/01-javascript-and-async-programming.md#js-arrays-q03)
- Источники / последняя проверка: `ECMAScript 2026, MDN: sparse arrays | 2026-10-08`

#### Вопрос

```js
const a = new Array(3);
const b = [undefined, undefined, undefined];

console.log(a.length, b.length);
console.log(a[0], b[0]);
console.log(0 in a, 0 in b);
console.log(Object.hasOwn(a, 0), Object.hasOwn(b, 0));
console.log(Object.keys(a), Object.keys(b));
```

Предскажите вывод. Дайте определения плотного массива, разреженного массива и пустого слота. Почему чтения `a[0]` недостаточно для диагностики структуры?

### JS-ARRAYS-Q04

**`delete` или `splice`: что именно удаляется?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.5. Arrays, Transformations & Copying`
- Уровень: `Junior`
- Тип: `compare | output | debugging`
- Приоритет/частота: `Core | F3`
- Связанные inventory IDs: `JS-29`, `JS-31`
- Статус modern/legacy: `современная основа`
- Ответ: [JS-ARRAYS-Q04](../answers/by-domain/01-javascript-and-async-programming.md#js-arrays-q04)
- Источники / последняя проверка: `ECMAScript 2026: delete, splice | 2026-10-08`

#### Вопрос

```js
const first = ["a", "b", "c"];
const second = ["a", "b", "c"];

console.log(delete first[1]);
const removed = second.splice(1, 1);

console.log(first, first.length, 1 in first);
console.log(second, second.length, removed);
```

Предскажите результат. Как удалить элемент последовательности без изменения исходного массива? Когда сохранение пустого слота могло бы быть намеренным?

### JS-ARRAYS-Q05

**Восстановите договоры мутирующих методов.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.5. Arrays, Transformations & Copying`
- Уровень: `Junior`
- Тип: `recall | compare`
- Приоритет/частота: `Core | F3`
- Связанные inventory IDs: `JS-29`
- Статус modern/legacy: `современная основа`
- Ответ: [JS-ARRAYS-Q05](../answers/by-domain/01-javascript-and-async-programming.md#js-arrays-q05)
- Источники / последняя проверка: `ECMAScript 2026: Array.prototype methods | 2026-10-08`

#### Вопрос

Для `push`, `pop`, `shift`, `unshift`, `splice`, `sort`, `reverse`, `fill` и `copyWithin` заполните матрицу: меняется ли исходник, что возвращается, может ли измениться `length`, копируются ли элементы-объекты. Затем найдите ошибку:

```js
let queue = ["a"];
queue = queue.push("b");
```

### JS-ARRAYS-Q06

**Сравните `slice`, `splice` и `toSpliced`.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.5. Arrays, Transformations & Copying`
- Уровень: `Junior`
- Тип: `compare | output`
- Приоритет/частота: `Core | F3`
- Связанные inventory IDs: `JS-29`
- Статус modern/legacy: `современная основа + современная copying alternative`
- Ответ: [JS-ARRAYS-Q06](../answers/by-domain/01-javascript-and-async-programming.md#js-arrays-q06)
- Источники / последняя проверка: `ECMAScript 2026: slice/splice/toSpliced | 2026-10-08`

#### Вопрос

Для одного исходника `["a", "b", "c", "d"]` объясните результаты `slice(1, 3)`, `splice(1, 2, "x")` и `toSpliced(1, 2, "x")`. Какие два метода возвращают принципиально разные вещи при похожей операции удаления? Как назвать API, который намеренно меняет переданный массив?

### JS-ARRAYS-Q07

**Выберите метод преобразования по форме результата.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.5. Arrays, Transformations & Copying`
- Уровень: `Junior`
- Тип: `conceptual | compare`
- Приоритет/частота: `Core | F3`
- Связанные inventory IDs: `JS-30`
- Статус modern/legacy: `современная основа`
- Ответ: [JS-ARRAYS-Q07](../answers/by-domain/01-javascript-and-async-programming.md#js-arrays-q07)
- Источники / последняя проверка: `ECMAScript 2026: iterative methods | 2026-10-08`

#### Вопрос

Для каждого требования выберите `map`, `filter`, `find`, `some`, `every`, `forEach`, `reduce` или обычный цикл: создать модель представления для каждого элемента; оставить активные; найти первый просроченный; проверить наличие ошибки; проверить валидность всех; записать аналитику; посчитать сумму; построить сложный результат с несколькими ранними выходами. Объясните возвращаемое значение и поведение при раннем выходе.

### JS-ARRAYS-Q08

**Найдите пропущенный `return` и путаницу `map`/`forEach`.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.5. Arrays, Transformations & Copying`
- Уровень: `Junior`
- Тип: `find-the-bug | output`
- Приоритет/частота: `Core | F3`
- Связанные inventory IDs: `JS-30`
- Статус modern/legacy: `современная основа`
- Ответ: [JS-ARRAYS-Q08](../answers/by-domain/01-javascript-and-async-programming.md#js-arrays-q08)
- Источники / последняя проверка: `ECMAScript 2026: map/forEach | 2026-10-08`

#### Вопрос

```js
const values = [1, 2, 3];

const first = values.map((value) => {
  value * 2;
});

const second = values.forEach((value) => value * 2);
```

Что находится в `first` и `second`? Исправьте оба намерения: получить удвоенный массив и выполнить логирование без создания лишнего массива.

### JS-ARRAYS-Q09

**Почему числа сортируются «неправильно» без функции сравнения?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.5. Arrays, Transformations & Copying`
- Уровень: `Junior`
- Тип: `output | explain`
- Приоритет/частота: `Core | F3`
- Связанные inventory IDs: `JS-32`
- Статус modern/legacy: `современная основа`
- Ответ: [JS-ARRAYS-Q09](../answers/by-domain/01-javascript-and-async-programming.md#js-arrays-q09)
- Источники / последняя проверка: `ECMAScript 2026, MDN: sort | 2026-10-08`

#### Вопрос

```js
const values = [2, 10, 1, 30];
const result = values.sort();

console.log(values);
console.log(result === values);
```

Предскажите результат. Напишите числовую функцию сравнения для возрастания и убывания. Что гарантирует знак её результата?

### JS-ARRAYS-Q10

**Проследите поведение разных методов на разреженном массиве.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.5. Arrays, Transformations & Copying`
- Уровень: `Mid`
- Тип: `output | compare | why`
- Приоритет/частота: `Professional | F3`
- Связанные inventory IDs: `JS-30`, `JS-31`
- Статус modern/legacy: `современная точность интервью`
- Ответ: [JS-ARRAYS-Q10](../answers/by-domain/01-javascript-and-async-programming.md#js-arrays-q10)
- Источники / последняя проверка: `ECMAScript 2026: map/filter/find/some/every/reduce; runtime | 2026-10-08`

#### Вопрос

```js
const input = [1, , 3];
const visits = {};

const mapped = input.map((value, index) => {
  (visits.map ??= []).push([index, value]);
  return value * 2;
});

const filtered = input.filter((value, index) => {
  (visits.filter ??= []).push([index, value]);
  return true;
});

input.find((value, index) => {
  (visits.find ??= []).push([index, value]);
  return false;
});
```

Предскажите `mapped`, `filtered`, списки посещений и наличие индекса `1` в результатах. Затем сравните поведение `forEach`, `some`, `every` и `reduce` для пустого слота.

### JS-ARRAYS-Q11

**Сравните `slice`, spread и методы Change Array by Copy на разреженном массиве.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.5. Arrays, Transformations & Copying`
- Уровень: `Mid`
- Тип: `output | compare`
- Приоритет/частота: `Professional | F3`
- Связанные inventory IDs: `JS-29`, `JS-31`
- Статус modern/legacy: `современная copying semantics`
- Ответ: [JS-ARRAYS-Q11](../answers/by-domain/01-javascript-and-async-programming.md#js-arrays-q11)
- Источники / последняя проверка: `ECMAScript 2026, MDN: copying array methods; runtime | 2026-10-08`

#### Вопрос

```js
const source = ["a", , "c"];
const bySlice = source.slice();
const bySpread = [...source];
const reversed = source.toReversed();
const replaced = source.with(0, "A");
const spliced = source.toSpliced(0, 0);
const sorted = source.toSorted();
```

Для каждого результата укажите значения, `length` и наличие индекса `1`. Почему «все копирующие API одинаково копируют разреженный массив» — неверная модель?

### JS-ARRAYS-Q12

**Исправьте случайную мутацию входных данных.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.5. Arrays, Transformations & Copying`
- Уровень: `Mid`
- Тип: `debugging | refactoring | API-design`
- Приоритет/частота: `Professional | F3`
- Связанные inventory IDs: `JS-29`, `JS-32`
- Статус modern/legacy: `современная production-рекомендация`
- Ответ: [JS-ARRAYS-Q12](../answers/by-domain/01-javascript-and-async-programming.md#js-arrays-q12)
- Источники / последняя проверка: `ECMAScript 2026: sort/toSorted | 2026-10-08`

#### Вопрос

```js
export function topUsers(users, limit) {
  return users
    .sort((a, b) => b.score - a.score)
    .slice(0, limit);
}
```

Найдите наблюдаемую мутацию и перепишите функцию с немутирующим договором. Затем предложите отдельно названный вариант, меняющий данные на месте. Когда локальный `sort()` нового массива остаётся разумным?

### JS-ARRAYS-Q13

**Найдите потерю данных в `filter(Boolean)`.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.5. Arrays, Transformations & Copying`
- Уровень: `Mid`
- Тип: `debugging | practical-scenario`
- Приоритет/частота: `Professional | F3`
- Связанные inventory IDs: `JS-30`
- Статус modern/legacy: `современная production-рекомендация`
- Ответ: [JS-ARRAYS-Q13](../answers/by-domain/01-javascript-and-async-programming.md#js-arrays-q13)
- Источники / последняя проверка: `ECMAScript 2026: filter, ToBoolean | 2026-10-08`

#### Вопрос

Телеметрия принимает `0`, `false` и пустую строку как значимые показания, а `null`/`undefined` означают отсутствие:

```js
const cleaned = readings.filter(Boolean);
```

Найдите ошибку, напишите точный предикат и объясните, при каком договоре `filter(Boolean)` остаётся допустимым. Как пустые слоты влияют на результат?

### JS-ARRAYS-Q14

**Диагностируйте `reduce` без начального значения.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.5. Arrays, Transformations & Copying`
- Уровень: `Mid`
- Тип: `output | debugging | why`
- Приоритет/частота: `Core | F3`
- Связанные inventory IDs: `JS-30`, `JS-31`
- Статус modern/legacy: `современная основа`
- Ответ: [JS-ARRAYS-Q14](../answers/by-domain/01-javascript-and-async-programming.md#js-arrays-q14)
- Источники / последняя проверка: `ECMAScript 2026: reduce | 2026-10-08`

#### Вопрос

Предскажите результат или ошибку независимо для `[1, 2, 3]`, `[]`, `new Array(3)` и `[, 2, 3]`:

```js
input.reduce((sum, value) => sum + value);
```

Как изменятся вызовы callback после добавления `0` как `initialValue`? Почему явное начальное значение улучшает тип и форму аккумулятора?

### JS-ARRAYS-Q15

**Объясните `some` и `every` на пустом массиве.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.5. Arrays, Transformations & Copying`
- Уровень: `Mid`
- Тип: `conceptual | output | why`
- Приоритет/частота: `Core | F2`
- Связанные inventory IDs: `JS-30`, `JS-31`
- Статус modern/legacy: `современная основа`
- Ответ: [JS-ARRAYS-Q15](../answers/by-domain/01-javascript-and-async-programming.md#js-arrays-q15)
- Источники / последняя проверка: `ECMAScript 2026: some/every | 2026-10-08`

#### Вопрос

Почему `[].some(predicate)` возвращает `false`, а `[].every(predicate)` — `true`, причём callback не вызывается? Как это влияет на проверку «форма содержит хотя бы одно поле и все поля валидны»? Что произойдёт для `new Array(3)`?

### JS-ARRAYS-Q16

**Проследите изменение массива во время обхода.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.5. Arrays, Transformations & Copying`
- Уровень: `Mid`
- Тип: `output | debugging`
- Приоритет/частота: `Professional | F2`
- Связанные inventory IDs: `JS-30`, `JS-31`
- Статус modern/legacy: `современная точность интервью`
- Ответ: [JS-ARRAYS-Q16](../answers/by-domain/01-javascript-and-async-programming.md#js-arrays-q16)
- Источники / последняя проверка: `ECMAScript 2026: iterative method ranges | 2026-10-08`

#### Вопрос

```js
const values = [1, 2, 3];
const seen = [];

values.forEach((value, index) => {
  seen.push(value);

  if (index === 0) {
    values.push(4);
    values[2] = 30;
  }

  if (index === 1) {
    delete values[2];
  }
});

console.log(seen, values);
```

Предскажите результат через фиксированную начальную длину и проверку наличия элемента. Чем `find` отличался бы для удалённого индекса? Почему `shift`/`splice` внутри callback особенно опасны для чтения?

### JS-ARRAYS-Q17

**Исправьте async callback в `forEach`.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.5. Arrays, Transformations & Copying`
- Уровень: `Mid`
- Тип: `debugging | conceptual`
- Приоритет/частота: `Professional | F3`
- Связанные inventory IDs: `JS-30`
- Статус modern/legacy: `современная основа; координация отложена до 1.10–1.11`
- Ответ: [JS-ARRAYS-Q17](../answers/by-domain/01-javascript-and-async-programming.md#js-arrays-q17)
- Источники / последняя проверка: `ECMAScript 2026: forEach/map callback contracts | 2026-10-08`

#### Вопрос

```js
async function saveAll(items) {
  items.forEach(async (item) => {
    await save(item);
  });

  return "done";
}
```

Почему `saveAll` может завершиться до сохранений и потерять ошибки? Что вернёт `items.map(async ...)`? Назовите последовательный и параллельный shape исправления, не разворачивая полную тему Promise coordination.

### JS-ARRAYS-Q18

**Исправьте функцию сравнения, возвращающую boolean.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.5. Arrays, Transformations & Copying`
- Уровень: `Mid`
- Тип: `find-the-bug | debugging | why`
- Приоритет/частота: `Core | F3`
- Связанные inventory IDs: `JS-32`
- Статус modern/legacy: `современная основа`
- Ответ: [JS-ARRAYS-Q18](../answers/by-domain/01-javascript-and-async-programming.md#js-arrays-q18)
- Источники / последняя проверка: `ECMAScript 2026: consistent comparator, MDN: sort | 2026-10-08`

#### Вопрос

```js
items.sort((a, b) => a.score > b.score);
```

Почему эта функция сравнения нарушает антисимметрию? Исправьте сортировку чисел по возрастанию и объясните чистоту, равенство, антисимметрию и транзитивность в интервью-форме. Что спецификация разрешает при несогласованной функции сравнения?

### JS-ARRAYS-Q19

**Реализуйте стабильную сортировку по нескольким полям.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.5. Arrays, Transformations & Copying`
- Уровень: `Mid`
- Тип: `implementation | practical-scenario`
- Приоритет/частота: `Professional | F3`
- Связанные inventory IDs: `JS-32`
- Статус modern/legacy: `современная production-практика`
- Ответ: [JS-ARRAYS-Q19](../answers/by-domain/01-javascript-and-async-programming.md#js-arrays-q19)
- Источники / последняя проверка: `ECMAScript 2026: stable sort, Intl.Collator | 2026-10-08`

#### Вопрос

Отсортируйте пользователей без изменения входа: `score` по убыванию, затем `name` по локали без учёта регистра, затем сохраните исходный порядок для полностью равных ключей. Используйте `Intl.Collator` разумно. Почему стабильность спецификации важна, но не заменяет явно заданный вторичный ключ?

### JS-ARRAYS-Q20

**Сравните `sort` и `toSorted` для пустых слотов и `undefined`.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.5. Arrays, Transformations & Copying`
- Уровень: `Mid`
- Тип: `output | compare`
- Приоритет/частота: `Professional | F2`
- Связанные inventory IDs: `JS-31`, `JS-32`
- Статус modern/legacy: `современная точность интервью`
- Ответ: [JS-ARRAYS-Q20](../answers/by-domain/01-javascript-and-async-programming.md#js-arrays-q20)
- Источники / последняя проверка: `ECMAScript 2026: sort/toSorted; runtime | 2026-10-08`

#### Вопрос

Для независимых массивов `[, undefined, "a", "b"]` выполните `sort()` и `toSorted()`. Укажите порядок, наличие последнего индекса и мутацию исходника. Вызывается ли функция сравнения для `undefined`? Какую сложность встроенного алгоритма можно обещать по спецификации?

### JS-ARRAYS-Q21

**Предскажите значения по умолчанию при деструктуризации, пустые слоты и `null`.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.5. Arrays, Transformations & Copying`
- Уровень: `Mid`
- Тип: `output | explain`
- Приоритет/частота: `Core | F3`
- Связанные inventory IDs: `JS-33`
- Статус modern/legacy: `современная основа`
- Ответ: [JS-ARRAYS-Q21](../answers/by-domain/01-javascript-and-async-programming.md#js-arrays-q21)
- Источники / последняя проверка: `ECMAScript 2026: destructuring | 2026-10-08`

#### Вопрос

```js
const input = ["Ada", , undefined, null, ["admin", "editor"]];
const [name, second = "B", third = "C", fourth = "D", [role], ...rest] = input;

console.log(name, second, third, fourth, role, rest);
```

Предскажите результат. Почему значение по умолчанию применяется к пустому слоту и `undefined`, но не к `null`? Как выглядят пропуск позиции, вложенный шаблон, rest и обмен значений?

### JS-ARRAYS-Q22

**Различите spread массива/вызова и object spread.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.5. Arrays, Transformations & Copying`
- Уровень: `Mid`
- Тип: `compare | why | practical-scenario`
- Приоритет/частота: `Professional | F2`
- Связанные inventory IDs: `JS-33`, `JS-34`
- Статус modern/legacy: `современная основа; iteration protocol отложен до 1.6`
- Ответ: [JS-ARRAYS-Q22](../answers/by-domain/01-javascript-and-async-programming.md#js-arrays-q22)
- Источники / последняя проверка: `ECMAScript 2026: spread syntax, MDN: argument limits | 2026-10-08`

#### Вопрос

Что требуется от значения в `[...value]` и `fn(...value)`, а что копирует `{ ...value }`? Какие ключи object spread пропускает? Почему оба вида остаются поверхностными? Почему `Math.max(...hugeArray)` не является универсальным решением для большого массива?

### JS-ARRAYS-Q23

**Проведите ревью object spread и `Object.assign`.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.5. Arrays, Transformations & Copying`
- Уровень: `Mid`
- Тип: `code-review | compare | output`
- Приоритет/частота: `Professional | F2`
- Связанные inventory IDs: `JS-33`, `JS-34`
- Статус modern/legacy: `современная точность рабочего кода`
- Ответ: [JS-ARRAYS-Q23](../answers/by-domain/01-javascript-and-async-programming.md#js-arrays-q23)
- Источники / последняя проверка: `ECMAScript 2026: CopyDataProperties, Object.assign | 2026-10-08`

#### Вопрос

Сравните геттеры источника, сеттеры целевого объекта, собственные перечисляемые строковые ключи и ключи-символы, сохранение дескрипторов и мутацию цели для `{ ...source }` и `Object.assign(target, source)`. Как действительно перенести дескрипторы? Почему и это не является глубокой копией?

### JS-ARRAYS-Q24

**Покажите общую вложенную ссылку после поверхностной копии.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.5. Arrays, Transformations & Copying`
- Уровень: `Mid`
- Тип: `output | debugging | explain`
- Приоритет/частота: `Core | F3`
- Связанные inventory IDs: `JS-34`
- Статус modern/legacy: `современная production-модель`
- Ответ: [JS-ARRAYS-Q24](../answers/by-domain/01-javascript-and-async-programming.md#js-arrays-q24)
- Источники / последняя проверка: `ECMAScript 2026: spread/slice; MDN: shallow copy | 2026-10-08`

#### Вопрос

```js
const source = [{ id: 1, meta: { active: false } }];
const copy = source.slice();

copy[0].meta.active = true;

console.log(source === copy);
console.log(source[0] === copy[0]);
console.log(source[0].meta === copy[0].meta);
console.log(source[0].meta.active);
```

Предскажите результат и нарисуйте идентичности. Исправьте обновление копированием только изменяемого пути.

### JS-ARRAYS-Q25

**Спроектируйте обновление со структурным разделением.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.5. Arrays, Transformations & Copying`
- Уровень: `Senior`
- Тип: `implementation | API-design | performance-reasoning`
- Приоритет/частота: `Advanced | F3`
- Связанные inventory IDs: `JS-29`, `JS-30`, `JS-34`
- Статус modern/legacy: `современная production-практика`
- Ответ: [JS-ARRAYS-Q25](../answers/by-domain/01-javascript-and-async-programming.md#js-arrays-q25)
- Источники / последняя проверка: `ECMAScript 2026 semantics, engineering analysis | 2026-10-08`

#### Вопрос

Реализуйте `updateLineQuantity(order, lineId, quantity)`. Функция не меняет `order`, создаёт новые идентичности только для корня, массива `lines`, найденной строки и её объекта `pricing`, сохраняет идентичности остальных строк и возвращает исходный `order`, если строка не найдена или значение не изменилось. Объясните пользу и риск структурного разделения для мемоизации и обнаружения изменений.

### JS-ARRAYS-Q26

**Сформулируйте договор глубокой копии для графа данных.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.5. Arrays, Transformations & Copying`
- Уровень: `Senior`
- Тип: `architecture | practical-production-scenario | interview-communication`
- Приоритет/частота: `Advanced | F3`
- Связанные inventory IDs: `JS-34`
- Статус modern/legacy: `современная инженерная модель`
- Ответ: [JS-ARRAYS-Q26](../answers/by-domain/01-javascript-and-async-programming.md#js-arrays-q26)
- Источники / последняя проверка: `WHATWG structured data, ECMAScript object model | 2026-10-08`

#### Вопрос

Перед выбором глубокой копии перечислите решения для циклов, повторных ссылок, прототипов/классов, дескрипторов/аксессоров, функций, ключей и значений `Symbol`, встроенных типов, DOM-объектов и объектов среды, закрытого/внутреннего состояния и стоимости большого графа. Когда ручное копирование известной схемы лучше стандартизованного или библиотечного общего алгоритма?

### JS-ARRAYS-Q27

**Проверьте циклы и повторные ссылки в `structuredClone`.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.5. Arrays, Transformations & Copying`
- Уровень: `Senior`
- Тип: `output | conceptual`
- Приоритет/частота: `Advanced | F3`
- Связанные inventory IDs: `JS-34`
- Статус modern/legacy: `современный Web/Node API`
- Ответ: [JS-ARRAYS-Q27](../answers/by-domain/01-javascript-and-async-programming.md#js-arrays-q27)
- Источники / последняя проверка: `WHATWG HTML structured data, MDN; runtime | 2026-10-08`

#### Вопрос

```js
const shared = { count: 1 };
const source = { first: shared, second: shared };
source.self = source;

const clone = structuredClone(source);

console.log(clone === source);
console.log(clone.self === clone);
console.log(clone.first === clone.second);
console.log(clone.first === source.first);
```

Предскажите результат. Почему сохранение общей ссылки внутри нового графа не означает общую ссылку с исходным графом?

### JS-ARRAYS-Q28

**Найдите границы `structuredClone` для класса и дескрипторов.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.5. Arrays, Transformations & Copying`
- Уровень: `Senior`
- Тип: `output | code-review | why`
- Приоритет/частота: `Advanced | F3`
- Связанные inventory IDs: `JS-34`
- Статус modern/legacy: `современная точность интервью`
- Ответ: [JS-ARRAYS-Q28](../answers/by-domain/01-javascript-and-async-programming.md#js-arrays-q28)
- Источники / последняя проверка: `WHATWG structured data, MDN structured clone; runtime | 2026-10-08`

#### Вопрос

Пользовательский класс содержит метод, закрытое поле, неперечисляемое свойство только для чтения и геттер. Что из этого обещает сохранить `structuredClone`, может ли геттер выполниться, станет ли результат экземпляром класса и какие значения приводят к `DataCloneError`? Назовите поддерживаемые встроенные типы, которые важно отличать от пользовательских классов.

### JS-ARRAYS-Q29

**Объясните перенос и отсоединение `ArrayBuffer`.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.5. Arrays, Transformations & Copying`
- Уровень: `Senior`
- Тип: `output | practical-scenario | API-design`
- Приоритет/частота: `Advanced | F2`
- Связанные inventory IDs: `JS-34`
- Статус modern/legacy: `современный platform API`
- Ответ: [JS-ARRAYS-Q29](../answers/by-domain/01-javascript-and-async-programming.md#js-arrays-q29)
- Источники / последняя проверка: `WHATWG HTML: StructuredSerializeWithTransfer, MDN; runtime | 2026-10-08`

#### Вопрос

```js
const buffer = new ArrayBuffer(4);
new Uint8Array(buffer)[0] = 7;

const clone = structuredClone(
  { buffer },
  { transfer: [buffer] },
);
```

Предскажите оба `byteLength` и первый байт результата. Чем перенос отличается от копирования, почему это смена владения и какие проверки нужны перед использованием в рабочей системе?

### JS-ARRAYS-Q30

**Проведите аудит цикла JSON-сериализации как клонирования.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.5. Arrays, Transformations & Copying`
- Уровень: `Senior`
- Тип: `code-review | compare | debugging`
- Приоритет/частота: `Advanced | F3`
- Связанные inventory IDs: `JS-34`
- Статус modern/legacy: `legacy/workaround knowledge → современная ограниченная рекомендация`
- Ответ: [JS-ARRAYS-Q30](../answers/by-domain/01-javascript-and-async-programming.md#js-arrays-q30)
- Источники / последняя проверка: `ECMAScript 2026: JSON.stringify, MDN | 2026-10-08`

#### Вопрос

Составьте матрицу потерь `JSON.parse(JSON.stringify(value))` для циклов, `BigInt`, `undefined` в объектах и массивах, функций, `Symbol`, `NaN`, бесконечностей, `Date`, `Map`, `Set`, пустых слотов, пользовательского прототипа, дескрипторов, повторных ссылок и `toJSON`. При каком узком договоре такой цикл допустим?

### JS-ARRAYS-Q31

**Проведите ревью API с неясным владением массива.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.5. Arrays, Transformations & Copying`
- Уровень: `Senior`
- Тип: `code-review | API-design | performance-reasoning`
- Приоритет/частота: `Advanced | F3`
- Связанные inventory IDs: `JS-29`, `JS-30`, `JS-32`, `JS-34`
- Статус modern/legacy: `современная production-практика`
- Ответ: [JS-ARRAYS-Q31](../answers/by-domain/01-javascript-and-async-programming.md#js-arrays-q31)
- Источники / последняя проверка: `ECMAScript 2026 semantics, engineering analysis | 2026-10-08`

#### Вопрос

API принимает массив строк таблицы, сортирует его, вызывает `filter(Boolean)`, меняет вложенные `meta`, затем делает `structuredClone` «для безопасности». Расставьте проблемы по приоритету: корректность, владение, функция сравнения, ложные значения, общие ссылки после поверхностной копии, граница клонирования, память и промежуточные массивы. Предложите ясный договор и план измерений, не оптимизируя заранее.

### JS-ARRAYS-Q32

**Объясните стратегию массивов и копирования как на Senior-интервью.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.5. Arrays, Transformations & Copying`
- Уровень: `Senior`
- Тип: `architecture | interview-communication | practical-production-scenario`
- Приоритет/частота: `Advanced | F2`
- Связанные inventory IDs: `JS-29`, `JS-30`, `JS-31`, `JS-32`, `JS-33`, `JS-34`
- Статус modern/legacy: `современная интеграция темы`
- Ответ: [JS-ARRAYS-Q32](../answers/by-domain/01-javascript-and-async-programming.md#js-arrays-q32)
- Источники / последняя проверка: `ECMAScript 2026, WHATWG structured data, engineering analysis | 2026-10-08`

#### Вопрос

За три минуты спроектируйте подготовку большой коллекции результатов поиска для интерфейса. Объясните: нормализацию разреженных и необязательных данных; выбор методов преобразования или цикла; стабильную сортировку; границу между мутирующим и немутирующим кодом; структурное разделение для одного обновления; необходимость или отсутствие глубокой копии; `structuredClone`/перенос на границе worker; тесты функции сравнения и договора клонирования; измерения времени, памяти и временных массивов.

## 1.6. Collections, Symbols & Iteration

Сначала ответьте по памяти. Для задач на вывод объясните ход рассуждения до запуска кода.

### JS-COLLECTIONS-Q01

**Когда выбрать объект, а когда `Map`?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.6. Collections, Symbols & Iteration`
- Уровень: `Junior`
- Тип: `compare`
- Приоритет/частота: `Core | F3`
- Связанные inventory IDs: `JS-35`
- Статус modern/legacy: `современный JavaScript`
- Ответ: [JS-COLLECTIONS-Q01](../answers/by-domain/01-javascript-and-async-programming.md#js-collections-q01)
- Источники / последняя проверка: `ECMAScript, MDN, engineering analysis | 2026-11-04`

#### Вопрос

Сравните объект настроек со структурой для произвольных ключей. Какие операции и свойства участвуют в выборе?

### JS-COLLECTIONS-Q02

**Сколько ключей сохранится?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.6. Collections, Symbols & Iteration`
- Уровень: `Junior`
- Тип: `output-prediction`
- Приоритет/частота: `Core | F3`
- Связанные inventory IDs: `JS-35`
- Статус modern/legacy: `современный JavaScript`
- Ответ: [JS-COLLECTIONS-Q02](../answers/by-domain/01-javascript-and-async-programming.md#js-collections-q02)
- Источники / последняя проверка: `ECMAScript, MDN, engineering analysis | 2026-11-04`

#### Вопрос

Предскажите результат и объясните различие между чтением и проверкой наличия.
```js
const index = new Map([[1, undefined], ["1", "text"]]);
console.log(index.size, index.get(1), index.has(1), index.has(2));
```

### JS-COLLECTIONS-Q03

**Почему запись не попала в `Map`?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.6. Collections, Symbols & Iteration`
- Уровень: `Junior`
- Тип: `debugging`
- Приоритет/частота: `Core | F3`
- Связанные inventory IDs: `JS-35`
- Статус modern/legacy: `современный JavaScript`
- Ответ: [JS-COLLECTIONS-Q03](../answers/by-domain/01-javascript-and-async-programming.md#js-collections-q03)
- Источники / последняя проверка: `ECMAScript, MDN, engineering analysis | 2026-11-04`

#### Вопрос

Найдите ошибку и скажите, что покажет вывод.
```js
const map = new Map();
map["ready"] = true;
console.log(map.get("ready"), map.size, map.ready);
```

### JS-COLLECTIONS-Q04

**Какие значения переживут дедупликацию?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.6. Collections, Symbols & Iteration`
- Уровень: `Junior`
- Тип: `output-prediction`
- Приоритет/частота: `Core | F2`
- Связанные inventory IDs: `JS-36`
- Статус modern/legacy: `современный JavaScript`
- Ответ: [JS-COLLECTIONS-Q04](../answers/by-domain/01-javascript-and-async-programming.md#js-collections-q04)
- Источники / последняя проверка: `ECMAScript, MDN, engineering analysis | 2026-11-04`

#### Вопрос

Назовите размер и порядок результата. Объясните судьбу двух объектов.
```js
const row = { id: 7 };
const values = new Set([NaN, NaN, -0, +0, row, { id: 7 }, row]);
console.log(values.size, [...values]);
```

### JS-COLLECTIONS-Q05

**Что означает одинаковое описание символов?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.6. Collections, Symbols & Iteration`
- Уровень: `Junior`
- Тип: `conceptual`
- Приоритет/частота: `Core | F2`
- Связанные inventory IDs: `JS-37`
- Статус modern/legacy: `современный JavaScript`
- Ответ: [JS-COLLECTIONS-Q05](../answers/by-domain/01-javascript-and-async-programming.md#js-collections-q05)
- Источники / последняя проверка: `ECMAScript, MDN, engineering analysis | 2026-11-04`

#### Вопрос

Сравните `Symbol("row") === Symbol("row")`, `Symbol.for("row") === Symbol.for("row")` и результат `Symbol.keyFor` для каждого вида.

### JS-COLLECTIONS-Q06

**Что обходит `for...of`, а что обходит `for...in`?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.6. Collections, Symbols & Iteration`
- Уровень: `Junior`
- Тип: `compare`
- Приоритет/частота: `Core | F2`
- Связанные inventory IDs: `JS-38`
- Статус modern/legacy: `современный JavaScript`
- Ответ: [JS-COLLECTIONS-Q06](../answers/by-domain/01-javascript-and-async-programming.md#js-collections-q06)
- Источники / последняя проверка: `ECMAScript, MDN, engineering analysis | 2026-11-04`

#### Вопрос

Сравните обход `Map` и объекта. Как получить собственные перечисляемые строковые пары объекта?

### JS-COLLECTIONS-Q07

**Достаточно ли индексов и `length` для spread?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.6. Collections, Symbols & Iteration`
- Уровень: `Junior`
- Тип: `output-prediction`
- Приоритет/частота: `Core | F2`
- Связанные inventory IDs: `JS-38`
- Статус modern/legacy: `современное поведение и совместимость`
- Ответ: [JS-COLLECTIONS-Q07](../answers/by-domain/01-javascript-and-async-programming.md#js-collections-q07)
- Источники / последняя проверка: `ECMAScript, MDN, engineering analysis | 2026-11-04`

#### Вопрос

Выберите результат и объясните, какой договор использует каждая операция. Один из вызовов может завершиться ошибкой во время выполнения.
```js
const source = { 0: "a", length: 1 };
console.log(Array.from(source));
console.log([...source]);
```

- A. Обе строки выводят `["a"]`.
- B. Первая выводит `["a"]`, вторая выбрасывает `TypeError`.
- C. Первая выбрасывает `TypeError`, вторая выводит `["a"]`.
- D. Первая выводит `[]`, вторая выбрасывает `TypeError`.

### JS-COLLECTIONS-Q08

**Когда ключ переезжает в конец `Map`?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.6. Collections, Symbols & Iteration`
- Уровень: `Mid`
- Тип: `output-prediction`
- Приоритет/частота: `Professional | F2`
- Связанные inventory IDs: `JS-35`
- Статус modern/legacy: `современный JavaScript`
- Ответ: [JS-COLLECTIONS-Q08](../answers/by-domain/01-javascript-and-async-programming.md#js-collections-q08)
- Источники / последняя проверка: `ECMAScript, MDN, engineering analysis | 2026-11-04`

#### Вопрос

Предскажите порядок после каждого изменения.
```js
const map = new Map([["10", 10], ["2", 2]]);
map.set("10", 100);
console.log([...map.keys()]);
map.delete("10");
map.set("10", 10);
console.log([...map.keys()]);
```

### JS-COLLECTIONS-Q09

**Можно ли всегда заменить `Map` на объект перед JSON?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.6. Collections, Symbols & Iteration`
- Уровень: `Mid`
- Тип: `code-review`
- Приоритет/частота: `Professional | F2`
- Связанные inventory IDs: `JS-35`
- Статус modern/legacy: `современный JavaScript`
- Ответ: [JS-COLLECTIONS-Q09](../answers/by-domain/01-javascript-and-async-programming.md#js-collections-q09)
- Источники / последняя проверка: `ECMAScript, MDN, engineering analysis | 2026-11-04`

#### Вопрос

В индексе встречаются ключи `7`, `"7"`, два объекта и символ. Коллега предлагает `JSON.stringify(Object.fromEntries(index))`. Где теряется информация и какой договор предложить?

### JS-COLLECTIONS-Q10

**Как удалить дубликаты по ID и сохранить первое совпадение?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.6. Collections, Symbols & Iteration`
- Уровень: `Mid`
- Тип: `implementation`
- Приоритет/частота: `Professional | F2`
- Связанные inventory IDs: `JS-36`
- Статус modern/legacy: `современный JavaScript`
- Ответ: [JS-COLLECTIONS-Q10](../answers/by-domain/01-javascript-and-async-programming.md#js-collections-q10)
- Источники / последняя проверка: `ECMAScript, MDN, engineering analysis | 2026-11-04`

#### Вопрос

Реализуйте функцию для итерируемых строк с полем `id`. Сохраните входной порядок и исходные объекты. Проверьте повтор ID у разных экземпляров, а также `0` и `"0"`.

### JS-COLLECTIONS-Q11

**Что хранить в `WeakMap`, `WeakSet` и `WeakRef`?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.6. Collections, Symbols & Iteration`
- Уровень: `Mid`
- Тип: `compare`
- Приоритет/частота: `Professional | F2`
- Связанные inventory IDs: `JS-36`
- Статус modern/legacy: `современный JavaScript`
- Ответ: [JS-COLLECTIONS-Q11](../answers/by-domain/01-javascript-and-async-programming.md#js-collections-q11)
- Источники / последняя проверка: `ECMAScript, MDN, engineering analysis | 2026-11-04`

#### Вопрос

Для трёх случаев предложите API: размеры временных объектов, отметка о посещении экземпляра, шанс переиспользовать дорогой объект. Нужна ещё выгрузка всех активных ID. Куда её поместить?

### JS-COLLECTIONS-Q12

**Что делают слабые коллекции с недопустимым ключом?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.6. Collections, Symbols & Iteration`
- Уровень: `Mid`
- Тип: `output-prediction`
- Приоритет/частота: `Professional | F2`
- Связанные inventory IDs: `JS-36`
- Статус modern/legacy: `современное поведение и совместимость`
- Ответ: [JS-COLLECTIONS-Q12](../answers/by-domain/01-javascript-and-async-programming.md#js-collections-q12)
- Источники / последняя проверка: `ECMAScript, MDN, engineering analysis | 2026-11-04`

#### Вопрос

Назовите результат каждого запроса и место исключения. Последняя строка намеренно ошибочна во время выполнения.
```js
const token = Symbol("row");
const registered = Symbol.for("row");
const cache = new WeakMap([[token, 7]]);
console.log(cache.get(token), cache.get(registered), cache.delete(1));
cache.set(registered, 8);
```

### JS-COLLECTIONS-Q13

**Насколько скрыто символьное свойство?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.6. Collections, Symbols & Iteration`
- Уровень: `Mid`
- Тип: `code-review`
- Приоритет/частота: `Professional | F2`
- Связанные inventory IDs: `JS-37`
- Статус modern/legacy: `современный JavaScript`
- Ответ: [JS-COLLECTIONS-Q13](../answers/by-domain/01-javascript-and-async-programming.md#js-collections-q13)
- Источники / последняя проверка: `ECMAScript, MDN, engineering analysis | 2026-11-04`

#### Вопрос

В объекте есть собственное перечисляемое свойство `[marker]`. Оно отсутствует в `Object.keys`. Можно ли считать его приватным? Что увидят `Reflect.ownKeys`, `Object.getOwnPropertySymbols` и `{ ...obj }`?

### JS-COLLECTIONS-Q14

**Почему ключ с правильным названием не запускает обход?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.6. Collections, Symbols & Iteration`
- Уровень: `Mid`
- Тип: `debugging`
- Приоритет/частота: `Professional | F2`
- Связанные inventory IDs: `JS-37`
- Статус modern/legacy: `современный JavaScript`
- Ответ: [JS-COLLECTIONS-Q14](../answers/by-domain/01-javascript-and-async-programming.md#js-collections-q14)
- Источники / последняя проверка: `ECMAScript, MDN, engineering analysis | 2026-11-04`

#### Вопрос

Коллега реализовал метод `[Symbol.for("Symbol.iterator")]`. Внутри метод возвращает рабочий итератор, но `for...of` выбрасывает `TypeError`. Что исправить? Назовите ещё две точки расширения языка.

### JS-COLLECTIONS-Q15

**Как обеспечить два независимых обхода?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.6. Collections, Symbols & Iteration`
- Уровень: `Mid`
- Тип: `implementation`
- Приоритет/частота: `Professional | F2`
- Связанные inventory IDs: `JS-38`
- Статус modern/legacy: `современный JavaScript`
- Ответ: [JS-COLLECTIONS-Q15](../answers/by-domain/01-javascript-and-async-programming.md#js-collections-q15)
- Источники / последняя проверка: `ECMAScript, MDN, engineering analysis | 2026-11-04`

#### Вопрос

Напишите повторно обходимый диапазон `[start, end)` для безопасных целых границ. Запустите два итератора и продвиньте один на два шага, а другой на один. Какой результат нужен?

### JS-COLLECTIONS-Q16

**Что выдаст генератор до и после исчерпания?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.6. Collections, Symbols & Iteration`
- Уровень: `Mid`
- Тип: `output-prediction`
- Приоритет/частота: `Professional | F2`
- Связанные inventory IDs: `JS-38`
- Статус modern/legacy: `современный JavaScript`
- Ответ: [JS-COLLECTIONS-Q16](../answers/by-domain/01-javascript-and-async-programming.md#js-collections-q16)
- Источники / последняя проверка: `ECMAScript, MDN, engineering analysis | 2026-11-04`

#### Вопрос

Предскажите три результата. Где окажется `return "end"`?
```js
function* values() {
  yield undefined;
  yield "item";
  return "end";
}
const cursor = values();
console.log(cursor.next());
console.log([...cursor]);
console.log(cursor.next());
```

### JS-COLLECTIONS-Q17

**Когда начнётся тело генератора и куда уйдёт аргумент `next`?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.6. Collections, Symbols & Iteration`
- Уровень: `Mid`
- Тип: `output-prediction`
- Приоритет/частота: `Professional | F2`
- Связанные inventory IDs: `JS-38`
- Статус modern/legacy: `современный JavaScript`
- Ответ: [JS-COLLECTIONS-Q17](../answers/by-domain/01-javascript-and-async-programming.md#js-collections-q17)
- Источники / последняя проверка: `ECMAScript, MDN, engineering analysis | 2026-11-04`

#### Вопрос

Предскажите порядок записей в журнале.
```js
function* ask(log) {
  log.push("start");
  const answer = yield "prompt";
  log.push(answer);
  return "end";
}
const log = [];
const cursor = ask(log);
log.push("created");
const first = cursor.next("ignored");
const last = cursor.next("yes");
console.log(log, first, last);
```

### JS-COLLECTIONS-Q18

**Когда достаточно `for await...of`, а когда нужен массив?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.6. Collections, Symbols & Iteration`
- Уровень: `Mid`
- Тип: `compare`
- Приоритет/частота: `Professional | F2`
- Связанные inventory IDs: `JS-38`
- Статус modern/legacy: `современный JavaScript`
- Ответ: [JS-COLLECTIONS-Q18](../answers/by-domain/01-javascript-and-async-programming.md#js-collections-q18)
- Источники / последняя проверка: `ECMAScript, MDN, engineering analysis | 2026-11-04`

#### Вопрос

В интерфейсе можно показать первые записи по мере загрузки или дождаться всех перед показом. Сравните `for await...of` и `Array.fromAsync`.

### JS-COLLECTIONS-Q19

**Безопасно ли менять `Map` в процессе обхода?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.6. Collections, Symbols & Iteration`
- Уровень: `Senior`
- Тип: `code-review`
- Приоритет/частота: `Advanced | F2`
- Связанные inventory IDs: `JS-35`
- Статус modern/legacy: `современный JavaScript`
- Ответ: [JS-COLLECTIONS-Q19](../answers/by-domain/01-javascript-and-async-programming.md#js-collections-q19)
- Источники / последняя проверка: `ECMAScript, MDN, engineering analysis | 2026-11-04`

#### Вопрос

Как поведёт себя этот код? Фрагмент намеренно не завершается. Объясните причину и предложите тест с ограничением шагов.
```js
const map = new Map([["a", 1]]);
for (const [key, value] of map) {
  map.delete(key);
  map.set(key, value);
}
```

### JS-COLLECTIONS-Q20

**Как сверить видимые и выбранные ID?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.6. Collections, Symbols & Iteration`
- Уровень: `Senior`
- Тип: `practical-production-scenario`
- Приоритет/частота: `Advanced | F2`
- Связанные inventory IDs: `JS-35`, `JS-36`
- Статус modern/legacy: `современное поведение и совместимость`
- Ответ: [JS-COLLECTIONS-Q20](../answers/by-domain/01-javascript-and-async-programming.md#js-collections-q20)
- Источники / последняя проверка: `ECMAScript, MDN, engineering analysis | 2026-11-04`

#### Вопрос

Есть `Set` выбранных ID и `Map` видимых строк. Выберите операцию, объясните договор правого операнда и предложите вариант для старого рантайма, где важен порядок выбранных ID.

### JS-COLLECTIONS-Q21

**Почему `Map<Id, WeakRef<Row>>` не решает ограничение кеша?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.6. Collections, Symbols & Iteration`
- Уровень: `Senior`
- Тип: `architecture`
- Приоритет/частота: `Advanced | F2`
- Связанные inventory IDs: `JS-36`
- Статус modern/legacy: `современный JavaScript`
- Ответ: [JS-COLLECTIONS-Q21](../answers/by-domain/01-javascript-and-async-programming.md#js-collections-q21)
- Источники / последняя проверка: `ECMAScript, MDN, engineering analysis | 2026-11-04`

#### Вопрос

Требуется максимальный размер индекса и неизменный результат при попадании или промахе. Объясните, что удерживается сильно, как выбрать структуру и что тестировать.

### JS-COLLECTIONS-Q22

**Кто закрывает источник при `break` и ошибке `next()`?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.6. Collections, Symbols & Iteration`
- Уровень: `Senior`
- Тип: `debugging`
- Приоритет/частота: `Advanced | F2`
- Связанные inventory IDs: `JS-38`
- Статус modern/legacy: `современный JavaScript`
- Ответ: [JS-COLLECTIONS-Q22](../answers/by-domain/01-javascript-and-async-programming.md#js-collections-q22)
- Источники / последняя проверка: `ECMAScript, MDN, engineering analysis | 2026-11-04`

#### Вопрос

В итераторе есть `return()` и ресурс. Сравните `break`, исключение в теле цикла, исключение из `next()` и отказ от ручного обхода.

### JS-COLLECTIONS-Q23

**Как обработать префикс большого источника?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.6. Collections, Symbols & Iteration`
- Уровень: `Senior`
- Тип: `performance-diagnosis`
- Приоритет/частота: `Advanced | F2`
- Связанные inventory IDs: `JS-38`
- Статус modern/legacy: `современное поведение и совместимость`
- Ответ: [JS-COLLECTIONS-Q23](../answers/by-domain/01-javascript-and-async-programming.md#js-collections-q23)
- Источники / последняя проверка: `ECMAScript, MDN, engineering analysis | 2026-11-04`

#### Вопрос

Из большой или бесконечной синхронной последовательности нужно взять первые пять совпадений. Предложите современный и переносимый варианты и объясните ограничение ленивости.

### JS-COLLECTIONS-Q24

**Как спроектировать ограниченную асинхронную выдачу?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.6. Collections, Symbols & Iteration`
- Уровень: `Senior`
- Тип: `architecture`
- Приоритет/частота: `Advanced | F2`
- Связанные inventory IDs: `JS-35`, `JS-36`, `JS-37`, `JS-38`
- Статус modern/legacy: `современный JavaScript`
- Ответ: [JS-COLLECTIONS-Q24](../answers/by-domain/01-javascript-and-async-programming.md#js-collections-q24)
- Источники / последняя проверка: `ECMAScript, MDN, engineering analysis | 2026-11-04`

#### Вопрос

Страницы поиска иногда содержат записи с одинаковыми ID, а метаданные измерения принадлежат отдельному экземпляру строки. Нужно взять первые уникальные записи, остановить потребителя по лимиту и объяснить проверку границы. Какие структуры и протоколы выбрать?

## 1.7. Modules, Errors & Serialization

Сначала ответьте по памяти. Код запускайте только после собственного прогноза. Именованные наборы файлов независимы друг от друга.

### JS-MODULES-Q01

**Что принадлежит области модуля?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.7. Modules, Errors & Serialization`
- Уровень: `Junior`
- Тип: `conceptual`
- Приоритет/частота: `Core | F3`
- Связанные inventory IDs: `JS-41`
- Статус modern/legacy: `современный JavaScript`
- Ответ: [JS-MODULES-Q01](../answers/by-domain/01-javascript-and-async-programming.md#js-modules-q01)
- Источники / последняя проверка: `ECMAScript 2026, Node.js, MDN, документация сборщиков; ссылки в главе | 2026-11-05`

#### Вопрос

В ESM объявлены `const secret = 1` и `export const visible = 2`. Что доступно потребителю, появляется ли `visible` в `globalThis` и чему равен верхнеуровневый `this`?

### JS-MODULES-Q02

**Выберите правильный импорт.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.7. Modules, Errors & Serialization`
- Уровень: `Junior`
- Тип: `multiple-choice | output-prediction`
- Приоритет/частота: `Core | F3`
- Связанные inventory IDs: `JS-41`
- Статус modern/legacy: `современный JavaScript`
- Ответ: [JS-MODULES-Q02](../answers/by-domain/01-javascript-and-async-programming.md#js-modules-q02)
- Источники / последняя проверка: `ECMAScript 2026, Node.js, MDN, документация сборщиков; ссылки в главе | 2026-11-05`

#### Вопрос

Набор `q02`, Node.js, точка входа `main.mjs`:
```js
// file: api.mjs
export default (n) => n * 2;
export const limit = 3;
```
```js
// file: main.mjs
import * as api from "./api.mjs";
console.log(api.default(api.limit));
```
Выберите результат: A — `6`; B — `TypeError`, потому что default не входит в `*`; C — `api` является функцией; D — `limit` станет глобальным.

### JS-MODULES-Q03

**Почему значение видно до строки import?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.7. Modules, Errors & Serialization`
- Уровень: `Junior`
- Тип: `why | explain`
- Приоритет/частота: `Core | F2`
- Связанные inventory IDs: `JS-41`, `JS-42`
- Статус modern/legacy: `современный JavaScript`
- Ответ: [JS-MODULES-Q03](../answers/by-domain/01-javascript-and-async-programming.md#js-modules-q03)
- Источники / последняя проверка: `ECMAScript 2026, Node.js, MDN, документация сборщиков; ссылки в главе | 2026-11-05`

#### Вопрос

В ациклическом графе без TLA зависимость печатает `"dep"`, потребитель сначала пишет `console.log("main")`, а ниже содержит статический импорт зависимости. Назовите порядок и объясните три этапа обработки модуля.

### JS-MODULES-Q04

**Что меняется через живую привязку?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.7. Modules, Errors & Serialization`
- Уровень: `Junior`
- Тип: `conceptual | compare`
- Приоритет/частота: `Core | F2`
- Связанные inventory IDs: `JS-42`
- Статус modern/legacy: `современный JavaScript`
- Ответ: [JS-MODULES-Q04](../answers/by-domain/01-javascript-and-async-programming.md#js-modules-q04)
- Источники / последняя проверка: `ECMAScript 2026, Node.js, MDN, документация сборщиков; ссылки в главе | 2026-11-05`

#### Вопрос

Источник экспортирует `let count = 0` и функцию, увеличивающую его. Потребитель импортирует `count` и сохраняет `const saved = count`. Что покажут оба имени после вызова функции? Может ли потребитель присвоить `count = 10`?

### JS-MODULES-Q05

**Куда распространяется исключение?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.7. Modules, Errors & Serialization`
- Уровень: `Junior`
- Тип: `output-prediction`
- Приоритет/частота: `Core | F3`
- Связанные inventory IDs: `JS-43`
- Статус modern/legacy: `современный JavaScript`
- Ответ: [JS-MODULES-Q05](../answers/by-domain/01-javascript-and-async-programming.md#js-modules-q05)
- Источники / последняя проверка: `ECMAScript 2026, Node.js, MDN, документация сборщиков; ссылки в главе | 2026-11-05`

#### Вопрос

Самостоятельный `.mjs`:
```js
const log = [];
function run() { log.push("run"); throw new Error("bad"); }
try { run(); log.push("after"); }
catch (error) { log.push(error.message); }
finally { log.push("close"); }
console.log(log);
```
Назовите результат и роль каждого блока.

### JS-MODULES-Q06

**Равны ли корректный JSON и корректные настройки?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.7. Modules, Errors & Serialization`
- Уровень: `Junior`
- Тип: `compare`
- Приоритет/частота: `Core | F2`
- Связанные inventory IDs: `JS-44`
- Статус modern/legacy: `современный JavaScript`
- Ответ: [JS-MODULES-Q06](../answers/by-domain/01-javascript-and-async-programming.md#js-modules-q06)
- Источники / последняя проверка: `ECMAScript 2026, Node.js, MDN, документация сборщиков; ссылки в главе | 2026-11-05`

#### Вопрос

Какие из строк `"null"`, `"42"`, `"[]"`, `"{\"theme\":\"dark\"}"` являются корректным JSON? Доказывает ли успешный разбор договор `{ version: 1, theme: "light" | "dark" }`?

### JS-MODULES-Q07

**Что теряется при сериализации?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.7. Modules, Errors & Serialization`
- Уровень: `Junior`
- Тип: `output-prediction`
- Приоритет/частота: `Core | F2`
- Связанные inventory IDs: `JS-44`
- Статус modern/legacy: `современный JavaScript`
- Ответ: [JS-MODULES-Q07](../answers/by-domain/01-javascript-and-async-programming.md#js-modules-q07)
- Источники / последняя проверка: `ECMAScript 2026, Node.js, MDN, документация сборщиков; ссылки в главе | 2026-11-05`

#### Вопрос

Самостоятельный `.mjs`:
```js
console.log(JSON.stringify({ a: undefined, b: NaN, c: [undefined, , 2] }));
console.log(JSON.stringify(undefined));
```
Сначала назовите тип каждого результата.

### JS-MODULES-Q08

**Почему два default ведут себя по-разному?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.7. Modules, Errors & Serialization`
- Уровень: `Mid`
- Тип: `output-prediction`
- Приоритет/частота: `Professional | F2`
- Связанные inventory IDs: `JS-42`
- Статус modern/legacy: `современный JavaScript`
- Ответ: [JS-MODULES-Q08](../answers/by-domain/01-javascript-and-async-programming.md#js-modules-q08)
- Источники / последняя проверка: `ECMAScript 2026, Node.js, MDN, документация сборщиков; ссылки в главе | 2026-11-05`

#### Вопрос

Набор `q08`, Node.js, `node main.mjs`:
```js
// file: source.mjs
let n = 1;
export default n;
export { n as current };
n = 4;
```
```js
// file: main.mjs
import initial, { current } from "./source.mjs";
console.log(initial, current);
```
Что изменится при замене `export default n` на `export { n as default }`?

### JS-MODULES-Q09

**Найдите причину падения цикла.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.7. Modules, Errors & Serialization`
- Уровень: `Mid`
- Тип: `debugging`
- Приоритет/частота: `Professional | F2`
- Связанные inventory IDs: `JS-42`
- Статус modern/legacy: `современный JavaScript`
- Ответ: [JS-MODULES-Q09](../answers/by-domain/01-javascript-and-async-programming.md#js-modules-q09)
- Источники / последняя проверка: `ECMAScript 2026, Node.js, MDN, документация сборщиков; ссылки в главе | 2026-11-05`

#### Вопрос

В наборе `cycle-bad` главы `a.mjs` импортирует `b`, затем инициализирует `a = 1`. В `b.mjs` верхнеуровневое `export const b = a + 1`. Объясните ошибку при запуске `a.mjs` и предложите два изменения с разным архитектурным эффектом.

### JS-MODULES-Q10

**Каков договор import()?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.7. Modules, Errors & Serialization`
- Уровень: `Mid`
- Тип: `API-design | explain`
- Приоритет/частота: `Professional | F2`
- Связанные inventory IDs: `JS-42`
- Статус modern/legacy: `современный JavaScript`
- Ответ: [JS-MODULES-Q10](../answers/by-domain/01-javascript-and-async-programming.md#js-modules-q10)
- Источники / последняя проверка: `ECMAScript 2026, Node.js, MDN, документация сборщиков; ссылки в главе | 2026-11-05`

#### Вопрос

Условно загрузите форматтер по одному из двух заранее известных имён. Что получит вызывающий код, где обработать ошибку загрузки и гарантирует ли язык отдельный файл сборки?

### JS-MODULES-Q11

**TLA останавливает весь процесс?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.7. Modules, Errors & Serialization`
- Уровень: `Mid`
- Тип: `conceptual | compare`
- Приоритет/частота: `Professional | F2`
- Связанные inventory IDs: `JS-42`
- Статус modern/legacy: `современный JavaScript`
- Ответ: [JS-MODULES-Q11](../answers/by-domain/01-javascript-and-async-programming.md#js-modules-q11)
- Источники / последняя проверка: `ECMAScript 2026, Node.js, MDN, документация сборщиков; ссылки в главе | 2026-11-05`

#### Вопрос

Модуль конфигурации экспортирует результат `await load()`. Что ждут его статические потребители, что будет при отклонении и почему функция `loadConfig()` иногда удобнее?

### JS-MODULES-Q12

**Почему CommonJS вернул старый объект?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.7. Modules, Errors & Serialization`
- Уровень: `Mid`
- Тип: `debugging | legacy`
- Приоритет/частота: `Professional | F3`
- Связанные inventory IDs: `JS-41`
- Статус modern/legacy: `🧓 Legacy / совместимость CommonJS`
- Ответ: [JS-MODULES-Q12](../answers/by-domain/01-javascript-and-async-programming.md#js-modules-q12)
- Источники / последняя проверка: `ECMAScript 2026, Node.js, MDN, документация сборщиков; ссылки в главе | 2026-11-05`

#### Вопрос

Набор `q12`, Node.js, `node main.cjs`:
```js
// file: api.cjs
exports.ready = false;
exports = { ready: true };
```
```js
// file: main.cjs
console.log(require("./api.cjs").ready);
```
Объясните и исправьте именно замену экспорта.

### JS-MODULES-Q13

**Почему именованный CJS-импорт не обновился?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.7. Modules, Errors & Serialization`
- Уровень: `Mid`
- Тип: `output-prediction | interoperability`
- Приоритет/частота: `Professional | F2`
- Связанные inventory IDs: `JS-41`, `JS-42`
- Статус modern/legacy: `🧓 Legacy / совместимость CommonJS`
- Ответ: [JS-MODULES-Q13](../answers/by-domain/01-javascript-and-async-programming.md#js-modules-q13)
- Источники / последняя проверка: `ECMAScript 2026, Node.js, MDN, документация сборщиков; ссылки в главе | 2026-11-05`

#### Вопрос

В наборе `interop` главы после `api.increment()` `api.count` равен `1`, а импортированное `{ count }` равно `0`. Почему? Можно ли рассчитывать на именованные импорты любого CommonJS-пакета?

### JS-MODULES-Q14

**Как finally заменяет результат?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.7. Modules, Errors & Serialization`
- Уровень: `Mid`
- Тип: `multiple-choice | output-prediction`
- Приоритет/частота: `Professional | F3`
- Связанные inventory IDs: `JS-43`
- Статус modern/legacy: `современный JavaScript`
- Ответ: [JS-MODULES-Q14](../answers/by-domain/01-javascript-and-async-programming.md#js-modules-q14)
- Источники / последняя проверка: `ECMAScript 2026, Node.js, MDN, документация сборщиков; ссылки в главе | 2026-11-05`

#### Вопрос

Самостоятельный `.mjs`:
```js
function result() {
  try { throw new Error("failed"); }
  catch (error) { throw error; }
  finally { return 7; }
}
console.log(result());
```
A — выброс исходной ошибки; B — `7`; C — `undefined`; D — `SyntaxError`. Что изменить для сохранения ошибки?

### JS-MODULES-Q15

**Как сохранить цепочку ошибок?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.7. Modules, Errors & Serialization`
- Уровень: `Mid`
- Тип: `implementation | debugging`
- Приоритет/частота: `Professional | F3`
- Связанные inventory IDs: `JS-43`
- Статус modern/legacy: `современный JavaScript`
- Ответ: [JS-MODULES-Q15](../answers/by-domain/01-javascript-and-async-programming.md#js-modules-q15)
- Источники / последняя проверка: `ECMAScript 2026, Node.js, MDN, документация сборщиков; ссылки в главе | 2026-11-05`

#### Вопрос

На границе импорта код делает `throw new Error(error.message)`. Что теряется? Покажите договор пользовательской ошибки с устойчивым кодом и причиной. Когда достаточно `throw error`?

### JS-MODULES-Q16

**Что увидит replacer после toJSON?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.7. Modules, Errors & Serialization`
- Уровень: `Mid`
- Тип: `output-prediction`
- Приоритет/частота: `Professional | F2`
- Связанные inventory IDs: `JS-44`
- Статус modern/legacy: `современный JavaScript`
- Ответ: [JS-MODULES-Q16](../answers/by-domain/01-javascript-and-async-programming.md#js-modules-q16)
- Источники / последняя проверка: `ECMAScript 2026, Node.js, MDN, документация сборщиков; ссылки в главе | 2026-11-05`

#### Вопрос

Самостоятельный `.mjs`:
```js
const seen = [];
const text = JSON.stringify({ when: new Date("2026-01-01T00:00:00.000Z") },
  (key, value) => { if (key === "when") seen.push(typeof value); return value; });
console.log(seen, text);
```
Сработал бы здесь `value instanceof Date` для поля `when`?

### JS-MODULES-Q17

**Как reviver может удалить весь результат?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.7. Modules, Errors & Serialization`
- Уровень: `Mid`
- Тип: `debugging | output-prediction`
- Приоритет/частота: `Professional | F2`
- Связанные inventory IDs: `JS-44`
- Статус modern/legacy: `современный JavaScript`
- Ответ: [JS-MODULES-Q17](../answers/by-domain/01-javascript-and-async-programming.md#js-modules-q17)
- Источники / последняя проверка: `ECMAScript 2026, Node.js, MDN, документация сборщиков; ссылки в главе | 2026-11-05`

#### Вопрос

Самостоятельный `.mjs`:
```js
const result = JSON.parse('{"n":2}', (key, value) => {
  if (key === "n") return value * 2;
});
console.log(result);
```
Каков порядок посещений и что исправить?

### JS-MODULES-Q18

**Поймает ли catch возвращённое отклонение?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.7. Modules, Errors & Serialization`
- Уровень: `Mid`
- Тип: `debugging`
- Приоритет/частота: `Professional | F3`
- Связанные inventory IDs: `JS-43`
- Статус modern/legacy: `современный JavaScript`
- Ответ: [JS-MODULES-Q18](../answers/by-domain/01-javascript-and-async-programming.md#js-modules-q18)
- Источники / последняя проверка: `ECMAScript 2026, Node.js, MDN, документация сборщиков; ссылки в главе | 2026-11-05`

#### Вопрос

Сравните `try { return fail(); } catch (...) { ... }` и `try { return await fail(); } catch (...) { ... }` внутри `async function`, если `fail()` возвращает отклонённое обещание. Как не оставить отказ без наблюдения?

### JS-MODULES-Q19

**Проведите ревью dual package.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.7. Modules, Errors & Serialization`
- Уровень: `Senior`
- Тип: `code-review | API-design`
- Приоритет/частота: `Advanced | F3`
- Связанные inventory IDs: `JS-41`
- Статус modern/legacy: `🧓 Legacy / совместимость CommonJS`
- Ответ: [JS-MODULES-Q19](../answers/by-domain/01-javascript-and-async-programming.md#js-modules-q19)
- Источники / последняя проверка: `ECMAScript 2026, Node.js, MDN, документация сборщиков; ссылки в главе | 2026-11-05`

#### Вопрос

У пакета `exports.import` и `exports.require` указывают на независимые реализации, каждая создаёт `cache` и `class Item`. Оба пути используются в одном процессе. Какие отказы возможны, как воспроизвести их и какие варианты договора предложить?

### JS-MODULES-Q20

**Как ответить на require(esm) без устаревшего правила?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.7. Modules, Errors & Serialization`
- Уровень: `Senior`
- Тип: `interoperability | version-analysis`
- Приоритет/частота: `Advanced | F2`
- Связанные inventory IDs: `JS-41`, `JS-42`
- Статус modern/legacy: `🧓 Legacy / совместимость CommonJS`
- Ответ: [JS-MODULES-Q20](../answers/by-domain/01-javascript-and-async-programming.md#js-modules-q20)
- Источники / последняя проверка: `ECMAScript 2026, Node.js, MDN, документация сборщиков; ссылки в главе | 2026-11-05`

#### Вопрос

Сопоставьте Node.js 20.18.2, 22.13.1, 24.21.0 и 26.4.0 без флагов. У первой ESM-зависимости только `export const n = 1`, у второй TLA находится на два импорта глубже. Что проверять перед предложением решения?

### JS-MODULES-Q21

**Почему сборка сломалась после sideEffects: false?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.7. Modules, Errors & Serialization`
- Уровень: `Senior`
- Тип: `code-review | performance-reasoning`
- Приоритет/частота: `Advanced | F2`
- Связанные inventory IDs: `JS-42`
- Статус modern/legacy: `современный JavaScript`
- Ответ: [JS-MODULES-Q21](../answers/by-domain/01-javascript-and-async-programming.md#js-modules-q21)
- Источники / последняя проверка: `ECMAScript 2026, Node.js, MDN, документация сборщиков; ссылки в главе | 2026-11-05`

#### Вопрос

Библиотека экспортирует функции и при загрузке регистрирует расширение. После уменьшения сборки регистрация исчезла. Объясните роль статических импортов, `usedExports` и `sideEffects`. Какой минимальный эксперимент подтвердит вывод?

### JS-MODULES-Q22

**Как передать точный большой ID?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.7. Modules, Errors & Serialization`
- Уровень: `Senior`
- Тип: `API-design | output-prediction`
- Приоритет/частота: `Advanced | F2`
- Связанные inventory IDs: `JS-44`
- Статус modern/legacy: `современный JavaScript`
- Ответ: [JS-MODULES-Q22](../answers/by-domain/01-javascript-and-async-programming.md#js-modules-q22)
- Источники / последняя проверка: `ECMAScript 2026, Node.js, MDN, документация сборщиков; ссылки в главе | 2026-11-05`

#### Вопрос

Сервис присылает большой целый ID числом JSON за пределами безопасного диапазона `Number`. Поможет ли `BigInt(value)` в обычном `reviver`? Какие два договора возможны и как проверить совместимость?

### JS-MODULES-Q23

**Можно ли отличить синтаксис от ошибки преобразования?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.7. Modules, Errors & Serialization`
- Уровень: `Senior`
- Тип: `debugging | reliability`
- Приоритет/частота: `Advanced | F2`
- Связанные inventory IDs: `JS-43`, `JS-44`
- Статус modern/legacy: `современный JavaScript`
- Ответ: [JS-MODULES-Q23](../answers/by-domain/01-javascript-and-async-programming.md#js-modules-q23)
- Источники / последняя проверка: `ECMAScript 2026, Node.js, MDN, документация сборщиков; ссылки в главе | 2026-11-05`

#### Вопрос

Один `try` окружает `JSON.parse(text, reviver)` и проверку схемы. Любой `SyntaxError` показывается как «неверный JSON», любой другой отказ заменяется `{}`. Что в таком договоре двусмысленно и как его изменить?

### JS-MODULES-Q24

**Спроектируйте границу импорта настроек.**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.7. Modules, Errors & Serialization`
- Уровень: `Senior`
- Тип: `design | interview-communication`
- Приоритет/частота: `Advanced | F2`
- Связанные inventory IDs: `JS-41`, `JS-42`, `JS-43`, `JS-44`
- Статус modern/legacy: `современный JavaScript`
- Ответ: [JS-MODULES-Q24](../answers/by-domain/01-javascript-and-async-programming.md#js-modules-q24)
- Источники / последняя проверка: `ECMAScript 2026, Node.js, MDN, документация сборщиков; ссылки в главе | 2026-11-05`

#### Вопрос

За три минуты опишите модульный API импорта версии настроек из текста. Требуются ESM и CJS-потребитель, явный DTO, различение синтаксиса и схемы, сохранение причин, тесты ошибок и безопасная стратегия для TLA. Глубокую настройку сборки не обсуждайте.

## 1.8. Memory Management

Сначала ответьте по памяти. Для кода сформулируйте прогноз до запуска; ответы и критерии находятся отдельно.

### JS-MEMORY-Q01

**Кто освобождает память?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.8. Memory Management`
- Уровень: `Junior`
- Тип: `conceptual`
- Приоритет/частота: `Core | F2`
- Связанные inventory IDs: `JS-45`
- Статус modern/legacy: `современная практика; legacy и обзорные границы отмечены в главе`
- Ответ: [JS-MEMORY-Q01](../answers/by-domain/01-javascript-and-async-programming.md#js-memory-q01)
- Источники / последняя проверка: `ECMAScript 2026, DOM/HTML/File API, Chrome DevTools; ссылки в главе | 2026-11-06`

#### Вопрос

Опишите путь от создания объекта до возможного освобождения. Почему завершение функции не означает, что возвращённый ею объект уже не занимает память?

### JS-MEMORY-Q02

**Что убрало присваивание null?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.8. Memory Management`
- Уровень: `Junior`
- Тип: `output-prediction`
- Приоритет/частота: `Core | F2`
- Связанные inventory IDs: `JS-45`
- Статус modern/legacy: `современная практика; legacy и обзорные границы отмечены в главе`
- Ответ: [JS-MEMORY-Q02](../answers/by-domain/01-javascript-and-async-programming.md#js-memory-q02)
- Источники / последняя проверка: `ECMAScript 2026, DOM/HTML/File API, Chrome DevTools; ссылки в главе | 2026-11-06`

#### Вопрос

Предскажите вывод и нарисуйте оставшийся путь. Код переносим; каждый блок этого раздела независим.
```js
let model = { rows: [1, 2] };
const saved = [model];
model = null;
console.log(saved[0].rows.length);
```
Может ли этот вывод сказать, когда произойдёт GC?

### JS-MEMORY-Q03

**Всегда ли опасен цикл?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.8. Memory Management`
- Уровень: `Junior`
- Тип: `conceptual | why`
- Приоритет/частота: `Core | F2`
- Связанные inventory IDs: `JS-45`
- Статус modern/legacy: `современная практика; legacy и обзорные границы отмечены в главе`
- Ответ: [JS-MEMORY-Q03](../answers/by-domain/01-javascript-and-async-programming.md#js-memory-q03)
- Источники / последняя проверка: `ECMAScript 2026, DOM/HTML/File API, Chrome DevTools; ссылки в главе | 2026-11-06`

#### Вопрос

Два объекта ссылаются друг на друга. Все внешние пути к ним удалены. Выберите точную формулировку: A — цикл обязан остаться навсегда; B — оба уже освобождены; C — граф может быть собран, момент не обещан; D — сначала необходимо вручную удалить каждое внутреннее свойство. Объясните остальные варианты.

### JS-MEMORY-Q04

**Почему обработчик не снялся?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.8. Memory Management`
- Уровень: `Junior`
- Тип: `API | debugging`
- Приоритет/частота: `Core | F2`
- Связанные inventory IDs: `JS-45`
- Статус modern/legacy: `современная практика; legacy и обзорные границы отмечены в главе`
- Ответ: [JS-MEMORY-Q04](../answers/by-domain/01-javascript-and-async-programming.md#js-memory-q04)
- Источники / последняя проверка: `ECMAScript 2026, DOM/HTML/File API, Chrome DevTools; ссылки в главе | 2026-11-06`

#### Вопрос

Браузер. Назовите вывод и покажите ошибку жизненного цикла. Исправьте её без перехода к библиотеке.
```js
const target = new EventTarget();
let calls = 0;
const handler = () => { calls += 1; };
target.addEventListener("tick", handler);
target.removeEventListener("tick", () => { calls += 1; });
target.dispatchEvent(new Event("tick"));
console.log(calls);
```

### JS-MEMORY-Q05

**Конец вызова и жизнь замыкания**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.8. Memory Management`
- Уровень: `Junior`
- Тип: `explain | conceptual`
- Приоритет/частота: `Core | F2`
- Связанные inventory IDs: `JS-45`
- Статус modern/legacy: `современная практика; legacy и обзорные границы отмечены в главе`
- Ответ: [JS-MEMORY-Q05](../answers/by-domain/01-javascript-and-async-programming.md#js-memory-q05)
- Источники / последняя проверка: `ECMAScript 2026, DOM/HTML/File API, Chrome DevTools; ссылки в главе | 2026-11-06`

#### Вопрос

Фабрика возвращает функцию, читающую `report.rows`. Отчёт больше нигде намеренно не сохраняется. Почему после завершения фабрики он может оставаться доступным? Является ли это автоматически утечкой?

### JS-MEMORY-Q06

**Кому принадлежит blob URL?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.8. Memory Management`
- Уровень: `Junior`
- Тип: `API | scenario`
- Приоритет/частота: `Core | F2`
- Связанные inventory IDs: `JS-45`
- Статус modern/legacy: `современная практика; legacy и обзорные границы отмечены в главе`
- Ответ: [JS-MEMORY-Q06](../answers/by-domain/01-javascript-and-async-programming.md#js-memory-q06)
- Источники / последняя проверка: `ECMAScript 2026, DOM/HTML/File API, Chrome DevTools; ссылки в главе | 2026-11-06`

#### Вопрос

Предпросмотр создаёт адрес через `URL.createObjectURL(file)`. Затем локальная строка удаляется, а картинка остаётся на экране. Какие обязанности у владельца адреса при замене и закрытии? Можно ли всегда отзывать адрес сразу после присваивания `src`?

### JS-MEMORY-Q07

**Обнуление и удаление записи**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.8. Memory Management`
- Уровень: `Mid`
- Тип: `output-prediction | explain`
- Приоритет/частота: `Professional | F2`
- Связанные inventory IDs: `JS-45`
- Статус modern/legacy: `современная практика; legacy и обзорные границы отмечены в главе`
- Ответ: [JS-MEMORY-Q07](../answers/by-domain/01-javascript-and-async-programming.md#js-memory-q07)
- Источники / последняя проверка: `ECMAScript 2026, DOM/HTML/File API, Chrome DevTools; ссылки в главе | 2026-11-06`

#### Вопрос

Назовите оба результата. Какие связи изменились и какого вывода о памяти делать нельзя?
```js
let value = { id: 4 };
const holder = { value };
const index = new Map([["x", value]]);
value = null;
delete holder.value;
console.log(index.get("x").id);
index.delete("x");
console.log(index.size);
```

### JS-MEMORY-Q08

**Почему remove не завершил панель?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.8. Memory Management`
- Уровень: `Mid`
- Тип: `debugging | scenario`
- Приоритет/частота: `Professional | F2`
- Связанные inventory IDs: `JS-45`
- Статус modern/legacy: `современная практика; legacy и обзорные границы отмечены в главе`
- Ответ: [JS-MEMORY-Q08](../answers/by-domain/01-javascript-and-async-programming.md#js-memory-q08)
- Источники / последняя проверка: `ECMAScript 2026, DOM/HTML/File API, Chrome DevTools; ссылки в главе | 2026-11-06`

#### Вопрос

Панель зарегистрировала обработчик `resize` в `window`. Обработчик читает корневой узел панели. Закрытие вызывает только `panel.remove()`. Нарисуйте путь после закрытия, предложите очистку и объясните, почему обработчик на самом недостижимом узле — другой случай.

### JS-MEMORY-Q09

**Хватит ли once или abort?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.8. Memory Management`
- Уровень: `Mid`
- Тип: `API | trade-off`
- Приоритет/частота: `Professional | F2`
- Связанные inventory IDs: `JS-45`
- Статус modern/legacy: `современная практика; legacy и обзорные границы отмечены в главе`
- Ответ: [JS-MEMORY-Q09](../answers/by-domain/01-javascript-and-async-programming.md#js-memory-q09)
- Источники / последняя проверка: `ECMAScript 2026, DOM/HTML/File API, Chrome DevTools; ссылки в главе | 2026-11-06`

#### Вопрос

Редкое событие слушают с `{ once: true }`, но панель может закрыться раньше него. Достаточно ли этого для завершения? Что даёт `AbortController`, какие ресурсы он сам по себе не завершит?

### JS-MEMORY-Q10

**Что обязана сделать остановка таймера?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.8. Memory Management`
- Уровень: `Mid`
- Тип: `review | reliability`
- Приоритет/частота: `Professional | F2`
- Связанные inventory IDs: `JS-45`
- Статус modern/legacy: `современная практика; legacy и обзорные границы отмечены в главе`
- Ответ: [JS-MEMORY-Q10](../answers/by-domain/01-javascript-and-async-programming.md#js-memory-q10)
- Источники / последняя проверка: `ECMAScript 2026, DOM/HTML/File API, Chrome DevTools; ссылки в главе | 2026-11-06`

#### Вопрос

Интервал запускает чтение большого состояния. При закрытии разработчик обнуляет переменную с ID таймера. Что осталось в среде? Какие свойства должны быть у функции остановки, в том числе если её сохранят после вызова?

### JS-MEMORY-Q11

**Проверьте договор подписки**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.8. Memory Management`
- Уровень: `Mid`
- Тип: `coding | review`
- Приоритет/частота: `Professional | F2`
- Связанные inventory IDs: `JS-45`
- Статус modern/legacy: `современная практика; legacy и обзорные границы отмечены в главе`
- Ответ: [JS-MEMORY-Q11](../answers/by-domain/01-javascript-and-async-programming.md#js-memory-q11)
- Источники / последняя проверка: `ECMAScript 2026, DOM/HTML/File API, Chrome DevTools; ссылки в главе | 2026-11-06`

#### Вопрос

Источник хранит обработчики в `Set` и возвращает `unsubscribe()`. Предложите проверки для двух независимых подписчиков, повторной отписки и повторных циклов создания/закрытия. Почему ноль обработчиков ещё не доказывает освобождение всех данных процесса?

### JS-MEMORY-Q12

**Ограничен ли этот кеш?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.8. Memory Management`
- Уровень: `Mid`
- Тип: `review | performance`
- Приоритет/частота: `Professional | F2`
- Связанные inventory IDs: `JS-45`
- Статус modern/legacy: `современная практика; legacy и обзорные границы отмечены в главе`
- Ответ: [JS-MEMORY-Q12](../answers/by-domain/01-javascript-and-async-programming.md#js-memory-q12)
- Источники / последняя проверка: `ECMAScript 2026, DOM/HTML/File API, Chrome DevTools; ссылки в главе | 2026-11-06`

#### Вопрос

У кеша есть TTL, но просроченная запись удаляется только при чтении именно её ключа. Новые ключи добавляются постоянно, старые больше не читают. Есть ли ограничение удержания? Предложите политику и назовите её цену.

### JS-MEMORY-Q13

**Пик, прогрев или утечка?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.8. Memory Management`
- Уровень: `Mid`
- Тип: `scenario | performance`
- Приоритет/частота: `Professional | F2`
- Связанные inventory IDs: `JS-45`
- Статус modern/legacy: `современная практика; legacy и обзорные границы отмечены в главе`
- Ответ: [JS-MEMORY-Q13](../answers/by-domain/01-javascript-and-async-programming.md#js-memory-q13)
- Источники / последняя проверка: `ECMAScript 2026, DOM/HTML/File API, Chrome DevTools; ссылки в главе | 2026-11-06`

#### Вопрос

Классифицируйте гипотезы: A — во время импорта файла живут исходник и две копии; B — кеш после первого открытия стабилизировался на допустимом бюджете; C — после каждого закрытия остаётся новая панель в массиве истории; D — объектов после работы столько же, но GC часто прерывает работу. Какие измерения нужны?

### JS-MEMORY-Q14

**Маленькая функция и большой граф**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.8. Memory Management`
- Уровень: `Mid`
- Тип: `conceptual | debugging`
- Приоритет/частота: `Professional | F2`
- Связанные inventory IDs: `JS-45`
- Статус modern/legacy: `современная практика; legacy и обзорные границы отмечены в главе`
- Ответ: [JS-MEMORY-Q14](../answers/by-domain/01-javascript-and-async-programming.md#js-memory-q14)
- Источники / последняя проверка: `ECMAScript 2026, DOM/HTML/File API, Chrome DevTools; ссылки в главе | 2026-11-06`

#### Вопрос

В снимке функция имеет небольшой собственный размер и большой удерживаемый. Что означает разница? Можно ли обещать освобождение всех её вложенных данных, если удалить один внешний путь к функции?

### JS-MEMORY-Q15

**Что именно должен доказать тест?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.8. Memory Management`
- Уровень: `Mid`
- Тип: `testing | reliability`
- Приоритет/частота: `Professional | F2`
- Связанные inventory IDs: `JS-45`
- Статус modern/legacy: `современная практика; legacy и обзорные границы отмечены в главе`
- Ответ: [JS-MEMORY-Q15](../answers/by-domain/01-javascript-and-async-programming.md#js-memory-q15)
- Источники / последняя проверка: `ECMAScript 2026, DOM/HTML/File API, Chrome DevTools; ссылки в главе | 2026-11-06`

#### Вопрос

Разработчик предлагает тест: закрыть панель, подождать секунду, потребовать вызов `FinalizationRegistry` и падение памяти на 5 МБ. Какие утверждения в нём ненадёжны и какой договор можно проверить вместо них?

### JS-MEMORY-Q16

**Когда выбирать WeakMap?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.8. Memory Management`
- Уровень: `Senior`
- Тип: `trade-off | architecture`
- Приоритет/частота: `Advanced | F2`
- Связанные inventory IDs: `JS-45`
- Статус modern/legacy: `современная практика; legacy и обзорные границы отмечены в главе`
- Ответ: [JS-MEMORY-Q16](../answers/by-domain/01-javascript-and-async-programming.md#js-memory-q16)
- Источники / последняя проверка: `ECMAScript 2026, DOM/HTML/File API, Chrome DevTools; ссылки в главе | 2026-11-06`

#### Вопрос

Сравните: метаданные DOM-элемента, кеш результатов по строковому URL и обязательное закрытие подписки. Где уместна слабая связь? Почему `WeakRef` и финализатор не являются универсальной починкой?

### JS-MEMORY-Q17

**Постройте эксперимент до и после**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.8. Memory Management`
- Уровень: `Senior`
- Тип: `debugging | performance`
- Приоритет/частота: `Advanced | F2`
- Связанные inventory IDs: `JS-45`
- Статус modern/legacy: `современная практика; legacy и обзорные границы отмечены в главе`
- Ответ: [JS-MEMORY-Q17](../answers/by-domain/01-javascript-and-async-programming.md#js-memory-q17)
- Источники / последняя проверка: `ECMAScript 2026, DOM/HTML/File API, Chrome DevTools; ссылки в главе | 2026-11-06`

#### Вопрос

После двадцати открытий и закрытий окна вкладка стала тяжёлой. За три минуты опишите минимальный эксперимент со снимками: исходное состояние, действия, подозреваемый класс, путь, исправление, повтор. Учтите влияние консоли и единичную утечку.

### JS-MEMORY-Q18

**Создание упало посередине**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.8. Memory Management`
- Уровень: `Senior`
- Тип: `reliability | design`
- Приоритет/частота: `Advanced | F2`
- Связанные inventory IDs: `JS-45`
- Статус modern/legacy: `современная практика; legacy и обзорные границы отмечены в главе`
- Ответ: [JS-MEMORY-Q18](../answers/by-domain/01-javascript-and-async-programming.md#js-memory-q18)
- Источники / последняя проверка: `ECMAScript 2026, DOM/HTML/File API, Chrome DevTools; ссылки в главе | 2026-11-06`

#### Вопрос

Панель уже создала URL, добавила обработчик и таймер. Затем `subscribe()` выбросил исключение. До возвращения `dispose()` дело не дошло. Кто завершает ресурсы и как проверить, что очистка не затронула другую панель?

### JS-MEMORY-Q19

**Почему сохранённый dispose всё ещё опасен?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.8. Memory Management`
- Уровень: `Senior`
- Тип: `review | explain`
- Приоритет/частота: `Advanced | F2`
- Связанные inventory IDs: `JS-45`
- Статус modern/legacy: `современная практика; legacy и обзорные границы отмечены в главе`
- Ответ: [JS-MEMORY-Q19](../answers/by-domain/01-javascript-and-async-programming.md#js-memory-q19)
- Источники / последняя проверка: `ECMAScript 2026, DOM/HTML/File API, Chrome DevTools; ссылки в главе | 2026-11-06`

#### Вопрос

Менеджер хранит функции `dispose()` в массиве даже после их вызова. Одна из них сняла обработчики, но всё ещё замыкает DOM-узел. Какие два уровня исправления возможны? Нужно ли обнулять вообще все локальные переменные?

### JS-MEMORY-Q20

**Объясните план расследования и исправления**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.8. Memory Management`
- Уровень: `Senior`
- Тип: `interview-communication | design`
- Приоритет/частота: `Advanced | F2`
- Связанные inventory IDs: `JS-45`
- Статус modern/legacy: `современная практика; legacy и обзорные границы отмечены в главе`
- Ответ: [JS-MEMORY-Q20](../answers/by-domain/01-javascript-and-async-programming.md#js-memory-q20)
- Источники / последняя проверка: `ECMAScript 2026, DOM/HTML/File API, Chrome DevTools; ссылки в главе | 2026-11-06`

#### Вопрос

За 60 секунд объясните коллеге, почему GC не спасает от всех утечек. Затем предложите критерии готовности исправления для панели с кешем, таймером, подпиской и предпросмотром. Разделите доказанные свойства и ограничения измерений.

## 1.9. Event Loop & Scheduling

Сначала определите среду и сделайте прогноз. Каждый блок независим; если не отмечено иначе, простой код с таймерами и микрозадачами переносим между браузером и Node.js. Ответы находятся отдельно.

### JS-LOOP-Q01

**Где граница языка и среды?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.9. Event Loop & Scheduling`
- Уровень: `Junior`
- Тип: `conceptual`
- Приоритет/частота: `Core | F3`
- Связанные inventory IDs: `JS-46`
- Статус modern/legacy: `современная практика; границы сред и исторические политики отмечены в главе`
- Ответ: [JS-LOOP-Q01](../answers/by-domain/01-javascript-and-async-programming.md#js-loop-q01)
- Источники / последняя проверка: `ECMAScript 2026, HTML Standard, MDN, Node.js; ссылки в главе | 2026-11-06`

#### Вопрос

Назовите обязанности движка JavaScript и браузера при загрузке данных и вызове обработчика. Как сетевой результат попадает в JavaScript и почему «один поток» не описывает весь браузер?

### JS-LOOP-Q02

**Вложенный вызов или новая задача?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.9. Event Loop & Scheduling`
- Уровень: `Junior`
- Тип: `output-prediction`
- Приоритет/частота: `Core | F3`
- Связанные inventory IDs: `JS-46`
- Статус modern/legacy: `современная практика; границы сред и исторические политики отмечены в главе`
- Ответ: [JS-LOOP-Q02](../answers/by-domain/01-javascript-and-async-programming.md#js-loop-q02)
- Источники / последняя проверка: `ECMAScript 2026, HTML Standard, MDN, Node.js; ссылки в главе | 2026-11-06`

#### Вопрос

Переносимый блок. Назовите порядок и объясните состояние стека.
```js
console.log("one");
function run() {
  console.log("two");
  (() => console.log("three"))();
  console.log("four");
}
run();
console.log("five");
```

### JS-LOOP-Q03

**Что означает нулевая задержка?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.9. Event Loop & Scheduling`
- Уровень: `Junior`
- Тип: `multiple-choice | explain`
- Приоритет/частота: `Core | F3`
- Связанные inventory IDs: `JS-46`, `JS-49`
- Статус modern/legacy: `современная практика; границы сред и исторические политики отмечены в главе`
- Ответ: [JS-LOOP-Q03](../answers/by-domain/01-javascript-and-async-programming.md#js-loop-q03)
- Источники / последняя проверка: `ECMAScript 2026, HTML Standard, MDN, Node.js; ссылки в главе | 2026-11-06`

#### Вопрос

Выберите точное объяснение `setTimeout(fn, 0)`: A — прерывает текущую функцию; B — регистрирует будущий вызов с порогом допуска; C — гарантирует ровно четыре миллисекунды; D — создаёт новый поток выполнения `fn`. Объясните каждый неверный вариант.

### JS-LOOP-Q04

**Что такое контрольная точка?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.9. Event Loop & Scheduling`
- Уровень: `Junior`
- Тип: `conceptual`
- Приоритет/частота: `Core | F3`
- Связанные inventory IDs: `JS-47`
- Статус modern/legacy: `современная практика; границы сред и исторические политики отмечены в главе`
- Ответ: [JS-LOOP-Q04](../answers/by-domain/01-javascript-and-async-programming.md#js-loop-q04)
- Источники / последняя проверка: `ECMAScript 2026, HTML Standard, MDN, Node.js; ссылки в главе | 2026-11-06`

#### Вопрос

Объясните микрозадачу и контрольную точку. Приведите два источника микрозадач в браузере. Что произойдёт, если выполняемая микрозадача добавит следующую?

### JS-LOOP-Q05

**Какая часть Promise синхронна?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.9. Event Loop & Scheduling`
- Уровень: `Junior`
- Тип: `output-prediction`
- Приоритет/частота: `Core | F3`
- Связанные inventory IDs: `JS-48`
- Статус modern/legacy: `современная практика; границы сред и исторические политики отмечены в главе`
- Ответ: [JS-LOOP-Q05](../answers/by-domain/01-javascript-and-async-programming.md#js-loop-q05)
- Источники / последняя проверка: `ECMAScript 2026, HTML Standard, MDN, Node.js; ссылки в главе | 2026-11-06`

#### Вопрос

Переносимый блок. Предскажите журнал без запуска.
```js
const log = [];
new Promise(resolve => { log.push("inside"); resolve(); })
  .then(() => log.push("then"));
log.push("outside");
setTimeout(() => console.log(log), 0);
```

### JS-LOOP-Q06

**У какого API постоянный приоритет?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.9. Event Loop & Scheduling`
- Уровень: `Junior`
- Тип: `output-prediction`
- Приоритет/частота: `Core | F3`
- Связанные inventory IDs: `JS-47`, `JS-48`
- Статус modern/legacy: `современная практика; границы сред и исторические политики отмечены в главе`
- Ответ: [JS-LOOP-Q06](../answers/by-domain/01-javascript-and-async-programming.md#js-loop-q06)
- Источники / последняя проверка: `ECMAScript 2026, HTML Standard, MDN, Node.js; ссылки в главе | 2026-11-06`

#### Вопрос

Назовите результат. Затем объясните, изменится ли он при перестановке первых двух регистраций.
```js
const log = [];
queueMicrotask(() => log.push("q"));
Promise.resolve().then(() => log.push("p"));
setTimeout(() => console.log(log), 0);
```

### JS-LOOP-Q07

**Куда встанет вложенная микрозадача?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.9. Event Loop & Scheduling`
- Уровень: `Mid`
- Тип: `output-prediction`
- Приоритет/частота: `Professional | F3`
- Связанные inventory IDs: `JS-47`, `JS-48`
- Статус modern/legacy: `современная практика; границы сред и исторические политики отмечены в главе`
- Ответ: [JS-LOOP-Q07](../answers/by-domain/01-javascript-and-async-programming.md#js-loop-q07)
- Источники / последняя проверка: `ECMAScript 2026, HTML Standard, MDN, Node.js; ссылки в главе | 2026-11-06`

#### Вопрос

Предскажите массив и восстановите очередь после каждого шага.
```js
const log = [];
Promise.resolve().then(() => {
  log.push("first");
  queueMicrotask(() => log.push("last"));
});
queueMicrotask(() => log.push("middle"));
setTimeout(() => console.log(log), 0);
```

### JS-LOOP-Q08

**Все таймеры раньше микрозадач?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.9. Event Loop & Scheduling`
- Уровень: `Mid`
- Тип: `output-prediction`
- Приоритет/частота: `Professional | F3`
- Связанные inventory IDs: `JS-47`, `JS-48`
- Статус modern/legacy: `современная практика; границы сред и исторические политики отмечены в главе`
- Ответ: [JS-LOOP-Q08](../answers/by-domain/01-javascript-and-async-programming.md#js-loop-q08)
- Источники / последняя проверка: `ECMAScript 2026, HTML Standard, MDN, Node.js; ссылки в главе | 2026-11-06`

#### Вопрос

Браузер, один скрипт. Предскажите результат и объясните границу между обработчиками.
```js
const log = [];
setTimeout(() => {
  log.push("a");
  Promise.resolve().then(() => log.push("reaction"));
}, 0);
setTimeout(() => { log.push("b"); console.log(log); }, 0);
```

### JS-LOOP-Q09

**Когда реакция становится готовой?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.9. Event Loop & Scheduling`
- Уровень: `Mid`
- Тип: `output-prediction`
- Приоритет/частота: `Professional | F3`
- Связанные inventory IDs: `JS-48`
- Статус modern/legacy: `современная практика; границы сред и исторические политики отмечены в главе`
- Ответ: [JS-LOOP-Q09](../answers/by-domain/01-javascript-and-async-programming.md#js-loop-q09)
- Источники / последняя проверка: `ECMAScript 2026, HTML Standard, MDN, Node.js; ссылки в главе | 2026-11-06`

#### Вопрос

Покажите, в какой момент появляется каждая микрозадача.
```js
const log = ["sync"];
let release;
const pending = new Promise(resolve => { release = resolve; });
pending.then(() => log.push("reaction"));
setTimeout(() => { log.push("timer"); release(); }, 0);
queueMicrotask(() => log.push("queued"));
setTimeout(() => console.log(log), 0);
```

### JS-LOOP-Q10

**Почему отправка события не отложилась?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.9. Event Loop & Scheduling`
- Уровень: `Mid`
- Тип: `debugging | explain`
- Приоритет/частота: `Professional | F3`
- Связанные inventory IDs: `JS-46`, `JS-47`
- Статус modern/legacy: `современная практика; границы сред и исторические политики отмечены в главе`
- Ответ: [JS-LOOP-Q10](../answers/by-domain/01-javascript-and-async-programming.md#js-loop-q10)
- Источники / последняя проверка: `ECMAScript 2026, HTML Standard, MDN, Node.js; ссылки в главе | 2026-11-06`

#### Вопрос

Браузерный `dispatchEvent()` вызывается из обычной функции, а обработчик ставит микрозадачу. Коллега ожидает, что сначала функция целиком завершится и только потом начнётся обработчик. Что неверно? Можно ли этот эксперимент автоматически переносить на все реальные события пользователя?

### JS-LOOP-Q11

**Почему рекурсия без роста стека всё равно опасна?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.9. Event Loop & Scheduling`
- Уровень: `Mid`
- Тип: `why | performance`
- Приоритет/частота: `Professional | F3`
- Связанные inventory IDs: `JS-47`
- Статус modern/legacy: `современная практика; границы сред и исторические политики отмечены в главе`
- Ответ: [JS-LOOP-Q11](../answers/by-domain/01-javascript-and-async-programming.md#js-loop-q11)
- Источники / последняя проверка: `ECMAScript 2026, HTML Standard, MDN, Node.js; ссылки в главе | 2026-11-06`

#### Вопрос

Каждая микрозадача ставит следующую и возвращается. Почему стек не обязан расти, но страница может зависнуть? Как безопасно продемонстрировать проблему?

### JS-LOOP-Q12

**Передаёт ли await готового Promise время интерфейсу?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.9. Event Loop & Scheduling`
- Уровень: `Mid`
- Тип: `debugging | review`
- Приоритет/частота: `Professional | F3`
- Связанные inventory IDs: `JS-47`
- Статус modern/legacy: `современная практика; границы сред и исторические политики отмечены в главе`
- Ответ: [JS-LOOP-Q12](../answers/by-domain/01-javascript-and-async-programming.md#js-loop-q12)
- Источники / последняя проверка: `ECMAScript 2026, HTML Standard, MDN, Node.js; ссылки в главе | 2026-11-06`

#### Вопрос

В тяжёлом цикле после каждого элемента добавили `await Promise.resolve()`. Код стал асинхронным, но интерфейс всё ещё плохо отвечает. Объясните причину и предложите подход внутри scope этой главы.

### JS-LOOP-Q13

**Кто победит между источниками задач?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.9. Event Loop & Scheduling`
- Уровень: `Mid`
- Тип: `trade-off | explain`
- Приоритет/частота: `Professional | F3`
- Связанные inventory IDs: `JS-47`
- Статус modern/legacy: `современная практика; границы сред и исторические политики отмечены в главе`
- Ответ: [JS-LOOP-Q13](../answers/by-domain/01-javascript-and-async-programming.md#js-loop-q13)
- Источники / последняя проверка: `ECMAScript 2026, HTML Standard, MDN, Node.js; ссылки в главе | 2026-11-06`

#### Вопрос

Сеть, таймер и пользовательский ввод готовы примерно одновременно. Почему нельзя вывести общий порядок только из слов «они в очереди»? Что можно честно указать вместо полного порядка?

### JS-LOOP-Q14

**К чему относится минимум 4 мс?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.9. Event Loop & Scheduling`
- Уровень: `Mid`
- Тип: `API | conceptual`
- Приоритет/частота: `Professional | F2`
- Связанные inventory IDs: `JS-49`
- Статус modern/legacy: `современная практика; границы сред и исторические политики отмечены в главе`
- Ответ: [JS-LOOP-Q14](../answers/by-domain/01-javascript-and-async-programming.md#js-loop-q14)
- Источники / последняя проверка: `ECMAScript 2026, HTML Standard, MDN, Node.js; ссылки в главе | 2026-11-06`

#### Вопрос

Назовите точное условие HTML для вложенных таймеров с малой задержкой. Относится ли оно только к вложенности текста `setTimeout` и гарантирует ли период ровно 4 мс?

### JS-LOOP-Q15

**Можно ли обещать частоту фоновой вкладки?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.9. Event Loop & Scheduling`
- Уровень: `Senior`
- Тип: `review | reliability`
- Приоритет/частота: `Advanced | F2`
- Связанные inventory IDs: `JS-49`
- Статус modern/legacy: `современная практика; границы сред и исторические политики отмечены в главе`
- Ответ: [JS-LOOP-Q15](../answers/by-domain/01-javascript-and-async-programming.md#js-loop-q15)
- Источники / последняя проверка: `ECMAScript 2026, HTML Standard, MDN, Node.js; ссылки в главе | 2026-11-06`

#### Вопрос

В спецификации продукта написано: «скрытая вкладка каждую секунду выполняет интервал; rAF идёт 60 раз в секунду». В качестве доказательства приведена статья Chrome 88 с порогами ограничения. Проведите ревью и предложите договор восстановления.

### JS-LOOP-Q16

**Сколько осталось времени?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.9. Event Loop & Scheduling`
- Уровень: `Mid`
- Тип: `output-prediction | debugging`
- Приоритет/частота: `Professional | F2`
- Связанные inventory IDs: `JS-49`
- Статус modern/legacy: `современная практика; границы сред и исторические политики отмечены в главе`
- Ответ: [JS-LOOP-Q16](../answers/by-domain/01-javascript-and-async-programming.md#js-loop-q16)
- Источники / последняя проверка: `ECMAScript 2026, HTML Standard, MDN, Node.js; ссылки в главе | 2026-11-06`

#### Вопрос

Все входы — отметки одних часов, миллисекунды. Назовите результаты; объясните, почему опоздавший вызов не требует вычитать количество пропущенных тиков.
```js
const remaining = (deadline, now) => Math.max(0, Math.ceil((deadline - now) / 1000));
console.log(remaining(6000, 1000), remaining(6000, 4500), remaining(6000, 7000));
```

### JS-LOOP-Q17

**Может ли готовый таймер разорвать цикл?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.9. Event Loop & Scheduling`
- Уровень: `Junior`
- Тип: `conceptual | output-prediction`
- Приоритет/частота: `Core | F3`
- Связанные inventory IDs: `JS-46`, `JS-49`
- Статус modern/legacy: `современная практика; границы сред и исторические политики отмечены в главе`
- Ответ: [JS-LOOP-Q17](../answers/by-domain/01-javascript-and-async-programming.md#js-loop-q17)
- Источники / последняя проверка: `ECMAScript 2026, HTML Standard, MDN, Node.js; ссылки в главе | 2026-11-06`

#### Вопрос

Перед длинным обычным синхронным циклом поставлен нулевой таймер. Его порог наступил посередине цикла. Может ли обработчик выполниться между двумя инструкциями этого цикла? Изменится ли ответ, если уменьшить задержку ещё сильнее?

### JS-LOOP-Q18

**Что именно запрашивает rAF?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.9. Event Loop & Scheduling`
- Уровень: `Mid`
- Тип: `API | compare`
- Приоритет/частота: `Professional | F3`
- Связанные inventory IDs: `JS-47`
- Статус modern/legacy: `современная практика; границы сред и исторические политики отмечены в главе`
- Ответ: [JS-LOOP-Q18](../answers/by-domain/01-javascript-and-async-programming.md#js-loop-q18)
- Источники / последняя проверка: `ECMAScript 2026, HTML Standard, MDN, Node.js; ссылки в главе | 2026-11-06`

#### Вопрос

Сравните `requestAnimationFrame`, `queueMicrotask` и `setTimeout`: цель, однократность, связь с отображением и отмена. Почему rAF не означает «после paint»?

### JS-LOOP-Q19

**Влияет ли частота экрана на скорость?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.9. Event Loop & Scheduling`
- Уровень: `Mid`
- Тип: `output-prediction | performance`
- Приоритет/частота: `Professional | F3`
- Связанные inventory IDs: `JS-47`
- Статус modern/legacy: `современная практика; границы сред и исторические политики отмечены в главе`
- Ответ: [JS-LOOP-Q19](../answers/by-domain/01-javascript-and-async-programming.md#js-loop-q19)
- Источники / последняя проверка: `ECMAScript 2026, HTML Standard, MDN, Node.js; ссылки в главе | 2026-11-06`

#### Вопрос

Положение считается от первого кадра с отметкой `100` мс. Назовите результат и объясните, почему дополнительные кадры между этими отметками не меняют формулу.
```js
const position = now => 80 * (now - 100) / 1000;
console.log(position(100), position(600), position(1100));
```

### JS-LOOP-Q20

**Один ожидающий кадр и последнее значение**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.9. Event Loop & Scheduling`
- Уровень: `Senior`
- Тип: `review | design`
- Приоритет/частота: `Advanced | F3`
- Связанные inventory IDs: `JS-47`
- Статус modern/legacy: `современная практика; границы сред и исторические политики отмечены в главе`
- Ответ: [JS-LOOP-Q20](../answers/by-domain/01-javascript-and-async-programming.md#js-loop-q20)
- Источники / последняя проверка: `ECMAScript 2026, HTML Standard, MDN, Node.js; ссылки в главе | 2026-11-06`

#### Вопрос

Обновления состояния приходят много раз до следующего кадра. Предложите объект управления с `update(value)` и `dispose()`, который хранит последнее значение и не более одного rAF. Что делать с ID перед применением значения и с обновлением изнутри самого обработчика?

### JS-LOOP-Q21

**Что доказывает чтение DOM?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.9. Event Loop & Scheduling`
- Уровень: `Senior`
- Тип: `conceptual | debugging`
- Приоритет/частота: `Advanced | F3`
- Связанные inventory IDs: `JS-47`
- Статус modern/legacy: `современная практика; границы сред и исторические политики отмечены в главе`
- Ответ: [JS-LOOP-Q21](../answers/by-domain/01-javascript-and-async-programming.md#js-loop-q21)
- Источники / последняя проверка: `ECMAScript 2026, HTML Standard, MDN, Node.js; ссылки в главе | 2026-11-06`

#### Вопрос

Код изменил `textContent`, прочитал геометрию, дождался rAF и решил, что пользователь точно увидел промежуточную надпись. Какие части утверждения следуют из кода, а какие нет?

### JS-LOOP-Q22

**Как проверить планирование без хрупких миллисекунд?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.9. Event Loop & Scheduling`
- Уровень: `Senior`
- Тип: `testing | performance`
- Приоритет/частота: `Advanced | F3`
- Связанные inventory IDs: `JS-47`, `JS-49`
- Статус modern/legacy: `современная практика; границы сред и исторические политики отмечены в главе`
- Ответ: [JS-LOOP-Q22](../answers/by-domain/01-javascript-and-async-programming.md#js-loop-q22)
- Источники / последняя проверка: `ECMAScript 2026, HTML Standard, MDN, Node.js; ссылки в главе | 2026-11-06`

#### Вопрос

Разработайте проверки для порядка микрозадач, отмены таймера, расчёта остатка времени и анимации. Отделите чистую формулу, управляемые часы, реальные браузерные API и неподтверждённое ограничение фона.

### JS-LOOP-Q23

**Чем ограничен перенос в Node.js?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.9. Event Loop & Scheduling`
- Уровень: `Senior`
- Тип: `trade-off | compatibility`
- Приоритет/частота: `Advanced | F3`
- Связанные inventory IDs: `JS-46`, `JS-47`
- Статус modern/legacy: `современная практика; границы сред и исторические политики отмечены в главе`
- Ответ: [JS-LOOP-Q23](../answers/by-domain/01-javascript-and-async-programming.md#js-loop-q23)
- Источники / последняя проверка: `ECMAScript 2026, HTML Standard, MDN, Node.js; ссылки в главе | 2026-11-06`

#### Вопрос

В браузерную схему добавили `process.nextTick` и `setImmediate`, сохранили фиксированный порядок, а затем вывели рекомендацию для всех сред. Какие уточнения необходимы и какой глубины достаточно для этого раздела?

### JS-LOOP-Q24

**Объясните зависший индикатор**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.9. Event Loop & Scheduling`
- Уровень: `Senior`
- Тип: `interview-communication | design`
- Приоритет/частота: `Advanced | F3`
- Связанные inventory IDs: `JS-46`, `JS-47`, `JS-48`, `JS-49`
- Статус modern/legacy: `современная практика; границы сред и исторические политики отмечены в главе`
- Ответ: [JS-LOOP-Q24](../answers/by-domain/01-javascript-and-async-programming.md#js-loop-q24)
- Источники / последняя проверка: `ECMAScript 2026, HTML Standard, MDN, Node.js; ссылки в главе | 2026-11-06`

#### Вопрос

За минуту объясните, почему надпись «Загрузка» не появилась перед обработкой большого массива. Предложите план с порциями работы, объединёнными визуальными обновлениями и отменой. Какие гарантии вы можете и не можете дать?

## 1.10. Promises & `async`/`await`

Сначала рассуждайте по памяти. Блоки независимы; переносимые примеры с await запускайте отдельными модулями. Ответы и критерии оценки находятся отдельно.

### JS-PROMISE-Q01

**Состояние, решение и завершение**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.10. Promises & async/await`
- Уровень: `Junior`
- Тип: `conceptual`
- Приоритет/частота: `Core | F3`
- Связанные inventory IDs: `JS-50`
- Статус modern/legacy: `современный стандарт; границы среды и совместимость отмечены в главе`
- Ответ: [JS-PROMISE-Q01](../answers/by-domain/01-javascript-and-async-programming.md#js-promise-q01)
- Источники / последняя проверка: `ECMAScript 2026, DOM/Fetch/HTML Standard, MDN, Node.js; ссылки в главе | 2026-11-06`

#### Вопрос

Назовите три состояния Promise. Чем отличаются settled, fulfilled и resolved? Может ли уже resolved-обещание ещё ожидать результат?

### JS-PROMISE-Q02

**Что победит после resolve другого Promise?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.10. Promises & async/await`
- Уровень: `Junior`
- Тип: `output-prediction`
- Приоритет/частота: `Core | F3`
- Связанные inventory IDs: `JS-50`
- Статус modern/legacy: `современный стандарт; границы среды и совместимость отмечены в главе`
- Ответ: [JS-PROMISE-Q02](../answers/by-domain/01-javascript-and-async-programming.md#js-promise-q02)
- Источники / последняя проверка: `ECMAScript 2026, DOM/Fetch/HTML Standard, MDN, Node.js; ссылки в главе | 2026-11-06`

#### Вопрос

Переносимый блок, запуск отдельным модулем. Предскажите результат и объясните, когда решение зафиксировано.
```js
let finish;
const later = new Promise(resolve => { finish = resolve; });
const outer = new Promise((resolve, reject) => {
  resolve(later);
  reject("late rejection");
});
finish("ready");
console.log(await outer);
```

### JS-PROMISE-Q03

**Продолжится ли исполнитель после resolve?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.10. Promises & async/await`
- Уровень: `Junior`
- Тип: `output-prediction`
- Приоритет/частота: `Core | F3`
- Связанные inventory IDs: `JS-50`
- Статус modern/legacy: `современный стандарт; границы среды и совместимость отмечены в главе`
- Ответ: [JS-PROMISE-Q03](../answers/by-domain/01-javascript-and-async-programming.md#js-promise-q03)
- Источники / последняя проверка: `ECMAScript 2026, DOM/Fetch/HTML Standard, MDN, Node.js; ссылки в главе | 2026-11-06`

#### Вопрос

Назовите журнал. Объясните роль return и синхронного исключения в исполнителе.
```js
const log = [];
const p = new Promise(resolve => {
  log.push("inside"); resolve(3); log.push("after"); return 99;
});
log.push("outside");
log.push(await p);
console.log(log);
```

### JS-PROMISE-Q04

**Новая цепочка и принятие результата**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.10. Promises & async/await`
- Уровень: `Junior`
- Тип: `output-prediction`
- Приоритет/частота: `Core | F3`
- Связанные inventory IDs: `JS-50`
- Статус modern/legacy: `современный стандарт; границы среды и совместимость отмечены в главе`
- Ответ: [JS-PROMISE-Q04](../answers/by-domain/01-javascript-and-async-programming.md#js-promise-q04)
- Источники / последняя проверка: `ECMAScript 2026, DOM/Fetch/HTML Standard, MDN, Node.js; ссылки в главе | 2026-11-06`

#### Вопрос

Предскажите оба вывода.
```js
const p = Promise.resolve(2);
const q = p.then(value => Promise.resolve(value + 4));
console.log(p === q);
console.log(await q);
```

### JS-PROMISE-Q05

**Почему потерянный return опасен?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.10. Promises & async/await`
- Уровень: `Junior`
- Тип: `why | debugging`
- Приоритет/частота: `Core | F3`
- Связанные inventory IDs: `JS-50`, `JS-51`
- Статус modern/legacy: `современный стандарт; границы среды и совместимость отмечены в главе`
- Ответ: [JS-PROMISE-Q05](../answers/by-domain/01-javascript-and-async-programming.md#js-promise-q05)
- Источники / последняя проверка: `ECMAScript 2026, DOM/Fetch/HTML Standard, MDN, Node.js; ссылки в главе | 2026-11-06`

#### Вопрос

Обработчик then вызывает обещающий load(), но не возвращает его и ничего не ожидает. Что получит следующее звено? Кто заметит внутренний отказ? Что меняет добавление void перед load()?

### JS-PROMISE-Q06

**Что обещает async-функция?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.10. Promises & async/await`
- Уровень: `Junior`
- Тип: `conceptual | compare`
- Приоритет/частота: `Core | F3`
- Связанные inventory IDs: `JS-53`
- Статус modern/legacy: `современный стандарт; границы среды и совместимость отмечены в главе`
- Ответ: [JS-PROMISE-Q06](../answers/by-domain/01-javascript-and-async-programming.md#js-promise-q06)
- Источники / последняя проверка: `ECMAScript 2026, DOM/Fetch/HTML Standard, MDN, Node.js; ссылки в главе | 2026-11-06`

#### Вопрос

Что возвращает async-функция при return 7, при throw и при return уже существующего Promise? Когда начинается тело и создаёт ли async отдельный поток?

### JS-PROMISE-Q07

**Ожидает ли await массив обещаний?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.10. Promises & async/await`
- Уровень: `Junior`
- Тип: `output-prediction`
- Приоритет/частота: `Core | F3`
- Связанные inventory IDs: `JS-53`
- Статус modern/legacy: `современный стандарт; границы среды и совместимость отмечены в главе`
- Ответ: [JS-PROMISE-Q07](../answers/by-domain/01-javascript-and-async-programming.md#js-promise-q07)
- Источники / последняя проверка: `ECMAScript 2026, DOM/Fetch/HTML Standard, MDN, Node.js; ссылки в главе | 2026-11-06`

#### Вопрос

Назовите результаты. Чем map отличается от forEach с async-функцией?
```js
const list = [2, 3].map(async n => n * 2);
console.log((await list) === list);
console.log(await Promise.all(list));
```

### JS-PROMISE-Q08

**Выберите договор комбинатора**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.10. Promises & async/await`
- Уровень: `Junior`
- Тип: `API | compare`
- Приоритет/частота: `Core | F3`
- Связанные inventory IDs: `JS-52`
- Статус modern/legacy: `современный стандарт; границы среды и совместимость отмечены в главе`
- Ответ: [JS-PROMISE-Q08](../answers/by-domain/01-javascript-and-async-programming.md#js-promise-q08)
- Источники / последняя проверка: `ECMAScript 2026, DOM/Fetch/HTML Standard, MDN, Node.js; ссылки в главе | 2026-11-06`

#### Вопрос

Какой метод нужен для всех обязательных успехов, полного отчёта, первого окончательного исхода и первого успеха? Кто запускает фабрики и отменяет проигравших?

### JS-PROMISE-Q09

**Что синхронно у чужого then?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.10. Promises & async/await`
- Уровень: `Mid`
- Тип: `output-prediction`
- Приоритет/частота: `Professional | F3`
- Связанные inventory IDs: `JS-50`
- Статус modern/legacy: `современный стандарт; границы среды и совместимость отмечены в главе`
- Ответ: [JS-PROMISE-Q09](../answers/by-domain/01-javascript-and-async-programming.md#js-promise-q09)
- Источники / последняя проверка: `ECMAScript 2026, DOM/Fetch/HTML Standard, MDN, Node.js; ссылки в главе | 2026-11-06`

#### Вопрос

Предскажите журнал и объясните чтение свойства отдельно от вызова метода.
```js
const log = [];
const x = { get then() {
  log.push("get");
  return resolve => { log.push("call"); resolve(8); };
}};
const p = Promise.resolve(x);
log.push("next");
console.log(await p, log);
```

### JS-PROMISE-Q10

**Можно ли вернуть новое обещание в него самого?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.10. Promises & async/await`
- Уровень: `Mid`
- Тип: `output-prediction`
- Приоритет/частота: `Professional | F3`
- Связанные inventory IDs: `JS-50`
- Статус modern/legacy: `современный стандарт; границы среды и совместимость отмечены в главе`
- Ответ: [JS-PROMISE-Q10](../answers/by-domain/01-javascript-and-async-programming.md#js-promise-q10)
- Источники / последняя проверка: `ECMAScript 2026, DOM/Fetch/HTML Standard, MDN, Node.js; ссылки в главе | 2026-11-06`

#### Вопрос

Назовите результат и объясните отличие от обычного возврата другого Promise.
```js
const p = Promise.resolve(1);
let next;
next = p.then(() => next);
console.log(await next.catch(error => error.name));
```

### JS-PROMISE-Q11

**Кого защищает catch исходного обещания?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.10. Promises & async/await`
- Уровень: `Mid`
- Тип: `review | reliability`
- Приоритет/частота: `Professional | F3`
- Связанные inventory IDs: `JS-51`
- Статус modern/legacy: `современный стандарт; границы среды и совместимость отмечены в главе`
- Ответ: [JS-PROMISE-Q11](../answers/by-domain/01-javascript-and-async-programming.md#js-promise-q11)
- Источники / последняя проверка: `ECMAScript 2026, DOM/Fetch/HTML Standard, MDN, Node.js; ссылки в главе | 2026-11-06`

#### Вопрос

От p создана ветвь q через then, и в её обработчике выбрасывается ошибка. К p уже присоединён catch. Достаточно ли этого? Как проверить владение отказом без падения основного тестового процесса?

### JS-PROMISE-Q12

**Восстановление успеха после catch**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.10. Promises & async/await`
- Уровень: `Mid`
- Тип: `output-prediction`
- Приоритет/частота: `Professional | F3`
- Связанные inventory IDs: `JS-51`
- Статус modern/legacy: `современный стандарт; границы среды и совместимость отмечены в главе`
- Ответ: [JS-PROMISE-Q12](../answers/by-domain/01-javascript-and-async-programming.md#js-promise-q12)
- Источники / последняя проверка: `ECMAScript 2026, DOM/Fetch/HTML Standard, MDN, Node.js; ссылки в главе | 2026-11-06`

#### Вопрос

Предскажите вывод и назовите момент изменения исхода.
```js
const value = await Promise.reject("missing")
  .catch(() => 5)
  .then(n => n * 2);
console.log(value);
```

### JS-PROMISE-Q13

**Ловит ли второй аргумент then ошибку первого?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.10. Promises & async/await`
- Уровень: `Mid`
- Тип: `output-prediction`
- Приоритет/частота: `Professional | F3`
- Связанные inventory IDs: `JS-51`
- Статус modern/legacy: `современный стандарт; границы среды и совместимость отмечены в главе`
- Ответ: [JS-PROMISE-Q13](../answers/by-domain/01-javascript-and-async-programming.md#js-promise-q13)
- Источники / последняя проверка: `ECMAScript 2026, DOM/Fetch/HTML Standard, MDN, Node.js; ссылки в главе | 2026-11-06`

#### Вопрос

Назовите журнал.
```js
const log = [];
await Promise.resolve()
  .then(() => { throw new Error("work"); }, () => log.push("neighbor"))
  .catch(error => log.push(error.message));
console.log(log);
```

### JS-PROMISE-Q14

**Сохранит ли finally прежний исход?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.10. Promises & async/await`
- Уровень: `Mid`
- Тип: `output-prediction`
- Приоритет/частота: `Professional | F3`
- Связанные inventory IDs: `JS-51`
- Статус modern/legacy: `современный стандарт; границы среды и совместимость отмечены в главе`
- Ответ: [JS-PROMISE-Q14](../answers/by-domain/01-javascript-and-async-programming.md#js-promise-q14)
- Источники / последняя проверка: `ECMAScript 2026, DOM/Fetch/HTML Standard, MDN, Node.js; ссылки в главе | 2026-11-06`

#### Вопрос

Предскажите оба результата. Получает ли обработчик finally исходное значение аргументом?
```js
console.log(await Promise.resolve(4).finally(() => 90));
console.log(await Promise.reject("old")
  .finally(() => Promise.reject("new"))
  .catch(value => value));
```

### JS-PROMISE-Q15

**Нужно ли вернуть очистку?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.10. Promises & async/await`
- Уровень: `Mid`
- Тип: `scenario | review`
- Приоритет/частота: `Professional | F3`
- Связанные inventory IDs: `JS-51`
- Статус modern/legacy: `современный стандарт; границы среды и совместимость отмечены в главе`
- Ответ: [JS-PROMISE-Q15](../answers/by-domain/01-javascript-and-async-programming.md#js-promise-q15)
- Источники / последняя проверка: `ECMAScript 2026, DOM/Fetch/HTML Standard, MDN, Node.js; ссылки в главе | 2026-11-06`

#### Вопрос

Очистка close() возвращает Promise. Сравните finally(() => close()) и finally(() => { close(); }). Когда операция считается законченной и где может потеряться отказ?

### JS-PROMISE-Q16

**Всегда ли return await избыточен?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.10. Promises & async/await`
- Уровень: `Mid`
- Тип: `output-prediction`
- Приоритет/частота: `Professional | F3`
- Связанные inventory IDs: `JS-51`, `JS-53`
- Статус modern/legacy: `современный стандарт; границы среды и совместимость отмечены в главе`
- Ответ: [JS-PROMISE-Q16](../answers/by-domain/01-javascript-and-async-programming.md#js-promise-q16)
- Источники / последняя проверка: `ECMAScript 2026, DOM/Fetch/HTML Standard, MDN, Node.js; ссылки в главе | 2026-11-06`

#### Вопрос

Предскажите два результата.
```js
async function a() {
  try { return Promise.reject("outside"); } catch { return "caught"; }
}
async function b() {
  try { return await Promise.reject("inside"); } catch { return "caught"; }
}
console.log(await a().catch(x => x), await b());
```

### JS-PROMISE-Q17

**Где возник лишний каскад?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.10. Promises & async/await`
- Уровень: `Mid`
- Тип: `review | performance`
- Приоритет/частота: `Professional | F3`
- Связанные inventory IDs: `JS-53`
- Статус modern/legacy: `современный стандарт; границы среды и совместимость отмечены в главе`
- Ответ: [JS-PROMISE-Q17](../answers/by-domain/01-javascript-and-async-programming.md#js-promise-q17)
- Источники / последняя проверка: `ECMAScript 2026, DOM/Fetch/HTML Standard, MDN, Node.js; ссылки в главе | 2026-11-06`

#### Вопрос

Код сначала делает await getProfile(), затем await getSettings(), хотя настройки не зависят от профиля. Предложите исправление. Почему заранее запустить settings и присоединить к нему await только после долгого profile тоже бывает недостаточно?

### JS-PROMISE-Q18

**Почему синхронная фабрика сорвала подготовку набора?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.10. Promises & async/await`
- Уровень: `Mid`
- Тип: `debugging | API`
- Приоритет/частота: `Professional | F3`
- Связанные inventory IDs: `JS-50`, `JS-52`
- Статус modern/legacy: `современный стандарт; границы среды и совместимость отмечены в главе`
- Ответ: [JS-PROMISE-Q18](../answers/by-domain/01-javascript-and-async-programming.md#js-promise-q18)
- Источники / последняя проверка: `ECMAScript 2026, DOM/Fetch/HTML Standard, MDN, Node.js; ссылки в главе | 2026-11-06`

#### Вопрос

Фабрики вызывают в jobs.map(job => job()) перед Promise.all. Одна бросила синхронно. Какие последующие фабрики могут не стартовать? Когда полезен Promise.resolve().then(job), и что он меняет?

### JS-PROMISE-Q19

**В каком порядке будут результаты all?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.10. Promises & async/await`
- Уровень: `Mid`
- Тип: `output-prediction`
- Приоритет/частота: `Professional | F3`
- Связанные inventory IDs: `JS-52`
- Статус modern/legacy: `современный стандарт; границы среды и совместимость отмечены в главе`
- Ответ: [JS-PROMISE-Q19](../answers/by-domain/01-javascript-and-async-programming.md#js-promise-q19)
- Источники / последняя проверка: `ECMAScript 2026, DOM/Fetch/HTML Standard, MDN, Node.js; ссылки в главе | 2026-11-06`

#### Вопрос

Назовите результат независимо от порядка явного завершения.
```js
let a, b;
const first = new Promise(resolve => { a = resolve; });
const second = new Promise(resolve => { b = resolve; });
const both = Promise.all([first, second]);
b("B"); a("A");
console.log(await both);
```

### JS-PROMISE-Q20

**Что означает ранний отказ all?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.10. Promises & async/await`
- Уровень: `Mid`
- Тип: `scenario | reliability`
- Приоритет/частота: `Professional | F3`
- Связанные inventory IDs: `JS-52`
- Статус modern/legacy: `современный стандарт; границы среды и совместимость отмечены в главе`
- Ответ: [JS-PROMISE-Q20](../answers/by-domain/01-javascript-and-async-programming.md#js-promise-q20)
- Источники / последняя проверка: `ECMAScript 2026, DOM/Fetch/HTML Standard, MDN, Node.js; ссылки в главе | 2026-11-06`

#### Вопрос

Один вход all отклонился, другой продолжает запись. Значит ли отказ агрегата, что запись отменена и побочные эффекты не произойдут? Какой дополнительный договор нужен?

### JS-PROMISE-Q21

**Что находится в отчёте allSettled?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.10. Promises & async/await`
- Уровень: `Mid`
- Тип: `output-prediction`
- Приоритет/частота: `Professional | F3`
- Связанные inventory IDs: `JS-52`
- Статус modern/legacy: `современный стандарт; границы среды и совместимость отмечены в главе`
- Ответ: [JS-PROMISE-Q21](../answers/by-domain/01-javascript-and-async-programming.md#js-promise-q21)
- Источники / последняя проверка: `ECMAScript 2026, DOM/Fetch/HTML Standard, MDN, Node.js; ссылки в главе | 2026-11-06`

#### Вопрос

Предскажите результат. Что изменилось бы при ошибке обхода самого iterable?
```js
const result = await Promise.allSettled([Promise.reject("bad"), 3]);
console.log(result);
```

### JS-PROMISE-Q22

**Каким будет общий отказ any?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.10. Promises & async/await`
- Уровень: `Mid`
- Тип: `output-prediction`
- Приоритет/частота: `Professional | F3`
- Связанные inventory IDs: `JS-52`
- Статус modern/legacy: `современный стандарт; границы среды и совместимость отмечены в главе`
- Ответ: [JS-PROMISE-Q22](../answers/by-domain/01-javascript-and-async-programming.md#js-promise-q22)
- Источники / последняя проверка: `ECMAScript 2026, DOM/Fetch/HTML Standard, MDN, Node.js; ссылки в главе | 2026-11-06`

#### Вопрос

Предскажите errors и сравните any с race.
```js
let rejectFirst;
const first = new Promise((_, reject) => { rejectFirst = reject; });
const result = Promise.any([first, Promise.reject("B")]);
rejectFirst("A");
console.log(await result.catch(error => error.errors));
```

### JS-PROMISE-Q23

**Тайм-аут ожидания или отмена работы?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.10. Promises & async/await`
- Уровень: `Mid`
- Тип: `scenario | trade-off`
- Приоритет/частота: `Professional | F3`
- Связанные inventory IDs: `JS-52`, `JS-54`
- Статус modern/legacy: `современный стандарт; границы среды и совместимость отмечены в главе`
- Ответ: [JS-PROMISE-Q23](../answers/by-domain/01-javascript-and-async-programming.md#js-promise-q23)
- Источники / последняя проверка: `ECMAScript 2026, DOM/Fetch/HTML Standard, MDN, Node.js; ссылки в главе | 2026-11-06`

#### Вопрос

Запрос состязается с таймером отказа через Promise.race. Таймер победил. Что продолжает работать? Что убрать, если запрос победил первым? Можно ли игнорировать все проигравшие побочные эффекты?

### JS-PROMISE-Q24

**Сопоставьте пустые наборы**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.10. Promises & async/await`
- Уровень: `Mid`
- Тип: `multiple-choice | explain`
- Приоритет/частота: `Professional | F3`
- Связанные inventory IDs: `JS-52`
- Статус modern/legacy: `современный стандарт; границы среды и совместимость отмечены в главе`
- Ответ: [JS-PROMISE-Q24](../answers/by-domain/01-javascript-and-async-programming.md#js-promise-q24)
- Источники / последняя проверка: `ECMAScript 2026, DOM/Fetch/HTML Standard, MDN, Node.js; ссылки в главе | 2026-11-06`

#### Вопрос

Сопоставьте all([]), allSettled([]), any([]), race([]) с вариантами: A — fulfilled []; B — rejected AggregateError с errors []; C — pending без входа для завершения. Какие совпадают, и вызывается ли then пустого all синхронно?

### JS-PROMISE-Q25

**Почините асинхронный обход**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.10. Promises & async/await`
- Уровень: `Senior`
- Тип: `review | design`
- Приоритет/частота: `Advanced | F3`
- Связанные inventory IDs: `JS-51`, `JS-53`
- Статус modern/legacy: `современный стандарт; границы среды и совместимость отмечены в главе`
- Ответ: [JS-PROMISE-Q25](../answers/by-domain/01-javascript-and-async-programming.md#js-promise-q25)
- Источники / последняя проверка: `ECMAScript 2026, DOM/Fetch/HTML Standard, MDN, Node.js; ссылки в главе | 2026-11-06`

#### Вопрос

В UI используют await rows.forEach(async row => save(row)); затем показывают «готово». Нужно сохранить порядок при зависимых записях, а для независимых собрать все успехи либо отчёт частичного отказа. Какие варианты предложите и кто наблюдает ошибки?

### JS-PROMISE-Q26

**Что делает среда с потерянной ветвью?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.10. Promises & async/await`
- Уровень: `Senior`
- Тип: `debugging | compatibility`
- Приоритет/частота: `Advanced | F3`
- Связанные inventory IDs: `JS-51`
- Статус modern/legacy: `современный стандарт; границы среды и совместимость отмечены в главе`
- Ответ: [JS-PROMISE-Q26](../answers/by-domain/01-javascript-and-async-programming.md#js-promise-q26)
- Источники / последняя проверка: `ECMAScript 2026, DOM/Fetch/HTML Standard, MDN, Node.js; ссылки в главе | 2026-11-06`

#### Вопрос

Опишите проверку unhandled rejection в браузере и Node.js 22.13.1. Чем своевременный catch отличается от позднего? Можно ли заменить реальную проверку ручной отправкой события unhandledrejection?

### JS-PROMISE-Q27

**Кому принадлежит отменяемый таймер?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.10. Promises & async/await`
- Уровень: `Senior`
- Тип: `coding | reliability`
- Приоритет/частота: `Advanced | F2`
- Связанные inventory IDs: `JS-54`
- Статус modern/legacy: `современный стандарт; границы среды и совместимость отмечены в главе`
- Ответ: [JS-PROMISE-Q27](../answers/by-domain/01-javascript-and-async-programming.md#js-promise-q27)
- Источники / последняя проверка: `ECMAScript 2026, DOM/Fetch/HTML Standard, MDN, Node.js; ссылки в главе | 2026-11-06`

#### Вопрос

Предложите договор abortableDelay: неверная задержка, уже отменённый сигнал, отмена во время ожидания, нормальное завершение и очистка. Как сохранить причину null и проверить отсутствие лишних регистраций?

### JS-PROMISE-Q28

**Как объединить отмену владельца и срок?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.10. Promises & async/await`
- Уровень: `Senior`
- Тип: `API | trade-off`
- Приоритет/частота: `Advanced | F2`
- Связанные inventory IDs: `JS-54`
- Статус modern/legacy: `современный стандарт; границы среды и совместимость отмечены в главе`
- Ответ: [JS-PROMISE-Q28](../answers/by-domain/01-javascript-and-async-programming.md#js-promise-q28)
- Источники / последняя проверка: `ECMAScript 2026, DOM/Fetch/HTML Standard, MDN, Node.js; ссылки в главе | 2026-11-06`

#### Вопрос

Когда уместны AbortSignal.any и AbortSignal.timeout? Кто определяет причину, можно ли использовать контроллер повторно и равен ли браузерный timeout календарному дедлайну?

### JS-PROMISE-Q29

**Почему Fetch успел, а JSON не прочитан?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.10. Promises & async/await`
- Уровень: `Senior`
- Тип: `debugging | scenario`
- Приоритет/частота: `Advanced | F3`
- Связанные inventory IDs: `JS-51`, `JS-54`
- Статус modern/legacy: `современный стандарт; границы среды и совместимость отмечены в главе`
- Ответ: [JS-PROMISE-Q29](../answers/by-domain/01-javascript-and-async-programming.md#js-promise-q29)
- Источники / последняя проверка: `ECMAScript 2026, DOM/Fetch/HTML Standard, MDN, Node.js; ссылки в главе | 2026-11-06`

#### Вопрос

Fetch выдал Response со статусом 503; в другом запуске получен статус 200, но владелец отменил запрос до окончания тела. Какие разные проверки и отказы нужны? Отменяет ли это серверный эффект?

### JS-PROMISE-Q30

**Почему отмены недостаточно для поиска?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.10. Promises & async/await`
- Уровень: `Senior`
- Тип: `design | debugging`
- Приоритет/частота: `Advanced | F2`
- Связанные inventory IDs: `JS-54`, `JS-55`
- Статус modern/legacy: `современный стандарт; границы среды и совместимость отмечены в главе`
- Ответ: [JS-PROMISE-Q30](../answers/by-domain/01-javascript-and-async-programming.md#js-promise-q30)
- Источники / последняя проверка: `ECMAScript 2026, DOM/Fetch/HTML Standard, MDN, Node.js; ссылки в главе | 2026-11-06`

#### Вопрос

Запрос A отменили после начала B, но источник проигнорировал сигнал и позже вернул A. Как защитить UI, включая закрытие владельца? Каким тестом подтвердить исправление без задержек по времени?

### JS-PROMISE-Q31

**Что может испортить старый catch или finally?**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.10. Promises & async/await`
- Уровень: `Senior`
- Тип: `review | reliability`
- Приоритет/частота: `Advanced | F2`
- Связанные inventory IDs: `JS-55`
- Статус modern/legacy: `современный стандарт; границы среды и совместимость отмечены в главе`
- Ответ: [JS-PROMISE-Q31](../answers/by-domain/01-javascript-and-async-programming.md#js-promise-q31)
- Источники / последняя проверка: `ECMAScript 2026, DOM/Fetch/HTML Standard, MDN, Node.js; ссылки в главе | 2026-11-06`

#### Вопрос

Старый ответ уже запрещено применять, но catch старого запроса всё ещё показывает ошибку, а finally выключает индикатор или стирает контроллер нового запроса. Почему это та же гонка и где нужны проверки?

### JS-PROMISE-Q32

**Спроектируйте загрузку обязательных и необязательных данных**

- Статус: `approved`
- Область: `JavaScript и асинхронное программирование`
- Тема: `1.10. Promises & async/await`
- Уровень: `Senior`
- Тип: `interview-communication | design`
- Приоритет/частота: `Advanced | F3`
- Связанные inventory IDs: `JS-50`, `JS-51`, `JS-52`, `JS-53`, `JS-54`, `JS-55`
- Статус modern/legacy: `современный стандарт; границы среды и совместимость отмечены в главе`
- Ответ: [JS-PROMISE-Q32](../answers/by-domain/01-javascript-and-async-programming.md#js-promise-q32)
- Источники / последняя проверка: `ECMAScript 2026, DOM/Fetch/HTML Standard, MDN, Node.js; ссылки в главе | 2026-11-06`

#### Вопрос

За три минуты опишите загрузку профиля и необязательных уведомлений: независимый старт, различение отказов, сохранённые причины, сигнал, последний запрос и закрытие. Назовите проверяемые свойства и границы с 1.11.

## 1.11. Async Coordination Patterns

Вопросы для самостоятельного воспроизведения; ответы хранятся отдельно.
### JS-COORD-Q01

- Статус: `approved`
- Область: `JavaScript & Async Programming`
- Тема: Выбор механизма
- Уровень: `Junior`
- Тип: `conceptual | compare`
- Приоритет/частота: `core / F2`
- Связанные inventory IDs: `JS-56`, `JS-57`, `JS-58`
- Статус modern/legacy: `modern`
- Ответ: [отдельный ответ](../answers/by-domain/01-javascript-and-async-programming.md#js-coord-q01)
- Источники / последняя проверка: самостоятельная формулировка; [глава и источники](../../handbook/01-javascript-and-async-programming/11-async-coordination-patterns.md#источники-и-последняя-проверка), `2026-11-06`.

**Выбор механизма.** Для поиска после паузы, обновления позиции во время движения и не более трёх незавершённых загрузок выберите механизмы. Почему один из них не заменяет остальные?

### JS-COORD-Q02

- Статус: `approved`
- Область: `JavaScript & Async Programming`
- Тема: Два края debounce
- Уровень: `Junior`
- Тип: `API | compare`
- Приоритет/частота: `core / F3`
- Связанные inventory IDs: `JS-56`
- Статус modern/legacy: `modern`
- Ответ: [отдельный ответ](../answers/by-domain/01-javascript-and-async-programming.md#js-coord-q02)
- Источники / последняя проверка: самостоятельная формулировка; [глава и источники](../../handbook/01-javascript-and-async-programming/11-async-coordination-patterns.md#источники-и-последняя-проверка), `2026-11-06`.

**Два края debounce.** Что означают leading и trailing? Какие дополнительные правила нужно уточнить для одного входа и для сочетания обоих краёв?

### JS-COORD-Q03

- Статус: `approved`
- Область: `JavaScript & Async Programming`
- Тема: Последние аргументы и контекст
- Уровень: `Junior`
- Тип: `why | API`
- Приоритет/частота: `core / F3`
- Связанные inventory IDs: `JS-56`
- Статус modern/legacy: `modern`
- Ответ: [отдельный ответ](../answers/by-domain/01-javascript-and-async-programming.md#js-coord-q03)
- Источники / последняя проверка: самостоятельная формулировка; [глава и источники](../../handbook/01-javascript-and-async-programming/11-async-coordination-patterns.md#источники-и-последняя-проверка), `2026-11-06`.

**Последние аргументы и контекст.** Зачем обёртка debounce объявлена обычной функцией и зачем сохраняется получатель? Становятся ли переданные объекты снимком?

### JS-COORD-Q04

- Статус: `approved`
- Область: `JavaScript & Async Programming`
- Тема: Отмена и принудительное выполнение
- Уровень: `Junior`
- Тип: `conceptual | lifecycle`
- Приоритет/частота: `core / F3`
- Связанные inventory IDs: `JS-56`
- Статус modern/legacy: `modern`
- Ответ: [отдельный ответ](../answers/by-domain/01-javascript-and-async-programming.md#js-coord-q04)
- Источники / последняя проверка: самостоятельная формулировка; [глава и источники](../../handbook/01-javascript-and-async-programming/11-async-coordination-patterns.md#источники-и-последняя-проверка), `2026-11-06`.

**Отмена и принудительное выполнение.** Чем cancel отличается от flush? Как они относятся к уже начатому сетевому запросу?

### JS-COORD-Q05

- Статус: `approved`
- Область: `JavaScript & Async Programming`
- Тема: Ограничит ли all запуск?
- Уровень: `Junior`
- Тип: `output-prediction`
- Приоритет/частота: `core / F2`
- Связанные inventory IDs: `JS-58`
- Статус modern/legacy: `modern`
- Ответ: [отдельный ответ](../answers/by-domain/01-javascript-and-async-programming.md#js-coord-q05)
- Источники / последняя проверка: самостоятельная формулировка; [глава и источники](../../handbook/01-javascript-and-async-programming/11-async-coordination-patterns.md#источники-и-последняя-проверка), `2026-11-06`.

**Ограничит ли all запуск?.** Что окажется в журнале до await и ограничивает ли агрегат работу?
```js
const log = [];
const promises = [1, 2, 3].map(n => {
  log.push(n);
  return Promise.resolve(n);
});
console.log(log);
console.log(await Promise.all(promises));
```

### JS-COORD-Q06

- Статус: `approved`
- Область: `JavaScript & Async Programming`
- Тема: Сколько всего попыток?
- Уровень: `Junior`
- Тип: `conceptual | precision`
- Приоритет/частота: `core / F2`
- Связанные inventory IDs: `JS-58`
- Статус modern/legacy: `modern`
- Ответ: [отдельный ответ](../answers/by-domain/01-javascript-and-async-programming.md#js-coord-q06)
- Источники / последняя проверка: самостоятельная формулировка; [глава и источники](../../handbook/01-javascript-and-async-programming/11-async-coordination-patterns.md#источники-и-последняя-проверка), `2026-11-06`.

**Сколько всего попыток?.** В договоре maxAttempts=3 включает первый запуск. Сколько дополнительных запусков и пауз возможно? Что происходит после последнего отказа?

### JS-COORD-Q07

- Статус: `approved`
- Область: `JavaScript & Async Programming`
- Тема: Временная линия debounce
- Уровень: `Mid`
- Тип: `output-prediction`
- Приоритет/частота: `core / F3`
- Связанные inventory IDs: `JS-56`
- Статус modern/legacy: `modern`
- Ответ: [отдельный ответ](../answers/by-domain/01-javascript-and-async-programming.md#js-coord-q07)
- Источники / последняя проверка: самостоятельная формулировка; [глава и источники](../../handbook/01-javascript-and-async-programming/11-async-coordination-patterns.md#источники-и-последняя-проверка), `2026-11-06`.

**Временная линия debounce.** Задержка `wait` равна 100 мс. Время отсчитываем от первого вызова обёртки: сначала передаём значение A, через 40 мс от начала — B, через 80 мс — C. Для расчёта считаем, что таймеры не опаздывают.

Какие значения получит обработчик и когда он выполнится в каждом случае?

- Только после паузы: `leading=false`, `trailing=true`.
- Только в начале серии: `leading=true`, `trailing=false`.
- В начале и после паузы: `leading=true`, `trailing=true`.

Новые обращения не совпадают по времени с окончанием таймера.

### JS-COORD-Q08

- Статус: `approved`
- Область: `JavaScript & Async Programming`
- Тема: Временная линия throttle
- Уровень: `Mid`
- Тип: `output-prediction`
- Приоритет/частота: `core / F3`
- Связанные inventory IDs: `JS-57`
- Статус modern/legacy: `modern`
- Ответ: [отдельный ответ](../answers/by-domain/01-javascript-and-async-programming.md#js-coord-q08)
- Источники / последняя проверка: самостоятельная формулировка; [глава и источники](../../handbook/01-javascript-and-async-programming/11-async-coordination-patterns.md#источники-и-последняя-проверка), `2026-11-06`.

**Временная линия throttle.** Используем throttle из главы с немедленным первым и отложенным последним вызовом (`leading=true`, `trailing=true`), задержка — 100 мс. Сначала передаём обёртке значение A, через 40 мс от начала — B, через 80 мс — C, через 140 мс — D. Все отметки отсчитываются от первого вызова; таймеры в этом расчёте не опаздывают.

Какие значения получит обработчик и в какие моменты? Как изменится результат, если вместо этого использовать debounce с выполнением только после паузы?

### JS-COORD-Q09

- Статус: `approved`
- Область: `JavaScript & Async Programming`
- Тема: Нулевая задержка
- Уровень: `Mid`
- Тип: `why | host-boundary`
- Приоритет/частота: `core / F2`
- Связанные inventory IDs: `JS-56`, `JS-57`
- Статус modern/legacy: `modern`
- Ответ: [отдельный ответ](../answers/by-domain/01-javascript-and-async-programming.md#js-coord-q09)
- Источники / последняя проверка: самостоятельная формулировка; [глава и источники](../../handbook/01-javascript-and-async-programming/11-async-coordination-patterns.md#источники-и-последняя-проверка), `2026-11-06`.

**Нулевая задержка.** Как учебный debounce ведёт себя при wait=0 и leading=false? Что с нулём у учебного throttle? Можно ли ждать выполнения прямо в текущем стеке?

### JS-COORD-Q10

- Статус: `approved`
- Область: `JavaScript & Async Programming`
- Тема: Новая обёртка на каждом событии
- Уровень: `Mid`
- Тип: `debugging | review`
- Приоритет/частота: `core / F3`
- Связанные inventory IDs: `JS-56`
- Статус modern/legacy: `modern`
- Ответ: [отдельный ответ](../answers/by-domain/01-javascript-and-async-programming.md#js-coord-q10)
- Источники / последняя проверка: самостоятельная формулировка; [глава и источники](../../handbook/01-javascript-and-async-programming/11-async-coordination-patterns.md#источники-и-последняя-проверка), `2026-11-06`.

**Новая обёртка на каждом событии.** Найдите ошибку организации состояния; emit вызывается после каждого события.
```js
function emit(schedule, send, value) {
  const wrapped = schedule(send, 100);
  wrapped(value);
}
```

### JS-COORD-Q11

- Статус: `approved`
- Область: `JavaScript & Async Programming`
- Тема: Асинхронная функция внутри debounce
- Уровень: `Mid`
- Тип: `review | errors`
- Приоритет/частота: `core / F3`
- Связанные inventory IDs: `JS-56`
- Статус modern/legacy: `modern`
- Ответ: [отдельный ответ](../answers/by-domain/01-javascript-and-async-programming.md#js-coord-q11)
- Источники / последняя проверка: самостоятельная формулировка; [глава и источники](../../handbook/01-javascript-and-async-programming/11-async-coordination-patterns.md#источники-и-последняя-проверка), `2026-11-06`.

**Асинхронная функция внутри debounce.** Учебная обёртка возвращает undefined и вызывает async send без ожидания. Можно ли получить сетевой результат через await wrapped(value)? Кто обрабатывает отказ?

### JS-COORD-Q12

- Статус: `approved`
- Область: `JavaScript & Async Programming`
- Тема: Мутация аргумента до таймера
- Уровень: `Mid`
- Тип: `scenario | identity`
- Приоритет/частота: `core / F3`
- Связанные inventory IDs: `JS-56`
- Статус modern/legacy: `modern`
- Ответ: [отдельный ответ](../answers/by-domain/01-javascript-and-async-programming.md#js-coord-q12)
- Источники / последняя проверка: самостоятельная формулировка; [глава и источники](../../handbook/01-javascript-and-async-programming/11-async-coordination-patterns.md#источники-и-последняя-проверка), `2026-11-06`.

**Мутация аргумента до таймера.** В debounce передали объект {value:1}, затем до таймера заменили поле на 2. Что увидит обработчик? Как зафиксировать значение ввода?

### JS-COORD-Q13

- Статус: `approved`
- Область: `JavaScript & Async Programming`
- Тема: Инвариант и освобождение места
- Уровень: `Mid`
- Тип: `coding | invariant`
- Приоритет/частота: `core / F2`
- Связанные inventory IDs: `JS-58`
- Статус modern/legacy: `modern`
- Ответ: [отдельный ответ](../answers/by-domain/01-javascript-and-async-programming.md#js-coord-q13)
- Источники / последняя проверка: самостоятельная формулировка; [глава и источники](../../handbook/01-javascript-and-async-programming/11-async-coordination-patterns.md#источники-и-последняя-проверка), `2026-11-06`.

**Инвариант и освобождение места.** В какой момент увеличивать active и как обеспечить его уменьшение при синхронном throw, обычном значении и thenable? Почему это важно для повторного входа?

### JS-COORD-Q14

- Статус: `approved`
- Область: `JavaScript & Async Programming`
- Тема: Закрытие очереди
- Уровень: `Mid`
- Тип: `API | lifecycle`
- Приоритет/частота: `core / F2`
- Связанные inventory IDs: `JS-58`
- Статус modern/legacy: `modern`
- Ответ: [отдельный ответ](../answers/by-domain/01-javascript-and-async-programming.md#js-coord-q14)
- Источники / последняя проверка: самостоятельная формулировка; [глава и источники](../../handbook/01-javascript-and-async-programming/11-async-coordination-patterns.md#источники-и-последняя-проверка), `2026-11-06`.

**Закрытие очереди.** Что должно произойти с ожидающими обещаниями, новыми добавлениями и работающими задачами при close? Каков смысл повторного close?

### JS-COORD-Q15

- Статус: `approved`
- Область: `JavaScript & Async Programming`
- Тема: Частичный отчёт в правильном порядке
- Уровень: `Mid`
- Тип: `output-prediction`
- Приоритет/частота: `core / F2`
- Связанные inventory IDs: `JS-58`
- Статус modern/legacy: `modern`
- Ответ: [отдельный ответ](../answers/by-domain/01-javascript-and-async-programming.md#js-coord-q15)
- Источники / последняя проверка: самостоятельная формулировка; [глава и источники](../../handbook/01-javascript-and-async-programming/11-async-coordination-patterns.md#источники-и-последняя-проверка), `2026-11-06`.

**Частичный отчёт в правильном порядке.** Назовите порядок и состояния результата.
```js
const a = Promise.reject("A failed");
const b = Promise.resolve("B ok");
const report = await Promise.allSettled([a, b]);
console.log(report.map(x => x.status));
```

### JS-COORD-Q16

- Статус: `approved`
- Область: `JavaScript & Async Programming`
- Тема: Одновременность или запросы в секунду?
- Уровень: `Mid`
- Тип: `performance | compare`
- Приоритет/частота: `core / F2`
- Связанные inventory IDs: `JS-58`
- Статус modern/legacy: `modern`
- Ответ: [отдельный ответ](../answers/by-domain/01-javascript-and-async-programming.md#js-coord-q16)
- Источники / последняя проверка: самостоятельная формулировка; [глава и источники](../../handbook/01-javascript-and-async-programming/11-async-coordination-patterns.md#источники-и-последняя-проверка), `2026-11-06`.

**Одновременность или запросы в секунду?.** Почему concurrency=2 не соблюдает серверную квоту два запроса в секунду? Какая дополнительная граница нужна при большом производителе?

### JS-COORD-Q17

- Статус: `approved`
- Область: `JavaScript & Async Programming`
- Тема: Расчёт полного разброса
- Уровень: `Mid`
- Тип: `output-prediction`
- Приоритет/частота: `core / F2`
- Связанные inventory IDs: `JS-58`
- Статус modern/legacy: `modern`
- Ответ: [отдельный ответ](../answers/by-domain/01-javascript-and-async-programming.md#js-coord-q17)
- Источники / последняя проверка: самостоятельная формулировка; [глава и источники](../../handbook/01-javascript-and-async-programming/11-async-coordination-patterns.md#источники-и-последняя-проверка), `2026-11-06`.

**Расчёт полного разброса.** Полный разброс: floor(sample * min(maximum, base * 2 ** (failedAttempt - 1))). base=100, maximum=250, sample=0.5. Назовите первые четыре паузы. Может ли выпасть ноль?

### JS-COORD-Q18

- Статус: `approved`
- Область: `JavaScript & Async Programming`
- Тема: Допустимость повторной попытки
- Уровень: `Mid`
- Тип: `scenario | reliability`
- Приоритет/частота: `core / F2`
- Связанные inventory IDs: `JS-58`
- Статус modern/legacy: `modern`
- Ответ: [отдельный ответ](../answers/by-domain/01-javascript-and-async-programming.md#js-coord-q18)
- Источники / последняя проверка: самостоятельная формулировка; [глава и источники](../../handbook/01-javascript-and-async-programming/11-async-coordination-patterns.md#источники-и-последняя-проверка), `2026-11-06`.

**Допустимость повторной попытки.** Как различить временный безопасный отказ и отказ, который не надо повторять? Достаточно ли статуса 503 или имени TypeError?

### JS-COORD-Q19

- Статус: `approved`
- Область: `JavaScript & Async Programming`
- Тема: Сигнал во время паузы
- Уровень: `Mid`
- Тип: `debugging | cancellation`
- Приоритет/частота: `core / F2`
- Связанные inventory IDs: `JS-58`
- Статус modern/legacy: `modern`
- Ответ: [отдельный ответ](../answers/by-domain/01-javascript-and-async-programming.md#js-coord-q19)
- Источники / последняя проверка: самостоятельная формулировка; [глава и источники](../../handbook/01-javascript-and-async-programming/11-async-coordination-patterns.md#источники-и-последняя-проверка), `2026-11-06`.

**Сигнал во время паузы.** Реальный запрос поддерживает сигнал, но ожидание между попытками реализовано обычным setTimeout. Что упущено? Какие проверки требуются на границах?

### JS-COORD-Q20

- Статус: `approved`
- Область: `JavaScript & Async Programming`
- Тема: Мутация ключа идемпотентности
- Уровень: `Mid`
- Тип: `review | safety`
- Приоритет/частота: `core / F2`
- Связанные inventory IDs: `JS-58`
- Статус modern/legacy: `modern`
- Ответ: [отдельный ответ](../answers/by-domain/01-javascript-and-async-programming.md#js-coord-q20)
- Источники / последняя проверка: самостоятельная формулировка; [глава и источники](../../handbook/01-javascript-and-async-programming/11-async-coordination-patterns.md#источники-и-последняя-проверка), `2026-11-06`.

**Мутация ключа идемпотентности.** Клиент создаёт платёж и на каждой повторной попытке генерирует новый ключ идемпотентности. Почему это не защищает от дубля после потерянного ответа?

### JS-COORD-Q21

- Статус: `approved`
- Область: `JavaScript & Async Programming`
- Тема: Отмена без фактического завершения
- Уровень: `Senior`
- Тип: `design | invariant`
- Приоритет/частота: `core / F2`
- Связанные inventory IDs: `JS-58`
- Статус modern/legacy: `modern`
- Ответ: [отдельный ответ](../answers/by-domain/01-javascript-and-async-programming.md#js-coord-q21)
- Источники / последняя проверка: самостоятельная формулировка; [глава и источники](../../handbook/01-javascript-and-async-programming/11-async-coordination-patterns.md#источники-и-последняя-проверка), `2026-11-06`.

**Отмена без фактического завершения.** Активная фабрика игнорирует сигнал. Почему нельзя сразу уменьшить active при abort? Как в учебном договоре завершается её Promise?

### JS-COORD-Q22

- Статус: `approved`
- Область: `JavaScript & Async Programming`
- Тема: Вложенный ограничитель
- Уровень: `Senior`
- Тип: `debugging | deadlock`
- Приоритет/частота: `core / F2`
- Связанные inventory IDs: `JS-58`
- Статус modern/legacy: `modern`
- Ответ: [отдельный ответ](../answers/by-domain/01-javascript-and-async-programming.md#js-coord-q22)
- Источники / последняя проверка: самостоятельная формулировка; [глава и источники](../../handbook/01-javascript-and-async-programming/11-async-coordination-patterns.md#источники-и-последняя-проверка), `2026-11-06`.

**Вложенный ограничитель.** Предел 1. Внешняя задача заняла место и ожидает run внутренней задачи того же ограничителя. Каков цикл ожидания и что изменить?

### JS-COORD-Q23

- Статус: `approved`
- Область: `JavaScript & Async Programming`
- Тема: Повторы нескольких слоёв
- Уровень: `Senior`
- Тип: `architecture | reliability`
- Приоритет/частота: `core / F2`
- Связанные inventory IDs: `JS-58`
- Статус modern/legacy: `modern`
- Ответ: [отдельный ответ](../answers/by-domain/01-javascript-and-async-programming.md#js-coord-q23)
- Источники / последняя проверка: самостоятельная формулировка; [глава и источники](../../handbook/01-javascript-and-async-programming/11-async-coordination-patterns.md#источники-и-последняя-проверка), `2026-11-06`.

**Повторы нескольких слоёв.** Три уровня делают до трёх попыток каждый. Оцените верхнюю границу обращений к нижнему сервису и предложите договор ответственности.

### JS-COORD-Q24

- Статус: `approved`
- Область: `JavaScript & Async Programming`
- Тема: Где ожидать backoff?
- Уровень: `Senior`
- Тип: `trade-off | design`
- Приоритет/частота: `core / F2`
- Связанные inventory IDs: `JS-58`
- Статус modern/legacy: `modern`
- Ответ: [отдельный ответ](../answers/by-domain/01-javascript-and-async-programming.md#js-coord-q24)
- Источники / последняя проверка: самостоятельная формулировка; [глава и источники](../../handbook/01-javascript-and-async-programming/11-async-coordination-patterns.md#источники-и-последняя-проверка), `2026-11-06`.

**Где ожидать backoff?.** Сравните limiter.run(() => retry(operation)) и retry(() => limiter.run(operation)). Когда занято место, что ограничивается и где возможны лишние очереди?

### JS-COORD-Q25

- Статус: `approved`
- Область: `JavaScript & Async Programming`
- Тема: Retry-After и общий срок
- Уровень: `Senior`
- Тип: `scenario | protocol`
- Приоритет/частота: `core / F2`
- Связанные inventory IDs: `JS-58`
- Статус modern/legacy: `modern`
- Ответ: [отдельный ответ](../answers/by-domain/01-javascript-and-async-programming.md#js-coord-q25)
- Источники / последняя проверка: самостоятельная формулировка; [глава и источники](../../handbook/01-javascript-and-async-programming/11-async-coordination-patterns.md#источники-и-последняя-проверка), `2026-11-06`.

**Retry-After и общий срок.** Сервис просит Retry-After:120, клиент готов ждать ещё 2 секунды. Можно ли зажать задержку до 2 секунд и повторить? Какие форматы заголовка существуют?

### JS-COORD-Q26

- Статус: `approved`
- Область: `JavaScript & Async Programming`
- Тема: Память и обратное давление
- Уровень: `Senior`
- Тип: `performance | design`
- Приоритет/частота: `core / F2`
- Связанные inventory IDs: `JS-58`
- Статус modern/legacy: `modern`
- Ответ: [отдельный ответ](../answers/by-domain/01-javascript-and-async-programming.md#js-coord-q26)
- Источники / последняя проверка: самостоятельная формулировка; [глава и источники](../../handbook/01-javascript-and-async-programming/11-async-coordination-patterns.md#источники-и-последняя-проверка), `2026-11-06`.

**Память и обратное давление.** Производитель сразу создал миллион записей очереди при concurrency=2. Что не решено и как разделить ограничения без нового фреймворка?

### JS-COORD-Q27

- Статус: `approved`
- Область: `JavaScript & Async Programming`
- Тема: Старый ответ во время паузы поиска
- Уровень: `Senior`
- Тип: `debugging | UI`
- Приоритет/частота: `core / F2`
- Связанные inventory IDs: `JS-56`, `JS-58`
- Статус modern/legacy: `modern`
- Ответ: [отдельный ответ](../answers/by-domain/01-javascript-and-async-programming.md#js-coord-q27)
- Источники / последняя проверка: самостоятельная формулировка; [глава и источники](../../handbook/01-javascript-and-async-programming/11-async-coordination-patterns.md#источники-и-последняя-проверка), `2026-11-06`.

**Старый ответ во время паузы поиска.** Новый текст уже введён, следующий debounce ещё не сработал, прежний запрос завершился. Когда менять версию и отменять запрос, чтобы старый ответ не попал в UI?

### JS-COORD-Q28

- Статус: `approved`
- Область: `JavaScript & Async Programming`
- Тема: План проверки координации
- Уровень: `Senior`
- Тип: `interview-communication | testing`
- Приоритет/частота: `core / F2`
- Связанные inventory IDs: `JS-56`, `JS-57`, `JS-58`
- Статус modern/legacy: `modern`
- Ответ: [отдельный ответ](../answers/by-domain/01-javascript-and-async-programming.md#js-coord-q28)
- Источники / последняя проверка: самостоятельная формулировка; [глава и источники](../../handbook/01-javascript-and-async-programming/11-async-coordination-patterns.md#источники-и-последняя-проверка), `2026-11-06`.

**План проверки координации.** Как проверить временные линии, очередь, retry и DOM, не полагаясь на точные задержки реальной машины? Где заканчиваются выводы теста?
