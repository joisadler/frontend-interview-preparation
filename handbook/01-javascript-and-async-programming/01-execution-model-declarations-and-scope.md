# 1.1. Модель выполнения, объявления и области видимости (Execution Model, Declarations & Scope)

> Статус: `черновик — третья калибровочная версия`
>
> Связанные inventory IDs: `JS-01`, `JS-02`, `JS-03`, `JS-04`, `JS-22`
>
> Последняя содержательная проверка: `2026-09-28`

## Как устроена глава

Весь материал находится здесь. Не нужно сначала читать теорию, затем открывать отдельные вопросы, а потом искать ответы.

Каждый блок устроен одинаково:

1. реальный вопрос с интервью;
2. **короткий ответ**, который можно дать вслух за 30–60 секунд;
3. только необходимое пояснение;
4. небольшой пример или типичная ловушка.

Для настоящей проверки себя в конце остаются отдельные упражнения без видимых решений. Полные темы функций и closures будут в 1.3, модулей — в 1.7, event loop — в 1.9. Здесь они затронуты только там, где без них нельзя объяснить scope.

## Ментальная модель в одной картинке

Представьте программу как офис:

- **область видимости (scope)** — комната;
- **привязка (binding)** — запись имени в журнале комнаты;
- поиск имени идёт из текущей комнаты наружу;
- ближайшая запись с тем же именем скрывает внешнюю — это **shadowing**;
- объявления заносятся в журналы до выполнения обычных строк — отсюда наблюдаемое поведение **hoisting**;
- у `let` и `const` запись уже есть, но до инициализации (initialization) ею нельзя пользоваться — это **TDZ**;
- вызовы функций складываются как незавершённые задачи: последний вызов должен завершиться первым — это **call stack**.

Аналогия нужна только для памяти. JavaScript-движок не обязан буквально создавать комнаты, журналы или обычные JS-объекты для каждой области.

---

## Основы: имена, объявления и scope

<a id="js-scope-q03"></a>
### 1. Что такое переменная и чем declaration отличается от initialization и assignment?

_Junior · conceptual · `JS-01`, `JS-03`_

**Короткий ответ.** В разговорной речи переменная — именованный доступ к значению. Точнее, **идентификатор (identifier)** — имя в коде, **привязка (binding)** связывает это имя с состоянием и значением, а **значение (value)** — сами данные. **Объявление (declaration)** вводит имя, **инициализация (initialization)** впервые даёт привязке значение, а последующее **присваивание (assignment)** меняет его.

```js
let count = 1;
count = 2;
```

- `count` — identifier;
- `let count` — объявление;
- создание внутренней записи для `count` — создание привязки;
- первое значение `1` — инициализация;
- новое значение `2` — присваивание.

Жизненный цикл `let` / `const` удобно видеть так:

```text
вход в область видимости
  → привязка создана, но ещё не инициализирована
  → TDZ: читать нельзя
  → выполняется объявление
  → инициализация завершена, TDZ закончилась
  → последующее присваивание возможно только там, где разрешено
```

У `var` другое начало: новая привязка заранее инициализируется значением `undefined`. Поэтому её можно прочитать до строки с инициализатором (initializer).

`const` запрещает переназначить саму привязку, но не замораживает объект:

```js
const user = { name: "Ada" };
user.name = "Grace"; // допустимо
// user = {};         // TypeError
```

**Ловушка.** Инициализация — не просто «первое присваивание»: до неё лексическая привязка уже существует, но находится в TDZ.

<a id="js-scope-q01"></a>
### 2. Чем отличаются `var`, `let` и `const`?

_Junior · compare · `JS-01`_

**Короткий ответ.** `var` имеет область видимости функции (function scope), заранее получает `undefined` и допускает повторное объявление. `let` и `const` имеют блочную область (block scope) и находятся в TDZ до своей строки. `let` можно переназначать, `const` — нельзя. В современном коде используют `const` по умолчанию и `let`, когда значение действительно меняется; `var` нужно знать для legacy-кода и интервью.

| Свойство | `var` | `let` | `const` |
|---|---|---|---|
| Scope | ближайшая функция / верх script или module | block | block |
| До строки declaration | `undefined` | TDZ | TDZ |
| Initializer обязателен | нет | нет | да |
| Reassignment | да | да | нет |
| Redeclaration в той же scope | обычно да | нет | нет |

```js
function example() {
  if (true) {
    var fromVar = 1;
    const fromConst = 2;
  }

  console.log(fromVar); // 1
  // console.log(fromConst); // ReferenceError
}
```

Механическая замена `var` на `let` может изменить scope, TDZ, допустимость повторных объявлений и поведение callbacks в цикле. Старый код сначала анализируют, потом рефакторят.

<a id="js-scope-q02"></a>
### 3. Что такое область видимости (scope) и какие области бывают?

_Junior · conceptual · `JS-02`_

**Короткий ответ.** Область видимости определяет, в какой части кода имя относится к конкретной привязке. Основные границы — global, function, block и module scope. JavaScript использует **лексическую область видимости (lexical scope)**: поиск зависит от места, где код написан, а не от места вызова функции.

- **Global scope** — внешняя область среды выполнения.
- **Function scope** — параметры, локальные имена и `var` конкретной функции.
- **Block scope** — `{ ... }`, тело цикла, `catch`, единый блок `switch`; ограничивает `let`, `const` и `class`.
- **Module scope** — верхний уровень конкретного ES module; его объявления не становятся общими глобальными именами.

`Lexical scope` — не пятый вид фигурных скобок. Это правило: вложенный код может искать имена во внешних областях, определённых структурой исходного кода.

```js
const rate = 2;

function calculate(value) {
  const fee = 1;
  return value * rate + fee;
}
```

`calculate` видит собственные `value` и `fee`, затем внешний `rate`. Внешний код не видит `fee`.

<a id="js-scope-q09"></a>
### 4. Как JavaScript решает, к какой переменной относится имя?

_Mid · output / explain · `JS-02`_

**Короткий ответ.** Поиск начинается в текущей lexical scope и идёт наружу. Как только binding найден, поиск прекращается. Если ближайший binding ещё в TDZ, JavaScript бросит `ReferenceError`, а не возьмёт одноимённую внешнюю переменную.

```js
const name = "global";

function makeReader() {
  const name = "factory";
  return function read() {
    return name;
  };
}

function run(reader) {
  const name = "caller";
  console.log(reader());
}

run(makeReader()); // "factory"
```

Функция `read` была написана внутри `makeReader`, поэтому её внешняя lexical scope — `makeReader`, а не вызывающая функция `run`. Место вызова не перестраивает scope chain.

Это необходимое следствие closures, но полная тема closures остаётся в 1.3.

**Identifier и property — разные поиски:**

```js
// console.log(missingName); // ReferenceError: binding не найден

const config = {};
console.log(config.missingName); // undefined: config найден, property отсутствует
```

---

## Как JavaScript подготавливает и выполняет код

### 5. Что происходит до выполнения первой строки?

_Mid · conceptual · `JS-02`, `JS-03`_
**Короткий ответ.** Для интервью достаточно двух шагов: сначала JavaScript определяет scope, создаёт bindings и проверяет конфликты объявлений; затем выполняет инструкции по порядку. Поэтому declarations могут влиять на код раньше своей текстовой позиции, хотя строки физически не перемещаются.

```text
1. Подготовка declarations
   → какие имена существуют?
   → в какой scope?
   → какое у каждого начальное состояние?
   → нет ли запрещённого конфликта?

2. Выполнение
   → инструкции идут по порядку
   → expressions вычисляются
   → происходят initialization и assignment
```

Это рабочая модель, а не один универсальный алгоритм для любого кода. У script, module, function и block детали различаются. Названия вроде `GlobalDeclarationInstantiation` полезны только в очень глубоком разговоре.

<a id="js-scope-q08"></a>
### 6. Чем отличаются scope, Environment Record, execution context и call stack?

_Mid · compare / explain · `JS-02`_

**Короткий ответ.** Scope отвечает, где имя видно в исходном коде. **Environment Record** — точная модель хранения bindings во время выполнения. **Execution context** хранит состояние выполняемого script, module или вызова функции. **Call stack** показывает порядок активных вызовов функций.

| Понятие | Вопрос |
|---|---|
| scope | Где это имя относится к этому binding? |
| Environment Record | Где модель языка хранит bindings и ссылку наружу? |
| execution context | Какое состояние сейчас нужно выполняемому коду? |
| call stack | Какие вызовы ещё не завершены и в каком порядке? |

```js
function first() {
  second();
}

function second() {
  return "done";
}

first();
```

Внутри `second` стек выглядит как `entry → first → second`. После `return` вызовы снимаются в обратном порядке.

<a id="js-scope-q10"></a>
#### Почему обычный block не добавляет stack frame?

**Короткий ответ.** Block создаёт block scope для лексических declarations, но не вызывает функцию. Поэтому новый function execution context и новый stack frame не появляются.

```js
function render() {
  if (true) {
    const label = "Details";
    console.log(label);
  }
}
```

**Точность для Senior.** В спецификации execution context содержит ссылки `LexicalEnvironment` и `VariableEnvironment` на Environment Records. Движок вправе оптимизировать реализацию; не называйте эти записи обычными JS-объектами.

<a id="js-scope-q16"></a>
### 7. Что такое hoisting и почему код не «перемещается вверх»?

_Junior → Mid · explain · `JS-03`_

**Короткий ответ.** **Hoisting** — неформальное имя наблюдаемого поведения: declarations обрабатываются до обычного выполнения строк. Код не переписывается. Разница между объявлениями определяется состоянием binding до своей строки.

| Declaration | Состояние до своей строки |
|---|---|
| `var value` | initialized: `undefined` |
| `let value` | binding существует, но TDZ |
| `const value = ...` | binding существует, но TDZ |
| `class Value {}` | binding существует, но TDZ |
| `function value() {}` | обычно уже содержит функцию |
| `var value = function () {}` | `value === undefined`; expression ещё не вычислено |
| `const value = function () {}` | `value` в TDZ |

Фраза «`let` и `const` не hoisted» тоже неточна: их bindings уже существуют, но не initialized.

<a id="js-scope-q04"></a>
### 8. Какие результаты дадут `var`, TDZ и `typeof` до declaration?

_Junior · output prediction · `JS-03`_

**Вопрос 1:**

```js
console.log(total); // undefined
var total = 3;
```

**Ответ.** Binding `total` уже initialized значением `undefined`; `= 3` выполнится позже как assignment.

**Вопрос 2:**

```js
console.log(score); // ReferenceError
let score = 3;
```

**Ответ.** Binding `score` найден, но находится в TDZ.

**Вопрос 3:**

```js
console.log(typeof later); // ReferenceError
const later = 3;
```

**Ответ.** `typeof` не обходит TDZ.

**Вопрос 4:**

```js
console.log(typeof neverDeclared); // "undefined"
```

**Ответ.** Здесь binding вообще не существует; только для такого unresolved identifier у `typeof` есть специальное безопасное поведение.

TDZ начинается при входе в scope, а не просто «на строках выше declaration»:

```js
const state = "outer";

{
  // console.log(state); // ReferenceError: найден inner binding в TDZ
  const state = "inner";
}
```

<a id="js-scope-q05"></a>
### 9. Почему function declaration и function expression доступны в разное время?

_Junior · compare / output · `JS-03`, ограниченно `JS-12`_

**Короткий ответ.** Function declaration обычно получает объект функции во время подготовки declarations. Function expression создаётся только при выполнении своей строки и следует правилам переменной, в которую его записывают.

```js
ready(); // работает

function ready() {
  return true;
}
```

```js
run(); // TypeError: run сейчас undefined

var run = function () {
  return true;
};
```

```js
start(); // ReferenceError: start в TDZ

const start = function () {
  return true;
};
```

`ReferenceError` означает, что значение binding нельзя получить. `TypeError` во втором примере означает: binding найден, но текущее `undefined` нельзя вызвать как функцию.

---

## Shadowing, redeclaration и ранние ошибки

<a id="js-scope-q06"></a>
### 10. Чем shadowing отличается от redeclaration и illegal shadowing?

_Junior · conceptual · `JS-04`_

**Короткий ответ.** **Shadowing** — два разных bindings с одинаковым именем во вложенных scopes; ближайший скрывает внешний. **Redeclaration** — попытка снова объявить имя в той же эффективной scope. Термин **illegal shadowing** обычно используют для случая, когда `var` выходит за границу блока и конфликтует с внешним `let` / `const`; точнее это конфликт declarations.

Допустимое shadowing:

```js
const mode = "outer";

{
  const mode = "inner";
  console.log(mode); // "inner"
}
```

Внешний `var` и внутренний block `let` тоже создают разные bindings и допустимы. Но этот код не компилируется:

```text
let mode = "outer";
{
  var mode = "inner"; // SyntaxError
}
```

`var` принадлежал бы окружающей function/global scope и столкнулся бы там с `let mode`.

Даже легальное shadowing стоит убрать, если читателю трудно понять, какое имя используется.

<a id="js-scope-q11"></a>
### 11. Какие redeclaration rules действительно нужно помнить?

_Mid · find the bug · `JS-01`, `JS-04`_

**Короткий ответ.** В одной scope повторный `var` обычно разрешён. `let` и `const` нельзя повторно объявить, и они конфликтуют с `var` того же имени. Такой конфликт часто является `SyntaxError` до выполнения кода.

| Уже есть | новый `var` | новый `let` | новый `const` |
|---|---:|---:|---:|
| `var` | обычно ✅ | ❌ | ❌ |
| `let` | ❌ | ❌ | ❌ |
| `const` | ❌ | ❌ | ❌ |

```text
console.log("не выполнится");
let id = 1;
var id = 2; // SyntaxError до обычного выполнения
```

Это **ранняя ошибка (Early Error)** внутри одной разобранной единицы. Даже строка выше конфликта не выполнится.

Повторный `var` не сбрасывает прежнее значение:

```js
var score = 10;
var score;
console.log(score); // 10
```

<a id="js-scope-q14"></a>
### 12. Почему одинаковые `let` / `const` в разных `case` конфликтуют?

_Mid · debugging · `JS-04`_

**Короткий ответ.** Все `case` одного `switch` делят один lexical block. Разные ветки выполнения не означают разные scopes. Добавьте `{}` вокруг каждой ветки.

Проблема:

```text
switch (status) {
  case "idle":
    const message = "Waiting";
    break;
  case "done":
    const message = "Complete"; // SyntaxError
}
```

Исправление:

```js
switch (status) {
  case "idle": {
    const message = "Waiting";
    console.log(message);
    break;
  }
  case "done": {
    const message = "Complete";
    console.log(message);
    break;
  }
}
```

---

## Strict mode, globals и разные среды выполнения

<a id="js-scope-q07"></a>
### 13. Что меняет strict mode и откуда берутся accidental globals?

_Junior → Mid · debugging · `JS-22`_

**Короткий ответ.** В sloppy classic script assignment в неизвестное имя может создать property глобального объекта. В **strict mode** тот же код бросает `ReferenceError`. ES modules strict автоматически. Современный код должен объявлять bindings явно и ловить такие ошибки линтером.

```js
function update(items) {
  total = items.length; // declaration забыто
}
```

- sloppy classic script: может появиться `globalThis.total`;
- strict code / ES module: `ReferenceError`;
- исправление: `const total = items.length; return total;` или явное изменение объекта-владельца.

`delete` удаляет **property**, а не variable binding:

```js
const config = { debug: true };
delete config.debug; // удаляется property
```

- `delete globalThis.total` работает с property и зависит от его `configurable` descriptor;
- локальные `let`, `const`, parameters и `var` так удалить нельзя;
- `delete identifier` в strict code — `SyntaxError`.

<a id="js-scope-q12"></a>
### 14. Почему global binding не всегда является property `globalThis`?

_Mid · compare · `JS-02`, `JS-22`_

**Короткий ответ.** `globalThis` — ссылка на глобальное значение `this`, а не словарь всех доступных имён. В browser classic script верхнеуровневый `var` часто создаёт property глобального объекта, а `let` / `const` — отдельные global lexical bindings. В ES module все объявления module-scoped и не публикуются в `globalThis`.

| Среда | `var` верхнего уровня | `let` / `const` верхнего уровня | Strict автоматически |
|---|---|---|---|
| browser classic script | часто property `globalThis` | global lexical binding, не property | нет |
| browser ES module | module scope | module scope | да |
| Node.js ES module | module scope | module scope | да |
| Node.js CommonJS | локален function wrapper | локальны wrapper | нет для всего файла |

Таблица предполагает чистую среду без заранее существующего одноимённого property.

<a id="js-scope-q19"></a>
### 15. Как отвечать на вопрос о верхнем уровне, если среда не указана?

_Senior · practical scenario · `JS-02`, `JS-22`_

**Короткий ответ.** Сначала уточнить: classic script, browser module, Node ESM, CommonJS, Worker или console. Без этого вопрос о `var`, strict mode и `globalThis` может не иметь одного ответа.

Например, такой контракт ненадёжен:

```js
var registry = { enabled: true };
console.log(globalThis.registry.enabled);
```

Он может работать в classic browser script, но в ESM `registry` остаётся module-scoped, а в CommonJS — локальным для wrapper. Если глобальный API действительно нужен, публикуйте его явно:

```js
globalThis.myLibrary = {
  registry: { enabled: true },
};
```

Обычный современный вариант — `export` / `import`, а не скрытый global contract.

<a id="js-scope-q17"></a>
### 16. Что такое Global Environment Record и нужно ли рассказывать это на обычном интервью?

_Senior · optional precision · `JS-02`_

**Короткий ответ.** Это спецификационная модель global bindings в classic script. Она объясняет, почему global `var` может отражаться в global object, а global `let` / `const` — нет. В базовом ответе достаточно наблюдаемого правила; внутренние названия нужны только если интервьюер углубляется.

Упрощённо Global Environment Record объединяет:

- **Object Environment Record** — связан с global object и обслуживает подходящие classic-script `var` / function declarations;
- **Declarative Environment Record** — хранит global `let`, `const` и `class` bindings.

ES modules используют собственное module environment. Реальный движок не обязан реализовать эти записи как два обычных объекта.

---

## Практические задачи, debugging и code review

<a id="js-scope-q13"></a>
### 17. Почему callbacks в `for (var ...)` видят одно значение, а в `for (let ...)` — разные?

_Mid · output prediction · `JS-02`, ограниченно `JS-15`_

**Короткий ответ.** `var` создаёт один общий binding цикла. Все closures читают его после цикла, когда там уже финальное значение. `for (let ...)` создаёт отдельный binding для каждой итерации.

```js
const fromVar = [];

for (var i = 0; i < 3; i += 1) {
  fromVar.push(() => i);
}

console.log(fromVar.map((read) => read())); // [3, 3, 3]
```

```js
const fromLet = [];

for (let i = 0; i < 3; i += 1) {
  fromLet.push(() => i);
}

console.log(fromLet.map((read) => read())); // [0, 1, 2]
```

Точная формулировка: closure сохраняет доступ к binding, а не автоматически копирует value.

<a id="js-scope-q15"></a>
### 18. Что не так с этим legacy-кодом и как его исправить?

_Mid · code review · `JS-01`, `JS-02`, `JS-22`_

```js
function register(items) {
  handlers = {};

  for (var i = 0; i < items.length; i += 1) {
    handlers[i] = function () {
      return items[i];
    };
  }
}
```

**Ответ.** Здесь две ошибки корректности:

1. `handlers` не объявлен: sloppy classic script создаст accidental global, strict code бросит `ReferenceError`.
2. Все functions используют один `var i`; после цикла `i === items.length`, поэтому чтение обычно вернёт `undefined`.

Минимальное исправление:

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

Если нужно сохранить именно текущее value элемента даже после изменения массива, внутри итерации захватите `const item = items[i]` и возвращайте `item`. Это уже решение о контракте, а не о scope.

<a id="js-scope-q18"></a>
### 19. Почему два отдельных classic scripts могут конфликтовать только в production?

_Senior · debugging scenario · `JS-02`, `JS-04`_

Предположим, приложение раньше загрузило:

```html
<script>
  let config = { mode: "app" };
</script>
```

Затем legacy vendor script пытается выполнить `var config`.

**Короткий ответ.** Global lexical binding `config` из первого classic script уже существует. При подготовке declarations второго script его `var config` конфликтует с этим именем, поэтому второй script получает `SyntaxError` до выполнения своих обычных строк.

Это может не воспроизводиться в dev, если bundler изолирует файлы как modules или function wrappers. Проверять нужно реальный способ загрузки production-кода.

Надёжное решение — modules или явный namespace с одним владельцем. Перестановка scripts лишь меняет порядок конфликта, но не решает проблему владения именем.

<a id="js-scope-q20"></a>
### 20. Как безопасно сделать мост к legacy global API?

_Senior · small implementation · `JS-22`_

**Короткий ответ.** Передать root явно, выбрать namespace, проверить collision и удалять только собственную установленную ссылку. Такой мост нужен для совместимости; обычный новый код должен использовать modules.

```js
function installLegacyApi(root, api) {
  const key = "frontendInterview";

  if (Object.hasOwn(root, key)) {
    throw new Error(`${key} is already installed`);
  }

  root[key] = api;

  return function uninstall() {
    if (root[key] !== api) return false;
    return delete root[key];
  };
}
```

Здесь нет unresolved assignment, collision не перезаписывается, а cleanup не удалит чужую замену. `delete` всё равно зависит от descriptor property.

<a id="js-scope-analysis"></a>
### 21. Как системно решать любую output-задачу на scope?

_Junior → Senior · interview method_

**Короткий ответ.** Не начинайте выполнять строки в голове. Сначала определите среду, scopes и bindings; только после этого переходите к runtime.

1. **Среда:** classic script, ESM, CommonJS?
2. **Конфликты:** есть ли SyntaxError до выполнения?
3. **Границы:** global/module → functions → blocks.
4. **Bindings:** где созданы; начальное состояние — function, `undefined` или TDZ?
5. **Lookup:** от текущей scope наружу; ближайший найденный binding побеждает.
6. **Выполнение:** теперь идите по строкам, вызовам и `return`.
7. **Точный результат:** value, `undefined`, `ReferenceError`, `TypeError` или `SyntaxError`.

Этот алгоритм надёжнее заучивания десятков отдельных «hoisting tricks».

---

## Что точно не стоит говорить на интервью

- «JavaScript физически переносит declarations наверх» — нет, это модель наблюдаемого поведения.
- «`let` и `const` не hoisted» — bindings создаются заранее, но остаются в TDZ.
- «`const` делает объект immutable» — он запрещает reassignment binding.
- «Любая global variable лежит в `globalThis`» — зависит от declaration и среды.
- «Каждая scope создаёт stack frame» — block scope не является вызовом функции.
- «Closure копирует value» — closure сохраняет доступ к binding.

## Упражнения

Теория и interview Q&A уже находятся в этой главе. Отдельно оставлена только практика, где ответы не должны быть видны заранее:

- [9 упражнений: recall → prediction → explanation → debugging → review → implementation](../../exercises/prompts/by-domain/01-javascript-and-async-programming.md)
- решения находятся в отдельном файле и открываются только после собственной попытки;
- комплексная задача: `JS-SCOPE-EX09`.

## Чек-лист готовности

### Explain

- [ ] За 30–60 секунд сравниваю `var`, `let`, `const`.
- [ ] Объясняю scope, lookup, hoisting и TDZ без мифа о переносе кода.
- [ ] Различаю scope, Environment Record, execution context и call stack.

### Recognize / predict

- [ ] Предсказываю `undefined`, `ReferenceError`, `TypeError` и ранний `SyntaxError`.
- [ ] Нахожу shadowing, redeclaration, TDZ и loop-binding trap.
- [ ] Уточняю runtime перед ответом про top-level и `globalThis`.

### Implement / debug / review

- [ ] Выбираю `const` / `let` осознанно и безопасно рефакторю `var`.
- [ ] Убираю accidental globals и скрытые global contracts.
- [ ] Отличаю ошибку корректности от необязательного style improvement.

## Coverage

| Inventory ID | Где раскрыт |
|---|---|
| `JS-01` | Q1–2, Q10–11, Q18 |
| `JS-02` | Q3–6, вложенный вопрос о block/call stack, Q14–19 |
| `JS-03` | Q1, Q5, Q7–9 |
| `JS-04` | Q10–12, Q19 |
| `JS-22` | Q13–16, Q18, Q20 |

Ограниченные cross-references: `JS-12` только для declaration/expression timing; `JS-15` только для loop bindings; `BR-05` только для synchronous call stack; `JS-41–42` только для module scope и automatic strict mode.

## Источники

- [ECMAScript 2026 — Execution Contexts and Environment Records](https://tc39.es/ecma262/2026/multipage/executable-code-and-execution-contexts.html)
- [ECMAScript 2026 — Declarations and Statements](https://tc39.es/ecma262/2026/multipage/ecmascript-language-statements-and-declarations.html)
- [ECMAScript 2026 — Scripts and Modules](https://tc39.es/ecma262/2026/multipage/ecmascript-language-scripts-and-modules.html)
- [MDN — Hoisting](https://developer.mozilla.org/en-US/docs/Glossary/Hoisting)
- [MDN — `var`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/var), [`let`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let), [`const`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/const)
- [MDN — Strict mode](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Strict_mode)
- [MDN — `delete`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/delete)
- [MDN — `globalThis`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/globalThis)
- [HTML Living Standard — `script`](https://html.spec.whatwg.org/multipage/scripting.html#the-script-element)
- [Node.js — The module wrapper](https://nodejs.org/api/modules.html#the-module-wrapper)

Дата проверки: **2026-09-28**.
