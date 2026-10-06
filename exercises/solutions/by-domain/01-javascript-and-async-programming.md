# 1. JavaScript и асинхронное программирование — решения упражнений

> Статус: `частично готово — решения разделов 1.1 и 1.2 одобрены; разделы 1.3–1.12 остаются placeholders`
>
> Условия: [отдельный файл с упражнениями](../../prompts/by-domain/01-javascript-and-async-programming.md)
>
> Разделы 1.3–1.12 остаются заглушками.

## 1.1. Модель выполнения, объявления и области видимости

### JS-SCOPE-EX01

- Статус: `approved`
- Условие: [JS-SCOPE-EX01](../../prompts/by-domain/01-javascript-and-async-programming.md#js-scope-ex01)
- Последняя проверка: `2026-09-23`

#### Логика решения

Таблица должна отражать жизненный цикл привязки имени (binding), а не описывать воображаемое физическое «перемещение объявлений наверх».

#### Решение

| Форма | Область видимости (scope) | До выполнения объявления | Повторное присваивание | Повторное объявление в той же области | Примечание |
|---|---|---|---:|---:|---|
| `var x` | функция или верхний уровень скрипта/модуля; не блок | новая привязка инициализирована значением `undefined`; совместимая существующая привязка переиспользуется, но не сбрасывается | да | ещё один `var` обычно допустим | знание для интервью и поддержки устаревшего кода |
| `let x` | лексический/блочный | не инициализирован, TDZ | да | нет | используйте при намеренном повторном присваивании |
| `const x = v` | лексический/блочный | не инициализирован, TDZ | нет | нет | современный выбор по умолчанию; объект всё ещё может изменяться |
| `function f() {}` | область, содержащая объявление | обычно инициализирован объектом функции | зависит от контекста объявления | конфликты зависят от контекста | можно вызвать до текстовой позиции объявления |
| `var f = function () {}` | область объявления `var` | `f === undefined`; выражение ещё не вычислено | да | правила `var` | ранний вызов приводит к `TypeError` |
| `const f = function () {}` | лексический/блочный | `f` не инициализирован и находится в TDZ | нет | нет | раннее чтение приводит к `ReferenceError` |

Определения:

- **Объявление (declaration):** синтаксическая конструкция, которая вводит имя; подготовка объявлений может создать новую привязку или переиспользовать совместимую существующую.
- **Инициализация (initialization):** первое значение, переданное вновь созданной привязке.
- **Присваивание (assignment):** последующая запись в уже инициализированную изменяемую привязку.
- **Временная мёртвая зона (TDZ):** период от входа в область до инициализации лексической привязки.
- **Ранняя статическая ошибка (Early Error):** ошибка статической семантики, обнаруженная для одной разбираемой единицы до её выполнения. Более поздний классический скрипт вместо этого может выбросить `SyntaxError` во время подготовки глобальных объявлений; такой сбой формально не является Early Error.

Если не указано иное, таблица предполагает новое имя. Повторный `var`, переиспользование параметра/функции и совместимые уже существующие глобальные свойства не сбрасываются в `undefined`.

#### Сложность

Неприменимо: это модель для воспроизведения по памяти.

#### Альтернативные подходы

Когда базовая таблица будет усвоена, добавьте строки для `class` и именованных функциональных выражений. Это полезные уточняющие вопросы, но для первого прохода они не обязательны.

#### Типичные ошибки

- Утверждать, что `let`/`const` не существуют до своей строки.
- Утверждать, что `const` делает объект неизменяемым.
- Утверждать, что функциональное выражение подчиняется подъёму объявлений так же, как объявление функции.

### JS-SCOPE-EX02

- Статус: `approved`
- Условие: [JS-SCOPE-EX02](../../prompts/by-domain/01-javascript-and-async-programming.md#js-scope-ex02)
- Последняя проверка: `2026-09-23`

#### Логика решения

Сначала определите, успешно ли проходят синтаксический разбор и подготовка объявлений. Только после этого трассируйте чтения во время выполнения.

#### Решение

| Фрагмент | Результат | Причина |
|---|---|---|
| A | выводит `undefined`, затем `7` | `var score` инициализируется значением `undefined`; позже инициализатор присваивает `7` |
| B | `ReferenceError`, вывода нет | в момент чтения `score` является неинициализированной лексической привязкой |
| C | `ReferenceError`, вывода нет | внутренний `score` затеняет внешний во всём блоке и находится в TDZ |
| D | выводит `"undefined"`, затем выбрасывает `ReferenceError` | `missing` не разрешается ни в одном окружении; `present` существует в TDZ |
| E | `TypeError`, вывода нет | `run` успешно разрешается в инициализированное значение `undefined`, которое нельзя вызвать |
| F | ранний `SyntaxError`, вывода нет | одна область не может одновременно содержать лексический `id` и `var id` |

#### Сложность

Неприменимо.

#### Альтернативные подходы

Для каждого фрагмента нарисуйте временную шкалу состояний: вход в область → состояние привязки → чтение → объявление и инициализатор. Это медленнее, но полезно, если навык активного воспроизведения ещё не восстановлен.

#### Типичные ошибки

- Предсказывать `"before"` для F.
- Называть ошибку в E `ReferenceError`.
- Считать, что в C будет прочитан внешний `score`.
- Считать `typeof` безопасным во всех случаях.

### JS-SCOPE-EX03

- Статус: `approved`
- Условие: [JS-SCOPE-EX03](../../prompts/by-domain/01-javascript-and-async-programming.md#js-scope-ex03)
- Последняя проверка: `2026-09-23`

#### Логика решения

Активная вызывающая функция находится в стеке вызовов (call stack), но не попадает автоматически во внешнюю лексическую цепочку вызываемой функции.

#### Решение

Итоговый вывод:

```text
scope:build!
```

В момент выполнения `return label + suffix`:

- `suffix`: запись окружения текущего блока `if` → найдено значение `"!"`.
- `label`: запись окружения текущего блока `if` → не найден; запись вызова возвращённой функции → не найден; захваченная запись вызова `build` → найдено значение `"scope:build"`.
- До глобального `label` поиск не доходит.
- Локальный `label` функции `invoke` вообще не входит в эту лексическую цепочку.

Стек вызовов (`call stack`) в этот момент:

```text
возвращённая функция (true)    ← выполняется
invoke(report)
входной скрипт
```

`build` уже отсутствует в стеке вызовов, но соответствующее окружение остаётся достижимым через `report`.

#### Сложность

В концептуальной модели ручной поиск от неразрешённого имени до найденной привязки занимает `O(d)`, где `d` — глубина лексической вложенности. Это модель рассуждения, а не гарантия стоимости поиска в оптимизированном движке.

#### Альтернативные подходы

Вместо полной схемы Environment Records можно подписать у каждого идентификатора соответствующее объявление. Полную цепочку records полезно рисовать, когда место вызова специально служит отвлекающим фактором.

#### Типичные ошибки

- Искать в `invoke` раньше, чем в захваченном окружении `build`.
- Оставлять `build` в активном стеке вызовов после возврата из функции.
- Приписывать блоку `if` собственный execution context функции.

### JS-SCOPE-EX04

- Статус: `approved`
- Условие: [JS-SCOPE-EX04](../../prompts/by-domain/01-javascript-and-async-programming.md#js-scope-ex04)
- Последняя проверка: `2026-09-23`

#### Логика решения

Сильный ответ с ограничением по времени ставит в приоритет определение, причинную модель и один показательный пример.

#### Решение

Возможный ответ на 45 секунд:

> `var` имеет область видимости функции либо верхнего уровня. Во время подготовки объявлений новая привязка инициализируется значением `undefined`, а совместимый повторный `var` переиспользует существующую привязку, не сбрасывая её. Значение можно присваивать повторно. `let` и `const` — блочные лексические объявления: их привязки существуют с момента входа в область, но остаются неинициализированными в TDZ. `let` допускает повторное присваивание, а привязку `const` нельзя связать с другим значением, хотя сам объект может изменяться. В современном коде я по умолчанию использую `const`, выбираю `let`, когда нужно повторное присваивание, а `var` сохраняю как знание для отладки, интервью и поддержки устаревшего кода.

Возможный ответ на 60 секунд:

> Вызов функции создаёт контекст выполнения (execution context) в стеке вызовов. Разрешение идентификаторов моделируется через записи окружения (Environment Records): текущая запись содержит локальные привязки и ссылку `[[OuterEnv]]`, поэтому поиск следует лексической вложенности исходного кода, а не цепочке вызывающих функций. До обычного выполнения механизмы подготовки объявлений создают привязки. Новая привязка `var` инициализируется значением `undefined`; лексические объявления остаются неинициализированными в TDZ; объявление функции обычно сразу получает объект функции. Это наблюдаемое поведение называют подъёмом объявлений (hoisting), но исходный код физически никуда не перемещается. Блок может добавить запись окружения, не добавляя кадр в стек вызовов.

#### Сложность

Целевая длительность: 45 и 60 секунд.

#### Альтернативные подходы

В качестве примера можно взять один фрагмент на прогнозирование вывода, но не тратьте весь ответ на его пошаговое выполнение.

#### Типичные ошибки

- Перечислять правила без единой причинной модели.
- Тратить всё время на названия алгоритмов спецификации.
- Уходить в обсуждение tasks/microtasks или полноценных сценариев closures.

### JS-SCOPE-EX05

- Статус: `approved`
- Условие: [JS-SCOPE-EX05](../../prompts/by-domain/01-javascript-and-async-programming.md#js-scope-ex05)
- Последняя проверка: `2026-09-23`

#### Логика решения

Отделяйте неквалифицированное присваивание от явной записи в свойство.

#### Решение

В классическом скрипте в нестрогом режиме (sloppy mode):

- `record` верхнего уровня — глобальная привязка функции, которая обычно также отражается как свойство глобального объекта;
- `event` — привязка параметра, локальная для каждого вызова;
- при первом вызове в чистой изолированной среде (realm) с обычным расширяемым глобальным объектом выражение `lastEvent = event` создаёт настраиваемое свойство, потому что `lastEvent` не разрешается ни в одном окружении; последующие вызовы обновляют это свойство;
- `count` — локальный `var` с областью видимости функции;
- `globalThis.count = count` явно создаёт или обновляет свойство глобального объекта;
- логи выводят `"open"` и `1`.

При добавлении `"use strict"` или загрузке кода как ES-модуля первое присваивание выбрасывает `ReferenceError`; вычисление и запись счётчика, а также последующие логи не выполняются.

После выполнения нестрогой версии выражение `delete globalThis.lastEvent` явно удаляет обычно настраиваемое свойство, созданное случайной глобальной переменной, и возвращает `true`. Строгий код, содержащий `delete lastEvent`, получает ранний `SyntaxError`. Оператор `delete` работает со свойствами; он не удаляет локальную привязку `count` или привязку, созданную через `let`/`const`.

Минимальное исправление, сохраняющее явную глобальную видимость:

```js
function record(event) {
  globalThis.lastEvent = event;
  const count = (globalThis.count || 0) + 1;
  globalThis.count = count;
}
```

Более чистый API с явным владельцем состояния:

```js
function createRecorder() {
  let lastEvent;
  let count = 0;

  return {
    record(event) {
      lastEvent = event;
      count += 1;
    },
    snapshot() {
      return { lastEvent, count };
    },
  };
}
```

В реальном модуле экспортируйте `createRecorder` либо один намеренно созданный экземпляр recorder-объекта.

#### Сложность

Каждый вызов `record` и `snapshot` занимает `O(1)` времени; состояние требует `O(1)` памяти.

#### Альтернативные подходы

Если для интеграции лучше подходят внедрение зависимостей (dependency injection) и внешний владелец, передавайте в `record` изменяемый объект состояния.

#### Типичные ошибки

- Считать локальный `var count` глобальным.
- Полагать, что строгий режим лишь предотвращает создание глобального свойства, после чего функция продолжает выполнение.
- Использовать `delete lastEvent` как стратегию очистки переменной.

### JS-SCOPE-EX06

- Статус: `approved`
- Условие: [JS-SCOPE-EX06](../../prompts/by-domain/01-javascript-and-async-programming.md#js-scope-ex06)
- Последняя проверка: `2026-09-23`

#### Логика решения

Вложенный `var result` принадлежит области функции, а все ветви `case` без дополнительных блоков используют общий лексический блок `switch` (`CaseBlock`).

#### Решение

```js
function format(kind) {
  let result = "unknown";

  if (kind === "short") {
    result = "S";
  }

  switch (kind) {
    case "long": {
      const suffix = "!";
      result = "Long" + suffix;
      break;
    }
    case "verbose": {
      const suffix = "!!";
      result = "Verbose" + suffix;
      break;
    }
  }

  return result;
}
```

Исходное тело функции отклоняется до того, как функцию можно вызвать: `var result` конфликтует с лексическим `result`, а повторные объявления `suffix` конфликтуют в общей области конструкции `switch`.

#### Сложность

`O(1)` по времени и `O(1)` дополнительной памяти.

#### Альтернативные подходы

Таблица соответствий может оказаться чище в рабочем коде, но намеренно обходит учебную цель этого упражнения — исправление областей видимости.

#### Типичные ошибки

- Заменять `var result` на второй `let result` внутри `if`: он создаст shadowing, а не обновит внешний `result`.
- Исправлять только конфликт в `if` и пропускать проблему в `switch`.
- Утверждать, что parser разбирает только выбранную ветвь `case`.

### JS-SCOPE-EX07

- Статус: `approved`
- Условие: [JS-SCOPE-EX07](../../prompts/by-domain/01-javascript-and-async-programming.md#js-scope-ex07)
- Последняя проверка: `2026-09-23`

#### Логика решения

Проверяйте корректность и владение состоянием раньше, чем стиль.

#### Решение

Замечания в порядке серьёзности:

1. **Высокая — корректность:** все функции обратного вызова используют один и тот же `var index`; после цикла он равен `buttons.length`. Если `active` имеет значение `true`, то `buttons[index]` обычно равен `undefined`, а обращение к `.id` выбрасывает `TypeError`.
2. **Высокая — зависимость от окружения:** `callbacks = []` создаёт случайную глобальную переменную в нестрогом классическом скрипте, но выбрасывает ошибку в строгом коде и модулях.
3. **Средняя — владение состоянием:** `active` и `callbacks` — общие глобальные значения без документированного жизненного цикла. Нужно выяснить, зависят ли от них внешние скрипты.
4. **Низкая — сопровождаемость:** выбор объявлений скрывает, какое состояние должно изменяться.

Если для совместимости нужны исходная глобальная переменная `active` из классического скрипта и свойство `callbacks`, создаваемое при вызове `install`, минимальное явное исправление выглядит так:

```js
var active = true;

function install(buttons) {
  globalThis.callbacks = [];

  for (let index = 0; index < buttons.length; index += 1) {
    globalThis.callbacks.push(function () {
      if (active) {
        return buttons[index].id;
      }
    });
  }
}
```

Публичное свойство сохраняется ради совместимости вместе с исходным моментом создания и признаком настраиваемости, но теперь его владелец указан явно, а общая привязка цикла исправлена.

Целевой модульный вариант:

```js
export function createCallbacks(buttons, isActive) {
  const callbacks = [];

  for (let index = 0; index < buttons.length; index += 1) {
    callbacks.push(() => (
      isActive() ? buttons[index].id : undefined
    ));
  }

  return callbacks;
}
```

Тесты:

- один и несколько элементов возвращают собственные ID;
- выключенное состояние возвращает `undefined`;
- повторная установка не смешивает коллекции;
- выполнение в строгом режиме не создаёт неожиданных глобальных значений;
- следует выбрать и проверить, наблюдают ли функции обратного вызова последующее изменение массива или сохраняют снимок значения (snapshot).

#### Сложность

Создание занимает `O(n)` времени и `O(n)` памяти; каждый вызов функции обратного вызова выполняется за `O(1)`.

#### Альтернативные подходы

Если функция обратного вызова должна быть связана с исходным элементом, а не с текущим содержимым ячейки массива, на каждой итерации захватывайте `const button = buttons[index]`.

#### Типичные ошибки

- Ограничиваться замечанием «используйте `let`».
- Удалять глобальные значения без проверки контракта с устаревшим кодом.
- Считать `active` заведомо случайной глобальной переменной, когда требования неизвестны.

### JS-SCOPE-EX08

- Статус: `approved`
- Условие: [JS-SCOPE-EX08](../../prompts/by-domain/01-javascript-and-async-programming.md#js-scope-ex08)
- Последняя проверка: `2026-09-23`

#### Логика решения

Выбор объявления определяет, получает ли каждая функция обратного вызова отдельную привязку итерации. Вторая привязка каждой итерации определяет семантику значения: актуальное на момент вызова (live) или сохранённый снимок (snapshot).

#### Решение

Live-значения:

```js
function createReaders(values) {
  const readers = [];

  for (let index = 0; index < values.length; index += 1) {
    readers.push(() => ({
      index,
      value: values[index],
    }));
  }

  return readers;
}
```

Snapshot-значения:

```js
function createReaders(values) {
  const readers = [];

  for (let index = 0; index < values.length; index += 1) {
    const value = values[index];
    readers.push(() => ({ index, value }));
  }

  return readers;
}
```

В обеих версиях `for (let ...)` создаёт новую привязку `index` для каждой итерации. Версия со снимком также создаёт отдельную привязку `value` на каждой итерации; версия с актуальным значением читает ячейку массива в момент вызова.

Характерные проверки:

```js
const values = ["a", "b", "c"];
const readers = createReaders(values);

console.assert(readers.length === 3);
console.assert(readers[0]().index === 0);
console.assert(readers[2]().value === "c");

values[0] = "changed";
// Live-контракт: readers[0]().value === "changed"
// Snapshot-контракт: readers[0]().value === "a"

console.assert(createReaders([]).length === 0);
```

#### Сложность

Создание занимает `O(n)` времени и `O(n)` памяти. Каждое чтение выполняется за `O(1)`.

#### Альтернативные подходы

Для контракта со снимком выражение `values.map((value, index) => () => ({ index, value }))` идиоматично, но запрещено условиями, чтобы упражнение явно проверяло семантику привязок цикла.

#### Типичные ошибки

- Использовать `var index` и захватывать одну общую привязку.
- Утверждать, что версия с актуальным значением сохраняет снимок `values[index]`.
- Не указывать явно, выбран контракт с актуальным значением или со снимком.

### JS-SCOPE-EX09

- Статус: `approved`
- Условие: [JS-SCOPE-EX09](../../prompts/by-domain/01-javascript-and-async-programming.md#js-scope-ex09)
- Последняя проверка: `2026-09-23`

#### Логика решения

Анализируйте файлы в порядке загрузки. Подготовка объявлений (declaration instantiation) происходит до выполнения соответствующего файла, а сбой одного классического скрипта не отменяет задним числом уже завершившийся скрипт.

#### Решение

Предположим чистую изолированную среду браузера и обычный последовательный порядок выполнения блокирующих внешних классических скриптов.

1. `bootstrap.js` успешно проходит подготовку объявлений и выполнение:
   - `var mode` создаёт глобальную `var`-привязку и обычно ненастраиваемое свойство глобального объекта; затем инициализатор присваивает ему значение `"legacy"`;
   - присваивание `sharedCount = 0` в нестрогом режиме создаёт настраиваемое свойство глобального объекта.
2. До выполнения файла `widget.js` его лексическое объявление верхнего уровня `let mode` конфликтует с существующим глобальным `var mode` и ограничивающим повторное объявление глобальным свойством. `GlobalDeclarationInstantiation` завершается с `SyntaxError`, поэтому скрипт не доходит до выполнения инструкций. Такой сбой при взаимодействии отдельных записей скриптов (**Script Records**) формально не является ранней статической ошибкой.
   - `"widget start"` не выводится;
   - `makeHandlers` не устанавливается, потому что скрипт не доходит до выполнения.
3. `app.js` является модулем:
   - его `var mode` имеет область видимости модуля и не конфликтует с глобальным именем классического скрипта;
   - подготовка и выполнение модуля завершаются успешно, поскольку одно лишь определение и экспорт `start` не выполняет тело функции;
   - `sharedCount` разрешается через внешнее глобальное окружение, потому что соответствующее свойство уже существует;
   - `makeHandlers` остаётся неразрешённым и выбросит `ReferenceError`, когда выполнение `start` дойдёт до этого вызова.

Если другой модуль импортирует и вызовет `start(nodes)`, сначала увеличится `sharedCount`, после чего вызов отсутствующего `makeHandlers` выбросит ошибку. Вывода от функций обратного вызова цикла не будет, потому что обработчики не создаются.

Дефекты в порядке серьёзности:

1. **Высокая:** конфликт глобальных объявлений классических скриптов не позволяет выполнить `widget.js`.
2. **Высокая:** модуль зависит от необъявленного глобального `makeHandlers`, который не был установлен из-за предыдущего сбоя.
3. **Высокая:** предполагаемый цикл создания функций обратного вызова использовал бы один общий `var i`, поэтому каждая функция обращалась бы к индексу `nodes.length`.
4. **Средняя:** `sharedCount` — случайная глобальная переменная с неявным владельцем.
5. **Средняя:** одинаковое имя `mode` обозначает несвязанное состояние в глобальном и модульном окружениях.

Минимальное исправление при смешанной загрузке:

```js
// bootstrap.js — классический скрипт
var mode = "legacy";
globalThis.sharedCount = 0;
```

```js
// widget.js — классический скрипт
console.log("widget start");
let widgetMode = "widget";

function makeHandlers(nodes) {
  const handlers = [];

  for (let i = 0; i < nodes.length; i += 1) {
    handlers.push(() => `${widgetMode}:${nodes[i].id}`);
  }

  return handlers;
}
```

```js
// app.js — модуль
var mode = "module";

export function start(nodes) {
  globalThis.sharedCount += 1;
  return globalThis.makeHandlers(nodes);
}
```

Так глобальный контракт с устаревшим кодом сохраняется явно. В классическом браузерном скрипте объявление функции верхнего уровня доступно через глобальный объект; рабочий код должен документировать и тестировать эту зависимость.

Более чистый полностью модульный вариант:

```js
// widget.js
const widgetMode = "widget";

export function makeHandlers(nodes) {
  const handlers = [];

  for (let i = 0; i < nodes.length; i += 1) {
    handlers.push(() => `${widgetMode}:${nodes[i].id}`);
  }

  return handlers;
}
```

```js
// app.js
import { makeHandlers } from "./widget.js";

let sharedCount = 0;

export function start(nodes) {
  sharedCount += 1;
  return makeHandlers(nodes);
}

export function getSharedCount() {
  return sharedCount;
}
```

`bootstrap.js` следует либо преобразовать в модуль, экспортирующий фактическую конфигурацию, либо удалить, если его состояние больше не нужно.

#### Сложность

Создание обработчиков занимает `O(n)` времени и сохраняет `O(n)` памяти; каждый вызов обработчика выполняется за `O(1)`.

#### Альтернативные подходы

Для поэтапной миграции вместо нескольких глобальных значений можно предоставить ровно один документированный namespace, например `globalThis.legacyApp`. Это всё ещё переходное решение, а не конечный модульный дизайн.

#### Типичные ошибки

- Предсказывать вывод `"widget start"` до `SyntaxError` на этапе подготовки объявлений.
- Считать, что модульный `var mode` перезаписывает `globalThis.mode`.
- Считать, что `makeHandlers` существует только потому, что исходный файл был загружен.
- Не заметить, что `sharedCount` изменяется до сбоя последующего вызова.
- Исправить конфликт имён, но оставить общую привязку `var i`.

## 1.2. Значения, типы, равенство и преобразование типов

### JS-VALUES-EX01

- Статус: `approved`
- Условие: [JS-VALUES-EX01](../../prompts/by-domain/01-javascript-and-async-programming.md#js-values-ex01)
- Последняя проверка: `2026-10-01`

#### Логика решения

Сначала разделите universe values на primitives и objects, затем отдельно наложите три независимые оси: `typeof`, truthiness и equality semantics.

#### Решение

| Primitive | Representative value | `typeof` |
|---|---|---|
| Undefined | `undefined` | `"undefined"` |
| Null | `null` | `"object"` — историческая особенность |
| Boolean | `true` | `"boolean"` |
| Number | `42`, `NaN`, `Infinity`, `-0` | `"number"` |
| BigInt | `42n` | `"bigint"` |
| String | `"hello"` | `"string"` |
| Symbol | `Symbol("id")` | `"symbol"` |

Все остальные values являются objects. Arrays — objects; functions — callable objects, для которых `typeof` возвращает удобную специальную строку `"function"`.

Falsy values: `false`, `0`, `-0`, `0n`, `NaN`, `""`, `null`, `undefined`. Nullish values — только `null` и `undefined`.

| Семантика | `NaN` и `NaN` | `0` и `-0` | Где встречается |
|---|---:|---:|---|
| `===` | нет | да | обычное strict equality, `indexOf()` |
| `Object.is` / SameValue | да | нет | точная проверка edge cases |
| SameValueZero | да | да | `includes()`, `Set`, `Map` keys |

Primitive value нельзя изменить: операция создаёт другое value. Binding можно или нельзя переназначить в зависимости от объявления, а object mutation изменяет состояние существующей identity.

#### Типичные ошибки

- Называть `null`, `[]` или `{}` отдельными результатами `typeof` без объяснения value category.
- Добавлять `"0"`, `"false"` или пустой array в falsy list.
- Говорить, что `const` делает object immutable.

### JS-VALUES-EX02

- Статус: `approved`
- Условие: [JS-VALUES-EX02](../../prompts/by-domain/01-javascript-and-async-programming.md#js-values-ex02)
- Последняя проверка: `2026-10-01`

#### Решение

| Expression | Result | Type / причина |
|---|---|---|
| `typeof null` | `"object"` | string; historical oddity |
| `typeof NaN` | `"number"` | string; `NaN` — Number value |
| `Number("")` | `0` | number |
| `Number("12px")` | `NaN` | number |
| `Boolean("0")` | `true` | boolean; non-empty string |
| `"5" + 2` | `"52"` | string branch binary `+` |
| `"5" - 2` | `3` | number; numeric coercion |
| `1 + 2 + "3"` | `"33"` | сначала `3`, затем concatenation |
| `NaN === NaN` | `false` | boolean |
| `Object.is(NaN, NaN)` | `true` | boolean |
| `Object.is(0, -0)` | `false` | boolean |
| `[NaN].includes(NaN)` | `true` | boolean; SameValueZero |
| `0n == 0` | `true` | boolean; abstract equality |
| `0n === 0` | `false` | boolean; разные types |

`1n + 1` и `+1n` бросают `TypeError`: арифметический `+` не смешивает BigInt с Number, а unary plus не поддерживает BigInt. Это exceptions, не результаты `NaN`.

#### Типичные ошибки

- Считать `NaN` отдельным JavaScript type.
- Применять одно правило coercion ко всем operators.
- Забывать, что equality expression всегда возвращает boolean.

### JS-VALUES-EX03

- Статус: `approved`
- Условие: [JS-VALUES-EX03](../../prompts/by-domain/01-javascript-and-async-programming.md#js-values-ex03)
- Последняя проверка: `2026-10-01`

#### Логика решения

До вызова bindings `original` и `alias` содержат одинаковое reference value к identity A. Параметр `profile` получает копию того же reference value. Push меняет array внутри A; последующий reassignment связывает только локальный `profile` с новой identity B.

#### Решение

```text
{ name: "Ada", tags: ["reviewed"] }
true
```

Pure alternative:

```js
function update(profile) {
  return {
    ...profile,
    tags: [...profile.tags, "reviewed"],
  };
}

const updated = update(original);
```

Короткий ответ для интервью: JavaScript передаёт arguments by value. Для object этим value является доступ к object identity. Caller и parameter получают два bindings с одинаковым reference value, поэтому mutation общей identity видна обоим. Reassignment меняет только parameter binding и не может переназначить caller binding.

#### Сложность

Исходная mutation — `O(1)` amortized для push. Pure version копирует `tags`, поэтому занимает `O(n)` времени и дополнительной памяти.

### JS-VALUES-EX04

- Статус: `approved`
- Условие: [JS-VALUES-EX04](../../prompts/by-domain/01-javascript-and-async-programming.md#js-values-ex04)
- Последняя проверка: `2026-10-01`

#### Решение

```js
function readPreferences(user) {
  return {
    pageSize: user.settings?.pageSize ?? 20,
    nickname: user.profile?.nickname ?? "Anonymous",
    compact: user.settings?.compact ?? true,
    city: user.profile?.address?.city ?? "Unknown",
  };
}
```

`||` подменял допустимые `0`, `""` и `false`, потому что проверяет truthiness. `??` подставляет fallback только для `null`/`undefined`. В `(user.profile?.address).city` optional chain заканчивается перед `.city`; если промежуточный result `undefined`, обычный property access бросает `TypeError`.

Minimal cases:

| Input characteristic | Expected |
|---|---|
| все nested objects отсутствуют | defaults |
| `pageSize: 0` | `0` |
| `nickname: ""` | `""` |
| `compact: false` | `false` |
| `address: null` | `city: "Unknown"` |

Optional chaining подавляет только отсутствие base в цепочке. Исключение внутри существующего getter или вызванного method продолжает распространяться; это правильно для диагностики реального defect.

### JS-VALUES-EX05

- Статус: `approved`
- Условие: [JS-VALUES-EX05](../../prompts/by-domain/01-javascript-and-async-programming.md#js-values-ex05)
- Последняя проверка: `2026-10-01`

#### Логика решения

Validation должна ответить не только «можно ли получить Number», а «соответствует ли input grammar и domain range». Fixed-scale money нормализуется в integer minor units на boundary.

#### Решение

```js
function parsePriceCents(input) {
  if (typeof input !== "string" || !/^(0|[1-9]\d*)\.\d{2}$/.test(input)) {
    throw new TypeError("price must be a canonical decimal with two places");
  }

  const [whole, fraction] = input.split(".");
  const cents = Number(whole) * 100 + Number(fraction);

  if (!Number.isSafeInteger(cents)) {
    throw new RangeError("price is outside the safe integer range");
  }

  return cents;
}

function parseQuantity(input) {
  if (typeof input !== "string" || !/^[1-9]\d*$/.test(input)) {
    throw new TypeError("quantity must be a positive integer string");
  }

  const quantity = Number(input);
  if (!Number.isSafeInteger(quantity)) {
    throw new RangeError("quantity is outside the safe integer range");
  }
  return quantity;
}

function charge(rawPrice, rawQuantity) {
  const priceCents = parsePriceCents(rawPrice);
  const quantity = parseQuantity(rawQuantity);
  const totalCents = priceCents * quantity;

  if (!Number.isSafeInteger(totalCents)) {
    throw new RangeError("total is outside the safe integer range");
  }

  return totalCents;
}

console.assert(charge("0.10", "3") === 30);
```

Global `isNaN` предварительно coercing input и поэтому принимает слишком широкий набор форм. `Number.EPSILON` — spacing около `1`, а не финансовая policy. Позднее округление не исправляет потерянный input contract и неоднозначность, на каком этапе округлять tax/discount; это должно быть частью requirements.

#### Типичные ошибки

- Принимать `""` как zero.
- Хранить cents без проверки safe integer после multiplication.
- Считать `toFixed(2)` внутренней money model, хотя он возвращает string для display.

### JS-VALUES-EX06

- Статус: `approved`
- Условие: [JS-VALUES-EX06](../../prompts/by-domain/01-javascript-and-async-programming.md#js-values-ex06)
- Последняя проверка: `2026-10-01`

#### Решение

Outer spread создаёт только новый `filter`. `range` и `tags` продолжают ссылаться на nested values из `DEFAULT_FILTER`. Первый вызов меняет defaults на `{ from: 1, to: 100 }` и `["active"]`; второй — на `{ from: 2, to: 100 }` и `["active", "active"]`. Более того, result первого вызова наблюдает последующие изменения shared nested values. Переданный `overrides.tags` тоже будет мутирован.

Минимальный refactor:

```js
function createFilter(overrides = {}) {
  const filter = {
    ...DEFAULT_FILTER,
    ...overrides,
    range: {
      ...DEFAULT_FILTER.range,
      ...overrides.range,
    },
    tags: [...(overrides.tags ?? DEFAULT_FILTER.tags), "active"],
  };

  filter.range.from += 1;
  return filter;
}
```

Контракт должен сказать, что function не мутирует defaults/inputs и передаёт caller новую outer identity, новый `range` и новый `tags`. Shallow `Object.freeze(DEFAULT_FILTER)` не замораживает nested objects; deep-freeze мог бы выявлять mutation, но не создаёт returned ownership и не заменяет refactor.

#### Сложность

Копирование tags занимает `O(n)` времени и памяти; остальные operations — `O(1)`.

### JS-VALUES-EX07

- Статус: `approved`
- Условие: [JS-VALUES-EX07](../../prompts/by-domain/01-javascript-and-async-programming.md#js-values-ex07)
- Последняя проверка: `2026-10-01`

#### Решение

```text
[] == false                 → true
[] == ![]                   → true
[1] == 1                    → true
({ valueOf: () => 4 }) + 1 → 5
({ toString: () => "4" }) + 1 → "41"
```

Первые две цепочки:

```text
[] == false
[] == 0
"" == 0
0 == 0

[] == ![]
[] == false   // [] truthy, поэтому ![] === false
...           // далее та же цепочка
```

`[1]` через `ToPrimitive` становится `"1"`, затем numeric comparison даёт `1 == 1`. Для ordinary object default hint сначала пробует `valueOf`; если он возвращает primitive `4`, addition остаётся numeric. Во втором object inherited `valueOf` возвращает object, затем custom `toString` даёт `"4"`, и `+` выбирает concatenation.

Для `score`: `Number(score)` → `10`; `String(score)` → `"ten"`; `score + 1` → `11`. Number/default hints начинают с `valueOf`, string hint — с `toString`.

Puzzle проверяет способность пошагово применять truthiness, abstract equality и `ToPrimitive`. В production лучше explicit normalization и `===`: код не должен заставлять reviewer вручную исполнять многоступенчатый coercion algorithm.

### JS-VALUES-EX08

- Статус: `approved`
- Условие: [JS-VALUES-EX08](../../prompts/by-domain/01-javascript-and-async-programming.md#js-values-ex08)
- Последняя проверка: `2026-10-01`

#### Решение

```js
function parseIntegerField(name, rawValue, { min, max = Number.MAX_SAFE_INTEGER }) {
  if (typeof rawValue !== "string" || !/^[1-9]\d*$/.test(rawValue)) {
    throw new TypeError(`${name} must be a canonical positive integer string`);
  }

  const value = Number(rawValue);
  if (!Number.isSafeInteger(value) || value < min || value > max) {
    throw new RangeError(`${name} is outside the allowed range`);
  }
  return value;
}

function normalizeSearchParams(raw) {
  if (raw === null || typeof raw !== "object" || Array.isArray(raw)) {
    throw new TypeError("raw must be an object");
  }

  const page = raw.page == null
    ? 1
    : parseIntegerField("page", raw.page, { min: 1 });
  const limit = raw.limit == null
    ? 20
    : parseIntegerField("limit", raw.limit, { min: 1, max: 100 });
  const query = raw.query ?? "";
  const exact = raw.exact ?? false;

  if (typeof query !== "string") {
    throw new TypeError("query must be a string");
  }
  if (typeof exact !== "boolean") {
    throw new TypeError("exact must be a boolean");
  }

  return { page, limit, query, exact };
}
```

Representative table-driven cases:

```js
const validCases = [
  [{}, { page: 1, limit: 20, query: "", exact: false }],
  [{ page: "2", limit: "100" }, { page: 2, limit: 100, query: "", exact: false }],
  [{ query: "", exact: false }, { page: 1, limit: 20, query: "", exact: false }],
  [{ page: null, limit: undefined }, { page: 1, limit: 20, query: "", exact: false }],
];

const invalidCases = [
  { page: " 1" },
  { page: "1.5" },
  { limit: "101" },
  { limit: "1e2" },
  { query: false },
  { exact: "false" },
  { page: "9007199254740993" },
  null,
];
```

В реальном test runner valid cases сравниваются deep equality, а для invalid cases проверяются type/message exception. `raw.page == null` здесь допустимая узкая team-policy форма; при полном запрете `==` её заменяют двумя strict comparisons.

#### Сложность

Время `O(p + l)`, где `p` и `l` — длины numeric strings; дополнительная память `O(1)` помимо result.

### JS-VALUES-EX09

- Статус: `approved`
- Условие: [JS-VALUES-EX09](../../prompts/by-domain/01-javascript-and-async-programming.md#js-values-ex09)
- Последняя проверка: `2026-10-01`

#### Решение

```js
function dedupeReadings(values) {
  return [...new Set(values)];
}

function dedupeSignedReadings(values) {
  const result = [];

  for (const value of values) {
    if (!result.some((existing) => Object.is(existing, value))) {
      result.push(value);
    }
  }

  return result;
}
```

Первая функция использует SameValueZero: repeated `NaN` объединяются, как и `0`/`-0`. Вторая использует SameValue: `NaN` объединяется, signs of zero различаются.

Для object readings нужна domain equality, а не identity. При контракте `sensorId: string`, `value: number` можно построить collision-resistant key:

```js
function numberKey(value) {
  if (Number.isNaN(value)) return "NaN";
  if (Object.is(value, -0)) return "-0";
  return String(value);
}

function dedupeSensorReadings(readings) {
  const seen = new Set();
  const result = [];

  for (const reading of readings) {
    const key = `${reading.sensorId.length}:${reading.sensorId}|${numberKey(reading.value)}`;
    if (seen.has(key)) continue;
    seen.add(key);
    result.push(reading);
  }

  return result;
}
```

Tests должны подтвердить repeated `NaN`, отдельные `0`/`-0`, сохранение первого object, одинаковые поля разных identities и разные sensor IDs.

#### Сложность

`Set` и key-based version ожидаемо работают за `O(n)` времени и `O(n)` памяти. Простая signed primitive version через `some` — `O(n²)`; для большого input её можно заменить типизированным key strategy после фиксации поддерживаемых value types.

### JS-VALUES-EX10

- Статус: `approved`
- Условие: [JS-VALUES-EX10](../../prompts/by-domain/01-javascript-and-async-programming.md#js-values-ex10)
- Последняя проверка: `2026-10-01`

#### Логика решения

Самые серьёзные defects — mutation shared/caller-owned `coupon`, широкий coercion untrusted input и floating-point money. Затем идут `||` вместо nullish contract, broken ownership, loose equality и отсутствие overflow/rounding policy.

#### Решение

```js
function parseCents(input, field) {
  if (typeof input !== "string" || !/^(0|[1-9]\d*)\.\d{2}$/.test(input)) {
    throw new TypeError(`${field} must be a canonical decimal with two places`);
  }

  const [whole, fraction] = input.split(".");
  const cents = Number(whole) * 100 + Number(fraction);
  if (!Number.isSafeInteger(cents)) {
    throw new RangeError(`${field} is outside the safe integer range`);
  }
  return cents;
}

function parseQuantity(input) {
  if (typeof input !== "string" || !/^[1-9]\d*$/.test(input)) {
    throw new TypeError("quantity must be a positive integer string");
  }
  const quantity = Number(input);
  if (!Number.isSafeInteger(quantity)) {
    throw new RangeError("quantity is outside the safe integer range");
  }
  return quantity;
}

function normalizeCoupon(input) {
  if (input == null) {
    return { code: null, discountPercent: 0 };
  }
  if (typeof input !== "object" || Array.isArray(input)) {
    throw new TypeError("coupon must be an object or nullish");
  }

  const code = input.code ?? null;
  const discountPercent = input.discountPercent ?? 0;

  if (code !== null && typeof code !== "string") {
    throw new TypeError("coupon.code must be a string or null");
  }
  if (
    !Number.isInteger(discountPercent) ||
    discountPercent < 0 ||
    discountPercent > 100
  ) {
    throw new RangeError("coupon.discountPercent must be an integer from 0 to 100");
  }

  return { code, discountPercent };
}

function prepareOrder(raw) {
  if (raw === null || typeof raw !== "object" || Array.isArray(raw)) {
    throw new TypeError("order must be an object");
  }

  const unitPriceCents = parseCents(raw.unitPrice, "unitPrice");
  const expectedTotalCents = parseCents(raw.expectedTotal, "expectedTotal");
  const quantity = parseQuantity(raw.quantity ?? "1");
  const coupon = normalizeCoupon(raw.coupon);

  const subtotal = BigInt(unitPriceCents) * BigInt(quantity);
  const discountNumerator = subtotal * BigInt(coupon.discountPercent);
  const discount = (discountNumerator + 50n) / 100n; // half-up, positive amounts
  const total = subtotal - discount;

  if (total > BigInt(Number.MAX_SAFE_INTEGER)) {
    throw new RangeError("total is outside the safe integer range");
  }

  const totalCents = Number(total);
  if (totalCents !== expectedTotalCents) {
    throw new Error("total mismatch");
  }

  return {
    quantity,
    unitPriceCents,
    coupon,
    totalCents,
  };
}
```

Focused tests:

```js
console.assert(
  prepareOrder({
    unitPrice: "10.00",
    expectedTotal: "18.00",
    quantity: "2",
    coupon: { code: "TEN", discountPercent: 10 },
  }).totalCents === 1800,
);

const coupon = { code: "FREE", discountPercent: 100 };
prepareOrder({
  unitPrice: "5.00",
  expectedTotal: "0.00",
  quantity: "1",
  coupon,
});
console.assert(coupon.discountPercent === 100);
```

Invalid tests должны покрыть whitespace price/quantity, missing required price, fraction quantity, unsafe quantity, percent `101`, wrong coupon type, overflow и mismatched expected total. Здесь явно выбрана half-up policy для положительных сумм; другой domain может требовать bankers rounding или распределение rounding по line items.

#### Сложность

Вычисление выполняется за `O(d)` по числу digits во входных строках; дополнительная память постоянна для ограниченного набора полей.

#### Типичные ошибки

- Исправить `==` на `===`, сохранив разные types двух operands.
- Использовать `??`, но оставить shared nested coupon.
- Вычислять discount через binary floating point и сравнивать approximate money.
- Не документировать rounding point и policy.
