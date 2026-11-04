# 1. JavaScript и асинхронное программирование — условия упражнений

> Статус: `частично готово — упражнения 1.1–1.6 одобрены; 1.7–1.12 остаются заглушками`
>
> Не открывайте [файл с решениями](../../solutions/by-domain/01-javascript-and-async-programming.md), пока не выполните собственную попытку.
>
> Упражнения разделов 1.1–1.6 одобрены. Разделы 1.7–1.12 остаются заглушками.

## 1.1. Модель выполнения, объявления и области видимости

Последовательность: **воспроизведение по памяти → прогнозирование → объяснение → отладка → ревью кода → реализация → комплексная задача**.

### JS-SCOPE-EX01

**Восстановите матрицу объявлений по памяти**

- Статус: `approved`
- Раздел: `JavaScript и асинхронное программирование`
- Сложность: `Junior | воспроизведение по памяти`
- Проверяемые навыки: `терминология, жизненный цикл объявления, рекомендации для рабочего кода`
- Связанные ID из inventory: `JS-01`, `JS-03`
- Решение: [JS-SCOPE-EX01](../../solutions/by-domain/01-javascript-and-async-programming.md#js-scope-ex01)

#### Задание

Не заглядывая в главу handbook, составьте таблицу для следующих форм:

- `var`;
- `let`;
- `const`;
- объявление функции (function declaration);
- функциональное выражение, сохранённое в `var`;
- функциональное выражение, сохранённое в `const`.

Для каждой строки укажите:

1. область видимости;
2. состояние привязки (binding) до строки объявления;
3. правило повторного присваивания;
4. правило повторного объявления в той же области видимости;
5. одно замечание для рабочего кода или интервью.

Затем дайте определения терминам **declaration**, **initialization**, **assignment**, **TDZ** и **early error** — по одному предложению на термин.

#### Ограничения

- Максимальное время: 8 минут.
- Не используйте формулировку «перемещается наверх».
- Сначала пометьте неуверенные ячейки; не подсматривайте ответы.

#### Критерии самопроверки

- [ ] Присутствуют все запрошенные строки и столбцы.
- [ ] Для каждого термина дано определение одним предложением.
- [ ] Неуверенные ячейки были отмечены до проверки.
- [ ] Рекомендации для рабочего кода отделены от знаний для интервью и поддержки устаревшего кода.

### JS-SCOPE-EX02

**Предскажите значения, ошибки и фазу сбоя**

- Статус: `approved`
- Раздел: `JavaScript и асинхронное программирование`
- Сложность: `Junior → Mid | прогнозирование`
- Проверяемые навыки: `hoisting, TDZ, shadowing, классификация ошибок`
- Связанные ID из inventory: `JS-01`, `JS-03`, `JS-04`
- Решение: [JS-SCOPE-EX02](../../solutions/by-domain/01-javascript-and-async-programming.md#js-scope-ex02)

#### Задание

Рассматривайте фрагменты A–F как независимые скрипты. До запуска каждого фрагмента запишите:

- точный вывод до первого сбоя;
- будет ли результатом `undefined`, конкретное значение или ошибка, и какого класса;
- является ли сбой ранней статической ошибкой (Early Error) или происходит во время выполнения;
- состояние привязки в момент каждого чтения.

#### A

```js
console.log(score);
var score = 7;
console.log(score);
```

#### B

```js
console.log(score);
let score = 7;
```

#### C

```js
const score = 5;
{
  console.log(score);
  const score = 7;
}
```

#### D

```js
console.log(typeof missing);
console.log(typeof present);
let present = true;
```

#### E

```js
run();
var run = () => "ok";
```

#### F

```js
console.log("before");
let id = 1;
var id = 2;
```

#### Ограничения

- Не запускайте код, пока не запишете прогнозы для всех шести фрагментов.
- После запуска объясните каждое расхождение через привязки, а не заученный лозунг.

#### Критерии самопроверки

- [ ] Для всех шести независимых фрагментов записан прогноз.
- [ ] Для каждого сбоя указаны класс ошибки и фаза.
- [ ] Каждое чтение объяснено через состояние привязки.
- [ ] Расхождения после запуска объяснены, а не просто исправлены.

### JS-SCOPE-EX03

**Проследите разрешение идентификаторов**

- Статус: `approved`
- Раздел: `JavaScript и асинхронное программирование`
- Сложность: `Mid | объяснение`
- Проверяемые навыки: `записи окружения, лексический поиск, стек вызовов`
- Связанные ID из inventory: `JS-02`
- Решение: [JS-SCOPE-EX03](../../solutions/by-domain/01-javascript-and-async-programming.md#js-scope-ex03)

#### Задание

Для каждого отмеченного чтения перечислите проверяемые записи окружения (Environment Records) в правильном порядке и укажите найденную привязку.

```js
const label = "global";

function build(prefix) {
  const label = `${prefix}:build`;

  return function (enabled) {
    if (enabled) {
      const suffix = "!";
      return label + suffix; // чтение 1: label; чтение 2: suffix
    }

    return label; // чтение 3
  };
}

function invoke(callback) {
  const label = "invoke";
  return callback(true);
}

const report = build("scope");
console.log(invoke(report));
```

Также изобразите стек вызовов (call stack) в момент, когда `report` вычисляет `return label + suffix`.

#### Ограничения

- Отличайте активного вызывающего от внешнего лексического окружения.
- Не утверждайте, что блок создаёт ещё один фрейм вызова функции.

#### Критерии самопроверки

- [ ] Для каждого отмеченного чтения явно указан порядок поиска.
- [ ] Схемы лексического окружения и стека вызовов нарисованы отдельно.
- [ ] Учтены и место определения, и место вызова.
- [ ] Итоговый вывод указан только после трассировки.

### JS-SCOPE-EX04

**Два объяснения с ограничением по времени**

- Статус: `approved`
- Раздел: `JavaScript и асинхронное программирование`
- Сложность: `Junior → Mid | коммуникация`
- Проверяемые навыки: `активное воспроизведение, терминология, краткое объяснение`
- Связанные ID из inventory: `JS-01`, `JS-02`, `JS-03`
- Решение: [JS-SCOPE-EX04](../../solutions/by-domain/01-javascript-and-async-programming.md#js-scope-ex04)

#### Задание

Запишите два ответа:

1. **45 секунд:** сравните `var`, `let` и `const`.
2. **60 секунд:** объясните контекст выполнения, записи окружения, цепочку областей, подъём объявлений и TDZ как единую непротиворечивую модель.

Для каждого ответа используйте структуру:

```text
определение → ментальная модель → один пример → одна ловушка или правило для рабочего кода
```

#### Ограничения

- Во время первой записи не используйте заметки.
- Не говорите, что «движок перемещает код».
- Не тратьте время на механизм планирования event loop или полноценные сценарии использования closures.

#### Критерии самопроверки

- [ ] Концептуальная корректность.
- [ ] Точная терминология воспроизведена без подсказок.
- [ ] Приведён один конкретный пример.
- [ ] Границы темы ясны, нерелевантных отступлений нет.
- [ ] Ответ укладывается в отведённое время.

### JS-SCOPE-EX05

**Отладьте глобальные переменные с поведением, зависящим от окружения**

- Статус: `approved`
- Раздел: `JavaScript и асинхронное программирование`
- Сложность: `Mid | отладка`
- Проверяемые навыки: `строгий режим, случайные глобальные переменные, глобальный объект, предположения о среде выполнения`
- Связанные ID из inventory: `JS-02`, `JS-22`
- Решение: [JS-SCOPE-EX05](../../solutions/by-domain/01-javascript-and-async-programming.md#js-scope-ex05)

#### Задание

Устаревший файл аналитики загружается как классический браузерный скрипт:

```js
function record(event) {
  lastEvent = event;
  var count = (globalThis.count || 0) + 1;
  globalThis.count = count;
}

record("open");

console.log(globalThis.lastEvent);
console.log(globalThis.count);
```

Ответьте на вопросы:

1. В нестрогом режиме (sloppy mode) классифицируйте `lastEvent`, локальный для функции `count` и `globalThis.count` как привязки и/или свойства (properties), явно указав владельца каждого имени.
2. Что изменится после добавления `"use strict"`?
3. Что изменится, если тот же исходный код загрузить как ES-модуль?
4. Какое состояние должно оставаться локальным, возвращаться наружу или иметь явного владельца?
5. Предложите сначала минимальное исправление, а затем более чистый API.
6. После выполнения нестрогой версии предскажите результат `delete globalThis.lastEvent`. Сравните его со строгим кодом, содержащим `delete lastEvent`, и объясните, почему `delete` не предназначен для очистки локальных переменных.

#### Ограничения

- Явно помечайте выводы для классического браузерного скрипта и браузерного модуля.
- Не используйте эксперименты в консоли DevTools как доказательство.
- В минимальном исправлении сохраните наблюдаемое поведение счётчика.

#### Критерии самопроверки

- [ ] Для всех трёх запрошенных имён указан владелец.
- [ ] Нестрогий режим, строгий режим и модуль разобраны отдельно.
- [ ] Оба варианта исправления сохраняют или явно документируют наблюдаемое поведение.
- [ ] Обе формы удаления разобраны с учётом цели операции и фазы сбоя.

### JS-SCOPE-EX06

**Исправьте конфликты объявлений**

- Статус: `approved`
- Раздел: `JavaScript и асинхронное программирование`
- Сложность: `Mid | отладка`
- Проверяемые навыки: `redeclaration, illegal shadowing, область видимости switch, early errors`
- Связанные ID из inventory: `JS-01`, `JS-04`
- Решение: [JS-SCOPE-EX06](../../solutions/by-domain/01-javascript-and-async-programming.md#js-scope-ex06)

#### Задание

Найдите все дефекты синтаксического разбора и объявлений и исправьте их минимальным изменением областей видимости:

```js
function format(kind) {
  let result = "unknown";

  if (kind === "short") {
    var result = "S";
  }

  switch (kind) {
    case "long":
      const suffix = "!";
      result = "Long" + suffix;
      break;
    case "verbose":
      const suffix = "!!";
      result = "Verbose" + suffix;
      break;
  }

  return result;
}
```

Затем укажите, может ли до исправления выполниться хотя бы один вызов `format`.

#### Ограничения

- Сохраните все предполагаемые возвращаемые строки.
- Не заменяйте всю функцию таблицей соответствий: это упражнение посвящено областям видимости.
- Объясните, почему взаимоисключающие ветви потока управления (`control flow`) не устраняют конфликты объявлений.

#### Критерии самопроверки

- [ ] Найдены все конфликты объявлений.
- [ ] Каждое изменение минимально и обосновано.
- [ ] Сохранены все предполагаемые возвращаемые строки.
- [ ] Объяснена фаза сбоя.

### JS-SCOPE-EX07

**Ревью кода с фокусом на области видимости**

- Статус: `approved`
- Раздел: `JavaScript и асинхронное программирование`
- Сложность: `Mid → Senior | ревью кода`
- Проверяемые навыки: `корректность, приоритизация замечаний, владение глобальным состоянием, поэтапный рефакторинг`
- Связанные ID из inventory: `JS-01`, `JS-02`, `JS-03`, `JS-22`
- Решение: [JS-SCOPE-EX07](../../solutions/by-domain/01-javascript-and-async-programming.md#js-scope-ex07)

#### Задание

Проведите ревью этой интеграции через классический скрипт:

```js
var active = true;

function install(buttons) {
  callbacks = [];

  for (var index = 0; index < buttons.length; index += 1) {
    callbacks.push(function () {
      if (active) {
        return buttons[index].id;
      }
    });
  }
}
```

Подготовьте:

1. замечания ревью, упорядоченные по серьёзности;
2. прогноз поведения после завершения `install`;
3. минимальное исправление, сохраняющее совместимость;
4. целевой дизайн на основе модулей;
5. тесты, которые вы добавили бы перед миграцией интеграции с устаревшим кодом.

#### Ограничения

- Отделяйте дефекты корректности от стилистических предпочтений.
- Укажите, должно ли состояние `active` быть общим намеренно или оказалось глобальным случайно. Если это неизвестно, запросите контракт.
- Не переписывайте код целиком без связи с задачей.

#### Критерии самопроверки

- [ ] Замечания отсортированы по серьёзности и категории.
- [ ] Рассмотрены корректность, владение состоянием и сопровождаемость.
- [ ] Минимальное исправление отделено от целевого дизайна.
- [ ] Тесты покрывают и поведение, и окружение выполнения.

### JS-SCOPE-EX08

**Реализуйте стабильные функции обратного вызова для каждого индекса**

- Статус: `approved`
- Раздел: `JavaScript и асинхронное программирование`
- Сложность: `Mid | реализация`
- Проверяемые навыки: `привязки отдельных итераций, выбор объявления, тестирование`
- Связанные ID из inventory: `JS-01`, `JS-02`
- Решение: [JS-SCOPE-EX08](../../solutions/by-domain/01-javascript-and-async-programming.md#js-scope-ex08)

#### Задание

Реализуйте функцию:

```js
function createReaders(values) {
  // вернуть по одной функции без аргументов для каждого элемента
}
```

Контракт:

```js
const values = ["a", "b", "c"];
const readers = createReaders(values);

readers[0](); // { index: 0, value: "a" }
readers[2](); // { index: 2, value: "c" }
```

Выберите и задокументируйте одну из двух семантик:

- **актуальное значение на момент вызова (live):** функция чтения видит последующую замену значения в `values[index]`;
- **снимок (snapshot):** функция чтения сохраняет значение, существовавшее при создании.

#### Ограничения

- Используйте цикл.
- Не используйте IIFE, `bind`, изменяемую глобальную переменную или вспомогательный метод перебора массива.
- Используйте современные объявления.
- Добавьте тесты для пустого входного массива, трёх элементов и выбранной семантики актуального значения или снимка.
- Объясните отдельную привязку каждой итерации.

#### Критерии самопроверки

- [ ] Проверены все примеры контракта и граничные случаи.
- [ ] Поведение с актуальным значением или снимком указано явно.
- [ ] Выбор объявлений обоснован.
- [ ] Указана временная и пространственная сложность.

### JS-SCOPE-EX09

**Интервью-задача — миграция областей видимости**

- Статус: `approved`
- Раздел: `JavaScript и асинхронное программирование`
- Сложность: `Senior | комплексная задача`
- Проверяемые навыки: `прогнозирование, классификация окружений, отладка, ревью, реализация, коммуникация`
- Связанные ID из inventory: `JS-01`, `JS-02`, `JS-03`, `JS-04`, `JS-22`
- Решение: [JS-SCOPE-EX09](../../solutions/by-domain/01-javascript-and-async-programming.md#js-scope-ex09)

#### Задание

Страница мигрирует с классических скриптов на модули.

```html
<script src="bootstrap.js"></script>
<script src="widget.js"></script>
<script type="module" src="app.js"></script>
```

```js
// bootstrap.js — классический скрипт, нестрогий режим
var mode = "legacy";
sharedCount = 0;
```

```js
// widget.js — классический скрипт
console.log("widget start");
let mode = "widget";

function makeHandlers(nodes) {
  const handlers = [];

  for (var i = 0; i < nodes.length; i += 1) {
    handlers.push(() => `${mode}:${nodes[i].id}`);
  }

  return handlers;
}
```

```js
// app.js — ES-модуль
var mode = "module";

export function start(nodes) {
  sharedCount += 1;
  return makeHandlers(nodes);
}
```

Не выполняя код:

1. Определите, завершаются ли для каждого файла подготовка объявлений и выполнение.
2. Перечислите весь вывод и все ошибки в фактическом порядке.
3. Определите, какие имена являются привязками, какие — свойствами (properties) глобального объекта, а какие недоступны через границу модуля.
4. Найдите все дефекты корректности и владения состоянием.
5. Спроектируйте минимальное исправление, сохранив схему загрузки из трёх файлов.
6. Спроектируйте более чистый целевой вариант, полностью основанный на модулях.
7. Дайте трёхминутное объяснение своего анализа в формате интервью.

#### Ограничения

- Явно укажите предположения о чистой изолированной среде браузера и обычном порядке выполнения внешних скриптов.
- В полностью модульном варианте не добавляйте свойства в `globalThis`.
- Ограничьте обсуждение функций и замыканий только теми последствиями области видимости, которые нужны для этой задачи.
- Ранжируйте дефекты по серьёзности, а не просто перечисляйте их.

#### Критерии самопроверки

- [ ] Все три файла разобраны в порядке загрузки.
- [ ] Вывод и сбои расположены по порядку, для каждого указана фаза.
- [ ] Классифицированы привязки, свойства и видимость между файлами.
- [ ] Дефекты ранжированы, а не просто перечислены.
- [ ] Минимальное исправление отделено от целевой архитектуры.
- [ ] В объяснении используется терминология привязок и окружений и соблюдаются границы темы.

## 1.2. Значения, типы, равенство и преобразование типов

Последовательность: **воспроизведение по памяти → прогнозирование → объяснение → отладка → ревью кода → реализация → комплексная задача**.

### JS-VALUES-EX01

**Восстановите карту values и сравнений по памяти**

- Статус: `approved`
- Раздел: `JavaScript и асинхронное программирование`
- Сложность: `Junior | воспроизведение по памяти`
- Проверяемые навыки: `primitive types, typeof, falsy/nullish, equality semantics`
- Связанные ID из inventory: `JS-05`, `JS-06`, `JS-08`, `JS-09`
- Решение: [JS-VALUES-EX01](../../solutions/by-domain/01-javascript-and-async-programming.md#js-values-ex01)

#### Задание

Не заглядывая в handbook:

1. Перечислите семь primitive types и отдельно опишите object values.
2. Для каждого primitive запишите representative literal или способ создания и результат `typeof`.
3. Перечислите все falsy values и затем только nullish values.
4. Заполните матрицу для `===`, `Object.is` и SameValueZero: совпадают ли `NaN` с собой и `0` с `-0`; где каждая семантика используется.
5. Одним предложением разграничьте primitive immutability, binding reassignment и object mutation.

#### Ограничения

- Максимальное время: 8 минут.
- Сначала отметьте неуверенные ячейки.
- Не включайте objects, пустые arrays или string `"0"` в falsy values.

#### Критерии самопроверки

- [ ] Названы все семь primitives.
- [ ] Учтены `typeof null`, functions и arrays.
- [ ] Falsy и nullish не смешаны.
- [ ] Три equality semantics сопоставлены с реальными APIs.
- [ ] Mutability value отделена от возможности переназначить binding.

### JS-VALUES-EX02

**Предскажите values, types и ошибки**

- Статус: `approved`
- Раздел: `JavaScript и асинхронное программирование`
- Сложность: `Junior → Mid | прогнозирование`
- Проверяемые навыки: `typeof, NaN, BigInt, operator +, truthiness, equality`
- Связанные ID из inventory: `JS-06`, `JS-07`, `JS-08`, `JS-09`, `JS-10`
- Решение: [JS-VALUES-EX02](../../solutions/by-domain/01-javascript-and-async-programming.md#js-values-ex02)

#### Задание

Считайте строки независимыми. Для каждой запишите value, type или класс ошибки и короткую цепочку преобразований:

```js
typeof null;
typeof NaN;
Number("");
Number("12px");
Boolean("0");
"5" + 2;
"5" - 2;
1 + 2 + "3";
NaN === NaN;
Object.is(NaN, NaN);
Object.is(0, -0);
[NaN].includes(NaN);
0n == 0;
0n === 0;
```

Отдельно предскажите намеренно ошибочные expressions:

```js
1n + 1;
+1n;
```

#### Критерии самопроверки

- [ ] Для каждого результата указан type.
- [ ] String branch `+` отделена от numeric coercion `-`.
- [ ] `NaN`, signed zero и BigInt объяснены разными правилами.
- [ ] Ошибочные expressions помечены как `TypeError`, а не `NaN`.

### JS-VALUES-EX03

**Объясните pass-by-value через identities**

- Статус: `approved`
- Раздел: `JavaScript и асинхронное программирование`
- Сложность: `Mid | объяснение`
- Проверяемые навыки: `bindings, identity, shared reference, mutation, reassignment`
- Связанные ID из inventory: `JS-05`, `JS-11`
- Решение: [JS-VALUES-EX03](../../solutions/by-domain/01-javascript-and-async-programming.md#js-values-ex03)

#### Задание

Не запускайте код до ответа:

```js
function update(profile) {
  profile.tags.push("reviewed");
  profile = { name: "replacement", tags: [] };
  profile.tags.push("local");
}

const original = { name: "Ada", tags: [] };
const alias = original;

update(original);

console.log(original);
console.log(alias === original);
```

1. Нарисуйте bindings и object identities до вызова, внутри функции после каждой строки и после возврата.
2. Предскажите output.
3. Дайте 45-секундный ответ без фразы «object передаётся по reference».
4. Покажите, как написать pure alternative, которая не мутирует input.

#### Критерии самопроверки

- [ ] Параметр показан как отдельный binding.
- [ ] Mutation общей identity отделена от reassignment параметра.
- [ ] Pure alternative создаёт и outer object, и новый `tags` array.
- [ ] Ответ использует формулировку «reference value передаётся by value».

### JS-VALUES-EX04

**Отладьте defaulting и optional chaining**

- Статус: `approved`
- Раздел: `JavaScript и асинхронное программирование`
- Сложность: `Mid | debugging`
- Проверяемые навыки: `truthy/falsy, nullish, ||, ??, continuous optional chain`
- Связанные ID из inventory: `JS-08`, `JS-40`
- Решение: [JS-VALUES-EX04](../../solutions/by-domain/01-javascript-and-async-programming.md#js-values-ex04)

#### Задание

Форма должна сохранять допустимые `0`, `""` и `false`; fallback применяется только к `null`/`undefined`.

```js
function readPreferences(user) {
  return {
    pageSize: user.settings?.pageSize || 20,
    nickname: user.profile?.nickname || "Anonymous",
    compact: user.settings?.compact || true,
    city: (user.profile?.address).city || "Unknown",
  };
}
```

1. Найдите каждый bug для input с отсутствующими nested objects и с допустимыми falsy values.
2. Объясните, почему parentheses меняют optional-chain protection.
3. Исправьте функцию без необоснованного проглатывания ошибок из существующих getters/methods.
4. Составьте minimal test table.

#### Критерии самопроверки

- [ ] `??` применён только там, где contract nullish.
- [ ] Optional chain остаётся continuous до `.city`.
- [ ] Не утверждается, что `?.` подавляет произвольные исключения.
- [ ] Тесты различают отсутствующее значение и допустимое falsy value.

### JS-VALUES-EX05

**Исправьте numeric validation и расчёт денег**

- Статус: `approved`
- Раздел: `JavaScript и асинхронное программирование`
- Сложность: `Mid | debugging | production scenario`
- Проверяемые навыки: `NaN, finite/safe integer checks, floating point, money boundary`
- Связанные ID из inventory: `JS-07`, `JS-10`
- Решение: [JS-VALUES-EX05](../../solutions/by-domain/01-javascript-and-async-programming.md#js-values-ex05)

#### Задание

```js
function charge(rawPrice, rawQuantity) {
  const price = Number(rawPrice);
  const quantity = Number(rawQuantity);

  if (isNaN(price) || isNaN(quantity)) {
    throw new Error("invalid input");
  }

  return price * quantity;
}

console.log(charge("0.10", "3") === 0.3);
```

1. Найдите неожиданно принятые inputs: empty/whitespace, infinities, fractions и unsafe integers.
2. Сформулируйте отдельный contract для price и quantity.
3. Перепишите boundary: price принимает canonical decimal с двумя знаками, quantity — positive safe integer.
4. Верните total в integer minor units.
5. Объясните, почему global `isNaN`, `Number.EPSILON` и округление только в самом конце не заменяют contract.

#### Критерии самопроверки

- [ ] Grammar проверяется до или вместе с conversion.
- [ ] Использованы finite/safe/range checks согласно contract.
- [ ] Денежная сумма остаётся integer minor units.
- [ ] Rounding policy не маскируется floating-point trick.

### JS-VALUES-EX06

**Проведите code review shared defaults**

- Статус: `approved`
- Раздел: `JavaScript и асинхронное программирование`
- Сложность: `Mid → Senior | code review`
- Проверяемые навыки: `object identity, shallow copy, ownership, mutation`
- Связанные ID из inventory: `JS-05`, `JS-11`
- Решение: [JS-VALUES-EX06](../../solutions/by-domain/01-javascript-and-async-programming.md#js-values-ex06)

#### Задание

```js
const DEFAULT_FILTER = {
  range: { from: 0, to: 100 },
  tags: [],
};

function createFilter(overrides = {}) {
  const filter = { ...DEFAULT_FILTER, ...overrides };
  filter.tags.push("active");
  filter.range.from += 1;
  return filter;
}
```

1. Ранжируйте findings по серьёзности.
2. Предскажите результаты двух последовательных вызовов без overrides.
3. Учтите случай caller-owned `overrides.tags`.
4. Предложите минимальный refactor и API ownership contract.
5. Объясните, почему `Object.freeze(DEFAULT_FILTER)` без других изменений не является полным решением.

#### Критерии самопроверки

- [ ] Outer copy не назван deep copy.
- [ ] Найдены shared `range` и `tags`.
- [ ] Учтена mutation caller-owned input.
- [ ] Исправление копирует только нужные nested boundaries.

### JS-VALUES-EX07

**Разберите coercion puzzle как алгоритм, а не фокус**

- Статус: `approved`
- Раздел: `JavaScript и асинхронное программирование`
- Сложность: `Mid → Senior | prediction | explanation`
- Проверяемые навыки: `abstract equality, ToPrimitive, valueOf, toString, operator +`
- Связанные ID из inventory: `JS-09`, `JS-10`
- Решение: [JS-VALUES-EX07](../../solutions/by-domain/01-javascript-and-async-programming.md#js-values-ex07)

#### Задание

Покажите conversion steps для каждого expression:

```js
[] == false;
[] == ![];
[1] == 1;
({ valueOf: () => 4 }) + 1;
({ toString: () => "4" }) + 1;
```

Затем разберите:

```js
const score = {
  valueOf() {
    return 10;
  },
  toString() {
    return "ten";
  },
};

Number(score);
String(score);
score + 1;
```

Закончите двумя рекомендациями: что этот puzzle проверяет на интервью и почему такой код не является production pattern.

#### Критерии самопроверки

- [ ] `![]` вычислено до loose equality.
- [ ] Object operands проходят `ToPrimitive`.
- [ ] Hints и порядок `valueOf`/`toString` объяснены.
- [ ] Interview knowledge отделено от production guidance.

### JS-VALUES-EX08

**Реализуйте typed normalization boundary**

- Статус: `approved`
- Раздел: `JavaScript и асинхронное программирование`
- Сложность: `Senior | implementation`
- Проверяемые навыки: `explicit coercion, nullish defaulting, validation, stable output types`
- Связанные ID из inventory: `JS-06`, `JS-07`, `JS-08`, `JS-10`, `JS-40`
- Решение: [JS-VALUES-EX08](../../solutions/by-domain/01-javascript-and-async-programming.md#js-values-ex08)

#### Задание

Реализуйте `normalizeSearchParams(raw)` для object с возможными полями:

- `page`: отсутствует/nullish или canonical positive integer string;
- `limit`: отсутствует/nullish или canonical integer string от `1` до `100`;
- `query`: отсутствует/nullish или string; пустая string допустима;
- `exact`: отсутствует/nullish или boolean; `false` допустим.

Defaults: `{ page: 1, limit: 20, query: "", exact: false }`.

Требования:

- не принимайте whitespace, fractions, signs, exponent notation, infinities или unsafe integers для numeric fields;
- не используйте truthiness как validation;
- returned object содержит стабильные types `number`, `number`, `string`, `boolean`;
- не мутируйте `raw`;
- добавьте table-driven tests минимум для 8 случаев.

#### Критерии самопроверки

- [ ] Nullish defaults не уничтожают `""` и `false`.
- [ ] Numeric grammar проверена отдельно от representable range.
- [ ] Ошибка указывает конкретное поле.
- [ ] Tests включают boundary values и invalid types.

### JS-VALUES-EX09

**Реализуйте domain-aware дедупликацию readings**

- Статус: `approved`
- Раздел: `JavaScript и асинхронное программирование`
- Сложность: `Senior | implementation | trade-off`
- Проверяемые навыки: `SameValueZero, Object.is, identity, domain keys`
- Связанные ID из inventory: `JS-07`, `JS-09`
- Решение: [JS-VALUES-EX09](../../solutions/by-domain/01-javascript-and-async-programming.md#js-values-ex09)

#### Задание

Реализуйте две функции:

```js
dedupeReadings(values); // SameValueZero semantics
dedupeSignedReadings(values); // NaN equal, +0 and -0 distinct
```

Обе должны сохранять порядок первого появления. Затем расширьте reasoning для objects `{ sensorId, value }`: одинаковыми считаются readings с тем же `sensorId` и value по signed semantics.

Добавьте tests для repeated `NaN`, `0`, `-0`, strings, repeated object identity и разных objects с одинаковыми полями. Обоснуйте сложность и выбранную key/comparator strategy.

#### Критерии самопроверки

- [ ] SameValueZero version не переизобретает `Set` без причины.
- [ ] Signed version различает zero через `Object.is` или явный key.
- [ ] Structural domain rule не перепутана с object identity.
- [ ] Порядок первого появления сохранён.

### JS-VALUES-EX10

**Интервью-задача — стабилизируйте checkout boundary**

- Статус: `approved`
- Раздел: `JavaScript и асинхронное программирование`
- Сложность: `Senior | комплексная задача`
- Проверяемые навыки: `identity, coercion, equality, defaults, numeric safety, code review, communication`
- Связанные ID из inventory: `JS-05`, `JS-06`, `JS-07`, `JS-08`, `JS-09`, `JS-10`, `JS-11`, `JS-40`
- Решение: [JS-VALUES-EX10](../../solutions/by-domain/01-javascript-and-async-programming.md#js-values-ex10)

#### Задание

```js
const DEFAULT_ORDER = {
  quantity: 1,
  coupon: { code: null, discountPercent: 0 },
};

function prepareOrder(raw) {
  const order = { ...DEFAULT_ORDER, ...raw };

  order.quantity = order.quantity || 1;
  order.coupon.discountPercent = Number(
    order.coupon?.discountPercent || 0,
  );

  const subtotal = Number(order.unitPrice) * order.quantity;
  const discount = subtotal * (order.coupon.discountPercent / 100);
  order.total = subtotal - discount;

  if (order.total == raw.expectedTotal) {
    return order;
  }

  throw new Error("total mismatch");
}
```

Контракт продукта:

- `unitPrice` и `expectedTotal` приходят как decimal strings с ровно двумя знаками;
- `quantity` — positive safe integer string;
- coupon отсутствует/nullish либо содержит code и integer percent `0..100`;
- функция не должна мутировать defaults или caller-owned nested objects;
- result должен использовать integer cents и stable types.

Выполните полный review:

1. Нарисуйте identities и найдите shared mutation.
2. Найдите coercion, defaulting, optional chaining, equality и floating-point defects.
3. Предложите validation/normalization pipeline.
4. Реализуйте исправленную функцию и focused tests.
5. Ранжируйте findings по риску.
6. Дайте трёхминутное интервью-объяснение: mental model → bugs → production design → trade-offs.

#### Критерии самопроверки

- [ ] Не осталось implicit numeric coercion на business boundary.
- [ ] Money хранится и сравнивается в integer cents.
- [ ] Все nested values имеют ясное ownership.
- [ ] `0`, empty/missing и invalid input различаются по contract.
- [ ] Сравнение результата использует подходящую semantics.
- [ ] Объяснение не называет JavaScript pass-by-reference.

## 1.3. Функции, замыкания и функциональные паттерны

Последовательность: **воспроизведение по памяти → прогнозирование → объяснение → отладка → ревью кода → реализация → комплексная задача**.

### JS-FUNCTIONS-EX01

**Восстановите карту функций по памяти**

- Статус: `approved`
- Раздел: `JavaScript и асинхронное программирование`
- Сложность: `Junior | воспроизведение по памяти`
- Проверяемые навыки: `терминология, формы функций, параметры, вызов`
- Связанные ID из inventory: `JS-12`, `JS-13`, `JS-14`, `JS-19`
- Решение: [JS-FUNCTIONS-EX01](../../solutions/by-domain/01-javascript-and-async-programming.md#js-functions-ex01)

#### Задание

Не заглядывая в handbook, составьте:

1. таблицу для объявления функции, анонимного и именованного выражений и стрелочной функции;
2. определения функции первого класса, колбэка и функции высшего порядка;
3. таблицу для параметра, аргумента, значения по умолчанию, остаточного параметра, `arguments` и `fn.length`;
4. четыре формы вызова обычной функции и источник `this` в каждой;
5. по одному предложению о замыкании, чистой функции, каррировании и частичном применении.

#### Ограничения

- 10 минут.
- Не используйте формулировку «стрелочная функция — это короткая обычная функция».
- Не используйте формулировку «замыкание копирует переменные».

#### Критерии самопроверки

- [ ] Указаны момент создания, наличие собственных `this` и `arguments`, а также возможность вызова через `new`.
- [ ] Колбэк описан через контракт.
- [ ] `call/apply` отделены от `bind`.
- [ ] Замыкание описано через живую привязку.

### JS-FUNCTIONS-EX02

**Предскажите результат, ошибки и арность**

- Статус: `approved`
- Раздел: `JavaScript и асинхронное программирование`
- Сложность: `Junior → Mid | прогнозирование`
- Проверяемые навыки: `момент создания функций, именованное выражение, значения по умолчанию, arguments, length`
- Связанные ID из inventory: `JS-12`, `JS-19`
- Решение: [JS-FUNCTIONS-EX02](../../solutions/by-domain/01-javascript-and-async-programming.md#js-functions-ex02)

#### Задание

Рассматривайте фрагменты независимо:

#### A

```js
console.log(run());
function run() {
  return "ready";
}
```

#### B

```js
console.log(run());
let run = function () {
  return "late";
};
```

#### C

```js
const fn = function inside() {
  return typeof inside;
};
console.log(fn(), typeof inside);
```

#### D

```js
let seed = 0;
function next(id = ++seed, copy = id) {
  return [id, copy, seed];
}
console.log(next(), next(10), next(undefined, 20));
```

#### E

```js
function inspect(a, b = 2, ...rest) {
  return [inspect.length, arguments.length, rest.length];
}
console.log(inspect("A", "B", "C", "D"));
```

Для каждого до запуска запишите результат или ошибку и правило, которое к ним приводит.

#### Критерии самопроверки

- [ ] `ReferenceError` и `TypeError` не перепутаны.
- [ ] Вычисление значений по умолчанию прослежено слева направо.
- [ ] `length`, `arguments.length` и длина остаточного параметра не смешаны.

### JS-FUNCTIONS-EX03

**Нарисуйте привязки и идентичности объектов в замыкании**

- Статус: `approved`
- Раздел: `JavaScript и асинхронное программирование`
- Сложность: `Mid | объяснение`
- Проверяемые навыки: `лексический захват, мутация, переназначение, общее состояние`
- Связанные ID из inventory: `JS-15`, `JS-21`
- Решение: [JS-FUNCTIONS-EX03](../../solutions/by-domain/01-javascript-and-async-programming.md#js-functions-ex03)

#### Задание

```js
function createStore() {
  let state = { version: 0 };

  return {
    mutate() {
      state.version += 1;
    },
    replace() {
      state = { version: 10 };
    },
    snapshot() {
      return state;
    },
  };
}

const store = createStore();
const first = store.snapshot();
store.mutate();
const second = store.snapshot();
store.replace();
const third = store.snapshot();
```

Нарисуйте привязку `state` и идентичности объектов после каждого шага. Предскажите результаты сравнений и значения `version`. Затем добавьте метод, который возвращает неизменяемый снимок текущего состояния верхнего уровня, и объясните ограничение поверхностной копии.

### JS-FUNCTIONS-EX04

**Исправьте ошибку замыкания в цикле тремя способами**

- Статус: `approved`
- Раздел: `JavaScript и асинхронное программирование`
- Сложность: `Mid | debugging`
- Проверяемые навыки: `привязка var, отдельный let на итерацию, снимок через фабрику`
- Связанные ID из inventory: `JS-15`
- Решение: [JS-FUNCTIONS-EX04](../../solutions/by-domain/01-javascript-and-async-programming.md#js-functions-ex04)

#### Задание

```js
const handlers = [];

for (var index = 0; index < 3; index += 1) {
  handlers.push(() => index);
}
```

1. Объясните `[3,3,3]` через привязки.
2. Исправьте через `let`.
3. Исправьте, сохранив `var`, через фабрику или IIFE.
4. Исправьте через API перебора, если стиль проекта это допускает.
5. Сравните читаемость вариантов и ценность старого решения для поддержки legacy-кода.

### JS-FUNCTIONS-EX05

**Диагностируйте потерю контекста и идентичность при очистке**

- Статус: `approved`
- Раздел: `JavaScript и асинхронное программирование`
- Сложность: `Mid | debugging`
- Проверяемые навыки: `this, call/apply/bind, стабильная идентичность колбэка`
- Связанные ID из inventory: `JS-13`, `JS-16`, `JS-17`
- Решение: [JS-FUNCTIONS-EX05](../../solutions/by-domain/01-javascript-and-async-programming.md#js-functions-ex05)

#### Задание

```js
const controller = {
  count: 0,
  onClick(step) {
    this.count += step;
  },
  mount(button) {
    button.addEventListener(
      "click",
      this.onClick.bind(this, 1),
    );
  },
  unmount(button) {
    button.removeEventListener(
      "click",
      this.onClick.bind(this, 1),
    );
  },
};
```

1. Найдите ошибку идентичности функции.
2. Покажите эквивалентный разовый вызов через `call` и `apply`.
3. Исправьте `mount` и `unmount`, сохранив одну ссылку на привязанную функцию.
4. Покажите альтернативный стрелочный адаптер и сравните, что он захватывает.
5. Сделайте очистку идемпотентной.

### JS-FUNCTIONS-EX06

**Проведите ревью контракта колбэка и функции высшего порядка**

- Статус: `approved`
- Раздел: `JavaScript и асинхронное программирование`
- Сложность: `Mid | ревью кода`
- Проверяемые навыки: `сигнатура колбэка, момент вызова, ошибки, побочные эффекты`
- Связанные ID из inventory: `JS-14`, `JS-21`
- Решение: [JS-FUNCTIONS-EX06](../../solutions/by-domain/01-javascript-and-async-programming.md#js-functions-ex06)

#### Задание

```js
function processRows(rows, transform) {
  return rows.map(transform);
}

const ids = processRows(["10", "20", "30"], parseInt);

function withAudit(operation) {
  return (input) => {
    auditLog.push(input);
    return operation(input);
  };
}
```

Найдите ошибку сигнатуры и скрытый побочный эффект. Полностью опишите контракт колбэка `processRows`. Переработайте код так, чтобы основание системы счисления и зависимость аудита были явными. Решите, должен ли аудит выполняться до или после операции и что делать при исключении.

### JS-FUNCTIONS-EX07

**Исправьте проблему удержания памяти**

- Статус: `approved`
- Раздел: `JavaScript и асинхронное программирование`
- Сложность: `Mid → Senior | диагностика производительности`
- Проверяемые навыки: `цепочка удержания, минимальный захват, очистка обработчика и таймера`
- Связанные ID из inventory: `JS-15`
- Решение: [JS-FUNCTIONS-EX07](../../solutions/by-domain/01-javascript-and-async-programming.md#js-functions-ex07)

#### Задание

```js
function mountPanel(button, response) {
  const onClick = () => renderTitle(response.page.title);
  button.addEventListener("click", onClick);

  const timer = setInterval(
    () => refresh(response.session),
    1000,
  );
}
```

`response` содержит большой граф объектов. Панель многократно монтируется и размонтируется.

1. Нарисуйте цепочки удержания.
2. Верните идемпотентную функцию очистки.
3. Захватите только нужные значения.
4. Объясните, когда извлечение поля не уменьшит удерживаемый граф.
5. Опишите план проверки с помощью снимков кучи.

### JS-FUNCTIONS-EX08

**Реализуйте фабрику на замыкании с закрытым состоянием**

- Статус: `approved`
- Раздел: `JavaScript и асинхронное программирование`
- Сложность: `Mid | implementation`
- Проверяемые навыки: `фабрика, инкапсуляция, общие замыкания, проверка данных`
- Связанные ID из inventory: `JS-14`, `JS-15`, `JS-19`
- Решение: [JS-FUNCTIONS-EX08](../../solutions/by-domain/01-javascript-and-async-programming.md#js-functions-ex08)

#### Задание

Реализуйте `createTokenBucket({ capacity, refill })`:

- закрытое целочисленное состояние `tokens` начинается со значения `capacity`;
- `take(count = 1)` выполняется как одна неделимая операция и возвращает логическое значение успеха;
- `add(count = refill)` не позволяет состоянию превысить `capacity`;
- `read()` возвращает снимок текущего состояния;
- `reset()` возвращает начальное состояние;
- недопустимая конфигурация или количество приводит к исключению;
- два созданных контейнера не разделяют состояние.

Добавьте точечные тесты и объясните жизненный цикл замыкания.

### JS-FUNCTIONS-EX09

**Реализуйте ограниченную мемоизацию**

- Статус: `approved`
- Раздел: `JavaScript и асинхронное программирование`
- Сложность: `Senior | реализация + производительность`
- Проверяемые навыки: `мемоизация, идентичность ключей Map, LRU, жизненный цикл кеша`
- Связанные ID из inventory: `JS-15`, `JS-21`
- Решение: [JS-FUNCTIONS-EX09](../../solutions/by-domain/01-javascript-and-async-programming.md#js-functions-ex09)

#### Задание

Реализуйте `memoizeUnary(operation, { maxSize })`:

- `maxSize` — положительное целое число;
- попадание в кеш корректно работает и для результата `undefined`;
- попадание обновляет давность использования записи;
- при переполнении удаляется ключ, использованный раньше всех остальных;
- наружу доступны `clear()` и `size()` только для чтения, но сам `Map` не раскрывается;
- синхронное исключение не кэшируется.

Добавьте тесты для примитивов, идентичности объектов, удаления старой записи и `undefined`. Отдельно обсудите политику для промисов, отклонений и TTL.

### JS-FUNCTIONS-EX10

**Реализуйте частичное применение и конвейер**

- Статус: `approved`
- Раздел: `JavaScript и асинхронное программирование`
- Сложность: `Mid | implementation`
- Проверяемые навыки: `частичное применение, порядок композиции, чистые этапы`
- Связанные ID из inventory: `JS-20`, `JS-21`
- Решение: [JS-FUNCTIONS-EX10](../../solutions/by-domain/01-javascript-and-async-programming.md#js-functions-ex10)

#### Задание

1. Реализуйте `partial(operation, ...preset)`.
2. Реализуйте `pipe(...operations)`.
3. Соберите конвейер `сырые данные пользователя → проверка → нормализация → модель представления`.
4. Оставьте этапы чистыми и именованными.
5. Добавьте тест, который ловит обратный порядок.
6. Объясните, почему автоматическое каррирование по `fn.length` не входит в решение.

### JS-FUNCTIONS-EX11

**Выберите безопасный подход для рабочего кода**

- Статус: `approved`
- Раздел: `JavaScript и асинхронное программирование`
- Сложность: `Senior | архитектура + ревью кода`
- Проверяемые навыки: `формы функций, контекст, замыкания, чистота, компромиссы`
- Связанные ID из inventory: `JS-12`, `JS-13`, `JS-14`, `JS-15`, `JS-16`, `JS-17`, `JS-21`
- Решение: [JS-FUNCTIONS-EX11](../../solutions/by-domain/01-javascript-and-async-programming.md#js-functions-ex11)

#### Задание

Для каждого сценария выберите решение и обоснуйте его:

1. Колбэк форматирования цены без состояния.
2. Метод DOM-контроллера, который многократно регистрируется и снимается.
3. Настроенный валидатор с неизменяемыми правилами.
4. Кеш с жизненным циклом одного запроса.
5. Большая общая модель, из которой нужна только одна подпись.
6. Конвейер с проверкой данных, вводом-выводом и аналитикой.

Для каждого укажите форму функции, зависимости и `this`, захваченное состояние, жизненный цикл идентичности функции, побочные эффекты и тесты. Не предлагайте один паттерн для всех случаев.

### JS-FUNCTIONS-EX12

**Интегрированная интервью-задача — стабилизируйте контроллер данных**

- Статус: `approved`
- Раздел: `JavaScript и асинхронное программирование`
- Сложность: `Senior | комплексная задача`
- Проверяемые навыки: `формы функций, параметры, колбэки, this/bind, замыкания, память, мемоизация, чистота, композиция, объяснение решения`
- Связанные ID из inventory: `JS-12`, `JS-13`, `JS-14`, `JS-15`, `JS-16`, `JS-17`, `JS-18`, `JS-19`, `JS-20`, `JS-21`
- Решение: [JS-FUNCTIONS-EX12](../../solutions/by-domain/01-javascript-and-async-programming.md#js-functions-ex12)

#### Задание

```js
function createController({
  button,
  fetchUsers,
  config = { prefix: "user" },
}) {
  const cache = new Map();
  let latestResponse;

  const normalize = (user) => {
    user.label = config.prefix + ":" + user.name.trim();
    analytics.track("normalized", user.id);
    return user;
  };

  return {
    async load(id, transform = this.normalize) {
      if (cache.has(id)) return cache.get(id);
      latestResponse = await fetchUsers(id);
      const result = latestResponse.users.map(transform);
      cache.set(id, result);
      return result;
    },
    normalize,
    mount() {
      button.addEventListener("click", this.load.bind(this, "current"));
    },
    unmount() {
      button.removeEventListener("click", this.load.bind(this, "current"));
    },
    readLatest: () => latestResponse,
  };
}
```

Проведите полное ревью и переработайте решение:

1. ошибка контекста и параметра по умолчанию;
2. сигнатура колбэка и контракт асинхронных ошибок;
3. мутация данных вызывающего кода и побочный эффект аналитики;
4. идентичность обработчика и очистка;
5. удерживаемый граф ответа;
6. неограниченный кеш и устаревание данных;
7. чистый именованный конвейер преобразований;
8. точечные тесты;
9. двухминутное объяснение в формате интервью;
10. обозначьте, что прототипы и классы остаются за границей 1.3.

#### Критерии самопроверки

- [ ] `load` работает как отделённая функция или контракт явно запрещает такой вызов.
- [ ] Обработчик удаляется по той же ссылке.
- [ ] Кеш ограничен или имеет короткую область жизни и очищается.
- [ ] Большой ответ не удерживается без требования продукта.
- [ ] Преобразование не мутирует данные вызывающего кода.
- [ ] Аналитика находится на явной границе побочных эффектов.
- [ ] Значения по умолчанию не маскируют недопустимую конфигурацию.
- [ ] Объяснение включает компромиссы, а не только исправленный код.

## 1.4. `this`, вызов функции и объектная модель

Последовательность: **воспроизведение по памяти → прогнозирование → объяснение → отладка → ревью кода → реализация → комплексная задача**.

### JS-OBJECTS-EX01

**Восстановите карту объектной модели по памяти**

- Статус: `approved`
- Раздел: `JavaScript и асинхронное программирование`
- Сложность: `Junior → Mid | воспроизведение по памяти`
- Проверяемые навыки: `this, способы создания объектов, прототипы, свойства, дескрипторы, уровни целостности, Proxy`
- Связанные ID из inventory: `JS-23`, `JS-24`, `JS-25`, `JS-26`, `JS-27`, `JS-28`, `JS-39`
- Решение: [JS-OBJECTS-EX01](../../solutions/by-domain/01-javascript-and-async-programming.md#js-objects-ex01)

#### Задание

Не заглядывая в handbook, за 15 минут составьте одну карту, в которой есть:

1. четыре способа определить `this` у обычной функции и отдельное правило для стрелочной функции;
2. различия между `call`, `apply` и `bind`, включая предварительно связанные аргументы и вызов связанной функции через `new`;
3. сравнение объектного литерала, фабрики, функции-конструктора, `Object.create` и класса;
4. связь между функцией-конструктором, её свойством `.prototype`, внутренним `[[Prototype]]` экземпляра и цепочкой прототипов;
5. две независимые оси свойств: собственные/унаследованные и перечислимые/неперечислимые;
6. поля дескриптора данных (data descriptor) и дескриптора доступа (accessor descriptor);
7. матрица `preventExtensions` / `seal` / `freeze`;
8. определения исходного объекта (target), обработчика (handler), перехватчика (trap) и получателя (receiver) для `Proxy`.

#### Ограничения

- Не используйте формулировку «класс создаёт другую модель наследования».
- Не называйте `.prototype` функции прототипом самой функции.
- Не называйте перечисляемость приватностью.
- Отметьте `__proto__` как устаревший accessor, а не как синоним `[[Prototype]]`.

#### Критерии самопроверки

- [ ] По карте можно восстановить путь `вызов → this → new → цепочка прототипов → класс`.
- [ ] Указаны явные различия чтения свойства, присваивания и определения собственного свойства.
- [ ] Для `freeze` явно записано слово «поверхностный».
- [ ] `Proxy` описан как отдельный объект с собственной идентичностью.

### JS-OBJECTS-EX02

**Предскажите `this`, аргументы и результат `new`**

- Статус: `approved`
- Раздел: `JavaScript и асинхронное программирование`
- Сложность: `Mid | прогнозирование`
- Проверяемые навыки: `this при вызове метода и явном вызове, лексический this, повторный bind, new`
- Связанные ID из inventory: `JS-23`, `JS-24`
- Решение: [JS-OBJECTS-EX02](../../solutions/by-domain/01-javascript-and-async-programming.md#js-objects-ex02)

#### Задание

Код выполняется в строгом режиме (strict mode). До запуска запишите точный результат каждой строки или тип ошибки и объясните его формой вызова.

```js
"use strict";

function describe(...parts) {
  return [this?.name ?? "none", parts.join("-")];
}

const service = { name: "service", describe };
const detached = service.describe;
const once = describe.bind({ name: "first" }, "A");
const twice = once.bind({ name: "second" }, "B");

console.log(service.describe("I"));
console.log(detached("D"));
console.log(describe.call({ name: "call" }, "X", "Y"));
console.log(describe.apply({ name: "apply" }, ["X", "Y"]));
console.log(twice("C"));

function Widget(name, size) {
  this.name = name;
  this.size = size;
}

const BoundWidget = Widget.bind(
  { name: "ignored" },
  "fixed",
);
const widget = new BoundWidget("large");

console.log(widget.name, widget.size);
console.log(widget instanceof Widget, widget instanceof BoundWidget);

function createPanel() {
  const lexicalOwner = { name: "lexical" };
  return {
    name: "panel",
    regular() {
      return this.name;
    },
    arrow: () => lexicalOwner.name,
  };
}

const panel = createPanel();
console.log(panel.regular(), panel.regular.call({ name: "other" }));
console.log(panel.arrow(), panel.arrow.call({ name: "other" }));
```

Затем ответьте:

1. Почему второй `bind` не заменяет уже связанный `this`?
2. Почему `new` игнорирует связанный объект, но сохраняет предварительно связанный аргумент?
3. Какая из двух функций объекта `panel` подходит для метода, которому нужен получатель, определяемый вызовом (`receiver`)?
4. Как вы передадите `service.describe` как колбэк, если API вызовет его без объекта?

### JS-OBJECTS-EX03

**Нарисуйте создание экземпляров и цепочки прототипов**

- Статус: `approved`
- Раздел: `JavaScript и асинхронное программирование`
- Сложность: `Mid | объяснение + прогнозирование`
- Проверяемые навыки: `new, Object.create, Constructor.prototype, instanceof, new.target, прототип null`
- Связанные ID из inventory: `JS-23`, `JS-24`
- Решение: [JS-OBJECTS-EX03](../../solutions/by-domain/01-javascript-and-async-programming.md#js-objects-ex03)

#### Задание

```js
function Account(name) {
  this.name = name;
}

Account.prototype.kind = "account";
Account.prototype.label = function label() {
  return `${this.kind}:${this.name}`;
};

const first = new Account("Ada");
const second = Object.create(Account.prototype);
Account.call(second, "Lin");

function ReturnsPrimitive() {
  this.ok = true;
  return 42;
}

function ReturnsObject() {
  this.ok = true;
  return { ok: false };
}

const primitiveResult = new ReturnsPrimitive();
const objectResult = new ReturnsObject();
const dictionary = Object.create(null);
dictionary.answer = 42;
```

1. Нарисуйте объекты-функции `Account`, `Account.prototype`, `first`, `second` и связи между ними.
2. Для `first` и `second` перечислите собственные и унаследованные свойства.
3. Предскажите результаты `label()`, `Object.getPrototypeOf`, `isPrototypeOf` и `instanceof`.
4. Объясните результаты `primitiveResult` и `objectResult` через пять шагов `new`.
5. Добавьте проверку `new.target`, которая запрещает вызов `Account` без `new`.
6. Объясните, почему стрелочная функция не подходит вместо `Account`.
7. Сравните словарь `dictionary` с `{}`: `toString`, `constructor`, `hasOwnProperty` и безопасная проверка ключей.
8. Перепишите старый код `value.__proto__ = Account.prototype` через современный API и объясните, почему динамическое изменение прототипа существующего объекта обычно не следует выбирать.
9. Назовите два ограничения `instanceof`, включая разные среды выполнения (realms), и объясните, почему `value.constructor === Account` не является надёжной проверкой типа.

### JS-OBJECTS-EX04

**Проследите поиск свойства, затенение и получателя у setter**

- Статус: `approved`
- Раздел: `JavaScript и асинхронное программирование`
- Сложность: `Mid | прогнозирование + объяснение`
- Проверяемые навыки: `поиск по цепочке прототипов, затенение, чтение и присваивание, получатель getter/setter`
- Связанные ID из inventory: `JS-24`, `JS-27`
- Решение: [JS-OBJECTS-EX04](../../solutions/by-domain/01-javascript-and-async-programming.md#js-objects-ex04)

#### Задание

Код выполняется в строгом режиме:

```js
"use strict";

const base = {
  prefix: "base",
  count: 1,
  get label() {
    return `${this.prefix}:${this.name}`;
  },
  set score(value) {
    this._score = Math.max(0, value);
  },
};

Object.defineProperty(base, "locked", {
  value: 10,
  writable: false,
  enumerable: true,
  configurable: true,
});

const user = Object.create(base);
user.prefix = "user";
user.name = "Ada";
user.count += 1;
user.score = -3;

console.log(user.label);
console.log(user.count, base.count);
console.log(user._score, Object.hasOwn(user, "score"));

delete user.prefix;
console.log(user.label);

user.locked = 20;
```

1. Предскажите вывод до последней строки и ошибку в последней строке.
2. На каждом присваивании укажите, выполняется ли запись в `user`, запись в `base` или вызов setter.
3. Объясните, почему getter и setter найдены в `base`, но получателем и значением `this` внутри них становится `user`.
4. Покажите безопасный способ создать собственное значение `locked` у `user`, не изменяя `base`, и назовите условие, при котором это возможно.
5. Объясните, чем `user.count += 1` отличается от изменения объекта, который хранится в унаследованном свойстве.

### JS-OBJECTS-EX05

**Составьте матрицу обнаружения и перечисления свойств**

- Статус: `approved`
- Раздел: `JavaScript и асинхронное программирование`
- Сложность: `Mid | прогнозирование + выбор API`
- Проверяемые навыки: `собственные и унаследованные, перечисляемые и неперечисляемые свойства, ключи-символы, Object.hasOwn, null prototype`
- Связанные ID из inventory: `JS-26`
- Решение: [JS-OBJECTS-EX05](../../solutions/by-domain/01-javascript-and-async-programming.md#js-objects-ex05)

#### Задание

```js
const token = Symbol("token");
const proto = { inheritedVisible: 1 };

Object.defineProperty(proto, "inheritedHidden", {
  value: 2,
  enumerable: false,
});

const record = Object.create(proto);
record.ownVisible = 3;
Object.defineProperty(record, "ownHidden", {
  value: 4,
  enumerable: false,
});
record[token] = 5;
```

Не запуская код, заполните таблицу результатов для:

- `Object.hasOwn(record, key)`;
- `key in record`;
- `Object.keys`, `Object.values`, `Object.entries`;
- `for...in`;
- `Object.getOwnPropertyNames`;
- `Object.getOwnPropertySymbols`;
- `Reflect.ownKeys`.

Проверьте четыре строковых ключа и `token`. Затем:

1. Напишите функцию, которая возвращает только собственные перечисляемые строковые свойства.
2. Напишите функцию, которая возвращает все собственные ключи, включая неперечисляемые и символы.
3. Покажите безопасную проверку собственного ключа для объекта с `null` prototype и для объекта, который содержит собственное свойство `hasOwnProperty`.
4. Объясните, почему ни неперечисляемость, ни symbol key не дают приватности.

### JS-OBJECTS-EX06

**Найдите ошибки в дескрипторах свойств**

- Статус: `approved`
- Раздел: `JavaScript и асинхронное программирование`
- Сложность: `Mid | debugging`
- Проверяемые навыки: `дескрипторы свойств с данными и accessor-свойств, значения флагов по умолчанию, getter/setter, defineProperty`
- Связанные ID из inventory: `JS-27`
- Решение: [JS-OBJECTS-EX06](../../solutions/by-domain/01-javascript-and-async-programming.md#js-objects-ex06)

#### Задание

Код выполняется в строгом режиме. Рассматривайте фрагменты B и C после исправления предыдущего фрагмента.

```js
"use strict";

const profile = { prefix: "user" };

// A
Object.defineProperty(profile, "name", {
  value: "Ada",
});
profile.name = "Lin";

// B
Object.defineProperty(profile, "displayName", {
  value: "cached",
  get() {
    return `${this.prefix}:${this.name}`;
  },
  enumerable: true,
});

// C
const scorePrototype = {
  set score(value) {
    this._score = Number(value);
  },
  get score() {
    return this._score ?? 0;
  },
};

const row = Object.create(scorePrototype);
row.score = "7";
```

1. Найдите причину ошибки в A и восстановите значения пропущенных флагов.
2. Исправьте A так, чтобы `name` можно было менять, видеть в `Object.keys` и при необходимости переопределять.
3. Объясните, почему B нельзя определить, и создайте корректный дескриптор доступа без скрытого кеша.
4. Предскажите собственные свойства `row`, значение `row.score` и получателя обоих вызовов accessor.
5. Получите и сравните дескрипторы через `Object.getOwnPropertyDescriptor` и `Object.getOwnPropertyDescriptors`.
6. Назовите риск getter с сетевым запросом, логированием или другой неожиданной побочной операцией.

### JS-OBJECTS-EX07

**Исправьте и объясните иерархию классов**

- Статус: `approved`
- Раздел: `JavaScript и асинхронное программирование`
- Сложность: `Mid → Senior | debugging + explanation`
- Проверяемые навыки: `extends, super, методы прототипа, поля, статические элементы, приватная метка`
- Связанные ID из inventory: `JS-25`
- Решение: [JS-OBJECTS-EX07](../../solutions/by-domain/01-javascript-and-async-programming.md#js-objects-ex07)

#### Задание

```js
class Entity {
  static category = "entity";
  #id;

  constructor(id) {
    this.#id = id;
  }

  static hasEntityBrand(value) {
    return #id in value;
  }

  readId() {
    return this.#id;
  }

  describe() {
    return `entity:${this.#id}`;
  }
}

class User extends Entity {
  role = "user";
  onSelect = () => this.describe();

  constructor(id, name) {
    this.name = name;
    super(id);
  }

  describe() {
    return `${super.describe()}:${this.name}`;
  }

  static create(input) {
    return new this(input.id, input.name);
  }
}
```

1. Найдите и исправьте ошибку derived constructor.
2. После исправления сравните расположение и перечисляемость `describe`, `readId`, `role` и `onSelect`.
3. Сравните идентичность `first.describe === second.describe` и `first.onSelect === second.onSelect`.
4. Объясните, почему отделённый `describe` теряет контекст, а отделённый `onSelect` продолжает работать.
5. Предскажите `User.category`, `User.create(...)`, `Entity.hasEntityBrand(user)` и вызов `Entity.prototype.readId.call({})`.
6. Объясните, есть ли у экземпляра `User` закрытое состояние класса `Entity` и может ли код класса `User` обратиться к `#id` напрямую.
7. Покажите закрытый метод и закрытое статическое поле в минимальном дополнении к примеру.
8. Решите, оправдано ли наследование в этом примере, или роли и форматирование лучше собрать композицией.

### JS-OBJECTS-EX08

**Проведите ревью способов создания объектов**

- Статус: `approved`
- Раздел: `JavaScript и асинхронное программирование`
- Сложность: `Mid → Senior | ревью кода + архитектура`
- Проверяемые навыки: `литерал, фабрика, функция-конструктор, Object.create, класс, композиция`
- Связанные ID из inventory: `JS-23`, `JS-24`, `JS-25`
- Решение: [JS-OBJECTS-EX08](../../solutions/by-domain/01-javascript-and-async-programming.md#js-objects-ex08)

#### Задание

Команде нужна модель счётчика с операциями `increment(step)`, `read()` и независимым состоянием каждого экземпляра. В будущем у части счётчиков может появиться отдельная политика проверки шага.

Сравните пять вариантов:

1. один объектный литерал;
2. фабрику с методами, создаваемыми при каждом вызове;
3. функцию-конструктор с общими методами в `.prototype`;
4. `Object.create(counterMethods)`;
5. класс `Counter` с методами прототипа или закрытым полем.

Для каждого варианта ответьте:

- сколько экземпляров удобно создавать;
- где хранится состояние и где находятся методы;
- разделяют ли экземпляры одну функцию-метод;
- как устроены наследование и расширение;
- можно ли скрыть состояние от прямого изменения;
- насколько очевидны `new`, `this` и проверки входных данных;
- как реализовать разные политики через композицию, не строя глубокую иерархию.

Выберите два разумных варианта для рабочего кода и набросайте их API. Не объявляйте фабрику или класс универсально лучшим решением.

### JS-OBJECTS-EX09

**Реализуйте один контракт фабрикой и конструктором**

- Статус: `approved`
- Раздел: `JavaScript и асинхронное программирование`
- Сложность: `Mid | implementation`
- Проверяемые навыки: `замыкание фабрики, функция-конструктор, общие методы прототипа, проверка данных`
- Связанные ID из inventory: `JS-23`, `JS-24`
- Решение: [JS-OBJECTS-EX09](../../solutions/by-domain/01-javascript-and-async-programming.md#js-objects-ex09)

#### Задание

Реализуйте контракт счётчика двумя способами:

```text
createCounter(initial, validateStep?) -> { increment, read }
new Counter(initial, validateStep?)   -> Counter
```

Требования:

- `initial` — safe integer;
- шаг по умолчанию равен `1`, каждый шаг проходит через `validateStep`;
- состояние разных экземпляров независимо;
- фабрика закрывает состояние в замыкании;
- функция-конструктор хранит состояние в экземпляре, а `increment` и `read` находятся в `Counter.prototype`;
- вызов `Counter` без `new` приводит к ясной ошибке через `new.target`;
- методы не создаются заново для каждого экземпляра конструктора;
- добавьте проверки результата, независимости экземпляров, идентичности методов и неправильных аргументов.

После реализации сравните инкапсуляцию и расход памяти. В качестве короткой альтернативы покажите, как тот же контракт на прототипах выглядел бы через класс.

### JS-OBJECTS-EX10

**Исправьте ложную гарантию глубокой неизменяемости**

- Статус: `approved`
- Раздел: `JavaScript и асинхронное программирование`
- Сложность: `Mid | отладка + рабочее решение`
- Проверяемые навыки: `preventExtensions, seal, freeze, поверхностная целостность, общие ссылки`
- Связанные ID из inventory: `JS-28`
- Решение: [JS-OBJECTS-EX10](../../solutions/by-domain/01-javascript-and-async-programming.md#js-objects-ex10)

#### Задание

```js
"use strict";

const defaults = {
  retries: 3,
  theme: {
    palette: {
      accent: "blue",
    },
  },
};

const config = {
  retries: defaults.retries,
  theme: defaults.theme,
};

Object.freeze(config);
config.theme.palette.accent = "red";

console.log(config.theme.palette.accent);
console.log(defaults.theme.palette.accent);
console.log(Object.isFrozen(config));
console.log(Object.isFrozen(config.theme));
```

1. Предскажите четыре строки вывода и нарисуйте общую ссылку.
2. Составьте матрицу допустимых операций для обычного объекта, `preventExtensions`, `seal` и `freeze`: добавление, удаление, изменение дескриптора и изменение существующего значения.
3. Для известной схемы `theme.palette.accent` реализуйте нормализацию, которая создаёт принадлежащие конфигурации вложенные объекты и замораживает каждый уровень.
4. Добавьте проверки `Object.isExtensible`, `Object.isSealed` и `Object.isFrozen` для каждого уровня.
5. Покажите, какие запрещённые операции в строгом режиме приводят к `TypeError`.
6. Объясните, почему `const config`, `Object.freeze(config)` и глубокая неизменяемость дают разные гарантии.
7. Если предложите универсальный `deepFreeze`, опишите работу с циклами, ключами-символами, внешними объектами и стоимостью обхода. Не превращайте задачу в самостоятельную тему копирования данных из 1.5.

### JS-OBJECTS-EX11

**Проведите ревью Proxy и исправьте перенаправление операций**

- Статус: `approved`
- Раздел: `JavaScript и асинхронное программирование`
- Сложность: `Senior | ревью кода + отладка`
- Проверяемые навыки: `получатель, Reflect, инварианты, идентичность, закрытые поля`
- Связанные ID из inventory: `JS-27`, `JS-39`
- Решение: [JS-OBJECTS-EX11](../../solutions/by-domain/01-javascript-and-async-programming.md#js-objects-ex11)

#### Задание

Рассматривайте фрагменты независимо.

```js
const target = {
  _value: 1,
  get value() {
    return this._value;
  },
};

const broken = new Proxy(target, {
  get(currentTarget, key) {
    return currentTarget[key];
  },
});

const child = Object.create(broken);
child._value = 9;

console.log(child.value);
```

```js
"use strict";

const fixedTarget = {};
Object.defineProperty(fixedTarget, "fixed", {
  value: 1,
  writable: false,
  configurable: false,
});

const liar = new Proxy(fixedTarget, {
  set() {
    return true;
  },
});

liar.fixed = 2;
```

```js
class Vault {
  #secret = 42;

  read() {
    return this.#secret;
  }
}

const vault = new Vault();
const wrappedVault = new Proxy(vault, {});
console.log(wrappedVault.read());
```

1. Предскажите результат или ошибку каждого фрагмента.
2. Исправьте `get` через `Reflect.get` и сохраните исходного получателя (`receiver`).
3. Объясните нарушенный инвариант во втором фрагменте и исправьте прозрачную запись через `Reflect.set`.
4. Объясните, почему пустой Proxy не прозрачен для закрытых полей и некоторых объектов с внутренними слотами (internal slots).
5. Оцените обходной путь с автоматическим `bind` методов к исходному объекту: идентичность функций, наследование, getter и ожидаемый `this`.
6. Перечислите последствия `proxy !== target` для `Map`, `Set`, `WeakMap`, сравнения и отладки.
7. Решите, где явная обёртка или дескриптор будет понятнее Proxy.

### JS-OBJECTS-EX12

**Реализуйте отзывной проверяемый фасад настроек**

- Статус: `approved`
- Раздел: `JavaScript и асинхронное программирование`
- Сложность: `Senior | implementation`
- Проверяемые навыки: `Proxy.revocable, проверка данных в перехватчиках, Reflect, контракты`
- Связанные ID из inventory: `JS-39`
- Решение: [JS-OBJECTS-EX12](../../solutions/by-domain/01-javascript-and-async-programming.md#js-objects-ex12)

#### Задание

Реализуйте:

```text
createSettingsView(target, schema) -> { proxy, revoke }
```

Контракт:

- `schema` содержит функции проверки разрешённых строковых ключей;
- чтение и стандартное перечисление прозрачно передаются целевому объекту;
- запись неизвестного ключа приводит к `TypeError`;
- значение, не прошедшее проверку, приводит к `TypeError`;
- удаление ключа из schema запрещено, а удаление другого существующего ключа передаётся целевому объекту;
- перехватчики возвращают результат подходящей операции `Reflect`, а не безусловный `true`;
- после `revoke()` любая операция через proxy приводит к `TypeError`;
- исходный объект и Proxy являются разными объектами.

Добавьте проверки успешной записи, двух отказов, `Object.keys`, удаления, отзыва и идентичности. Укажите временную сложность одной операции при условии, что доступ к правилу schema выполняется за `O(1)`.

### JS-OBJECTS-EX13

**Выберите понятный подход к объектной модели для рабочего кода**

- Статус: `approved`
- Раздел: `JavaScript и асинхронное программирование`
- Сложность: `Senior | архитектура + ревью кода`
- Проверяемые навыки: `способы создания, композиция, наследование, дескрипторы, компромиссы Proxy`
- Связанные ID из inventory: `JS-23`, `JS-24`, `JS-25`, `JS-26`, `JS-27`, `JS-28`, `JS-39`
- Решение: [JS-OBJECTS-EX13](../../solutions/by-domain/01-javascript-and-async-programming.md#js-objects-ex13)

#### Задание

Для каждого сценария выберите основной подход и обоснуйте его:

1. Один декларативный объект конфигурации без поведения.
2. Много однотипных сущностей с общими методами и проверяемым созданием.
3. Небольшой компонент с закрытым состоянием и двумя функциями управления.
4. Модель с тремя независимыми возможностями, которые комбинируются по-разному.
5. Совместимое свойство, которое должно вычисляться при чтении и не попадать в `Object.keys`.
6. Настройки, которые нельзя расширять, но существующие значения можно менять.
7. Проверка каждой записи на внешней границе, где набор полей определяется во время выполнения.
8. DOM-обработчик, которому нужна стабильная идентичность для последующего удаления.

Для каждого решения укажите:

- объектный литерал, фабрику, функцию-конструктор, `Object.create`, класс, композицию, дескриптор, API целостности, явную обёртку или Proxy;
- где находятся состояние и методы;
- нужен ли динамический `this`;
- как проверяются собственные ключи;
- что произойдёт с перечислением и сериализацией;
- как решение тестировать и отлаживать;
- более простой вариант, который вы отвергли, и причину.

Завершите ответ объяснением выбора одного из сценариев за 30–60 секунд, как на интервью.

### JS-OBJECTS-EX14

**Интегрированная интервью-задача — переработайте модель учётной записи**

- Статус: `approved`
- Раздел: `JavaScript и асинхронное программирование`
- Сложность: `Senior | комплексная задача`
- Проверяемые навыки: `this, прототипы, классы, дескрипторы, перечисление, целостность, ревью Proxy, композиция, объяснение на интервью`
- Связанные ID из inventory: `JS-23`, `JS-24`, `JS-25`, `JS-26`, `JS-27`, `JS-28`, `JS-39`
- Решение: [JS-OBJECTS-EX14](../../solutions/by-domain/01-javascript-and-async-programming.md#js-objects-ex14)

#### Задание

```js
"use strict";

const accountMethods = {
  get label() {
    return `${this.id}:${this.name}`;
  },
  rename(nextName) {
    this.name = nextName;
    this.audit("renamed");
  },
};

function createAccount(input, audit) {
  const account = Object.create(accountMethods);
  Object.assign(account, input);

  Object.defineProperty(account, "id", {
    value: input.id,
  });

  Object.freeze(account);

  return new Proxy(account, {
    get(target, key) {
      return target[key];
    },
    set(target, key, value) {
      target[key] = value;
      return true;
    },
  });
}

function promote(account) {
  Object.setPrototypeOf(account, {
    ...accountMethods,
    canDelete: true,
  });
}

function listFields(account) {
  const result = [];
  for (const key in account) result.push(key);
  return result;
}
```

Контракт продукта:

- `id` — непустая строка, видимая в `Object.keys`, но неизменяемая;
- `name` меняется только через `rename`, после проверки и с аудитом;
- `permissions` нормализуются в новый объект с логическими `read`, `write`, `remove` и не разделяются с входным объектом вызывающего кода;
- набор собственных публичных полей после создания нельзя расширять или сокращать;
- `label` и методы разделяются экземплярами и не перечисляются;
- право удаления определяется данными или отдельной функцией-возможностью, без динамического изменения цепочки прототипов;
- решение должно оставаться понятным в отладчике; Proxy допустим только с доказанной пользой.

Проведите полное ревью и переработайте решение:

1. Найдите проблемы с получателем, флагами дескриптора по умолчанию, перечислением, `freeze`, вложенным изменением, инвариантами Proxy, идентичностью и `Object.setPrototypeOf`.
2. Реализуйте исправленную модель через класс или явную фабрику на прототипах.
3. Сделайте аудит и изменение имени неразделимым публичным контрактом.
4. Обеспечьте поверхностную целостность экземпляра и отдельную целостность `permissions`.
5. Реализуйте возможность удаления композицией.
6. Добавьте точечные проверки собственных ключей, дескрипторов, методов прототипа, закрытого состояния, уровней целостности, общей ссылки, аудита и неправильного ввода.
7. Оцените временную сложность основных операций.
8. Дайте двухминутное объяснение для интервью: mental model → дефекты → выбранное устройство → компромиссы.

#### Критерии самопроверки

- [ ] Изменение `name` нельзя выполнить в обход проверки и аудита.
- [ ] Методы и getters находятся в prototype и не попадают в `Object.keys`.
- [ ] `id` имеет явно заданные флаги дескриптора.
- [ ] `permissions` не разделяет идентичность с входным объектом и заморожен отдельно.
- [ ] Экземпляр нельзя расширить или лишить собственных публичных полей.
- [ ] Нет динамического `Object.setPrototypeOf` и необоснованного Proxy.
- [ ] Проверки различают собственные/унаследованные и перечислимые/неперечислимые свойства.
- [ ] Объяснение сравнивает класс, фабрику и Proxy без лозунга «всегда использовать только один подход».

## 1.5. Arrays, Transformations & Copying

Последовательность: **воспроизведение по памяти → прогнозирование → объяснение → отладка → ревью кода → реализация → комплексная задача**.

### JS-ARRAYS-EX01

**Восстановите карту массивов и копирования по памяти**

- Статус: `approved`
- Раздел: `JavaScript и асинхронное программирование`
- Сложность: `Junior → Mid | воспроизведение по памяти`
- Проверяемые навыки: `length, пустые слоты, мутирующие/копирующие API, преобразования, функция сравнения, поверхностная/глубокая копия`
- Связанные ID из inventory: `JS-29`, `JS-30`, `JS-31`, `JS-32`, `JS-33`, `JS-34`
- Решение: [JS-ARRAYS-EX01](../../solutions/by-domain/01-javascript-and-async-programming.md#js-arrays-ex01)

#### Задание

Не заглядывая в handbook, за 15 минут создайте одну карту:

1. массив как indexed properties + `length`;
2. плотный / разреженный массив / пустой слот / явный `undefined`;
3. матрица `push`, `pop`, `shift`, `unshift`, `splice`, `sort`, `reverse`, `slice`, `concat`, spread, `toSorted`, `toSpliced`, `toReversed`, `with`;
4. выбор `map`, `filter`, `find`, `some`, `every`, `forEach`, `reduce`;
5. договор функции сравнения;
6. значения по умолчанию при деструктуризации, rest и три контекста spread;
7. схема идентичностей после поверхностной копии;
8. структурное разделение;
9. договор глубокой копии, `structuredClone`, перенос и ловушки JSON.

#### Критерии самопроверки

- [ ] Для каждого метода указаны mutation и return value.
- [ ] Поведение разреженного массива не сведено к одному универсальному правилу.
- [ ] Defaults включаются для `undefined`, но не для `null`.
- [ ] Новый контейнер не назван глубокой копией.
- [ ] `structuredClone` не обещает сохранить поведение пользовательского класса.

### JS-ARRAYS-EX02

**Предскажите `length`, пустые слоты и наличие свойств**

- Статус: `approved`
- Раздел: `JavaScript и асинхронное программирование`
- Сложность: `Junior → Mid | прогнозирование`
- Проверяемые навыки: `индексы массива, length, пустые слоты, delete, splice, собственные свойства`
- Связанные ID из inventory: `JS-29`, `JS-31`
- Решение: [JS-ARRAYS-EX02](../../solutions/by-domain/01-javascript-and-async-programming.md#js-arrays-ex02)

#### Задание

```js
const values = new Array(2);
values[4] = "e";
values["01"] = "padded";
values.note = "draft";

console.log(values.length);
console.log(0 in values, 2 in values, 4 in values);
console.log(Object.hasOwn(values, 1));
console.log(Object.keys(values));

delete values[4];
console.log(values.length, 4 in values);

values[3] = undefined;
console.log(values[3], 3 in values);

values.length = 1;
console.log(values.length);
console.log(3 in values);
console.log(values["01"], values.note);
```

1. Предскажите каждую строку.
2. Нарисуйте существующие свойства после каждого этапа.
3. Замените `delete` операцией, которая удаляет позицию последовательности со сдвигом.
4. Объясните разницу между увеличением и уменьшением `length`.

### JS-ARRAYS-EX03

**Выберите метод по возвращаемому контракту**

- Статус: `approved`
- Раздел: `JavaScript и асинхронное программирование`
- Сложность: `Junior → Mid | объяснение`
- Проверяемые навыки: `map, filter, find, some, every, forEach, reduce, loop`
- Связанные ID из inventory: `JS-30`
- Решение: [JS-ARRAYS-EX03](../../solutions/by-domain/01-javascript-and-async-programming.md#js-arrays-ex03)

#### Задание

Для каждого требования выберите один основной инструмент и обоснуйте возвращаемый договор, ранний выход и допустимые побочные эффекты:

1. создать display label для каждого пользователя;
2. оставить пользователей с доступом;
3. найти первого заблокированного;
4. узнать, есть ли администратор;
5. проверить, что все записи имеют ID;
6. отправить синхронную метрику по каждой записи;
7. получить сумму;
8. построить индекс с двумя счётчиками и возможностью немедленно завершить работу при ошибке;
9. последовательно выполнить асинхронную операцию для каждого элемента.

Отдельно объясните, почему `reduce` и цепочка methods не обязаны быть лучшим ответом для пунктов 8–9.

### JS-ARRAYS-EX04

**Проследите мутацию и возвращаемые значения**

- Статус: `approved`
- Раздел: `JavaScript и асинхронное программирование`
- Сложность: `Mid | прогнозирование + отладка`
- Проверяемые навыки: `push/pop/splice/sort/reverse, идентичность, владение`
- Связанные ID из inventory: `JS-29`, `JS-32`
- Решение: [JS-ARRAYS-EX04](../../solutions/by-domain/01-javascript-and-async-programming.md#js-arrays-ex04)

#### Задание

```js
const row = { id: 1 };
const input = [row, { id: 3 }, { id: 2 }];

const pushed = input.push({ id: 4 });
const removed = input.splice(1, 1);
const sorted = input.sort((a, b) => a.id - b.id);
const reversed = input.reverse();
const popped = input.pop();

console.log(pushed);
console.log(removed.map((item) => item.id));
console.log(sorted === input, reversed === input);
console.log(popped.id);
console.log(input.map((item) => item.id));
console.log(input[1] === row);
```

1. Предскажите вывод по шагам.
2. Укажите, какие references копировались или перемещались.
3. Перепишите конвейер так, чтобы исходный `input` остался неизменным.
4. Сформулируйте имя для варианта, который намеренно меняет принадлежащий ему массив.

### JS-ARRAYS-EX05

**Постройте матрицу поведения разреженного массива фактическим экспериментом**

- Статус: `approved`
- Раздел: `JavaScript и асинхронное программирование`
- Сложность: `Mid | эксперимент + объяснение`
- Проверяемые навыки: `пустые слоты, callbacks, slice, spread, API семейства Change Array by Copy`
- Связанные ID из inventory: `JS-30`, `JS-31`
- Решение: [JS-ARRAYS-EX05](../../solutions/by-domain/01-javascript-and-async-programming.md#js-arrays-ex05)

#### Задание

Для `const source = [1, , undefined, 4]` до запуска предскажите, затем фактически проверьте:

- посещённые `(index, value)` у `map`, `filter`, `forEach`, `find`, `some`, `every`, `reduce`;
- длину и `Object.hasOwn(result, index)` для `map`, `filter`, `slice`, spread, `Array.from`, `toSorted`, `toSpliced(0, 0)`, `toReversed`, `with(0, 9)`;
- расположение пустых слотов и явных `undefined` после `sort` и `toSorted`.

Не модифицируйте `Array.prototype`. Оформите результат как компактную таблицу и сформулируйте три правила, не обобщая их на все методы.

### JS-ARRAYS-EX06

**Исправьте ловушки callback**

- Статус: `approved`
- Раздел: `JavaScript и асинхронное программирование`
- Сложность: `Mid | отладка`
- Проверяемые навыки: `результат callback, map/forEach, filter(Boolean), аккумулятор reduce`
- Связанные ID из inventory: `JS-30`
- Решение: [JS-ARRAYS-EX06](../../solutions/by-domain/01-javascript-and-async-programming.md#js-arrays-ex06)

#### Задание

```js
function normalizeReadings(readings) {
  const numeric = readings
    .filter(Boolean)
    .map((value) => {
      Number(value);
    });

  const total = numeric.reduce((sum, value) => {
    sum + value;
  });

  const logged = numeric.map((value) => console.log(value));

  return { numeric, total, logged };
}
```

Договор: `0` — допустимое чтение; `null`/`undefined` удаляются; числовые строки преобразуются; нечисловые значения отклоняются; пустой вход даёт сумму `0`; логирование — побочный эффект без массива результата.

1. Найдите все defects.
2. Перепишите функцию с ясными стадиями.
3. Решите, нужен ли здесь `reduce` или обычный цикл.
4. Добавьте проверки для `0`, `"2"`, `null`, `"oops"` и `[]`.

### JS-ARRAYS-EX07

**Диагностируйте изменение коллекции и асинхронный callback**

- Статус: `approved`
- Раздел: `JavaScript и асинхронное программирование`
- Сложность: `Mid | прогнозирование + debugging`
- Проверяемые навыки: `фиксированная граница обхода, удаление, shift, договор асинхронного callback`
- Связанные ID из inventory: `JS-30`, `JS-31`
- Решение: [JS-ARRAYS-EX07](../../solutions/by-domain/01-javascript-and-async-programming.md#js-arrays-ex07)

#### Задание

```js
const values = [1, 2, 3, 4];
const seen = [];

values.forEach((value, index) => {
  seen.push(value);
  if (index === 0) values.shift();
  if (index === 1) values.push(5);
});

async function persistAll(items) {
  items.forEach(async (item) => {
    await persist(item);
  });
  return "saved";
}
```

1. Предскажите `seen` и финальный `values`.
2. Объясните исходную границу обхода и смещение индексов.
3. Перепишите удаление без mutation во время обхода.
4. Исправьте `persistAll` для последовательного контракта.
5. Покажите только shape параллельного варианта и назовите отложенные вопросы координации.

### JS-ARRAYS-EX08

**Исправьте функцию сравнения и реализуйте сортировку по нескольким полям**

- Статус: `approved`
- Раздел: `JavaScript и асинхронное программирование`
- Сложность: `Mid → Senior | debugging + implementation`
- Проверяемые навыки: `согласованная функция сравнения, стабильная сортировка, локаль, toSorted`
- Связанные ID из inventory: `JS-32`
- Решение: [JS-ARRAYS-EX08](../../solutions/by-domain/01-javascript-and-async-programming.md#js-arrays-ex08)

#### Задание

```js
function rankUsers(users) {
  return users.sort((a, b) => a.score < b.score);
}
```

Требуется: вход не меняется; score по убыванию; при равенстве name по `en` без учёта регистра; полностью равные ключи сохраняют входной порядок.

1. Объясните дефект функции сравнения, возвращающей boolean.
2. Реализуйте исправление через `toSorted` и один переиспользуемый `Intl.Collator`.
3. Добавьте тесты равенства, обратных пар, transitivity и стабильного tie.
4. Объясните, почему нельзя обещать конкретный sorting algorithm или универсальную complexity.

### JS-ARRAYS-EX09

**Перепишите мутацию через копирующие API**

- Статус: `approved`
- Раздел: `JavaScript и асинхронное программирование`
- Сложность: `Mid | refactoring`
- Проверяемые навыки: `toSorted, toSpliced, toReversed, with, RangeError`
- Связанные ID из inventory: `JS-29`, `JS-32`
- Решение: [JS-ARRAYS-EX09](../../solutions/by-domain/01-javascript-and-async-programming.md#js-arrays-ex09)

#### Задание

Перепишите без mutation входа:

```js
function prepare(items, index, replacement) {
  items[index] = replacement;
  items.splice(0, 1);
  items.reverse();
  items.sort((a, b) => a.rank - b.rank);
  return items;
}
```

1. Используйте `with`, `toSpliced`, `toReversed`, `toSorted`.
2. Сформулируйте поведение для пустого массива и индекса вне диапазона.
3. Покажите legacy-compatible вариант через `slice`/spread.
4. Оцените число временных массивов и предложите ясный локально мутирующий вариант для доказанного горячего пути.

### JS-ARRAYS-EX10

**Разберите деструктуризацию, rest и spread по контекстам**

- Статус: `approved`
- Раздел: `JavaScript и асинхронное программирование`
- Сложность: `Mid | прогнозирование + объяснение`
- Проверяемые навыки: `значения по умолчанию, вложенные шаблоны, rest, spread массива/вызова/объекта`
- Связанные ID из inventory: `JS-33`, `JS-34`
- Решение: [JS-ARRAYS-EX10](../../solutions/by-domain/01-javascript-and-async-programming.md#js-arrays-ex10)

#### Задание

```js
const source = [undefined, null, , ["x", "y"], 5, 6];
const [first = "A", second = "B", third = "C", [x], ...tail] = source;

const symbol = Symbol("token");
const proto = { inherited: true };
const options = Object.create(proto);
options.visible = 1;
Object.defineProperty(options, "hidden", { value: 2 });
options[symbol] = 3;

const copied = { visible: 0, ...options, visible: 4 };
```

1. Предскажите значения после деструктуризации и `tail`.
2. Перечислите собственные ключи `copied` и их значения.
3. Объясните значение по умолчанию для `undefined`/пустого слота в сравнении с `null`.
4. Сравните требование итерируемости для spread массива/вызова с правилом собственных перечисляемых свойств object spread.
5. Объясните риск `fn(...veryLargeArray)` без выдуманного числового лимита.

### JS-ARRAYS-EX11

**Исправьте ошибку поверхностной копии через структурное разделение**

- Статус: `approved`
- Раздел: `JavaScript и асинхронное программирование`
- Сложность: `Mid → Senior | debugging + implementation`
- Проверяемые навыки: `общая ссылка, вложенное неизменяемое обновление, идентичность без изменения`
- Связанные ID из inventory: `JS-34`
- Решение: [JS-ARRAYS-EX11](../../solutions/by-domain/01-javascript-and-async-programming.md#js-arrays-ex11)

#### Задание

```js
function activateUser(state, id) {
  const next = { ...state, users: [...state.users] };
  const user = next.users.find((item) => item.id === id);
  if (user) user.settings.active = true;
  return next;
}
```

1. Нарисуйте идентичности до и после вызова.
2. Покажите, какое исходное состояние меняется.
3. Реализуйте обновление, создающее новые корень, `users`, найденного пользователя и `settings`, но сохраняющее остальные идентичности.
4. Возвращайте исходный `state` для not-found и already-active.
5. Объясните связь с memoization/change detection без React-specific правил.

### JS-ARRAYS-EX12

**Сформулируйте требования к глубокой копии до выбора инструмента**

- Статус: `approved`
- Раздел: `JavaScript и асинхронное программирование`
- Сложность: `Senior | architecture + interview communication`
- Проверяемые навыки: `договор графа данных, циклы, повторные ссылки, прототипы, ресурсы, стоимость`
- Связанные ID из inventory: `JS-34`
- Решение: [JS-ARRAYS-EX12](../../solutions/by-domain/01-javascript-and-async-programming.md#js-arrays-ex12)

#### Задание

Редактор хочет «полностью клонировать документ для отмены». Документ содержит повторные ссылки на ресурсы, циклические ссылки на родителей, `Date`, `Map`, узлы пользовательских классов с методами и закрытыми полями, геттеры, функции, ссылки на DOM и `ArrayBuffer`.

1. Напишите не реализацию, а таблицу требований для каждого вида данных.
2. Выберите между ручным копированием доменной модели, `structuredClone`, JSON и библиотекой.
3. Укажите, что нельзя решить копированием без изменения модели.
4. Оцените стоимость большого графа и момент создания снимка состояния.
5. Дайте 60-секундное интервью-объяснение.

### JS-ARRAYS-EX13

**Проверьте `structuredClone`, повторные ссылки и перенос**

- Статус: `approved`
- Раздел: `JavaScript и асинхронное программирование`
- Сложность: `Senior | implementation + runtime verification`
- Проверяемые навыки: `циклы, повторные ссылки, встроенные типы, DataCloneError, передаваемые ресурсы`
- Связанные ID из inventory: `JS-34`
- Решение: [JS-ARRAYS-EX13](../../solutions/by-domain/01-javascript-and-async-programming.md#js-arrays-ex13)

#### Задание

Создайте переносимый runtime test, который проверяет:

1. новый root и новые nested objects;
2. сохранение cycle и repeated alias;
3. `Date`, `RegExp`, `Map`, `Set`, типизированный массив;
4. `DataCloneError` для function;
5. потерю пользовательского прототипа/метода и флагов дескриптора;
6. перенос `ArrayBuffer`, сохранение байтов и отсоединение исходника.

Отдельно перечислите browser-only host types, которые вы не можете считать переносимыми только по этому тесту.

### JS-ARRAYS-EX14

**Найдите потери цикла JSON-сериализации**

- Статус: `approved`
- Раздел: `JavaScript и асинхронное программирование`
- Сложность: `Mid → Senior | code review + prediction`
- Проверяемые навыки: `ловушки JSON-клонирования, повторные ссылки, toJSON`
- Связанные ID из inventory: `JS-34`
- Решение: [JS-ARRAYS-EX14](../../solutions/by-domain/01-javascript-and-async-programming.md#js-arrays-ex14)

#### Задание

Создайте матрицу для свойства объекта, элемента массива и значения верхнего уровня, где применимо:

- `undefined`, function, Symbol;
- `NaN`, infinities, `BigInt`;
- пустой слот;
- `Date`, `Map`, `Set`;
- пользовательский прототип, неперечисляемое свойство, геттер;
- repeated alias и cycle;
- custom `toJSON`.

Для каждого укажите результат, пропуск/преобразование/ошибку и потерю семантики. В конце сформулируйте единственный допустимый договор использования цикла сериализации как копии.

### JS-ARRAYS-EX15

**Проведите рабочее ревью API владения массивом**

- Статус: `approved`
- Раздел: `JavaScript и асинхронное программирование`
- Сложность: `Senior | code review + API design + performance reasoning`
- Проверяемые навыки: `владение, преобразования, функция сравнения, поверхностное/глубокое копирование, измерения`
- Связанные ID из inventory: `JS-29`, `JS-30`, `JS-31`, `JS-32`, `JS-34`
- Решение: [JS-ARRAYS-EX15](../../solutions/by-domain/01-javascript-and-async-programming.md#js-arrays-ex15)

#### Задание

```js
export function buildRows(input) {
  const rows = [...input];

  rows
    .filter(Boolean)
    .sort((a, b) => a.score > b.score)
    .forEach((row) => {
      row.meta.visible = true;
    });

  return JSON.parse(JSON.stringify(rows));
}
```

Договор продукта допускает `0` как строку-заглушку, сохраняет вход, сортирует строки-объекты по `score` убыванию и `name` возрастанию, обновляет только возвращённые строки-объекты и поддерживает `Date` в `meta`.

1. Ранжируйте defects.
2. Перепишите функцию с ясной нормализацией, функцией сравнения и владением.
3. Сохраните структурное разделение там, где это безопасно, или объясните осознанное копирование.
4. Уберите JSON trap.
5. Предложите тесты и измерения для 100, 10 000 и 1 000 000 элементов.

### JS-ARRAYS-EX16

**Интегрированный interview challenge: подготовка строк таблицы**

- Статус: `approved`
- Раздел: `JavaScript и асинхронное программирование`
- Сложность: `Senior | integrated interview challenge`
- Проверяемые навыки: `модель массива, разреженность, выбор метода, сортировка, копирование, структурное разделение, граница клонирования, объяснение`
- Связанные ID из inventory: `JS-29`, `JS-30`, `JS-31`, `JS-32`, `JS-33`, `JS-34`
- Решение: [JS-ARRAYS-EX16](../../solutions/by-domain/01-javascript-and-async-programming.md#js-arrays-ex16)

#### Задание

```js
function prepareTable(input, selectedId) {
  input.length = Math.max(input.length, 5);

  const rows = input
    .filter(Boolean)
    .map((row) => {
      if (row.id === selectedId) {
        row.meta.selected = true;
      }
      return row;
    });

  rows.sort((a, b) => a.score < b.score);

  const snapshot = JSON.parse(JSON.stringify(rows));
  return snapshot;
}
```

Вход может быть разреженным, `0` является допустимой строкой-заглушкой, строки-объекты содержат `Date`, а две строки могут ссылаться на один `meta`. Требуется немутирующий публичный договор, `score` по убыванию и `name` по возрастанию, сохранение значимых ложных данных, новый изменённый путь только для выбранной строки-объекта и явно сформулированный договор снимка состояния.

За 25 минут:

1. предскажите изменение `length`, пустые слоты и наблюдаемую мутацию;
2. найдите все correctness/ownership defects;
3. спроектируйте нормализацию разреженного входа;
4. выберите methods или цикл и объясните выбор;
5. реализуйте стабильную сортировку по нескольким полям без изменения входа;
6. реализуйте структурное разделение для выбранной строки;
7. замените цикл JSON-сериализации подходящим договором снимка состояния;
8. добавьте целевые тесты для пустых слотов, `undefined`, `0`, общего `meta`, `Date`, равных ключей функции сравнения и идентичности без изменения;
9. оцените временные массивы и предложите измерения;
10. дайте двухминутное объяснение: mental model → defects → ownership → algorithm → clone boundary → trade-offs.

#### Критерии самопроверки

- [ ] Исходный `input`, его `length` и вложенные объекты не меняются.
- [ ] Hole и explicit `undefined` нормализованы по явному правилу.
- [ ] `0` не теряется из-за truthiness.
- [ ] Comparator возвращает отрицательное/ноль/положительное и задаёт tie-break.
- [ ] Изменяемый путь скопирован; прочие разрешённые идентичности разделяются осознанно.
- [ ] Семантика снимка учитывает `Date`, повторные ссылки и поддерживаемые типы.
- [ ] Объяснение не уходит в 1.6 или полную JSON-сериализацию.

## 1.6. Collections, Symbols & Iteration

Последовательность: **воспроизведение по памяти → прогнозирование → объяснение → отладка → ревью кода → реализация → комплексная задача**.

### JS-COLLECTIONS-EX01

**Восстановите карту выбора коллекции**

- Статус: `approved`
- Раздел: `JavaScript и асинхронное программирование`
- Сложность: `Junior → Mid | воспроизведение по памяти`
- Проверяемые навыки: `Ключи, принадлежность, владение, протокол обхода`
- Связанные ID из inventory: `JS-35`, `JS-36`, `JS-37`, `JS-38`
- Решение: [JS-COLLECTIONS-EX01](../../solutions/by-domain/01-javascript-and-async-programming.md#js-collections-ex01)

#### Задание

Для каждого из `Object`, `Map`, `Set`, `WeakMap`, `WeakSet`, `WeakRef` назовите вопрос, на который он отвечает, допустимые ключи или значения, наличие обхода и влияние на время жизни. Затем произнесите разницу между `Symbol.iterator` и `next()`.

#### Критерии самопроверки

- [ ] Ваше правило учитывает `undefined` в `Map` и отсутствие `size` у слабых коллекций.

### JS-COLLECTIONS-EX02

**Проследите равенство и порядок**

- Статус: `approved`
- Раздел: `JavaScript и асинхронное программирование`
- Сложность: `Junior → Mid | прогнозирование`
- Проверяемые навыки: `Равенство ключей, порядок вставки`
- Связанные ID из inventory: `JS-35`, `JS-36`
- Решение: [JS-COLLECTIONS-EX02](../../solutions/by-domain/01-javascript-and-async-programming.md#js-collections-ex02)

#### Задание

Запишите результаты без запуска. Объясните, какие операции меняют размер, позицию и результат `has`.
```js
const row = { id: 1 };
const map = new Map([[NaN, "old"], [-0, "zero"], [row, undefined]]);
map.set(NaN, "new");
map.delete(0);
map.set(+0, "again");
console.log([...map.values()]);
console.log(map.has({ id: 1 }), map.has(row), new Set([row, row, { id: 1 }]).size);
```

#### Критерии самопроверки

- [ ] Вы отличаете изменение значения от удаления с повторной вставкой.

### JS-COLLECTIONS-EX03

**Объясните время жизни метаданных**

- Статус: `approved`
- Раздел: `JavaScript и асинхронное программирование`
- Сложность: `Mid | объяснение`
- Проверяемые навыки: `Слабая достижимость, символьные ключи`
- Связанные ID из inventory: `JS-36`, `JS-37`
- Решение: [JS-COLLECTIONS-EX03](../../solutions/by-domain/01-javascript-and-async-programming.md#js-collections-ex03)

#### Задание

Сравните два случая. В первом долго живущий `WeakMap` хранит запись `row → { row }`, но больше никто не держит ни строку, ни значение. Во втором значение также лежит во внешнем массиве. Объясните, что изменится, если заменить ключ на `Symbol.for("row")`.

#### Критерии самопроверки

- [ ] Объяснение не обещает момент сборки и показывает внешнюю сильную цепочку.

### JS-COLLECTIONS-EX04

**Почините пользовательский обход**

- Статус: `approved`
- Раздел: `JavaScript и асинхронное программирование`
- Сложность: `Mid | отладка`
- Проверяемые навыки: `Точная идентичность ключа протокола`
- Связанные ID из inventory: `JS-37`, `JS-38`
- Решение: [JS-COLLECTIONS-EX04](../../solutions/by-domain/01-javascript-and-async-programming.md#js-collections-ex04)

#### Задание

Следующий фрагмент намеренно выбрасывает `TypeError`. Исправьте его так, чтобы обход можно было повторить и он выдавал именно `"id"`, `"title"`.
```js
const columns = {
  *[Symbol.for("Symbol.iterator")]() {
    yield "id";
    yield "title";
  },
};
console.log([...columns]);
```

#### Критерии самопроверки

- [ ] Два обхода дают одинаковый результат, а два курсора независимы.

### JS-COLLECTIONS-EX05

**Проведите ревью индекса строк**

- Статус: `approved`
- Раздел: `JavaScript и асинхронное программирование`
- Сложность: `Mid → Senior | ревью кода`
- Проверяемые навыки: `Явный договор дедупликации и порядок`
- Связанные ID из inventory: `JS-35`, `JS-36`
- Решение: [JS-COLLECTIONS-EX05](../../solutions/by-domain/01-javascript-and-async-programming.md#js-collections-ex05)

#### Задание

Даны строки с ID типа `string | number`, включая `0`, `"0"`, `"10"` и `"2"`. Требование: последнее значение для каждого ID в порядке первого появления ключа. Что нарушено в коде? Предложите тесты, прежде чем исправлять.
```js
function indexRows(rows) {
  const index = {};
  for (const row of rows) index[row.id] = row;
  return Object.values(index);
}
```

#### Критерии самопроверки

- [ ] Проверены разный тип ID, порядок индексных строк и победитель дубликата.

### JS-COLLECTIONS-EX06

**Разберите слабый кеш**

- Статус: `approved`
- Раздел: `JavaScript и асинхронное программирование`
- Сложность: `Mid → Senior | отладка и ревью`
- Проверяемые навыки: `Управляемый промах `WeakRef``
- Связанные ID из inventory: `JS-36`
- Решение: [JS-COLLECTIONS-EX06](../../solutions/by-domain/01-javascript-and-async-programming.md#js-collections-ex06)

#### Задание

Коллега ждёт, пока после `row = null` тест увидит `undefined` в `deref()`. Индекс реализован как `Map<Id, WeakRef<Row>>` и обязан содержать до 100 ID. Объясните обе ошибки. Реализуйте только функцию чтения с пересозданием и покажите, как проверить попадание и промах без сборщика.

#### Критерии самопроверки

- [ ] Тестируемый промах не требует реального `WeakRef`; лимит индекса обсуждается отдельно.

### JS-COLLECTIONS-EX07

**Реализуйте итерацию по порциям**

- Статус: `approved`
- Раздел: `JavaScript и асинхронное программирование`
- Сложность: `Mid | реализация`
- Проверяемые навыки: `Пользовательский итератор, изоляция состояния`
- Связанные ID из inventory: `JS-38`
- Решение: [JS-COLLECTIONS-EX07](../../solutions/by-domain/01-javascript-and-async-programming.md#js-collections-ex07)

#### Задание

Напишите `chunks(values, size)` для массива и положительного безопасного целого размера. Каждый обход должен читать массив с начала и выдавать новый массив для каждой порции, включая неполную последнюю. Вход во время обхода считается неизменным. Сначала реализуйте `next()` вручную, затем перепишите через генератор. Проверьте пустой вход, независимые курсоры и недопустимый размер.

#### Критерии самопроверки

- [ ] Размер `0` отклоняется до начала обхода, состояние принадлежит каждому курсору.

### JS-COLLECTIONS-EX08

**Ограничьте обход и проверьте закрытие**

- Статус: `approved`
- Раздел: `JavaScript и асинхронное программирование`
- Сложность: `Mid → Senior | реализация`
- Проверяемые навыки: `Ленивость, раннее завершение, уборка`
- Связанные ID из inventory: `JS-38`
- Решение: [JS-COLLECTIONS-EX08](../../solutions/by-domain/01-javascript-and-async-programming.md#js-collections-ex08)

#### Задание

Реализуйте `take(source, limit)` как генератор для обычного итерируемого источника. `limit` — неотрицательное безопасное целое. Для нуля источник не открывается. Если лимит достигнут, не запрашивайте лишний элемент. Докажите, что потребление через `for...of` закрывает внутренний генератор при остановке и при досрочном выходе из внешнего цикла.

#### Критерии самопроверки

- [ ] В тесте есть счётчик запросов и признак освобождения в `finally`.

### JS-COLLECTIONS-EX09

**Проверьте завершение асинхронного источника**

- Статус: `approved`
- Раздел: `JavaScript и асинхронное программирование`
- Сложность: `Senior | отладка`
- Проверяемые навыки: `Асинхронный протокол, распространение ошибок`
- Связанные ID из inventory: `JS-38`
- Решение: [JS-COLLECTIONS-EX09](../../solutions/by-domain/01-javascript-and-async-programming.md#js-collections-ex09)

#### Задание

Сделайте асинхронный генератор, который ждёт передаваемый `load(page)` внутри `try` и записывает закрытие в `finally`. В двух тестах оборвите потребление после первой страницы и отклоните загрузку первой страницы. Какие события должны быть видны в каждом случае?

#### Критерии самопроверки

- [ ] Ранний выход не вызывает `load(2)`. Ошибка первой загрузки видна потребителю, и уборка происходит в обоих случаях.

### JS-COLLECTIONS-EX10

**Соберите ограниченную выдачу из страниц**

- Статус: `approved`
- Раздел: `JavaScript и асинхронное программирование`
- Сложность: `Senior | комплексная задача`
- Проверяемые навыки: `Асинхронный обход, дедупликация, идентичность, граница хранения`
- Связанные ID из inventory: `JS-35`, `JS-36`, `JS-37`, `JS-38`
- Решение: [JS-COLLECTIONS-EX10](../../solutions/by-domain/01-javascript-and-async-programming.md#js-collections-ex10)

#### Задание

Дан конечный асинхронный источник страниц, каждая страница — массив строк с `id` типа `string | number`. Реализуйте `collectFirstUnique(pages, limit)`. Оставляйте первое появление каждого ID, возвращайте исходные строки в порядке появления и прекращайте обход после `limit` уникальных. При нулевом лимите источник не открывается. Недопустимый лимит отклоняется. Объясните, где хранить размеры строк по экземпляру и как отправить ID в JSON, сохранив различие `7` и `"7"`.

#### Критерии самопроверки

- [ ] Проверьте повторы между страницами, пустую страницу, недобор, нулевой лимит и закрытие при раннем выходе. Проговорите, что будет, если потребуются все активные ID.
