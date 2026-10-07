# 1. JavaScript и асинхронное программирование — условия упражнений

> Статус: `частично готово — упражнения 1.1–1.3 одобрены; 1.4–1.12 остаются заглушками`
>
> Не открывайте [файл с решениями](../../solutions/by-domain/01-javascript-and-async-programming.md), пока не выполните собственную попытку.
>
> Разделы 1.4–1.12 остаются заглушками.

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
