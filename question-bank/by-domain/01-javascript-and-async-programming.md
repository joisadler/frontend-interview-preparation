# 1. JavaScript и асинхронное программирование — вопросы

> Статус: `частично готово — 1.1 одобрен; 1.2 готов к review; 1.3–1.12 остаются placeholders`
>
> Ответы: [в отдельном файле](../answers/by-domain/01-javascript-and-async-programming.md)
>
> Разделы 1.3–1.12 остаются заглушками (`placeholders`).

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

- Статус: `готово к review`
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

- Статус: `готово к review`
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

- Статус: `готово к review`
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

- Статус: `готово к review`
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

- Статус: `готово к review`
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

- Статус: `готово к review`
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

- Статус: `готово к review`
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

- Статус: `готово к review`
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

- Статус: `готово к review`
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

- Статус: `готово к review`
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

- Статус: `готово к review`
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

- Статус: `готово к review`
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

- Статус: `готово к review`
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

- Статус: `готово к review`
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

- Статус: `готово к review`
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

- Статус: `готово к review`
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

- Статус: `готово к review`
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

- Статус: `готово к review`
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

- Статус: `готово к review`
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

- Статус: `готово к review`
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

- Статус: `готово к review`
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

- Статус: `готово к review`
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

- Статус: `готово к review`
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

- Статус: `готово к review`
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
