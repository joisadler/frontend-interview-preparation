# 1. JavaScript & Async Programming — шпаргалка

> Объяснения: [handbook 1.1](../handbook/01-javascript-and-async-programming/01-execution-model-declarations-and-scope.md) · практика: [exercises](../exercises/prompts/by-domain/01-javascript-and-async-programming.md)

## 1.1. Execution Model, Declarations & Scope

`identifier` (имя) → `binding` (имя + state + value) → `value` (данные).

`declaration` → binding created → `initialization` впервые даёт value → последующий `assignment` меняет value.

- `let` / `const`: enter scope → binding **uninitialized = TDZ** → declaration + initialization → TDZ ends.
- `var`: scope setup → binding = `undefined` → initializer позже делает assignment.
- `function declaration`: binding обычно сразу = function.

| | Scope | До строки | Reassign | Redeclare |
|---|---|---|---:|---:|
| `var` | function | `undefined` | ✓ | обычно ✓ |
| `let` | block | TDZ | ✓ | ✗ |
| `const` | block | TDZ | ✗ | ✗ |

`const` default → `let` при reassignment → `var` только legacy. `const` ≠ immutable object.

**Scope:** global / module / function / block. **Lookup:** current → outer → …; nearest wins; TDZ не пропускает к outer. Lexical scope = место написания, не вызова.

**Execution:** declarations prepared → строки выполняются; hoisting ≠ перенос кода. Function call → new `execution context` + stack frame; block → scope, не frame. `Environment Record` = bindings + outer link.

**Traps:** `typeof undeclared` → `"undefined"`, но TDZ → `ReferenceError`; function declaration до строки ✓, `var fn = …` → `TypeError`, `const fn = …` → `ReferenceError`; shadowing ≠ redeclaration; все `case` делят scope; `for(var)` = один binding, `for(let)` = binding/iteration.

**Top level:** classic browser `var` часто → `globalThis` property, `let`/`const` → global lexical; ESM → module scope + strict; CommonJS → function wrapper. Sloppy unresolved assignment → accidental global; strict → `ReferenceError`; `delete` удаляет property, не binding.

**Output:** runtime? → early conflicts? → scopes → bindings (`function` / `undefined` / TDZ) → lookup → execute → `value` / `undefined` / `ReferenceError` / `TypeError` / `SyntaxError`.

## 1.2. Values, Types, Equality & Coercion
## 1.3. Functions, Closures & Functional Patterns
## 1.4. `this`, Invocation & Object Model
## 1.5. Arrays, Transformations & Copying
## 1.6. Collections, Symbols & Iteration
## 1.7. Modules, Errors & Serialization
## 1.8. Memory Management
## 1.9. Event Loop & Scheduling
## 1.10. Promises & `async`/`await`
## 1.11. Async Coordination Patterns
## 1.12. JavaScript Implementation Practice
