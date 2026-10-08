# 1. JavaScript и асинхронное программирование — решения упражнений

> Статус: `частично готово — решения 1.1–1.3 одобрены; решения 1.4 готовы к пользовательской проверке; 1.5–1.12 остаются заглушками`
>
> Условия: [отдельный файл с упражнениями](../../prompts/by-domain/01-javascript-and-async-programming.md)
>
> Раздел 1.4 готов к пользовательской проверке. Разделы 1.5–1.12 остаются заглушками.

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

## 1.3. Функции, замыкания и функциональные паттерны

### JS-FUNCTIONS-EX01

[Вернуться к условию](../../prompts/by-domain/01-javascript-and-async-programming.md#js-functions-ex01)

| Форма | Создание и доступность | Область имени | Собственные `this` / `arguments` | `new` |
|---|---|---|---:|---:|
| объявление | готово после подготовки объявлений | внешняя область | да | обычно да |
| анонимное выражение | при вычислении | внешняя привязка; имя может быть выведено из позиции | да | обычно да |
| именованное выражение | при вычислении | внешняя привязка и внутреннее имя самой функции | да | обычно да |
| стрелочная функция | при вычислении | внешняя привязка; имя может быть выведено из позиции | нет | нет |

Функция первого класса — это функция как обычное значение. Колбэк — функция, которую другой код вызывает по контракту. Функция высшего порядка принимает или возвращает функцию.

Параметр — привязка в определении; аргумент — значение конкретного вызова; значение по умолчанию применяется при отсутствии аргумента или `undefined`; остаточный параметр собирает оставшиеся аргументы в массив; `arguments` содержит все фактические аргументы обычной функции; `fn.length` считает параметры до первого значения по умолчанию и не учитывает остаточный параметр.

У обычной функции `this` определяется одним из основных вариантов: обычный вызов, вызов метода у объекта, явный `call`/`apply` или вызов конструктора. Замыкание сохраняет доступ к живым привязкам. Чистая функция не создаёт внешних наблюдаемых эффектов. Каррирование меняет форму всей цепочки вызовов; частичное применение фиксирует часть аргументов.

### JS-FUNCTIONS-EX02

[Вернуться к условию](../../prompts/by-domain/01-javascript-and-async-programming.md#js-functions-ex02)

- A → `"ready"`.
- B → `ReferenceError`: `run` в TDZ.
- C → `"function undefined"`.
- D → `[1,1,1] [10,10,1] [2,20,2]`.
- E → `[1,4,2]`: объявленная длина равна 1; передано четыре аргумента; остаточный параметр содержит `C,D`.

Объяснение: объявление функции инициализируется заранее; функция из выражения с `let` не создаётся до инициализации; внутреннее имя именованного выражения не выходит наружу; значения по умолчанию вычисляются при каждом вызове слева направо; подсчёт `length` заканчивается перед первым таким параметром.

### JS-FUNCTIONS-EX03

[Вернуться к условию](../../prompts/by-domain/01-javascript-and-async-programming.md#js-functions-ex03)

`first` и `second` ссылаются на объект A; мутация меняет `A.version` на 1. `replace` перенаправляет привязку `state` на объект B со значением `version === 10`; `third` ссылается на B.

```text
first === second  → true
first.version     → 1
second === third  → false
third.version     → 10
```

Поверхностный снимок:

```js
function snapshot() {
  return { ...state };
}
```

Он создаёт новый внешний объект. Любые вложенные объекты остаются общими.

### JS-FUNCTIONS-EX04

[Вернуться к условию](../../prompts/by-domain/01-javascript-and-async-programming.md#js-functions-ex04)

`var` даёт одну привязку с итоговым значением 3. Современное исправление:

```js
for (let index = 0; index < 3; index += 1) {
  handlers.push(() => index);
}
```

Фабрика:

```js
for (var index = 0; index < 3; index += 1) {
  handlers.push(
    ((snapshot) => () => snapshot)(index),
  );
}
```

Перебор коллекции:

```js
[0, 1, 2].forEach((index) => {
  handlers.push(() => index);
});
```

Для числового цикла яснее всего `let`. Фабрика или IIFE полезна для чтения старого кода. API перебора естественен, только когда коллекция уже представляет выполняемую работу.

### JS-FUNCTIONS-EX05

[Вернуться к условию](../../prompts/by-domain/01-javascript-and-async-programming.md#js-functions-ex05)

Каждый вызов `bind` создаёт другой колбэк. Один из вариантов исправления:

```js
const controller = {
  count: 0,
  onClick(step) {
    this.count += step;
  },
  mount(button) {
    this.unmount();
    this.button = button;
    this.boundClick ??= this.onClick.bind(this, 1);
    button.addEventListener("click", this.boundClick);
  },
  unmount() {
    this.button?.removeEventListener("click", this.boundClick);
    this.button = null;
  },
};
```

Эквивалентные разовые вызовы:

```js
controller.onClick.call(controller, 1);
controller.onClick.apply(controller, [1]);
```

Адаптер:

```js
controller.clickAdapter ??= () => controller.onClick(1);
```

Он замыкается над привязкой `controller`, а не хранит привязанного получателя. В обоих вариантах для очистки нужна стабильная ссылка на функцию.

### JS-FUNCTIONS-EX06

[Вернуться к условию](../../prompts/by-domain/01-javascript-and-async-programming.md#js-functions-ex06)

Явное преобразование:

```js
const ids = processRows(
  ["10", "20", "30"],
  (value) => Number.parseInt(value, 10),
);
```

Явная зависимость и выбранное правило для эффекта:

```js
function withAudit(operation, recordAudit) {
  return (input) => {
    const result = operation(input);
    recordAudit({ input, result, status: "success" });
    return result;
  };
}
```

Этот вариант записывает аудит только для успешных операций. Если ошибки тоже нужно регистрировать, используйте `try/catch`, сохраните сведения об ошибке и снова выбросьте её. Контракт `processRows` должен описывать синхронные вызовы, аргументы `(value, index, array)`, один вызов для каждого существующего элемента, сбор результатов и распространение исключений.

### JS-FUNCTIONS-EX07

[Вернуться к условию](../../prompts/by-domain/01-javascript-and-async-programming.md#js-functions-ex07)

```js
function mountPanel(button, response) {
  const title = response.page.title;
  const sessionId = response.session.id;
  let disposed = false;

  const onClick = () => renderTitle(title);
  const refreshSession = () => refresh(sessionId);

  button.addEventListener("click", onClick);
  const timer = setInterval(refreshSession, 1000);

  return function dispose() {
    if (disposed) return;
    disposed = true;
    button.removeEventListener("click", onClick);
    clearInterval(timer);
  };
}
```

Цепочки удержания начинаются в реестрах событий и таймеров. Извлечение `title` и `sessionId` помогает только в том случае, если они сами не ссылаются на большой граф. Для проверки несколько раз выполните монтаж и очистку, при возможности дождитесь или инициируйте сборку мусора средствами профилировщика, сравните снимки кучи и изучите цепочки удержания и число экземпляров.

### JS-FUNCTIONS-EX08

[Вернуться к условию](../../prompts/by-domain/01-javascript-and-async-programming.md#js-functions-ex08)

```js
function createTokenBucket({ capacity, refill = 1 }) {
  if (!Number.isSafeInteger(capacity) || capacity < 0) {
    throw new RangeError("capacity must be a non-negative safe integer");
  }
  if (!Number.isSafeInteger(refill) || refill < 1) {
    throw new RangeError("refill must be a positive safe integer");
  }

  let tokens = capacity;

  const validateCount = (count) => {
    if (!Number.isSafeInteger(count) || count < 1) {
      throw new RangeError("count must be a positive safe integer");
    }
  };

  return {
    take(count = 1) {
      validateCount(count);
      if (tokens < count) return false;
      tokens -= count;
      return true;
    },
    add(count = refill) {
      validateCount(count);
      tokens = Math.min(capacity, tokens + count);
      return tokens;
    },
    read() {
      return { tokens, capacity };
    },
    reset() {
      tokens = capacity;
      return tokens;
    },
  };
}
```

Точечные проверки:

```js
const first = createTokenBucket({ capacity: 2 });
const second = createTokenBucket({ capacity: 2 });
console.assert(first.take(2));
console.assert(!first.take());
console.assert(second.read().tokens === 2);
console.assert(first.add() === 1);
console.assert(first.reset() === 2);
```

Возвращённые методы сохраняют окружение контейнера достижимым. Когда внешний код перестаёт хранить API и связанные регистрации, сборщик мусора может освободить это окружение.

### JS-FUNCTIONS-EX09

[Вернуться к условию](../../prompts/by-domain/01-javascript-and-async-programming.md#js-functions-ex09)

```js
function memoizeUnary(operation, { maxSize = 100 } = {}) {
  if (!Number.isInteger(maxSize) || maxSize < 1) {
    throw new RangeError("maxSize must be a positive integer");
  }

  const cache = new Map();

  function memoized(key) {
    if (cache.has(key)) {
      const value = cache.get(key);
      cache.delete(key);
      cache.set(key, value);
      return value;
    }

    const value = operation(key);
    cache.set(key, value);

    if (cache.size > maxSize) {
      const oldest = cache.keys().next().value;
      cache.delete(oldest);
    }

    return value;
  }

  memoized.clear = () => cache.clear();
  memoized.size = () => cache.size;
  return memoized;
}
```

Показательные тесты:

```js
let calls = 0;
const memoized = memoizeUnary(
  (value) => {
    calls += 1;
    return value === "none" ? undefined : { value };
  },
  { maxSize: 2 },
);

memoized("none");
memoized("none");
console.assert(calls === 1);
memoized("a");
memoized("b"); // удаляет "none"
console.assert(memoized.size() === 2);

const key = {};
console.assert(memoized(key) === memoized(key));
console.assert(memoized({}) !== memoized({}));
```

Синхронное исключение возникает до `cache.set` и поэтому не сохраняется. Для отклонённых промисов, TTL и устаревающих данных нужны отдельные явные правила.

### JS-FUNCTIONS-EX10

[Вернуться к условию](../../prompts/by-domain/01-javascript-and-async-programming.md#js-functions-ex10)

```js
function partial(operation, ...preset) {
  return (...later) => operation(...preset, ...later);
}

function pipe(...operations) {
  return (input) =>
    operations.reduce(
      (value, operation) => operation(value),
      input,
    );
}

function validateRawUser(raw) {
  if (!raw || typeof raw.name !== "string") {
    throw new TypeError("name is required");
  }
  return raw;
}

function normalizeUser(raw) {
  return {
    ...raw,
    name: raw.name.trim(),
  };
}

function projectUser(user) {
  return {
    id: user.id,
    label: user.name,
  };
}

const prepareUser = pipe(
  validateRawUser,
  normalizeUser,
  projectUser,
);

console.assert(
  prepareUser({ id: 1, name: " Ada " }).label === "Ada",
);
```

Если поменять нормализацию и проверку местами, код обратится к недопустимым данным до проверки; точечный тест с неправильным вводом поймает эту ошибку. Автоматическое каррирование не добавлено, потому что `fn.length` не учитывает остаточный параметр и параметры после первого значения по умолчанию, а обёртки и `bind` меняют это свойство.

### JS-FUNCTIONS-EX11

[Вернуться к условию](../../prompts/by-domain/01-javascript-and-async-programming.md#js-functions-ex11)

Один из обоснованных вариантов:

| Сценарий | Решение |
|---|---|
| форматтер | именованная чистая функция или стрелочная функция; состояния нет |
| DOM-контроллер | обычный метод и один сохранённый привязанный колбэк либо сохранённый стрелочный адаптер; идемпотентная очистка |
| настроенный валидатор | фабрика возвращает именованное замыкание над небольшим неизменяемым набором правил |
| кеш одного запроса | замыкание с жизненным циклом запроса, ограничением и очисткой |
| одна подпись из большой модели | извлечь подпись и не захватывать корневой граф |
| проверка + ввод-вывод + аналитика | именованные чистые этапы проверки и нормализации; явная асинхронная функция, управляющая эффектами |

Тесты проверяют значения и эффекты отдельно: чистые этапы — по входу и результату, идентичность колбэка и очистку — через поддельный реестр, кеш — по ограничению размера, а преобразование — по отсутствию мутации данных вызывающего кода.

### JS-FUNCTIONS-EX12

[Вернуться к условию](../../prompts/by-domain/01-javascript-and-async-programming.md#js-functions-ex12)

Один из вариантов переработки:

```js
function createController({
  button,
  fetchUsers,
  track,
  prefix = "user",
  maxCacheSize = 20,
}) {
  if (!button?.addEventListener || !button?.removeEventListener) {
    throw new TypeError("button must implement EventTarget methods");
  }
  if (typeof fetchUsers !== "function" || typeof track !== "function") {
    throw new TypeError("fetchUsers and track must be functions");
  }
  if (typeof prefix !== "string") {
    throw new TypeError("prefix must be a string");
  }
  if (!Number.isInteger(maxCacheSize) || maxCacheSize < 1) {
    throw new RangeError("maxCacheSize must be positive");
  }

  const cache = new Map();
  let mounted = false;

  function normalizeUser(user) {
    return {
      ...user,
      label: prefix + ":" + user.name.trim(),
    };
  }

  function remember(id, users) {
    cache.delete(id);
    cache.set(id, users);
    if (cache.size > maxCacheSize) {
      cache.delete(cache.keys().next().value);
    }
  }

  async function load(id, transform = normalizeUser) {
    if (cache.has(id)) return cache.get(id);

    const response = await fetchUsers(id);
    const result = response.users.map((user) => transform(user));
    remember(id, result);
    track("users_loaded", { id, count: result.length });
    return result;
  }

  const onClick = () => {
    void load("current").catch((error) => {
      track("users_load_failed", { message: error.message });
    });
  };

  function mount() {
    if (mounted) return;
    mounted = true;
    button.addEventListener("click", onClick);
  }

  function unmount() {
    if (!mounted) return;
    mounted = false;
    button.removeEventListener("click", onClick);
    cache.clear();
  }

  return {
    load,
    mount,
    unmount,
    clearCache: () => cache.clear(),
    cacheSize: () => cache.size,
  };
}
```

Преобразование по умолчанию больше не зависит от `this` в месте вызова, поэтому отделённый `load` работает. Ссылка на обработчик стабильна. Корневой объект ответа не сохраняется. Преобразование возвращает новый внешний объект пользователя, а аналитика выполняется после успешной операции. Кеш ограничен областью контроллера, имеет предел и очищается в конце жизненного цикла. Точечные тесты должны покрывать отделённый вызов, повторные `mount` и `unmount`, регистрацию отклонения, удаление старой LRU-записи, неизменность входных данных и неправильные зависимости.

Резюме для интервью: сделайте форму вызова и зависимости явными, отделите чистое преобразование значений от эффектов, удерживайте только нужное состояние и обеспечьте очистку для каждого долгоживущего колбэка или кеша. Компромиссы прототипов и классов остаются в разделе 1.4.

## 1.4. `this`, вызов функции и объектная модель

### JS-OBJECTS-EX01

[Вернуться к условию](../../prompts/by-domain/01-javascript-and-async-programming.md#js-objects-ex01)

Один из вариантов карты:

| Механизм | Короткое правило |
|---|---|
| обычный вызов (default binding) | при `fn()` значение `this` равно `undefined` в строгом режиме; в старом нестрогом скрипте оно может стать глобальным объектом |
| вызов метода (implicit binding) | в `object.fn()` объект слева от точки становится получателем и значением `this` |
| явный вызов (explicit binding) | `call` и `apply` вызывают функцию сразу с переданным `this`; `bind` создаёт новую функцию |
| вызов через `new` (constructor binding) | `new Fn()` создаёт объект и вызывает `Fn` с этим объектом в `this` |
| стрелочная функция | собственного `this` нет; используется `this` окружающего лексического контекста |

У `call(thisArg, a, b)` аргументы перечисляются отдельно, у `apply(thisArg, [a, b])` передаются одним array-like объектом. `bind(thisArg, a)` откладывает вызов и может заранее связать начало списка аргументов. Повторный `bind` добавляет аргументы, но не заменяет уже связанный `this`. При `new BoundFn()` новый объект имеет приоритет над связанным `this`, а связанные аргументы сохраняются.

| Способ создания | Состояние | Методы и общее поведение | Основной компромисс |
|---|---|---|---|
| объектный литерал | в одном объекте | обычно в том же объекте | ясен для одного значения, но сам по себе не является фабрикой экземпляров |
| фабрика | в замыкании или возвращённом объекте | либо новые функции на экземпляр, либо явно разделяемый объект методов | гибкая композиция и закрытое состояние ценой возможных дополнительных функций |
| функция-конструктор | в `this` | в `Constructor.prototype` | явная модель на прототипах, но нужно корректно использовать `new` |
| `Object.create(proto)` | задаётся после создания | наследуется от переданного `proto` | цепочка видна напрямую, инициализацию нужно организовать отдельно |
| класс | в экземпляре и закрытых полях | обычные методы в `Class.prototype`; поля — в экземпляре | знакомый синтаксис и закрытые поля, но под ним остаётся та же цепочка прототипов |

`Constructor.prototype` — обычное свойство объекта-функции. При `new Constructor()` внутренний `[[Prototype]]` нового экземпляра связывается со значением `Constructor.prototype`. Сам объект-функция тоже имеет собственный `[[Prototype]]`; это другая связь. Чтение свойства идёт от объекта вверх по цепочке до найденного дескриптора или `null`. Собственное свойство с тем же ключом затеняет унаследованное.

Две оси свойств независимы:

| | Перечислимое | Неперечислимое |
|---|---|---|
| Собственное | обычно видит `Object.keys` | видит `Object.getOwnPropertyNames` или `Reflect.ownKeys` |
| Унаследованное | может увидеть `for...in` | обычное перечисление пропускает |

Дескриптор данных (data descriptor) содержит `value` и `writable`; дескриптор доступа (accessor descriptor) — `get` и `set`. Оба вида могут содержать `enumerable` и `configurable`, но смешивать `value`/`writable` с `get`/`set` нельзя.

Для обычного изменяемого свойства данных матрица выглядит так:

| Состояние | Добавить | Удалить | Перенастроить дескриптор | Изменить значение |
|---|---:|---:|---:|---:|
| обычный объект | да | да | да | да |
| `preventExtensions` | нет | да | да | да |
| `seal` | нет | нет | сильно ограничено | да, пока `writable: true` |
| `freeze` | нет | нет | нет | нет для свойства данных |

Все три операции поверхностны. Они не замораживают объект, на который указывает значение свойства. Setter у замороженного объекта тоже не превращается автоматически в пустую операцию: accessor остаётся функцией и может менять внешнее или закрытое состояние.

`Proxy` — новый объект-обёртка над исходным объектом (target). Обработчик (handler) содержит перехватчики (traps) внутренних операций. Получатель (receiver) — объект, с которого началась операция; он особенно важен для getter, setter и наследования. `Reflect` помогает передать стандартную операцию дальше с теми же аргументами. Proxy имеет иную идентичность, обязан соблюдать инварианты исходного объекта и может усложнить трассировку поведения.

`__proto__` — исторический accessor на `Object.prototype`. Он не является внутренним слотом `[[Prototype]]`. Для чтения используют `Object.getPrototypeOf`; создавать объект с нужной цепочкой лучше сразу через литерал, `new` или `Object.create`, а не менять цепочку готового объекта.

Частые ошибки: выбирать форму объекта по лозунгу, считать класс отдельной моделью наследования, проверять собственность через `obj.hasOwnProperty`, ожидать глубокую заморозку и считать неперечислимые свойства или ключи Symbol приватными.

### JS-OBJECTS-EX02

[Вернуться к условию](../../prompts/by-domain/01-javascript-and-async-programming.md#js-objects-ex02)

Точный вывод:

```text
[ 'service', 'I' ]
[ 'none', 'D' ]
[ 'call', 'X-Y' ]
[ 'apply', 'X-Y' ]
[ 'first', 'A-B-C' ]
fixed large
true true
panel other
lexical lexical
```

`service.describe("I")` использует вызов метода. После отделения метода выражение `detached("D")` становится обычным вызовом: в строгом режиме `this` равен `undefined`, а оператор `?.` позволяет вернуть `"none"` без ошибки. `call` и `apply` немедленно вызывают одну функцию; различается только упаковка аргументов.

`once` уже хранит `{ name: "first" }` как связанного получателя и `"A"` как первый аргумент. Второй `bind` не заменяет получателя, но добавляет `"B"`; аргумент `"C"` приходит при вызове. Поэтому функция получает `("A", "B", "C")`.

При `new BoundWidget("large")` создаётся новый экземпляр, а не используется объект `{ name: "ignored" }`. Предварительно связанное `"fixed"` остаётся первым аргументом, поэтому поля равны `fixed` и `large`. Специальная логика `instanceof` для связанной функции делегирует проверку исходной `Widget`, поэтому обе проверки дают `true`.

У `regular` значение `this` зависит от вызова. Стрелочная `arrow` замкнула `lexicalOwner`; `call` не может подменить её `this`. Для метода с динамическим получателем нужна обычная функция.

При передаче `service.describe` колбэком можно один раз создать и сохранить `service.describe.bind(service)`. Если API должен позднее удалить обработчик, нужна та же сохранённая ссылка. Альтернатива — сохранённый адаптер `(...args) => service.describe(...args)`. Стрелку, объявленную как метод объекта только ради короткого синтаксиса, выбирать нельзя: она не получает объект слева от точки как `this`.

Все операции примера выполняются за `O(1)`. Частая ошибка — приписывать `this` месту объявления обычной функции или ожидать, что повторный `bind` заменит получателя.

### JS-OBJECTS-EX03

[Вернуться к условию](../../prompts/by-domain/01-javascript-and-async-programming.md#js-objects-ex03)

Основные связи:

```text
Account --.prototype--> Account.prototype
first  --[[Prototype]]--> Account.prototype
second --[[Prototype]]--> Account.prototype
Account.prototype --[[Prototype]]--> Object.prototype --> null
Account --[[Prototype]]--> Function.prototype --> Object.prototype --> null
```

У `first` и `second` собственное свойство `name`; `kind` и `label` находятся через `Account.prototype`.

```js
console.assert(first.label() === "account:Ada");
console.assert(second.label() === "account:Lin");
console.assert(Object.getPrototypeOf(first) === Account.prototype);
console.assert(Object.getPrototypeOf(second) === Account.prototype);
console.assert(Account.prototype.isPrototypeOf(first));
console.assert(Account.prototype.isPrototypeOf(second));
console.assert(first instanceof Account);
console.assert(second instanceof Account);
```

`new ReturnsPrimitive()` игнорирует возвращённый primitive и отдаёт созданный объект `{ ok: true }`. `new ReturnsObject()` получает явно возвращённый объект `{ ok: false }` и отдаёт его вместо созданного экземпляра.

```js
console.assert(primitiveResult.ok === true);
console.assert(primitiveResult instanceof ReturnsPrimitive);
console.assert(objectResult.ok === false);
console.assert(!(objectResult instanceof ReturnsObject));
```

Пять шагов `new`: создать объект; связать его `[[Prototype]]` с текущим `Constructor.prototype`; вызвать функцию с новым объектом в `this`; проверить явный результат; вернуть явно возвращённый объект или функцию либо созданный объект. Явный primitive не заменяет экземпляр.

Защита от вызова без `new`:

```js
function Account(name) {
  if (!new.target) {
    throw new TypeError("Account must be called with new");
  }
  this.name = name;
}
```

Стрелочная функция не имеет внутреннего метода `[[Construct]]` и собственного свойства `.prototype`, поэтому `new (() => {})` приводит к `TypeError`.

У `dictionary` цепочка сразу заканчивается на `null`. Он не наследует `toString`, `constructor` и `hasOwnProperty`:

```js
console.assert(Object.getPrototypeOf(dictionary) === null);
console.assert(dictionary.toString === undefined);
console.assert(dictionary.constructor === undefined);
console.assert(dictionary.hasOwnProperty === undefined);
console.assert(Object.hasOwn(dictionary, "answer"));
```

Современный буквальный эквивалент старой записи для уже созданного объекта — `Object.setPrototypeOf(value, Account.prototype)`. Для нового объекта предпочтительнее сразу `Object.create(Account.prototype)`. Динамическое изменение цепочки прототипов ухудшает предсказуемость, может деоптимизировать доступ к свойствам и затрудняет ревью.

`instanceof` проверяет наличие `Constructor.prototype` в цепочке. Объект из другой среды выполнения (realm) обычно связан с другим `Array.prototype`, поэтому, например, `foreignArray instanceof Array` может быть `false`; для массивов есть `Array.isArray`. Проверка также зависит от текущего `.prototype` и может быть настроена через `Symbol.hasInstance`. Свойство `constructor` — обычное наследуемое и изменяемое свойство: его можно затенить, удалить или получить не от того прототипа. Поэтому `value.constructor === Account` не является надёжной общей проверкой типа.

Поиск свойства занимает `O(d)`, где `d` — пройденная глубина цепочки; создание и проверки в этой фиксированной цепочке практически постоянны. Частая ошибка — рисовать связь `first → Account`; экземпляр связан с `Account.prototype`, а не с самой функцией.

### JS-OBJECTS-EX04

[Вернуться к условию](../../prompts/by-domain/01-javascript-and-async-programming.md#js-objects-ex04)

До последней строки вывод будет таким:

```text
user:Ada
2 1
0 false
base:Ada
```

`user.prefix = "user"` и `user.name = "Ada"` создают собственные свойства. В `user.count += 1` сначала читается унаследованное `base.count === 1`, затем результат `2` записывается как собственное `user.count`; `base.count` не меняется.

Присваивание `user.score = -3` находит setter в `base`, но вызывает его с получателем `user`. Поэтому `this._score = 0` создаёт собственное свойство `_score` у `user`, а собственного свойства `score` не появляется. Getter `label` также найден в `base`, но читает `this.prefix` и `this.name` у `user`. После удаления собственного `prefix` поиск находит `base.prefix`, поэтому результат меняется на `base:Ada`.

`locked` — унаследованное свойство данных с `writable: false`. Обычное присваивание не может затенить его и в строгом режиме приводит к `TypeError`. Ни собственного `user.locked`, ни изменения `base.locked` не происходит.

Явное определение собственного свойства не использует обычный алгоритм присваивания:

```js
Object.defineProperty(user, "locked", {
  value: 20,
  writable: true,
  enumerable: true,
  configurable: true,
});

console.assert(user.locked === 20);
console.assert(base.locked === 10);
```

Это возможно, пока `user` расширяем и инварианты объекта или Proxy не запрещают операцию. Конфигурируемость одноимённого свойства в прототипе не управляет созданием собственного свойства потомка.

Если `base.options = { enabled: false }`, выражение `user.options.enabled = true` не присваивает `user.options`. Оно сначала получает одну общую ссылку из прототипа, затем меняет сам объект. В результате изменение видно и через `base.options`. Для собственного состояния нужен отдельный объект на экземпляр.

Стоимость поиска равна `O(d)` по глубине цепочки. Частые ошибки: считать, что setter выполняется с `this === base`, и считать любое присваивание автоматическим созданием собственного свойства.

### JS-OBJECTS-EX05

[Вернуться к условию](../../prompts/by-domain/01-javascript-and-async-programming.md#js-objects-ex05)

Матрица наличия:

| Ключ | `Object.hasOwn(record, key)` | `key in record` |
|---|---:|---:|
| `inheritedVisible` | `false` | `true` |
| `inheritedHidden` | `false` | `true` |
| `ownVisible` | `true` | `true` |
| `ownHidden` | `true` | `true` |
| `token` | `true` | `true` |

Результаты перечисления:

```js
Object.keys(record);                // ["ownVisible"]
Object.values(record);              // [3]
Object.entries(record);             // [["ownVisible", 3]]

const fromForIn = [];
for (const key in record) fromForIn.push(key);
// ["ownVisible", "inheritedVisible"]

Object.getOwnPropertyNames(record);   // ["ownVisible", "ownHidden"]
Object.getOwnPropertySymbols(record); // [token]
Reflect.ownKeys(record);              // ["ownVisible", "ownHidden", token]
```

`for...in` видит перечисляемые строковые свойства по цепочке; символы он не перечисляет. В данном примере порядок показан по обычному порядку ключей каждого объекта, но рабочий код не должен использовать `for...in` как способ получить только собственные данные.

Нужные функции:

```js
function ownEnumerableStringEntries(object) {
  return Object.entries(object);
}

function allOwnKeys(object) {
  return Reflect.ownKeys(object);
}
```

Если нужны только ключи, первая функция может вернуть `Object.keys(object)`. При работе внутри `for...in` собственность проверяют так:

```js
for (const key in record) {
  if (!Object.hasOwn(record, key)) continue;
  // собственное перечисляемое строковое свойство
}
```

`Object.hasOwn(value, key)` безопасен и для `Object.create(null)`, и для `{ hasOwnProperty: "data" }`. Прямой вызов `value.hasOwnProperty(key)` в обоих случаях ненадёжен; старый универсальный вариант выглядит как `Object.prototype.hasOwnProperty.call(value, key)`.

Неперечисляемый ключ доступен при прямом чтении и через API отражения (reflection API). Ключ-символ тоже можно получить, если символ известен, или найти через `Reflect.ownKeys`. Это средства управления обнаружением и конфликтами имён, а не защита данных. Языковую приватность дают закрытые поля класса, а закрытое состояние можно хранить в замыкании.

Все показанные проверки одного ключа обычно `O(1)` в практической модели. Перечисление стоит `O(n)` по числу возвращаемых или проверяемых свойств. Частая ошибка — путать «существует где-то в цепочке» с «принадлежит самому объекту».

### JS-OBJECTS-EX06

[Вернуться к условию](../../prompts/by-domain/01-javascript-and-async-programming.md#js-objects-ex06)

Если `Object.defineProperty` создаёт новое свойство и флаг пропущен, `writable`, `enumerable` и `configurable` получают `false`. Поэтому A создаёт `name` с `writable: false`, а последующее присваивание в строгом режиме приводит к `TypeError`.

Исправленный дескриптор данных:

```js
Object.defineProperty(profile, "name", {
  value: "Ada",
  writable: true,
  enumerable: true,
  configurable: true,
});

profile.name = "Lin";
console.assert(profile.name === "Lin");
console.assert(Object.keys(profile).includes("name"));
```

B смешивает поля двух несовместимых видов дескриптора: `value` и `get`. `Object.defineProperty` приводит к `TypeError`. Корректный вычисляемый accessor:

```js
Object.defineProperty(profile, "displayName", {
  get() {
    return `${this.prefix}:${this.name}`;
  },
  enumerable: true,
  configurable: true,
});

console.assert(profile.displayName === "user:Lin");
```

Setter `score` найден в `scorePrototype`, но получатель равен `row`. Присваивание создаёт собственный `row._score` со значением `7`; собственного `row.score` нет. Getter тоже вызывается с `this === row` и возвращает `7`.

```js
console.assert(row.score === 7);
console.assert(Object.hasOwn(row, "_score"));
console.assert(!Object.hasOwn(row, "score"));

console.log(
  Object.getOwnPropertyDescriptor(row, "_score"),
);
// { value: 7, writable: true, enumerable: true, configurable: true }

console.log(
  Object.getOwnPropertyDescriptor(scorePrototype, "score"),
);
// { get: [Function], set: [Function], enumerable: true, configurable: true }
```

Литерал объекта создаёт getter и setter как перечисляемые и настраиваемые свойства. `Object.getOwnPropertyDescriptors(profile)` возвращает карту дескрипторов всех собственных ключей и полезен, когда нужно сохранить их при переносе свойств; простое чтение и присваивание превратило бы accessor в вычисленное значение.

Getter должен выглядеть как чтение. Сетевой запрос, аналитика, изменение состояния или тяжёлая работа могут запускаться повторно при логировании, сериализации, шаблонизации или просмотре объекта в инструментах разработчика. Для заметного эффекта понятнее явный метод. Частые ошибки: ожидать у `defineProperty` те же значения флагов по умолчанию, что у объектного литерала, и считать `this` внутри унаследованного accessor самим прототипом.

### JS-OBJECTS-EX07

[Вернуться к условию](../../prompts/by-domain/01-javascript-and-async-programming.md#js-objects-ex07)

В derived constructor до `super()` нет инициализированного `this`. Исправление:

```js
class User extends Entity {
  constructor(id, name) {
    super(id);
    this.name = name;
  }
}
```

После него расположение членов такое:

| Член | Где находится | Перечисляемый | Разделяется экземплярами |
|---|---|---:|---:|
| `readId` | `Entity.prototype` | нет | да |
| `describe` для User | `User.prototype` | нет | да |
| `role` | собственное поле экземпляра | да | нет, значение создаётся на экземпляре |
| `onSelect` | собственное поле экземпляра | да | нет, новая стрелочная функция на экземпляр |
| `category` | собственное статическое поле у `Entity` | да | наследуется объектом-конструктором `User` |

Проверки:

```js
const first = new User("1", "Ada");
const second = new User("2", "Lin");

console.assert(first.describe === second.describe);
console.assert(first.onSelect !== second.onSelect);
console.assert(first.onSelect() === "entity:1:Ada");
console.assert(User.category === "entity");
console.assert(User.create({ id: "3", name: "Sam" }) instanceof User);
console.assert(Entity.hasEntityBrand(first));
```

Отделённый `describe` вызывается без экземпляра. Ссылка `super.describe` определяется лексически через метод класса, но вызов сохраняет текущий `this`; в данном случае он равен `undefined`, и доступ к приватному полю приводит к `TypeError`. Стрелочная `onSelect` захватила `this` во время инициализации экземпляра, поэтому отделённый вызов работает. Цена — отдельная функция на каждый экземпляр и перечисляемое собственное поле.

Экземпляр `User` получает закрытое состояние `Entity`, когда `super(id)` выполняет базовый конструктор. Метод `Entity.prototype.readId` может читать это состояние. Код класса `User` не может написать `this.#id`: закрытое имя доступно только в лексической области объявления `Entity`. `Entity.prototype.readId.call({})` приводит к `TypeError`, потому что у обычного объекта нет нужной приватной метки.

Минимальный пример закрытого метода и закрытого статического поля:

```js
class Formatter {
  static #prefix = "entity";

  #format(value) {
    return `${Formatter.#prefix}:${value}`;
  }

  format(value) {
    return this.#format(value);
  }
}
```

Если `User` действительно является разновидностью `Entity` и должен сохранять базовый контракт, неглубокое наследование оправдано. Если `role`, выбор подписи и обработчик — независимые возможности, композиция функций или внедрённых стратегий обычно проще: она не связывает изменения несколькими уровнями `super`. Частые ошибки: пытаться использовать `this` до `super()`, считать поля методами прототипа и ожидать, что приватное поле доступно подклассу по имени.

Создание экземпляра и вызов методов здесь имеют `O(1)`; память prototype method разделяется, а arrow field требует отдельную функцию на экземпляр.

### JS-OBJECTS-EX08

[Вернуться к условию](../../prompts/by-domain/01-javascript-and-async-programming.md#js-objects-ex08)

Сравнение:

| Вариант | Состояние | Методы | Сильная сторона | Ограничение |
|---|---|---|---|---|
| один литерал | в одном объекте | в нём же | минимальный код для одного счётчика | неудобно создавать много независимых значений |
| фабрика | в замыкании или результате | часто новые функции на вызов | закрытое состояние, явные зависимости, композиция | функции могут повторяться для каждого экземпляра |
| constructor | в `this` | общие функции в `.prototype` | экономное общее поведение и явная связь экземпляров | публичное состояние доступно напрямую; нужен `new` |
| `Object.create` | в созданном объекте | в переданном `counterMethods` | цепочка прототипов видна без конструктора | отдельная инициализация, менее привычный API команды |
| класс | в полях или `#count` | обычные методы в `.prototype` | закрытые поля, знакомый синтаксис, общие методы | легко построить лишнюю иерархию или перепутать методы с полями экземпляров |

Для рабочего кода разумны, например, фабрика с закрытым состоянием и класс с приватным полем. Выбор зависит от контракта и соглашений команды.

Набросок фабрики:

```js
function createCounter(initial, validateStep = Number.isSafeInteger) {
  let count = initial;

  return {
    increment(step = 1) {
      if (!validateStep(step)) throw new RangeError("invalid step");
      count += step;
      return count;
    },
    read() {
      return count;
    },
  };
}
```

Набросок класса:

```js
class Counter {
  #count;
  #validateStep;

  constructor(initial, validateStep = Number.isSafeInteger) {
    this.#count = initial;
    this.#validateStep = validateStep;
  }

  increment(step = 1) {
    if (!this.#validateStep(step)) throw new RangeError("invalid step");
    this.#count += step;
    return this.#count;
  }

  read() {
    return this.#count;
  }
}
```

Разную политику проверки лучше передать аргументом. Подклассы `PositiveCounter`, `EvenCounter`, `SmallCounter` быстро дали бы комбинаторный рост вариантов. В обоих решениях основные операции выполняются за `O(1)`. На интервью важно назвать не победителя, а требования: число экземпляров, закрытость состояния, общие методы, привычность API, композиция политик и профиль памяти.

### JS-OBJECTS-EX09

[Вернуться к условию](../../prompts/by-domain/01-javascript-and-async-programming.md#js-objects-ex09)

Общие проверки:

```js
function assertInitial(value) {
  if (!Number.isSafeInteger(value)) {
    throw new TypeError("initial must be a safe integer");
  }
}

function assertValidator(value) {
  if (typeof value !== "function") {
    throw new TypeError("validateStep must be a function");
  }
}

function assertStep(step, validateStep) {
  if (!Number.isSafeInteger(step) || !validateStep(step)) {
    throw new RangeError("invalid step");
  }
}

const acceptEveryStep = () => true;
```

Фабрика с закрытым состоянием:

```js
function createCounter(
  initial,
  validateStep = acceptEveryStep,
) {
  assertInitial(initial);
  assertValidator(validateStep);

  let count = initial;

  return {
    increment(step = 1) {
      assertStep(step, validateStep);
      count += step;
      return count;
    },
    read() {
      return count;
    },
  };
}
```

Constructor function с общими методами:

```js
function Counter(
  initial,
  validateStep = acceptEveryStep,
) {
  if (!new.target) {
    throw new TypeError("Counter must be called with new");
  }

  assertInitial(initial);
  assertValidator(validateStep);

  this._count = initial;
  Object.defineProperty(this, "_validateStep", {
    value: validateStep,
    writable: false,
    enumerable: false,
    configurable: false,
  });
}

Counter.prototype.increment = function increment(step = 1) {
  assertStep(step, this._validateStep);
  this._count += step;
  return this._count;
};

Counter.prototype.read = function read() {
  return this._count;
};
```

Точечные проверки:

```js
const factoryA = createCounter(1, (step) => step > 0);
const factoryB = createCounter(10, (step) => step > 0);
console.assert(factoryA.increment(2) === 3);
console.assert(factoryB.read() === 10);

const instanceA = new Counter(1, (step) => step > 0);
const instanceB = new Counter(10, (step) => step > 0);
console.assert(instanceA.increment(2) === 3);
console.assert(instanceB.read() === 10);
console.assert(instanceA.increment === instanceB.increment);
console.assert(!Object.hasOwn(instanceA, "increment"));
console.assert(Object.getPrototypeOf(instanceA) === Counter.prototype);

console.assert(factoryA.increment !== factoryB.increment);

console.assert(throws(() => Counter(0), TypeError));
console.assert(throws(() => createCounter(1.5), TypeError));
console.assert(throws(() => instanceA.increment(-1), RangeError));
```

Здесь `throws` — обычный тестовый helper конкретного проекта, который проверяет constructor ошибки. Если его нет, проверки выполняют через `try/catch` или API test runner.

Короткая форма класса с теми же общими методами могла бы хранить счётчик в `#count` и валидатор в `#validateStep`; методы `increment` и `read` всё равно находились бы в `Counter.prototype`.

Фабрика лучше закрывает состояние, но в показанном варианте создаёт две новые функции на экземпляр. Функция-конструктор разделяет методы, но `_count` остаётся доступным для прямой записи. Закрытые поля класса совмещают общие методы с языковой приватностью. Все операции имеют `O(1)` по времени и состоянию экземпляра. Частые ошибки: положить методы внутрь функции-конструктора, забыть проверить вызов без `new` и считать подчёркивание настоящей приватностью.

### JS-OBJECTS-EX10

[Вернуться к условию](../../prompts/by-domain/01-javascript-and-async-programming.md#js-objects-ex10)

Вывод:

```text
red
red
true
false
```

`config.theme` и `defaults.theme` указывают на один объект. `Object.freeze(config)` меняет только дескрипторы собственных свойств `config`; вложенные объекты не обходятся. Поэтому запись в `palette.accent` разрешена и видна через обе корневые ссылки.

Матрица для свойства данных, которое изначально имеет `configurable: true` и `writable: true`:

| Состояние объекта | Добавить | Удалить | Изменить дескриптор | Изменить существующее значение |
|---|---:|---:|---:|---:|
| обычный | да | да | да | да |
| `preventExtensions` | нет | да | да | да |
| `seal` | нет | нет | только совместимые изменения; `configurable` уже `false` | да, пока `writable: true` |
| `freeze` | нет | нет | нет, кроме идемпотентного описания | нет для свойства данных |

Нормализация известной схемы:

```js
function createFrozenConfig(input = {}) {
  const retries = input.retries ?? 3;
  const accent = input.theme?.palette?.accent ?? "blue";

  if (!Number.isSafeInteger(retries) || retries < 0) {
    throw new TypeError("retries must be a non-negative safe integer");
  }
  if (typeof accent !== "string" || accent.length === 0) {
    throw new TypeError("accent must be a non-empty string");
  }

  const palette = Object.freeze({ accent });
  const theme = Object.freeze({ palette });
  return Object.freeze({ retries, theme });
}

const sourceTheme = { palette: { accent: "green" } };
const safeConfig = createFrozenConfig({ theme: sourceTheme });

console.assert(safeConfig.theme !== sourceTheme);
console.assert(safeConfig.theme.palette !== sourceTheme.palette);
console.assert(Object.isFrozen(safeConfig));
console.assert(Object.isFrozen(safeConfig.theme));
console.assert(Object.isFrozen(safeConfig.theme.palette));
console.assert(!Object.isExtensible(safeConfig));
console.assert(Object.isSealed(safeConfig));
```

В строгом режиме следующие операции приводят к `TypeError`:

```js
safeConfig.extra = true;
delete safeConfig.retries;
safeConfig.retries = 4;
Object.defineProperty(safeConfig, "retries", { writable: true });
```

`const` запрещает повторное присваивание переменной, но не меняет объект. `freeze` фиксирует собственные свойства одного объекта. Глубокая неизменяемость требует пройти весь принадлежащий приложению граф или создать данные в форме, которая не раскрывает изменяемые ссылки.

Универсальный `deepFreeze` должен обходить все нужные собственные ключи, обычно через `Reflect.ownKeys`, хранить посещённые объекты для циклов и иметь правило для внешних объектов, функций, DOM-узлов и других значений с особыми внутренними слотами. Стоимость полного обхода — `O(n + e)` для объектов и связей, а не `O(1)`. В этой задаче явная нормализация фиксированной схемы проще и безопаснее. Частые ошибки: заморозить только корень, повторно использовать входной вложенный объект и обещать защиту от внешнего кода, который всё ещё владеет исходной ссылкой.

### JS-OBJECTS-EX11

[Вернуться к условию](../../prompts/by-domain/01-javascript-and-async-programming.md#js-objects-ex11)

Первый фрагмент выводит `1`. Перехватчик выполняет `currentTarget[key]`, поэтому getter вызывается с `this === target` и читает `target._value`. Исходный получатель `child`, где `_value === 9`, теряется.

Прозрачная передача чтения:

```js
const forwarded = new Proxy(target, {
  get(currentTarget, key, receiver) {
    return Reflect.get(currentTarget, key, receiver);
  },
});

const forwardedChild = Object.create(forwarded);
forwardedChild._value = 9;
console.assert(forwardedChild.value === 9);
```

Во втором фрагменте присваивание приводит к `TypeError`. Proxy не имеет права сообщить об успешной записи другого значения в собственное неконфигурируемое и неизменяемое свойство данных исходного объекта. Это инвариант, а не пожелание стиля. Прозрачный перехватчик:

```js
const honest = new Proxy(fixedTarget, {
  set(currentTarget, key, value, receiver) {
    return Reflect.set(currentTarget, key, value, receiver);
  },
});
```

`Reflect.set` вернёт `false`; присваивание в строгом режиме преобразует этот отказ в `TypeError`. Trap не должен безусловно возвращать `true`.

Третий фрагмент тоже приводит к `TypeError`. Метод получен через Proxy, а в выражении `wrappedVault.read()` получателем вызова становится Proxy. Приватная метка `Vault` установлена у исходного объекта, но не у Proxy. Похожая проблема возникает у некоторых встроенных объектов с внутренними слотами (internal slots).

Перехватчик, который автоматически связывает каждую функцию с исходным объектом, может заставить конкретный метод работать, но меняет семантику `this`, ломает ожидаемое наследование и без кеширования возвращает новую функцию при каждом чтении:

```js
wrapped.method === wrapped.method; // может стать false
```

Кеширование связанных функций добавляет состояние и новые углы поведения. Для `Vault` обычно понятнее явная обёртка с методом `read() { return vault.read(); }` или API, который не обещает прозрачность.

`proxy !== target`. Они являются разными ключами `Map`, `Set` и `WeakMap`, не проходят строгое сравнение и могут отдельно появляться в трассировках и логах. Обёртывание всего графа требует политики сохранения идентичности, иначе один исходный объект может получить несколько Proxy.

Дескриптор подходит для локального контроля одного свойства. Обычная функция или явная обёртка лучше, когда нужны проверка аргументов и видимый контракт. Proxy оправдан при действительно динамическом наборе операций: наблюдение, виртуализация, мембрана доступа или внутренний механизм фреймворка. Доступ к свойству остаётся `O(d)` по цепочке, но каждый перехват добавляет постоянную работу; в горячем пути её нужно измерять. Частые ошибки: забыть получателя, лгать о результате операции и считать пустой Proxy полностью прозрачным.

### JS-OBJECTS-EX12

[Вернуться к условию](../../prompts/by-domain/01-javascript-and-async-programming.md#js-objects-ex12)

Один из вариантов:

```js
function createSettingsView(target, schema) {
  if (target === null || typeof target !== "object") {
    throw new TypeError("target must be an object");
  }
  if (schema === null || typeof schema !== "object") {
    throw new TypeError("schema must be an object");
  }

  for (const key of Object.keys(schema)) {
    if (typeof schema[key] !== "function") {
      throw new TypeError(`schema.${key} must be a function`);
    }
  }

  return Proxy.revocable(target, {
    set(currentTarget, key, value, receiver) {
      if (typeof key !== "string" || !Object.hasOwn(schema, key)) {
        throw new TypeError(`unknown setting: ${String(key)}`);
      }
      if (!schema[key](value)) {
        throw new TypeError(`invalid value for ${key}`);
      }
      return Reflect.set(currentTarget, key, value, receiver);
    },

    deleteProperty(currentTarget, key) {
      if (typeof key === "string" && Object.hasOwn(schema, key)) {
        throw new TypeError(`cannot delete setting: ${key}`);
      }
      return Reflect.deleteProperty(currentTarget, key);
    },
  });
}
```

Проверки:

```js
function throws(operation, ErrorType) {
  try {
    operation();
    return false;
  } catch (error) {
    return error instanceof ErrorType;
  }
}

const target = {
  theme: "light",
  debug: false,
  temporary: 1,
};

const schema = Object.assign(Object.create(null), {
  theme: (value) => value === "light" || value === "dark",
  debug: (value) => typeof value === "boolean",
});

const { proxy, revoke } = createSettingsView(target, schema);

proxy.theme = "dark";
console.assert(target.theme === "dark");
console.assert(proxy !== target);
console.assert(Object.keys(proxy).join(",") === "theme,debug,temporary");

console.assert(throws(() => {
  proxy.extra = 1;
}, TypeError));

console.assert(throws(() => {
  proxy.debug = "yes";
}, TypeError));

console.assert(delete proxy.temporary);
console.assert(!Object.hasOwn(target, "temporary"));
console.assert(throws(() => {
  delete proxy.theme;
}, TypeError));

revoke();
console.assert(throws(() => proxy.theme, TypeError));
```

Неперехваченные чтение и перечисление передаются исходному объекту стандартным механизмом Proxy. `Reflect.set` сохраняет получателя и возвращает реальный результат; если дескриптор или расширяемость исходного объекта запрещают операцию, перехватчик не скрывает отказ. Проверка действует только для операций через Proxy: код с прямой ссылкой на исходный объект может её обойти, поэтому такой фасад сам по себе не является границей безопасности.

При доступе к правилу за `O(1)` каждое перехваченное присваивание и удаление тоже требует `O(1)` дополнительной работы; перечисление остаётся `O(n)`. Альтернатива для небольшого фиксированного набора настроек — явные методы `setTheme` и `setDebug`: их легче искать, типизировать и отлаживать.

### JS-OBJECTS-EX13

[Вернуться к условию](../../prompts/by-domain/01-javascript-and-async-programming.md#js-objects-ex13)

Один обоснованный набор решений:

| Сценарий | Основной подход | Почему | Отвергнутый избыточный вариант |
|---|---|---|---|
| одна конфигурация | объектный литерал, при необходимости нормализация и `freeze` | состояние видно прямо, поведения нет | класс добавит лишнюю конструкцию без общего поведения |
| много однотипных сущностей | класс или конструктор с общими методами прототипа | одна точка проверки, методы разделяются | отдельный литерал на экземпляр не задаёт создание |
| закрытое состояние и две операции | фабрика с замыканием | зависимости и жизненный цикл локальны | Proxy скрывает простой контракт за перехватами |
| три независимые возможности | композиция функций или стратегий | возможности комбинируются без глубокой иерархии | цепочка подклассов связывает независимые изменения |
| вычисляемое совместимое свойство | неперечислимый getter через `defineProperty` | точечное чтение без изменения всего объекта | Proxy слишком широк для одного известного ключа |
| нельзя расширять, значения меняются | `Object.preventExtensions` | запрещает новые ключи, не запрещая нужные записи | `freeze` сломает требуемые изменения |
| динамическая проверка записей | Proxy на контролируемой границе либо явный `set(key, value)` | Proxy охватывает неизвестные заранее ключи; метод проще трассировать | множество статических setters не подходит динамической схеме |
| DOM-обработчик | один сохранённый связанный метод или стрелочный адаптер | стабильная идентичность для добавления и удаления | новый `bind` при каждом вызове нельзя удалить старой ссылкой |

У литерала, результата фабрики и экземпляра состояние обычно является собственными свойствами; у фабрики оно также может жить в замыкании. Конструктор, класс и `Object.create` позволяют вынести поведение в прототип. Обычный метод прототипа получает динамический `this`; закрытое замыкание или сохранённая стрелка могут не зависеть от формы вызова.

Собственные ключи проверяют через `Object.hasOwn`. Перед выбором перечисления нужно решить, нужны ли унаследованные, неперечисляемые ключи и символы. `JSON.stringify` обычно берёт собственные перечисляемые строковые свойства и вызывает `toJSON`, если он есть; скрытый дескриптор и закрытое поле автоматически туда не попадут.

Проверки должны охватывать не только значения, но и форму объекта: `Object.getPrototypeOf`, `Object.keys`, дескрипторы, идентичность методов, отказ недопустимой операции и поведение отделённого вызова. Proxy требует отдельной проверки инвариантов, идентичности и получателя.

Пример ответа за 30–60 секунд для динамических настроек:

> Я сначала выясню, можно ли выразить запись явным методом `set(key, value)`: он проще для типов, поиска по коду и отладки. Proxy выберу, только если потребителю действительно нужен обычный синтаксис свойств при динамической схеме. Тогда перехватчик проверит ключ и значение, передаст запись через `Reflect.set` с исходным получателем и вернёт реальный результат. Исходный объект не должен утекать наружу, иначе проверку можно обойти. Я отдельно протестирую недоступные для записи свойства, перечисление, отзыв и различие идентичности исходного объекта и Proxy.

Частая ошибка — выбирать класс, фабрику или Proxy по моде. Сначала определяют владение состоянием, число экземпляров, требования к идентичности, перечислению, расширению и отладке.

### JS-OBJECTS-EX14

[Вернуться к условию](../../prompts/by-domain/01-javascript-and-async-programming.md#js-objects-ex14)

Основные проблемы исходника:

1. Getter и метод в `accountMethods` перечисляемы, потому что созданы литералом. `for...in` может вернуть унаследованные `label` и `rename` вместе с данными.
2. `Object.assign` принимает лишние ключи и сохраняет общую ссылку на `permissions`. Значение можно менять через исходный объект даже после поверхностного `freeze(account)`.
3. `audit` не сохраняется, поэтому `this.audit("renamed")` не выполняет переданный контракт.
4. `name` заморожен как собственное свойство данных, поэтому `rename` не может его изменить.
5. `id` сначала создаётся через `Object.assign`, а затем переопределяется неполным дескриптором. Для существующего свойства пропущенные флаги сохраняют прежние значения; только последующий `freeze` делает его недоступным для записи и ненастраиваемым. Код случайно получает нужный итог и скрывает намерение. Для нового свойства пропущенные флаги были бы `false`.
6. Перехватчик `get` использует исходный объект как получателя. Для `label` это пока даёт похожий результат, но ломает прозрачное наследование и поведение accessor-свойства. Нужен `Reflect.get(target, key, receiver)`.
7. Перехватчик `set` пытается записать в замороженный исходный объект и в строгом режиме получает `TypeError`. Если бы перехватчик просто вернул `true` для неконфигурируемого и неизменяемого свойства, это нарушило бы инвариант Proxy и тоже привело бы к `TypeError`.
8. Proxy имеет другую идентичность, усложняет логи и коллекции, но в примере не даёт полезного контракта.
9. `Object.setPrototypeOf` не сможет изменить прототип замороженного, нерасширяемого исходного объекта. Даже без `freeze` динамическая смена цепочки ухудшает предсказуемость и производительность.
10. `{ ...accountMethods }` при продвижении прочитает getter `label` во время spread и превратит результат в свойство данных. Это ещё одна причина не собирать поведение таким способом.

Один из исправленных вариантов использует класс для общих неперечислимых методов и закрытые поля для имени и аудита:

```js
function assertNonEmptyString(value, field) {
  if (typeof value !== "string" || value.trim().length === 0) {
    throw new TypeError(`${field} must be a non-empty string`);
  }
  return value.trim();
}

function normalizePermissions(value = {}) {
  if (value === null || typeof value !== "object") {
    throw new TypeError("permissions must be an object");
  }

  for (const key of ["read", "write", "remove"]) {
    if (Object.hasOwn(value, key) && typeof value[key] !== "boolean") {
      throw new TypeError(`permissions.${key} must be boolean`);
    }
  }

  return Object.freeze({
    read: value.read === true,
    write: value.write === true,
    remove: value.remove === true,
  });
}

class Account {
  #name;
  #audit;

  constructor(input, audit) {
    if (input === null || typeof input !== "object") {
      throw new TypeError("input must be an object");
    }
    if (typeof audit !== "function") {
      throw new TypeError("audit must be a function");
    }

    const id = assertNonEmptyString(input.id, "id");
    const name = assertNonEmptyString(input.name, "name");
    const permissions = normalizePermissions(input.permissions);

    this.#name = name;
    this.#audit = audit;

    Object.defineProperties(this, {
      id: {
        value: id,
        writable: false,
        enumerable: true,
        configurable: false,
      },
      permissions: {
        value: permissions,
        writable: false,
        enumerable: true,
        configurable: false,
      },
    });

    Object.seal(this);
  }

  static isAccount(value) {
    return (
      value !== null &&
      typeof value === "object" &&
      #name in value
    );
  }

  get name() {
    return this.#name;
  }

  get label() {
    return `${this.id}:${this.#name}`;
  }

  rename(nextName) {
    const normalized = assertNonEmptyString(nextName, "name");
    const previous = this.#name;

    this.#name = normalized;
    try {
      this.#audit("account.renamed", {
        id: this.id,
        from: previous,
        to: normalized,
      });
    } catch (error) {
      this.#name = previous;
      throw error;
    }

    return this.#name;
  }

  toJSON() {
    return {
      id: this.id,
      name: this.#name,
      permissions: this.permissions,
    };
  }
}

function canDelete(account) {
  if (!Account.isAccount(account)) {
    throw new TypeError("account must be an Account");
  }
  return account.permissions.remove;
}
```

Точечные проверки:

```js
const events = [];
const inputPermissions = {
  read: true,
  write: false,
  remove: true,
};

function throws(operation, ErrorType) {
  try {
    operation();
    return false;
  } catch (error) {
    return error instanceof ErrorType;
  }
}

const account = new Account(
  {
    id: "a-1",
    name: "Ada",
    permissions: inputPermissions,
  },
  (type, payload) => events.push({ type, payload }),
);

console.assert(account.label === "a-1:Ada");
console.assert(Account.isAccount(account));
console.assert(Account.prototype.isPrototypeOf(account));
console.assert(!Object.hasOwn(account, "rename"));
console.assert(
  Object.getOwnPropertyDescriptor(
    Account.prototype,
    "rename",
  ).enumerable === false,
);

console.assert(Object.keys(account).join(",") === "id,permissions");
console.assert(Reflect.ownKeys(account).includes("id"));

const idDescriptor = Object.getOwnPropertyDescriptor(account, "id");
console.assert(idDescriptor.enumerable === true);
console.assert(idDescriptor.writable === false);
console.assert(idDescriptor.configurable === false);

console.assert(Object.isSealed(account));
console.assert(Object.isFrozen(account.permissions));
console.assert(account.permissions !== inputPermissions);

inputPermissions.read = false;
console.assert(account.permissions.read === true);

console.assert(account.rename("Lin") === "Lin");
console.assert(account.label === "a-1:Lin");
console.assert(events.length === 1);
console.assert(events[0].payload.from === "Ada");
console.assert(events[0].payload.to === "Lin");
console.assert(canDelete(account) === true);

console.assert(Reflect.set(account, "name", "Bypass") === false);
console.assert(Reflect.set(account, "extra", true) === false);
console.assert(Reflect.deleteProperty(account, "id") === false);
console.assert(throws(() => {
  new Account({ id: "", name: "Ada" }, () => {});
}, TypeError));
```

Класс хранит методы и getter в `Account.prototype`; синтаксис класса создаёт их неперечислимыми. `name` не является обычным свойством, поэтому присваивание не обходит `rename`. Если аудит бросает исключение, метод возвращает закрытое состояние к прежнему значению. Полную атомарность с внешней системой аудита JavaScript обеспечить не может: колбэк мог частично выполнить внешний эффект. Для такой границы нужен отдельный прикладной протокол.

`Object.seal(account)` управляет только собственными свойствами. Закрытые поля не являются обычными свойствами, поэтому метод продолжает менять `#name`. Из-за неизменяемых собственных свойств данных `Object.isFrozen(account)` может даже вернуть `true`, хотя закрытое состояние остаётся изменяемым; это важное ограничение API целостности объектов.

`canDelete` — отдельная возможность, зависящая от данных. Для неё не нужен новый прототип или подкласс. Proxy удалён: явный `rename` лучше показывает проверку и аудит, сохраняет идентичность экземпляра и проще отлаживается. Фабрика с замыканием также могла бы закрыть имя и аудит, но в простом варианте создавала бы методы на каждый экземпляр; общий объект методов потребовал бы отдельного хранилища состояния.

Создание выполняется за `O(1)` для фиксированной схемы permissions, `rename`, `label`, `canDelete` и проверки ключей — за `O(1)`. Перечисление стоит `O(n)` по числу собственных ключей. Методы занимают память один раз в прототипе; закрытое состояние и нормализованный объект permissions принадлежат каждому экземпляру.

Короткое интервью-объяснение:

> Исходник смешивал несколько механизмов без ясного контракта: перечисляемые методы прототипа попадали в `for...in`, `freeze` ломал `rename`, но не защищал общий вложенный объект, Proxy терял получателя и добавлял новую идентичность, а `setPrototypeOf` пытался менять уже нерасширяемый объект. Я оставил общие методы в неперечисляемом прототипе класса, закрыл имя и аудит закрытыми полями, явно описал неизменяемый `id`, нормализовал и отдельно заморозил принадлежащий экземпляру объект `permissions`, а поверхность экземпляра запечатал. Изменение имени теперь проходит только через один проверяемый метод. Право удаления выражено композицией функции и данных. Proxy здесь не даёт пользы, которая оправдала бы скрытый перехват и более сложную отладку.

Частые ошибки: считать `freeze` глубоким, забывать, что закрытые поля не входят в проверки целостности, использовать `for...in` как перечисление собственных данных и добавлять Proxy туда, где один явный метод точнее выражает контракт.
