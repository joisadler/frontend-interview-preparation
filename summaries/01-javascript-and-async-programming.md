# 1. JavaScript & Async Programming — краткая выжимка

> Для быстрого повторения. Если правило непонятно — откройте [полную главу 1.1](../handbook/01-javascript-and-async-programming/01-execution-model-declarations-and-scope.md). Для печати: [English A4 infographic](../infographics/01-javascript-and-async-programming/01-execution-model-declarations-and-scope.pdf).

## 1.1. Execution Model, Declarations & Scope

### 🧠 Одна модель

Программа как офис с комнатами:

- **scope** = комната;
- **binding** = запись имени в журнале комнаты;
- **identifier resolution** = поиск от текущей комнаты наружу;
- **shadowing** = ближняя запись с тем же именем скрывает дальнюю;
- **hoisting** = журнал готовят заранее, код физически не двигают;
- **TDZ** = имя уже записано, но доступ ещё закрыт;
- **call stack** = стопка незавершённых вызовов: последний вошёл → первый вышел.

### ⚡ Термины и жизненный цикл

`identifier` (имя в коде) → `binding` (связь имени с состоянием/значением) → `value`.

`declaration` объявляет имя → binding создаётся → `initialization` впервые даёт значение → последующий `assignment` меняет его.

| Объявление | Scope | До своей строки | Reassign | Redeclare в той же scope |
|---|---|---|---:|---:|
| `var` | function / верх script | `undefined` | ✅ | обычно ✅ |
| `let` | block | TDZ → `ReferenceError` | ✅ | ❌ |
| `const` | block | TDZ → `ReferenceError` | ❌ | ❌ |

🎯 В новом коде: `const` по умолчанию → `let`, если нужна смена значения → `var` только для legacy/interview knowledge. `const` фиксирует binding, **не** делает объект immutable.

### Scope и поиск имени

- **global scope** — глобальные имена среды;
- **module scope** — верхний уровень ES module, не global object;
- **function scope** — параметры, локальные имена и `var`;
- **block scope** — `{}`, `if`, `for`, `switch`; для `let` / `const`, но не обычного `var`;
- **lexical scope** — видимость определяется местом написания функции, а не местом её вызова.

Поиск: текущая scope → внешняя → ещё внешняя → не найдено = `ReferenceError`. Если ближайший binding найден, но он в TDZ, поиск **не** перескакивает к внешнему имени.

Свойство объекта — другой механизм: неизвестный identifier → `ReferenceError`; отсутствующее `object.key` → обычно `undefined`.

### Execution model

- До обычного выполнения JavaScript подготавливает объявления и проверяет конфликты.
- **execution context** = активное состояние выполняемого script/module/function.
- Вызов функции добавляет context в **call stack**; обычный блок создаёт scope, но не новый stack frame.
- **Lexical Environment / Environment Record** — точная модель хранения bindings и ссылки наружу. Не нужно утверждать, что это обычные JS-объекты.

### Hoisting, TDZ и функции

- `var` читается раньше своей строки как `undefined`.
- `let` / `const` / `class` существуют раньше строки, но до initialization находятся в **Temporal Dead Zone (TDZ)**.
- `typeof undeclaredName` → `"undefined"`, но `typeof name` в TDZ → `ReferenceError`.
- `function declaration` обычно можно вызвать раньше строки.
- `var fn = function…` раньше строки → `fn === undefined` → вызов даёт `TypeError`.
- `const fn = function…` раньше строки → TDZ → `ReferenceError`.

### Shadowing и конфликты

- **shadowing**: одинаковое имя, разные вложенные scopes — обычно допустимо.
- **redeclaration**: повторное объявление в той же эффективной scope.
- `let` / `const` конфликтуют друг с другом и с `var` той же scope → обычно `SyntaxError` до выполнения.
- Внешний `var` + внутренний block `let` — допустимо.
- Внешний `let` + `var` внутри обычного блока — конфликт: `var` принадлежит окружающей function/global scope. Это часто называют **illegal shadowing**.
- Все `case` одного `switch` делят одну block scope; отдельные `{}` предотвращают конфликты.

### Global, strict mode и legacy

| Где верхний уровень | Что происходит |
|---|---|
| browser classic script | `var` часто становится свойством `globalThis`; `let` / `const` — нет |
| browser / Node ES module | все объявления module-scoped; strict mode автоматически |
| Node CommonJS | файл обёрнут функцией; верхние объявления локальны модулю |

- Необъявленное присваивание в sloppy classic script может создать **accidental global**; strict mode → `ReferenceError`.
- `delete` удаляет **property**, не variable binding.
- 🧓 `with`, direct `eval`, Annex B block functions — узнавать, но не использовать как современный подход.

### Closure-related следствие

Closure сохраняет доступ к **binding**, а не копирует value: `for (var i…)` → одна общая `i`, поздние callbacks обычно видят финальное значение; `for (let i…)` → новый binding на каждую итерацию.

### 🪤 Алгоритм output prediction

1. Уточни среду: classic script / ES module / CommonJS.
2. Проверь ранние конфликты: если `SyntaxError`, выполнение не начнётся.
3. Нарисуй function и block boundaries.
4. Выпиши bindings и начальное состояние: `undefined` / TDZ / функция.
5. Для каждого имени ищи от текущей scope наружу.
6. Только теперь выполняй строки и называй точный результат: value / `undefined` / `ReferenceError` / `TypeError` / `SyntaxError`.

### 🗣️ Ответ за 30–60 секунд

> Scope определяет, где имя относится к конкретному binding. Поиск начинается в текущей lexical scope и идёт наружу. До выполнения строк объявления подготавливаются: `var` получает `undefined`, `let` и `const` остаются в TDZ, а function declaration обычно уже содержит функцию. Поэтому hoisting — не перенос кода, а наблюдаемый результат этой подготовки.

### ✅ Быстрая самопроверка

- Могу без подсказки сравнить `var` / `let` / `const`.
- Отличаю scope, execution context и call stack.
- Объясняю hoisting без фразы «код переносится вверх».
- Предсказываю TDZ, shadowing, redeclaration и function-expression ошибки.
- Уточняю runtime перед вопросом про `globalThis`.
- Объясняю разницу `for (var…)` и `for (let…)` через bindings.

### Практика

[20 вопросов](../question-bank/by-domain/01-javascript-and-async-programming.md) · [9 упражнений без решений](../exercises/prompts/by-domain/01-javascript-and-async-programming.md) · [полная глава](../handbook/01-javascript-and-async-programming/01-execution-model-declarations-and-scope.md)

## 1.2. Values, Types, Equality & Coercion

> Быстрое повторение: [полная глава](../handbook/01-javascript-and-async-programming/02-values-types-equality-and-coercion.md) · [English A4 infographic](../infographics/01-javascript-and-async-programming/02-values-types-equality-and-coercion.pdf)

### Values, identity, mutation

`binding → value`; object value даёт доступ к **identity**.

| Primitives (immutable) | Objects (mutable по умолчанию) |
|---|---|
| `undefined`, `null`, boolean, number, bigint, string, symbol | objects, arrays, functions, dates… |
| операция создаёт новое value | свойства существующей identity можно менять |
| сравнение обычно по value | equality — по identity |

`const` запрещает **reassignment binding**, но не object mutation. Spread / `Object.assign` = **shallow copy**: новый outer object, nested references остаются shared.

Arguments всегда передаются **by value**. Для object копируется reference value → mutation общей identity видна caller; reassignment parameter — нет.

### Type checks и special numbers

```text
typeof null        → "object"      typeof []          → "object"
typeof function(){}→ "function"    typeof NaN         → "number"
typeof 1n          → "bigint"      typeof Symbol()    → "symbol"
```

- `typeof undeclaredName` → `"undefined"`; но identifier в TDZ → `ReferenceError`.
- `undefined` = отсутствие значения по умолчанию; `null` = намеренно пусто по contract.
- `Symbol()` → уникальный primitive/key; `Symbol("x") !== Symbol("x")`.
- BigInt: integers arbitrary precision; `1n + 2n` ✅, `1n + 2` → `TypeError`; division truncates.
- `NaN !== NaN`; проверка → `Number.isNaN(value)`. Global `isNaN` сначала coercing input.
- `Number.isFinite` / `Number.isSafeInteger` проверяют разные domain constraints.
- `Object.is(-0, 0) === false`; `1 / -0 === -Infinity`.

Floating point: `0.1 + 0.2 !== 0.3`. Measurements → absolute + relative domain tolerance. Fixed-scale money → integer minor units + safe-range check + явная rounding policy.

### Falsy, nullish, defaults

Falsy: `false`, `0`, `-0`, `0n`, `NaN`, `""`, `null`, `undefined`.

Nullish: только `null`, `undefined`.

| Expression | Fallback when |
|---|---|
| `value || fallback` | value falsy |
| `value ?? fallback` | value nullish |

Short-circuit operators возвращают **operand**, не обязательно boolean. Для valid `0`, `""`, `false` defaults обычно требуют `??`.

Optional chaining:

- `user?.profile?.name` → `undefined`, если base nullish;
- undeclared root всё равно → `ReferenceError`;
- `obj.method?.()` бросит `TypeError`, если method существует, но не callable;
- `(obj?.a).b` разрывает continuous chain;
- не подавляет exceptions из существующих getters/methods.

### Equality semantics

| Семантика | `NaN` = `NaN` | `0` = `-0` | Где |
|---|---:|---:|---|
| `===` | ❌ | ✅ | default production comparison, `indexOf()` |
| `Object.is` / SameValue | ✅ | ❌ | точные numeric edge cases |
| SameValueZero | ✅ | ✅ | `includes()`, `Set`, `Map` keys |
| `==` | coercion | ✅ | legacy/interview; deliberate `value == null` = null или undefined |

Objects: `{a: 1} === {a: 1}` → `false`; один alias той же identity → `true`.

### Coercion pipeline

Prefer explicit boundary normalization:

```text
raw input → validate grammar/type → explicit Boolean/Number/String
          → validate finite/range/safe integer → stable domain type
```

- `Boolean(value)` использует falsy list.
- `Number("") → 0`, `Number(null) → 0`, `Number(undefined) → NaN`.
- `String(null) → "null"`; `String(Symbol())` работает, но implicit symbol concatenation бросает.
- Binary `+`: `ToPrimitive` обоих → если есть string, concatenation; иначе numeric addition.
- Другие arithmetic operators обычно идут в numeric coercion: `"5" - 2 → 3`.
- Relational comparison: string/string лексикографически; иначе свой algorithm — не «всегда Number обеих сторон».

`ToPrimitive(object, hint)`:

1. `[Symbol.toPrimitive](hint)`, если есть;
2. string hint: `toString()` → `valueOf()`;
3. number/default для обычного object: `valueOf()` → `toString()`;
4. нужен primitive result, иначе `TypeError`.

### 🪤 Output-prediction порядок

1. Определи value categories и operator.
2. Вычисли unary operations/short-circuit.
3. Для object проследи `ToPrimitive`.
4. Примени operator-specific conversion.
5. Назови value **и type**; отдельно отметь exception.

`[] == ![]` → `![]` is `false` → `[] == false` → `"" == 0` → `0 == 0` → `true`. Это проверка coercion model, не production style.

### ✅ Быстрая самопроверка

- Explain: primitives/objects, identity, pass-by-value, equality choices.
- Predict: `typeof`, falsy/nullish, `+`, `==`, `NaN`, `-0`, BigInt errors.
- Implement: normalization boundary, numeric validation, safe defaults.
- Debug: shared mutation, shallow-copy leaks, floating-point/money bugs.
- Review: explicit types/ownership, `===` by default, deliberate coercion only.

### Практика

[24 вопроса](../question-bank/by-domain/01-javascript-and-async-programming.md#12-значения-типы-равенство-и-преобразование-типов) · [10 упражнений без решений](../exercises/prompts/by-domain/01-javascript-and-async-programming.md#12-значения-типы-равенство-и-преобразование-типов)

## 1.3. Functions, Closures & Functional Patterns

> ⏳ Будет заполнено после авторизации и написания раздела 1.3.

## 1.4. `this`, Invocation & Object Model

> ⏳ Будет заполнено после авторизации и написания раздела 1.4.

## 1.5. Arrays, Transformations & Copying

> ⏳ Будет заполнено после авторизации и написания раздела 1.5.

## 1.6. Collections, Symbols & Iteration

> ⏳ Будет заполнено после авторизации и написания раздела 1.6.

## 1.7. Modules, Errors & Serialization

> ⏳ Будет заполнено после авторизации и написания раздела 1.7.

## 1.8. Memory Management

> ⏳ Будет заполнено после авторизации и написания раздела 1.8.

## 1.9. Event Loop & Scheduling

> ⏳ Будет заполнено после авторизации и написания раздела 1.9.

## 1.10. Promises & `async`/`await`

> ⏳ Будет заполнено после авторизации и написания раздела 1.10.

## 1.11. Async Coordination Patterns

> ⏳ Будет заполнено после авторизации и написания раздела 1.11.

## 1.12. JavaScript Implementation Practice

> ⏳ Будет заполнено после авторизации и написания раздела 1.12.
