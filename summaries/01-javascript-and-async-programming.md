# 1. JavaScript & Async Programming — краткая выжимка

> Для быстрого повторения. Если правило непонятно — откройте [полную главу 1.1](../handbook/01-javascript-and-async-programming/01-execution-model-declarations-and-scope.md).

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

> ⏳ Будет заполнено после авторизации и написания раздела 1.2.

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
