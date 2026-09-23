# 1. JavaScript & Async Programming — Answers

> Status: `partial draft — section 1.1 only; calibration review pending`
>
> Questions: [separate prompt file](../../by-domain/01-javascript-and-async-programming.md)
>
> Sections 1.2–1.12 remain placeholders.

## 1.1. Execution Model, Declarations & Scope

These are model answers and evaluation rubrics, not scripts that must be repeated word for word.

### JS-SCOPE-Q01

[Back to question](../../by-domain/01-javascript-and-async-programming.md#js-scope-q01)

`var` is function-scoped or top-level script/module-scoped rather than block-scoped. For a fresh name, declaration instantiation creates and initializes its binding to `undefined`; a compatible duplicate `var` reuses rather than resets an existing binding. It permits reassignment and generally permits another same-scope `var`.

`let` and `const` are lexical/block-scoped. Their bindings exist from entry into the scope but remain uninitialized in the TDZ until declaration evaluation. Neither permits a same-scope redeclaration. `let` permits later assignment; `const` requires initialization and forbids rebinding, but does not freeze an object value.

Production default: `const` unless reassignment is intended, then `let`. Avoid new `var`; retain it as legacy/debugging/interview knowledge.

Strong answer signals:

- distinguishes initialization from assignment;
- does not say `let`/`const` are “not hoisted”;
- distinguishes immutable binding from immutable object;
- includes the modern production rule.

### JS-SCOPE-Q02

[Back to question](../../by-domain/01-javascript-and-async-programming.md#js-scope-q02)

- Global scope is the outer scope of a script realm. In a classic browser script it is backed by a composite Global Environment Record.
- Function scope contains parameters, `var` declarations and declarations in the function body; each call has its own environment.
- Block scope is introduced for lexical declarations by constructs such as `{}`, loops, `catch` and the single `switch` CaseBlock.
- Module scope is private to the ES module; top-level declarations do not become global-object properties.

Lexical scope is the rule that identifier relationships follow source nesting. Lookup begins in the current Environment Record and follows `[[OuterEnv]]`; the caller does not redefine those relationships.

### JS-SCOPE-Q03

[Back to question](../../by-domain/01-javascript-and-async-programming.md#js-scope-q03)

For `let count = 1; count = 2;`:

1. the declaration says the scope has a `count` binding;
2. declaration instantiation creates it uninitialized;
3. evaluation of `let count = 1` initializes it with `1`;
4. `count = 2` is a later assignment.

TDZ exists because the binding is created before initialization. `const` is legal because it receives one initialization, but a later assignment is forbidden. Initialization is therefore not merely the first ordinary reassignment.

### JS-SCOPE-Q04

[Back to question](../../by-domain/01-javascript-and-async-programming.md#js-scope-q04)

1. `console.log(a)` prints `undefined`. The `var` binding is already initialized; the initializer assignment has not run.
2. Reading `b` throws `ReferenceError`. The lexical binding exists but is uninitialized in the TDZ.
3. `typeof c` also throws `ReferenceError`; `typeof` does not bypass an existing binding's TDZ.
4. `typeof neverDeclared` returns `"undefined"` because the identifier is unresolvable rather than an uninitialized lexical binding.

Each snippet must be treated independently because an uncaught error would stop the rest of one script.

### JS-SCOPE-Q05

[Back to question](../../by-domain/01-javascript-and-async-programming.md#js-scope-q05)

1. The function declaration call succeeds: its binding is initialized with the function object during declaration instantiation.
2. The `var` expression call throws `TypeError`: `ready` resolves successfully, but its current value is `undefined` and is not callable.
3. The `const` expression call throws `ReferenceError`: reading `ready` occurs in its TDZ.

The function expression itself is created only when that expression is evaluated. Its pre-declaration behavior is controlled by the declaration containing it.

### JS-SCOPE-Q06

[Back to question](../../by-domain/01-javascript-and-async-programming.md#js-scope-q06)

Shadowing uses separate nested bindings with the same name. Redeclaration tries to declare a name again in the same effective scope.

The first snippet is legal: `var mode` belongs to the outer var scope, while the block has a separate lexical `mode`.

The second is an early `SyntaxError`: the nested `var` is not block-scoped and would belong to the surrounding var scope, where the outer lexical `mode` already conflicts. “Illegal shadowing” is common interview wording, but “redeclaration conflict caused by `var` escaping the block” is more precise.

### JS-SCOPE-Q07

[Back to question](../../by-domain/01-javascript-and-async-programming.md#js-scope-q07)

In a sloppy classic script, assignment to the unresolvable `total` creates a global-object property. In strict code it throws `ReferenceError`; modules are strict automatically.

Minimal repair:

```js
function update(items) {
  const total = items.length;
  return total;
}
```

If another owner needs the value, return it or pass an explicit state object rather than writing a hidden global.

Preventive controls include ES modules/strict mode, lint rules such as `no-undef`, type checking and tests that assert no unexpected global property is created.

On the first call in a clean realm with an ordinary extensible global object, the sloppy accidental global is created as a configurable property, so `delete globalThis.total` operates explicitly on that property and returns `true`. Existing properties and host/exotic constraints can change property-write details. `delete` is a property operation, not a mechanism for removing lexical bindings. In strict source, `delete total` is an early `SyntaxError`; a local `let` or `const` binding cannot be removed with `delete`.

### JS-SCOPE-Q08

[Back to question](../../by-domain/01-javascript-and-async-programming.md#js-scope-q08)

An execution context is the specification state for executing code. The call stack orders active contexts. Scope is a static source-code visibility region. An Environment Record stores/resolves runtime bindings and links outward through `[[OuterEnv]]`.

When `outer()` is called, a new function execution context and function Environment Record are created and the context becomes active. Calling `inner()` does the same for `inner`; its outer relationship comes from where `inner` was defined. Entering an `if` block inside `inner` may create a block Environment Record and update the current lexical-environment reference, but it does not call a function or push another function execution context.

### JS-SCOPE-Q09

[Back to question](../../by-domain/01-javascript-and-async-programming.md#js-scope-q09)

Output:

```text
factory
```

For `name` inside the returned function, resolution checks:

1. the returned function's call Environment Record;
2. the environment captured from `makeReader`, where it finds `"factory"`;
3. it stops and does not continue to the global binding.

`run`'s local environment is not on this lexical chain. It is the caller's active context, but lexical scope follows definition-site nesting.

### JS-SCOPE-Q10

[Back to question](../../by-domain/01-javascript-and-async-programming.md#js-scope-q10)

In the specification model, evaluating a non-empty Block creates a new Declarative Environment Record and adjusts the current `LexicalEnvironment` reference while the block executes; engines may optimize it away when unobservable. No function is invoked.

Calling `f()` creates a function execution context, argument/parameter state and a function Environment Record, then pushes that context as the running context. Each recursive call gets another context.

Therefore scopes and stack frames are not one-to-one: nested blocks can add scopes inside one function frame, and one function definition can produce many call frames.

### JS-SCOPE-Q11

[Back to question](../../by-domain/01-javascript-and-async-programming.md#js-scope-q11)

- `first` is an early `SyntaxError`. The nested `var id` belongs to the function's var scope and conflicts with the function-body lexical `id`.
- `second` is valid. If `second()` is called, the block `let id` shadows the outer function-scoped `var id` and the call logs `2`; as written, the snippet only defines the function and produces no output.
- The two top-level `const id` declarations are an early `SyntaxError`.

For an early error in one parsed script/module/function body, normal evaluation of that unit never starts, so a preceding log in it does not run.

### JS-SCOPE-Q12

[Back to question](../../by-domain/01-javascript-and-async-programming.md#js-scope-q12)

Assuming a clean browser realm:

| Environment | First boolean | Second boolean |
|---|---:|---:|
| Classic script | `true` | `false` |
| ES module | `false` | `false` |

In a classic script, the Global Environment Record has an Object Record for suitable `var`/function bindings and a Declarative Record for lexical bindings. `fromVar` is reflected as a global-object property; `fromLet` is a global lexical binding but not a property.

In a module, both declarations are module-scoped, including `var`. Neither declaration creates a `globalThis` property. A pre-existing host property could change a raw comparison, which is why the clean-realm assumption matters.

### JS-SCOPE-Q13

[Back to question](../../by-domain/01-javascript-and-async-programming.md#js-scope-q13)

Output:

```text
[3, 3, 3]
[0, 1, 2]
```

The first three functions share one surrounding `var`-scoped `i` binding: function-scoped inside a function, script-global in a classic script, or module-local at module top level. They are called after the loop, when that binding contains `3`.

The `for (let ...)` semantics create a fresh per-iteration `j` binding. Each function closes over the binding for its own iteration. Closures capture access to bindings, not frozen copies produced by a timer.

### JS-SCOPE-Q14

[Back to question](../../by-domain/01-javascript-and-async-programming.md#js-scope-q14)

All cases are inside one `switch` CaseBlock, so the two `const message` declarations conflict even though control enters only one case.

Repair:

```js
function label(status) {
  switch (status) {
    case "idle": {
      const message = "Waiting";
      return message;
    }
    case "done": {
      const message = "Complete";
      return message;
    }
    default:
      return "Unknown";
  }
}
```

Each braced case has its own lexical scope.

### JS-SCOPE-Q15

[Back to question](../../by-domain/01-javascript-and-async-programming.md#js-scope-q15)

Severity-ranked findings:

1. **Correctness:** every handler closes over the same `var i`. After the loop `i === items.length`, so every handler returns `items[items.length]`, normally `undefined`.
2. **Correctness/ownership:** `handlers = {}` is an accidental global in sloppy code and a `ReferenceError` in strict/module code.
3. **Maintainability:** the hidden global makes repeated calls and consumers share undocumented state.
4. **Style/readability:** declarations do not communicate intended mutability.

Minimal safe repair:

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

If handlers should preserve the item value even when the array changes, capture `const item = items[i]` per iteration and return `item`; that is a contract decision, not merely a syntax preference.

A cleaner module API exports `register` and returns the handler collection. It does not expose a global at all.

### JS-SCOPE-Q16

[Back to question](../../by-domain/01-javascript-and-async-programming.md#js-scope-q16)

Model answer:

> Hoisting is an informal description of behavior created by declaration-instantiation work before normal statement evaluation; source lines are not moved. For a fresh name, a `var` binding is created and initialized to `undefined`, so an early read resolves; a compatible redeclaration does not reset an existing binding. `let`, `const` and `class` bindings are also created, but remain uninitialized in the TDZ, so an early read throws `ReferenceError`. A function declaration is normally initialized with its function object during instantiation, while a function expression is created only when the expression executes and therefore follows the lifecycle of its containing `var`, `let` or `const`.

Senior follow-up: name the appropriate instantiation algorithms only if useful; do not imply that an engine must allocate a specific object or run one universal “creation phase.”

### JS-SCOPE-Q17

[Back to question](../../by-domain/01-javascript-and-async-programming.md#js-scope-q17)

The Global Environment Record is a specification abstraction combining:

- an Object Environment Record tied to the host global object, used for suitable classic-script `var` and function bindings;
- a Declarative Environment Record for classic-script global `let`, `const` and `class` bindings.

Thus a top-level lexical declaration can be global without being `globalThis.name`. In a browser, `globalThis` exposes the global-this value; browser internals also involve `WindowProxy`, which is not needed for the basic answer.

ES modules use module environments instead. Their top-level declarations are not global-object properties and module code is strict automatically. None of this requires the engine to implement two ordinary JavaScript objects.

### JS-SCOPE-Q18

[Back to question](../../by-domain/01-javascript-and-async-programming.md#js-scope-q18)

When the second classic script performs global declaration instantiation, its `var config` conflicts with the existing global lexical `config` from the first script. The second script is rejected with `SyntaxError` before normal evaluation, so `"vendor starts"` does not log. This cross-Script failure occurs during `GlobalDeclarationInstantiation`; it is not formally an Early Error.

Immediate mitigation: rename/isolate the vendor's global name or load it through a wrapper that does not declare `config` globally. Changing the application's lexical declaration also requires changing source and starting a fresh page/realm; an already-instantiated global `let` binding cannot be deleted at runtime. Simply reordering can change which script fails but does not solve ownership.

Durable fix: use modules or an explicit namespaced integration contract so each component owns its bindings and intentionally exposes only a public API. Test the production loading mode, not only the bundler's development module graph.

### JS-SCOPE-Q19

[Back to question](../../by-domain/01-javascript-and-async-programming.md#js-scope-q19)

The code works as assumed only in a suitable classic browser script: top-level `var registry` creates/uses a global-object property.

It fails in a browser ES module and Node.js ESM because the `var` is module-scoped. It also fails in Node.js CommonJS because the file wrapper makes the `var` module-local. In those environments `globalThis.registry` is normally `undefined`, so reading `.enabled` throws.

If deliberate cross-script exposure is required, make it explicit:

```js
globalThis.myLibrary = {
  registry: { enabled: true },
};
```

That API needs documented naming, initialization, collision/version and cleanup rules. Prefer exporting the value when no global contract is required:

```js
export const registry = { enabled: true };
```

### JS-SCOPE-Q20

[Back to question](../../by-domain/01-javascript-and-async-programming.md#js-scope-q20)

```js
function installLegacyApi(root, api) {
  const key = "frontendInterview";

  if (Object.hasOwn(root, key)) {
    throw new Error(`${key} is already installed`);
  }

  root[key] = api;

  return function uninstall() {
    if (root[key] !== api) {
      return false;
    }

    return delete root[key];
  };
}
```

The root object is explicit and injectable, so no unresolved assignment creates an accidental global and no browser-only `window` assumption leaks into the helper. `Object.hasOwn` protects an existing own-property contract before installation. Cleanup checks identity so it does not delete a replacement installed by another owner.

`delete root[key]` targets an object property and can report descriptor-based failure. It cannot remove a `let`, `const`, parameter or local binding; strict `delete identifier` syntax is invalid.

Complexity is `O(1)` time and retained `O(1)` state. This bridge is appropriate only for deliberate legacy interoperability. A module should normally `export` the API and let consumers import it, avoiding shared global naming and lifecycle concerns.
