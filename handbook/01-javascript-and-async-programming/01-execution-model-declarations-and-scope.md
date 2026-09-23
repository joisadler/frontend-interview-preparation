# 1.1. Execution Model, Declarations & Scope

> Status: `draft — calibration review pending`
>
> Related inventory IDs: `JS-01`, `JS-02`, `JS-03`, `JS-04`, `JS-22`
>
> Last verified: `2026-09-23`
>
> Runtime verification: portable examples checked with Node.js `v26.4.0`; browser-only examples are explicitly labeled.

This chapter restores the model needed to reason about **where a name is visible, when its binding becomes usable, and which execution state is active**. It is intentionally narrower than the future chapters on functions/closures, modules, values and the event loop.

## Mental Model

Do not imagine that JavaScript “moves declarations to the top.” Use this model instead:

1. Before a scope is evaluated, the engine processes its declarations and creates the required **bindings**.
2. Different declarations initialize those bindings at different times.
3. While evaluating code, an identifier is resolved from the current environment outward.
4. Function calls add execution contexts to the call stack; entering an ordinary block changes the current lexical environment but does **not** add a function-call frame.

A useful interview shorthand is:

```text
source code
   ↓ parse + declaration instantiation
bindings for the scope exist with declaration-specific state
   ↓ evaluation
reads and writes resolve through the Environment Record chain
```

This is a deliberately simplified “creation → evaluation” model. The specification uses separate algorithms such as `GlobalDeclarationInstantiation`, `FunctionDeclarationInstantiation` and `BlockDeclarationInstantiation`, plus module linking/initialization.

For a nested read of `value`:

```text
current Environment Record
   └─ has "value"? use that binding
      otherwise ↓ [[OuterEnv]]
enclosing Environment Record
   └─ has "value"? use that binding
      otherwise ↓ [[OuterEnv]]
...
global Environment Record
   └─ no binding? ReferenceError on a normal read
```

Three distinctions prevent most mistakes:

- **Execution context** is the state required to execute code.
- **LexicalEnvironment** is the execution-context reference used for identifier resolution; in ES2026 it points to an Environment Record.
- **Scope** is the source-code region in which an identifier resolves to a binding, even if that binding is temporarily uninitialized.

They are related, but they are not synonyms.

## Core Concepts

| Term | Practical meaning |
|---|---|
| Binding | Association between an identifier and its current value/state. |
| Declaration | Syntax that introduces or declares a name, such as `let total`; declaration instantiation may create a fresh binding or reuse a compatible existing one. |
| Initialization | The first value supplied to a newly created binding; it ends the TDZ for a lexical binding. |
| Assignment | A later write to an already initialized mutable binding. |
| Execution context | Specification state for currently executing script, module, function or `eval` code. |
| Call stack | LIFO stack of active execution contexts in the common implementation/interview model. |
| `LexicalEnvironment` | Execution-context field pointing to the current Environment Record for name resolution. Blocks temporarily change this reference. |
| `VariableEnvironment` | Execution-context field identifying the Environment Record used for `var`-scoped declarations in this code. |
| Environment Record | Specification mechanism that stores/resolves bindings and refers to an outer record through `[[OuterEnv]]`. It need not be a literal runtime object or hash map. |
| Scope chain | Informal name for following `[[OuterEnv]]` during identifier resolution. |
| Lexical scope | Name resolution is determined by where code is written, not by which function calls it. |
| TDZ | Period in which a lexical binding exists but is still uninitialized. Reading it throws `ReferenceError`. |
| Hoisting | Informal description of observable pre-evaluation binding setup—not physical source-code movement. |
| Shadowing | An inner binding uses the same name as an outer binding and wins for reads in the inner region. |
| Early error | Static-semantic error detected for one parsed unit before its evaluation. A later classic script can instead fail with `SyntaxError` during global declaration instantiation; that is not formally an Early Error. |

### Scope boundaries at a glance

| Boundary | Typical bindings | Key consequence |
|---|---|---|
| Global script | top-level `var`, function, `let`, `const`, `class` | Classic browser scripts use a composite global environment. |
| Function | parameters, `var`, function-local lexical declarations | Each call gets a new function execution context and function environment. |
| Block | `let`, `const`, `class`, block function in standard strict/module code | A block can add an environment without adding a call-stack frame. |
| Module | top-level module declarations and imports | Module bindings are module-scoped, not properties of `globalThis`; modules are strict. |

“Lexical scope” is the rule by which these scopes relate. It is not simply a fifth boundary beside global, function, block and module scope.

## Detailed Explanation

### 1. ECMAScript and the host environment

ECMAScript specifies the language: syntax, types, declarations, functions, objects, execution contexts, Environment Records and evaluation semantics. A **host** embeds that language and supplies capabilities around it.

| ECMAScript responsibility | Host responsibility |
|---|---|
| `let`, `const`, `var`, functions, promises, standard built-ins | DOM, `window`, timers and browser event-loop integration |
| Binding creation and identifier resolution | Files, `process`, network and Node.js module loading |
| Execution-context and job semantics | How scripts are obtained, when callbacks are scheduled, host-specific globals |

The split matters in interviews:

- `setTimeout` is not defined by ECMAScript; browsers and Node.js provide timer APIs.
- `window` is a browser global and is absent in workers and Node.js.
- `globalThis` is the portable way to refer to the current global object, but top-level declarations do not all become its properties.
- Browser classic scripts, browser modules, Node.js ES modules and Node.js CommonJS files have different top-level environments.

This chapter uses the call stack only to explain synchronous execution. Tasks, microtasks and rendering belong to [1.9. Event Loop & Scheduling](09-event-loop-and-scheduling.md).

### 2. Execution contexts and the call stack

An execution context contains the state needed to execute code. In interview-level reasoning, the most relevant contexts are:

- a global/script or module context for the entry code;
- a new function execution context for every function call;
- an `eval` context, mostly legacy/special-case knowledge.

```js
const rate = 2;

function calculate(base) {
  const result = base * rate;
  return result;
}

calculate(5);
```

A useful trace:

```text
1. entry context is running
2. calculate(5) pushes a function execution context
3. calculate resolves base locally, then rate through [[OuterEnv]]
4. return removes calculate's context
5. control resumes in the entry context
```

Calling a function changes the call stack. Entering `{ ... }` normally does not:

```js
function render() {
  const mode = "full";

  if (mode === "full") {
    const label = "Details"; // new block Environment Record
    console.log(label);
  }
}
```

`render()` creates a function execution context. The `if` block creates a lexical scope for `label`, but not another function call frame.

### 3. Environments, Environment Records and identifier resolution

In the current specification model:

```text
Execution Context
├─ LexicalEnvironment  → current Environment Record for lookup
│                        ├─ local bindings
│                        └─ [[OuterEnv]] → enclosing Environment Record or null
└─ VariableEnvironment → Environment Record targeted by `var` declarations
```

Real engines may optimize this aggressively. Do not claim that every scope is materialized as a JavaScript object.

On function/script/module entry these context fields may initially identify the same record. Entering a block temporarily changes `LexicalEnvironment`; ordinary block syntax does not make `var` block-scoped.

Identifier resolution starts at the current Environment Record and walks outward until it finds a matching binding:

```js
const source = "global";

function outer() {
  const source = "outer";

  function inner() {
    console.log(source);
  }

  return inner;
}

const readSource = outer();
readSource(); // "outer"
```

`inner` resolves `source` from where `inner` was **defined**, not from where `readSource` is later called. The function retains access to the relevant outer environment. That is the closure consequence needed here; factories, memoization and retained-memory analysis belong to [1.3. Functions, Closures & Functional Patterns](03-functions-closures-and-functional-patterns.md).

If no binding is found, a normal read throws:

```js
console.log(missingName); // ReferenceError
```

An object property lookup such as `config.missingName` is a different operation and normally produces `undefined`; it is not lexical identifier resolution.

### 4. Global, function, block and module scope

#### Function and block scope

In the ordinary code covered here, `var` is scoped to the nearest function or top-level script/module environment. A plain block does not contain it:

```js
function example() {
  if (true) {
    var legacy = "function scoped";
    let modern = "block scoped";
  }

  console.log(legacy); // "function scoped"
  console.log(modern); // ReferenceError
}
```

`let`, `const` and `class` are lexical declarations. Their binding belongs to the surrounding block, function body, module or global lexical environment.

Class static initialization blocks are a class-specific exception that form their own `var` scope; that edge belongs with class semantics in section 1.4 rather than the core model here.

Blocks include more than standalone braces:

- `if`, `for`, `while` and `try` blocks;
- a `catch` parameter and its block;
- the single block that contains all `switch` cases.

The `switch` detail causes a realistic bug:

```js
switch (status) {
  case "idle":
    let message = "Waiting";
    break;
  case "done":
    let message = "Complete"; // SyntaxError: same switch block
    break;
}
```

Use braces when cases need same-named lexical bindings:

```js
switch (status) {
  case "idle": {
    const message = "Waiting";
    break;
  }
  case "done": {
    const message = "Complete";
    break;
  }
}
```

#### Module scope

An ES module has its own top-level scope:

```js
// settings.mjs or <script type="module">
const token = "local to this module";

console.log(globalThis.token); // undefined, unless the host already has such a property
```

Modules are strict mode automatically. The import/export graph, live bindings and cycles belong to [1.7. Modules, Errors & Serialization](07-modules-errors-and-serialization.md).

### 5. Declaration, binding creation, initialization and assignment

Consider:

```js
let count = 1;
count = 2;
```

There are distinct events:

1. `let count` declares a binding.
2. Scope instantiation creates that binding in an uninitialized state.
3. Evaluation of `let count = 1` initializes it with `1`.
4. `count = 2` assigns a later value.

This distinction explains the declaration families:

| Form | Scope | State before declaration line is evaluated | Reassignment | Same-scope redeclaration |
|---|---|---|---|---|
| `var x` | function or top-level script/module | a newly created binding is initialized to `undefined`; a compatible existing binding is reused | yes | another `var` generally allowed |
| `let x` | lexical/block | binding exists but is uninitialized (TDZ) | yes | no |
| `const x = value` | lexical/block | binding exists but is uninitialized (TDZ) | no | no |
| function declaration | enclosing scope; block rules depend on context | normally initialized with the function during declaration instantiation | binding rules depend on context | conflicts follow declaration rules |
| `var fn = function () {}` | scope of `var` | `fn` is `undefined`; function object not created yet | yes | `var` rules |
| `const fn = function () {}` | lexical scope | `fn` is in TDZ; function object not created yet | no | lexical rules |

The table assumes a fresh name unless noted. A duplicate `var`, a same-name parameter/function binding or a compatible pre-existing global property is not reset to `undefined`; `var existing;` has no runtime initializer write.

`const` protects the binding, not the object:

```js
const settings = { theme: "light" };
settings.theme = "dark"; // allowed
// settings = {};        // TypeError at assignment
```

Object identity and mutation are developed in [1.2. Values, Types, Equality & Coercion](02-values-types-equality-and-coercion.md).

### 6. Hoisting without the “moved code” myth

“Hoisting” is useful shorthand for behavior caused by declaration instantiation before ordinary statement evaluation. It is not an ECMAScript operation that rewrites this:

```js
console.log(total);
var total = 3;
```

into another source file.

The observed result is `undefined` because the `var` binding already exists and is initialized before the `console.log`; only the initializer assignment happens at its textual position.

By contrast:

```js
console.log(total);
let total = 3;
```

throws `ReferenceError` because the inner lexical binding exists but is uninitialized when read.

The declaration also shadows any outer name for the entire scope:

```js
const state = "outer";

{
  console.log(state); // ReferenceError, not "outer"
  const state = "inner";
}
```

Once the block is entered, lookup finds the inner `state`. The engine does not skip that binding merely because initialization appears later.

### 7. Temporal Dead Zone

The TDZ extends from entry into a lexical scope until evaluation initializes the binding. It is temporal in execution, even though its boundaries come from lexical structure.

```js
{
  // TDZ for user begins at block entry
  const user = { id: 1 }; // initialization ends TDZ
  console.log(user.id);
}
```

Important cases:

```js
console.log(typeof neverDeclared); // "undefined"
```

```js
console.log(typeof later); // ReferenceError
let later = 1;
```

`typeof` has a special result for an unresolvable identifier, but it does not bypass the TDZ of an existing lexical binding.

Self-reference is another TDZ read:

```js
let value = value; // ReferenceError
```

The right-hand `value` resolves to the new inner binding, not an outer one.

### 8. Function declarations and expressions in the hoisting discussion

This chapter covers only their binding timing. Function forms and APIs belong to section 1.3.

```js
declaration(); // works

function declaration() {
  return "ready";
}
```

The function declaration binding is initialized with the function before statement evaluation.

```js
expression(); // TypeError: expression is undefined

var expression = function () {
  return "ready";
};
```

The `var` binding exists as `undefined`, so the failure is “not a function,” not an unresolved name.

```js
expression(); // ReferenceError

const expression = function () {
  return "ready";
};
```

Here `expression` is in its TDZ. In a named function expression, the expression's own name is a separate inner binding, available inside that function rather than in the outer scope.

Block-level function declarations have standardized block scope in strict code and modules, but legacy sloppy browser-script behavior has Annex B compatibility rules. Modern production code should not depend on those cross-environment quirks.

### 9. Redeclaration, shadowing and illegal shadowing

**Redeclaration** concerns conflicting declarations in the same effective scope. **Shadowing** concerns different nested scopes. “Illegal shadowing” is common interview wording; more precisely it is a declaration conflict.

Legal shadowing:

```js
const label = "outer";

{
  const label = "inner";
  console.log(label); // "inner"
}

console.log(label); // "outer"
```

Also legal:

```js
var mode = "legacy outer";

{
  let mode = "modern inner";
  console.log(mode);
}
```

Illegal collision:

```js
let mode = "outer lexical";

{
  var mode = "same function/global var scope";
}
```

This is a `SyntaxError`. The `var` declaration is not block-scoped; it would need to create a binding in the surrounding function/global var scope, where it conflicts with the lexical declaration.

A practical matrix for one scope:

| Existing declaration | New `var` | New `let` | New `const` | New function declaration |
|---|---:|---:|---:|---:|
| `var` | generally allowed | error | error | context-dependent overlap; avoid relying on it |
| `let` | error | error | error | error |
| `const` | error | error | error | error |

Nested scopes can shadow unless a function-scoped `var` crosses a lexical declaration as in the illegal example. Detailed edge cases involving parameters, direct `eval`, web-legacy block functions and global property descriptors are low-value compared with being able to reason from the binding model.

Because many declaration conflicts are **early errors**, earlier statements do not run:

```js
console.log("will not print");
let id;
let id; // SyntaxError before evaluation
```

### 10. Browser global declarations

For a **classic browser script**:

```html
<script>
  var legacyGlobal = 1;
  let lexicalGlobal = 2;

  console.log(globalThis.legacyGlobal); // 1
  console.log(globalThis.lexicalGlobal); // undefined
</script>
```

The browser global environment is composite:

- an **Object Environment Record** handles suitable `var` and function declarations through the global object;
- a **Declarative Environment Record** holds global lexical declarations such as `let`, `const` and `class`.

Therefore, “global scope” does not mean “every global binding is a `window` property.” A top-level `let` in a classic script is still a global binding; it simply is not a global-object property.

For a **browser ES module**, top-level declarations—including `var`—are module-scoped and do not become global-object properties. Node.js differs again:

- Node.js ES modules have module scope.
- Node.js CommonJS wraps each file in a function, so a top-level `var` is module-local rather than a property of `globalThis`.
- REPLs and browser DevTools consoles may have host-specific persistence and should not be treated as a precise model for file execution.

Classic scripts are instantiated independently in load order. A lexical declaration in a later script is not visible—and is not in TDZ—while an earlier script runs; its binding is created when the later script performs `GlobalDeclarationInstantiation`. Once created, a global lexical binding can remain available to later classic scripts in the same realm.

Every output-prediction question about globals should name its environment.

### 11. Strict mode, accidental globals and `delete`

Classic scripts are not strict unless they opt in. Modules are always strict.

In sloppy code, assigning to an unresolved identifier can create a property on the global object:

```js
function save() {
  accidentalTotal = 3;
}

save();
console.log(globalThis.accidentalTotal); // 3 in a sloppy classic script
```

In strict code:

```js
"use strict";

function save() {
  accidentalTotal = 3; // ReferenceError
}
```

Modern production guidance:

- use ES modules where appropriate;
- keep strict checking enabled through the runtime/module system and linting;
- never rely on implicit global creation;
- declare ownership explicitly.

`delete` removes object properties; it does not erase lexical bindings:

```js
const config = { debug: true };
delete config.debug; // true; property removed
```

Assuming fresh names and an ordinary extensible browser global object, the key distinctions in a **sloppy** classic script are:

```js
var declared = 1;          // corresponding global property is normally non-configurable
accidental = 2;            // sloppy assignment normally creates a configurable property

delete globalThis.declared;   // false
delete globalThis.accidental; // true
```

In strict code, the explicit expression `delete globalThis.declared` attempts to remove the same non-configurable property but throws `TypeError` instead of returning `false`. Deleting a configurable property explicitly can still succeed in strict code.

Do not generalize any of those results to modules, CommonJS wrappers or console experiments.

In strict code, `delete identifier` is an early syntax error:

```js
"use strict";
delete declaredName; // SyntaxError
```

Use `delete object.property` when property removal is intended. There is no operator for deleting a `let`, `const` or local-variable binding.

### 12. The loop-binding consequence

The classic closure/output trap follows directly from scope:

```js
const readers = [];

for (var i = 0; i < 3; i += 1) {
  readers.push(() => i);
}

console.log(readers.map((read) => read())); // [3, 3, 3]
```

All callbacks close over one surrounding `var`-scoped `i` binding: function-scoped inside a function, script-global in a classic script, or module-local at module top level.

With `let`, a `for` loop creates a fresh per-iteration binding:

```js
const readers = [];

for (let i = 0; i < 3; i += 1) {
  readers.push(() => i);
}

console.log(readers.map((read) => read())); // [0, 1, 2]
```

That is enough closure knowledge for this chapter. The fuller model and memory implications remain in section 1.3.

### 13. Production guidance versus interview/legacy knowledge

#### Modern production baseline

- Prefer `const` when the binding will not be reassigned.
- Use `let` for intentional reassignment.
- Avoid `var` in new application code; know it well enough to debug existing code and answer interviews.
- Prefer modules and explicit imports/exports over shared global names.
- Configure lint rules such as `no-undef` and `no-var`.
- Use small scopes and avoid shadowing when it makes review harder, even when technically legal.

#### Legacy/interoperability knowledge

- Function-scoped `var`, global-object properties and sloppy accidental globals still appear in old scripts, third-party integrations and interviews.
- Block function declarations in sloppy web scripts have legacy compatibility behavior; do not build new code around it.
- Direct `eval` and `with` complicate static scope reasoning. `with` is forbidden in strict mode; neither deserves core implementation depth here.

#### Precise terminology without specification trivia

It is valuable to say “binding,” “Environment Record,” “declaration instantiation,” “uninitialized” and “early error.” It is usually not valuable in an interview to recite abstract-operation names or engine-internal storage layouts unless the interviewer asks.

## Examples

### Example 1 — Resolve from source position, not caller

```js
const role = "guest";

function createReader() {
  const role = "admin";
  return () => role;
}

function invoke(reader) {
  const role = "operator";
  return reader();
}

console.log(invoke(createReader())); // "admin"
```

The caller's `role` is irrelevant to lexical resolution inside the returned function.

### Example 2 — Three pre-declaration outcomes

```js
console.log(a); // undefined
var a = 1;
```

```js
console.log(b); // ReferenceError: TDZ
let b = 1;
```

```js
callMe(); // TypeError: callMe is undefined
var callMe = () => {};
```

The first reads an initialized `var` binding, the second reads an uninitialized lexical binding, and the third successfully resolves a binding whose current value is not callable.

### Example 3 — A Static Early Error beats runtime order

```js
console.log("start");

const key = "a";
var key = "b";
```

Nothing logs: the conflicting declarations produce a `SyntaxError` before normal evaluation.

### Example 4 — Block environment without a call

```js
const value = "outer";

{
  const value = "inner";
  console.log(value); // "inner"
}

console.log(value); // "outer"
```

The block adds an Environment Record. It does not push a function execution context.

### Example 5 — Explicit environment matters

```js
// Browser classic script
var classicName = "classic";
console.log(globalThis.classicName); // "classic"
```

```js
// Browser module or Node.js ES module
var moduleName = "module-local";
console.log(globalThis.moduleName); // normally undefined
```

The same declaration syntax does not imply the same relationship with the host global object.

## Common Mistakes

1. **Saying declarations are moved.** This predicts some outputs but fails for TDZ, functions and declaration conflicts.
2. **Treating scope and execution context as synonyms.** A block can create scope without a function call.
3. **Saying `let` and `const` are not hoisted.** Their bindings exist before the declaration line but remain uninitialized.
4. **Calling TDZ “the lines above `let`.”** It lasts from scope entry until initialization and depends on the executed path.
5. **Assuming `const` freezes an object.** It prevents rebinding only.
6. **Assuming every global is `window.someName`.** Global lexical bindings and module bindings are not global-object properties.
7. **Running ambiguous snippets in DevTools and generalizing the result.** Consoles may not behave like classic script or module files.
8. **Calling every same-name declaration shadowing.** Same-scope conflicts are redeclarations; nested same-name bindings are shadowing.
9. **Expecting `delete` to remove variables.** It targets properties.
10. **Using closure vocabulary without binding vocabulary.** Closures retain access to bindings, not frozen copies of all values.

## Interview Traps

### `typeof` is not a universal safety check

```js
typeof absent; // "undefined"
typeof presentLater; // ReferenceError
let presentLater;
```

Ask: is the name unresolvable, or is there an uninitialized lexical binding?

### An inner declaration hides the outer binding before its line

```js
let count = 10;

{
  console.log(count); // ReferenceError
  let count = 20;
}
```

Lookup finds the inner binding, then the TDZ check fails.

### `switch` cases share one lexical scope

Wrap cases in blocks if they declare the same lexical name.

### Illegal shadowing is usually an early error

Do not predict earlier logs. The program does not begin normal evaluation.

### Function expression errors depend on the containing declaration

- `var fn = ...` before assignment: `fn` is `undefined`, so calling it throws `TypeError`.
- `let`/`const fn = ...` before initialization: reading `fn` throws `ReferenceError`.
- function declaration: normally callable before its textual position.

### Global answers require an environment label

Ask whether the snippet is a browser classic script, browser module, Node.js ES module or Node.js CommonJS file.

### Strict-mode `delete identifier` is not a normal `false`

It is invalid syntax. `delete object.property` remains valid.

## Common Interview Questions

The full prompts and metadata are in the separate [JavaScript Question Bank](../../question-bank/by-domain/01-javascript-and-async-programming.md). Answers remain in the separate answer tree.

### Junior

- [`JS-SCOPE-Q01`](../../question-bank/by-domain/01-javascript-and-async-programming.md#js-scope-q01) — compare `var`, `let` and `const`.
- [`JS-SCOPE-Q02`](../../question-bank/by-domain/01-javascript-and-async-programming.md#js-scope-q02) — explain the scope boundaries.
- [`JS-SCOPE-Q03`](../../question-bank/by-domain/01-javascript-and-async-programming.md#js-scope-q03) — separate declaration, initialization and assignment.
- [`JS-SCOPE-Q04`](../../question-bank/by-domain/01-javascript-and-async-programming.md#js-scope-q04) — predict `var`/`let`/TDZ output.
- [`JS-SCOPE-Q05`](../../question-bank/by-domain/01-javascript-and-async-programming.md#js-scope-q05) — compare function declaration and expression timing.
- [`JS-SCOPE-Q06`](../../question-bank/by-domain/01-javascript-and-async-programming.md#js-scope-q06) — explain shadowing versus redeclaration.
- [`JS-SCOPE-Q07`](../../question-bank/by-domain/01-javascript-and-async-programming.md#js-scope-q07) — debug an accidental global.

### Mid

- [`JS-SCOPE-Q08`](../../question-bank/by-domain/01-javascript-and-async-programming.md#js-scope-q08) — relate execution contexts, environments and the call stack.
- [`JS-SCOPE-Q09`](../../question-bank/by-domain/01-javascript-and-async-programming.md#js-scope-q09) — trace lexical identifier resolution.
- [`JS-SCOPE-Q10`](../../question-bank/by-domain/01-javascript-and-async-programming.md#js-scope-q10) — explain why a block is not another call frame.
- [`JS-SCOPE-Q11`](../../question-bank/by-domain/01-javascript-and-async-programming.md#js-scope-q11) — find illegal redeclarations and state the failure phase.
- [`JS-SCOPE-Q12`](../../question-bank/by-domain/01-javascript-and-async-programming.md#js-scope-q12) — compare classic-script and module globals.
- [`JS-SCOPE-Q13`](../../question-bank/by-domain/01-javascript-and-async-programming.md#js-scope-q13) — predict loop callback values.
- [`JS-SCOPE-Q14`](../../question-bank/by-domain/01-javascript-and-async-programming.md#js-scope-q14) — debug `switch` case declarations.
- [`JS-SCOPE-Q15`](../../question-bank/by-domain/01-javascript-and-async-programming.md#js-scope-q15) — review legacy scope-sensitive code.

### Senior

- [`JS-SCOPE-Q16`](../../question-bank/by-domain/01-javascript-and-async-programming.md#js-scope-q16) — give a precise model of hoisting without over-teaching the spec.
- [`JS-SCOPE-Q17`](../../question-bank/by-domain/01-javascript-and-async-programming.md#js-scope-q17) — explain the browser Global Environment Record practically.
- [`JS-SCOPE-Q18`](../../question-bank/by-domain/01-javascript-and-async-programming.md#js-scope-q18) — diagnose a production-only global collision.
- [`JS-SCOPE-Q19`](../../question-bank/by-domain/01-javascript-and-async-programming.md#js-scope-q19) — review cross-runtime top-level assumptions.
- [`JS-SCOPE-Q20`](../../question-bank/by-domain/01-javascript-and-async-programming.md#js-scope-q20) — implement a deliberate legacy-global bridge with safe cleanup.

## How to Explain It in an Interview

### `var`, `let` and `const` — 30–45 seconds

> `var` is function- or top-level-script/module-scoped rather than block-scoped. A newly created `var` binding is initialized to `undefined` before statement evaluation, and a compatible same-scope `var` redeclaration generally reuses rather than resets the binding. `let` and `const` are block-scoped lexical declarations: their bindings exist from scope entry but stay uninitialized in the TDZ until their declaration runs. `let` can be reassigned; `const` cannot be rebound, although an object stored in it may still mutate. In modern code I default to `const`, use `let` for intentional reassignment, and keep `var` as legacy/debugging knowledge.

### Hoisting and TDZ — 45–60 seconds

> Hoisting is an informal name for observable behavior caused by declaration instantiation; the engine does not physically move source lines. For a fresh name, a `var` binding is initialized to `undefined` before execution reaches its initializer; a compatible redeclaration does not reset an existing binding. A `let`, `const` or `class` binding is also created before the declaration line, but it is uninitialized, so a read in the TDZ throws `ReferenceError`. Function declarations are initialized with their function objects early, while function expressions follow the lifecycle of the variable that contains them.

### Execution context and scope chain — 45–60 seconds

> A function call creates an execution context and pushes it onto the call stack. Name resolution is modeled separately with Environment Records: each record contains bindings and an `[[OuterEnv]]` reference. An identifier lookup starts locally and walks outward. Because that chain is determined by source nesting, a function resolves outer names from where it was defined, not from where it was called. Entering a block can add an Environment Record without adding another function-call frame.

### Browser globals and modules — 45–60 seconds

> In a classic browser script, the global environment has an object-backed part for many top-level `var` and function declarations and a declarative part for `let`, `const` and `class`. Therefore a top-level `var` may appear on `globalThis`, while a top-level `let` does not. ES modules have their own module scope, are strict automatically and do not expose top-level declarations as global-object properties. Node CommonJS differs again because files are wrapped in a function, so I always name the execution environment before predicting global behavior.

## Exercises

Open only the prompt file while practising; solutions are stored separately.

1. [`JS-SCOPE-EX01`](../../exercises/prompts/by-domain/01-javascript-and-async-programming.md#js-scope-ex01) — rebuild the declaration matrix from memory.
2. [`JS-SCOPE-EX02`](../../exercises/prompts/by-domain/01-javascript-and-async-programming.md#js-scope-ex02) — predict binding lifecycle outputs and error classes.
3. [`JS-SCOPE-EX03`](../../exercises/prompts/by-domain/01-javascript-and-async-programming.md#js-scope-ex03) — trace identifier resolution through nested environments.
4. [`JS-SCOPE-EX04`](../../exercises/prompts/by-domain/01-javascript-and-async-programming.md#js-scope-ex04) — record two 30–60 second explanations.
5. [`JS-SCOPE-EX05`](../../exercises/prompts/by-domain/01-javascript-and-async-programming.md#js-scope-ex05) — debug strict/sloppy accidental-global behavior.
6. [`JS-SCOPE-EX06`](../../exercises/prompts/by-domain/01-javascript-and-async-programming.md#js-scope-ex06) — repair redeclaration and `switch` scope defects.
7. [`JS-SCOPE-EX07`](../../exercises/prompts/by-domain/01-javascript-and-async-programming.md#js-scope-ex07) — perform a scope-focused code review.
8. [`JS-SCOPE-EX08`](../../exercises/prompts/by-domain/01-javascript-and-async-programming.md#js-scope-ex08) — implement stable per-index callbacks.
9. [`JS-SCOPE-EX09`](../../exercises/prompts/by-domain/01-javascript-and-async-programming.md#js-scope-ex09) — integrated interview challenge.

## Interview Challenge

Complete [`JS-SCOPE-EX09`](../../exercises/prompts/by-domain/01-javascript-and-async-programming.md#js-scope-ex09) without running the code first.

You will need to:

1. label the execution environment for every snippet;
2. distinguish static Early Errors, declaration-instantiation failures and evaluation-time exceptions;
3. trace scope lookup and callback bindings;
4. repair the code using modern production guidance;
5. explain the result aloud in under three minutes.

Score conceptual understanding, terminology recall, output accuracy, repair quality and communication separately.

## Checklist

### Explain

- [ ] I can distinguish execution context, call stack, Environment Record and scope.
- [ ] I can explain hoisting without saying code is physically moved.
- [ ] I can give a 30–60 second comparison of `var`, `let` and `const`.
- [ ] I can explain classic browser globals versus module scope.

### Recognize / predict

- [ ] I can identify global, function, block and module boundaries.
- [ ] I can trace identifier resolution and spot shadowing.
- [ ] I can predict `undefined`, `ReferenceError`, `TypeError` and early `SyntaxError`.
- [ ] I remember the `typeof` TDZ and `switch`-scope traps.
- [ ] I state the host environment before predicting global behavior.

### Implement

- [ ] I default to `const`, use `let` deliberately and avoid new `var`.
- [ ] I can create per-iteration callbacks without accidental shared bindings.
- [ ] I can replace shared globals with explicit module/API boundaries.

### Debug

- [ ] I can diagnose accidental globals and strict-mode differences.
- [ ] I can separate an unresolved identifier from a missing object property.
- [ ] I can locate declaration conflicts that prevent any evaluation.

### Review

- [ ] I can flag ambiguous shadowing, leaking globals and scope-dependent legacy code.
- [ ] I can distinguish correctness defects from optional style improvements.
- [ ] I can recommend a safe incremental refactor without changing unrelated behavior.

## Related Inventory IDs

| Inventory ID | Coverage in this chapter |
|---|---|
| `JS-01` | declaration lifecycle, scope, reassignment, redeclaration and production choice |
| `JS-02` | global/function/block/module scope, lexical resolution and host boundaries |
| `JS-03` | declaration instantiation, hoisting, TDZ and output prediction |
| `JS-04` | legal shadowing, illegal collisions, redeclaration and early errors |
| `JS-22` | strict mode, accidental globals, global properties and `delete` |

Limited cross-references only:

- `JS-12`: declaration versus expression is discussed only for binding timing; full function coverage remains in 1.3.
- `JS-15`: lexical capture is used only to explain scope and loop bindings; full closure coverage remains in 1.3.
- `BR-05`: the basic call-stack relationship is introduced, but browser scheduling remains in 8.2 and 1.9.
- `JS-41–42`: module scope and automatic strict mode are introduced, but module graph semantics remain in 1.7.

## Sources

Primary and authoritative references:

- [ECMAScript 2026 — Execution Contexts](https://tc39.es/ecma262/2026/multipage/executable-code-and-execution-contexts.html#sec-execution-contexts)
- [ECMAScript 2026 — Environment Records](https://tc39.es/ecma262/2026/multipage/executable-code-and-execution-contexts.html#sec-environment-records)
- [ECMAScript 2026 — Identifier Resolution](https://tc39.es/ecma262/2026/multipage/executable-code-and-execution-contexts.html#sec-getidentifierreference)
- [ECMAScript 2026 — GlobalDeclarationInstantiation](https://tc39.es/ecma262/2026/multipage/ecmascript-language-scripts-and-modules.html#sec-globaldeclarationinstantiation)
- [ECMAScript 2026 — Let and Const Declarations](https://tc39.es/ecma262/2026/multipage/ecmascript-language-statements-and-declarations.html#sec-let-and-const-declarations)
- [ECMAScript 2026 — The `var` Statement](https://tc39.es/ecma262/2026/multipage/ecmascript-language-statements-and-declarations.html#sec-variable-statement)
- [ECMAScript 2026 — Strict Mode Code](https://tc39.es/ecma262/2026/multipage/ecmascript-language-source-code.html#sec-strict-mode-code)
- [MDN — Hoisting](https://developer.mozilla.org/en-US/docs/Glossary/Hoisting)
- [MDN — `let`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let)
- [MDN — `var`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/var)
- [MDN — `const`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/const)
- [MDN — Function declarations](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/function)
- [MDN — Strict mode](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Strict_mode)
- [MDN — `delete`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/delete)
- [MDN — `globalThis`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/globalThis)
- [HTML Living Standard — The `script` element](https://html.spec.whatwg.org/multipage/scripting.html#the-script-element)
- [Node.js — The module wrapper](https://nodejs.org/api/modules.html#the-module-wrapper)

Source and runtime verification date: **2026-09-23**.
