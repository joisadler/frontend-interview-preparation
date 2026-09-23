# 1. JavaScript & Async Programming — Exercise Solutions

> Status: `partial draft — section 1.1 only; calibration review pending`
>
> Prompts: [separate exercise file](../../prompts/by-domain/01-javascript-and-async-programming.md)
>
> Sections 1.2–1.12 remain placeholders.

## 1.1. Execution Model, Declarations & Scope

### JS-SCOPE-EX01

- Status: `draft`
- Prompt location: [JS-SCOPE-EX01](../../prompts/by-domain/01-javascript-and-async-programming.md#js-scope-ex01)
- Last verified: `2026-09-23`

#### Reasoning

The table should track the binding lifecycle, not rewrite the source into an imaginary “hoisted” program.

#### Solution

| Form | Scope | Before declaration evaluation | Reassign | Same-scope redeclare | Note |
|---|---|---|---:|---:|---|
| `var x` | function or top-level script/module; not block | fresh binding: initialized to `undefined`; compatible existing binding: reused, not reset | yes | another `var` generally yes | legacy/interview knowledge |
| `let x` | lexical/block | uninitialized, TDZ | yes | no | use for intentional reassignment |
| `const x = v` | lexical/block | uninitialized, TDZ | no | no | default modern choice; object may still mutate |
| `function f() {}` | enclosing declaration scope | normally initialized with function object | context-dependent binding | context-dependent conflicts | callable before textual position |
| `var f = function () {}` | scope of `var` | `f === undefined`; expression not evaluated | yes | `var` rules | early call gives `TypeError` |
| `const f = function () {}` | lexical/block | `f` uninitialized, TDZ | no | no | early read gives `ReferenceError` |

Definitions:

- **Declaration:** syntax that introduces or declares a name; declaration instantiation may create a fresh binding or reuse a compatible existing one.
- **Initialization:** first value supplied to a newly created binding.
- **Assignment:** later write to an initialized mutable binding.
- **TDZ:** period from scope entry until a lexical binding is initialized.
- **Early error:** a static-semantic error detected for one parsed unit before its evaluation; a later classic script can instead throw `SyntaxError` during global declaration instantiation without that failure being a formal Early Error.

The table assumes a fresh name unless stated. Duplicate `var`, parameter/function reuse and compatible pre-existing global properties are not reset to `undefined`.

#### Complexity

Not applicable; this is a recall model.

#### Alternative Approaches

Add rows for `class` and named function expressions after the core table is stable. They are useful follow-ups, not required for the first recall pass.

#### Common Errors

- Saying `let`/`const` do not exist before their line.
- Saying `const` makes an object immutable.
- Saying a function expression is hoisted like a function declaration.

### JS-SCOPE-EX02

- Status: `draft`
- Prompt location: [JS-SCOPE-EX02](../../prompts/by-domain/01-javascript-and-async-programming.md#js-scope-ex02)
- Last verified: `2026-09-23`

#### Reasoning

First decide whether parsing/declaration instantiation succeeds. Only then trace runtime reads.

#### Solution

| Snippet | Result | Why |
|---|---|---|
| A | logs `undefined`, then `7` | `var score` is initialized to `undefined`; initializer later assigns `7` |
| B | `ReferenceError`, no output | `score` is an uninitialized lexical binding at the read |
| C | `ReferenceError`, no output | inner `score` shadows outer `score` throughout the block and is in TDZ |
| D | logs `"undefined"`, then throws `ReferenceError` | `missing` is unresolvable; `present` exists in TDZ |
| E | `TypeError`, no output | `run` resolves to initialized value `undefined`, which is not callable |
| F | early `SyntaxError`, no output | same scope cannot contain lexical `id` and `var id` |

#### Complexity

Not applicable.

#### Alternative Approaches

For each snippet draw a state timeline: scope entry → binding state → read → declaration/initializer. This is slower but useful when recall is rusty.

#### Common Errors

- Predicting `"before"` for F.
- Calling E a `ReferenceError`.
- Letting the outer `score` win in C.
- Treating `typeof` as universally safe.

### JS-SCOPE-EX03

- Status: `draft`
- Prompt location: [JS-SCOPE-EX03](../../prompts/by-domain/01-javascript-and-async-programming.md#js-scope-ex03)
- Last verified: `2026-09-23`

#### Reasoning

The active caller belongs on the call stack; it does not automatically belong in the callee's lexical outer chain.

#### Solution

Final output:

```text
scope:build!
```

At `return label + suffix`:

- `suffix`: current `if` block record → found as `"!"`.
- `label`: current `if` block record → not found; returned callback's call record → not found; captured `build` call record → found as `"scope:build"`.
- The global `label` is not reached.
- `invoke`'s local `label` is not on the lexical chain at all.

Call stack at that moment:

```text
returned callback (true)   ← running
invoke(report)
entry script
```

`build` is no longer on the call stack, but its relevant environment remains reachable through `report`.

#### Complexity

The manual lookup is `O(d)` in lexical nesting depth for a conceptual unresolved-to-found walk. This is a reasoning model, not a promise about engine lookup cost after optimization.

#### Alternative Approaches

Annotate each identifier in the source with its declaration rather than drawing full records. Use the full record chain when the call site is intended to distract.

#### Common Errors

- Searching `invoke` before the captured `build` environment.
- Putting `build` on the active call stack after it returned.
- Giving the `if` block a function execution context.

### JS-SCOPE-EX04

- Status: `draft`
- Prompt location: [JS-SCOPE-EX04](../../prompts/by-domain/01-javascript-and-async-programming.md#js-scope-ex04)
- Last verified: `2026-09-23`

#### Reasoning

A strong timed answer prioritizes definition, causal model and one discriminating example.

#### Solution

Possible 45-second answer:

> `var` is function- or top-level-scoped. A fresh binding is initialized to `undefined` during declaration instantiation; a compatible duplicate `var` reuses rather than resets an existing binding. It can be reassigned. `let` and `const` are block-scoped lexical declarations: their bindings exist from scope entry but remain uninitialized in the TDZ. `let` can be reassigned, while `const` cannot be rebound, although an object value can mutate. In modern code I default to `const`, use `let` for reassignment and keep `var` for legacy debugging and interviews.

Possible 60-second answer:

> A function call creates an execution context on the call stack. Identifier resolution is modeled through Environment Records: the current record holds local bindings and links to `[[OuterEnv]]`, so lookup follows source nesting rather than the caller. Before normal evaluation, declaration-instantiation work creates bindings. A fresh `var` binding is initialized to `undefined`; lexical declarations stay uninitialized in the TDZ; function declarations normally receive their function object. That observable behavior is called hoisting, but no source is physically moved. A block may add an Environment Record without adding a call-stack frame.

#### Complexity

Target duration: 45 and 60 seconds.

#### Alternative Approaches

Use a single output snippet as the example, but do not spend the whole answer dry-running it.

#### Common Errors

- Listing rules without one causal model.
- Using all the time on specification names.
- Detouring into tasks/microtasks or full closure use cases.

### JS-SCOPE-EX05

- Status: `draft`
- Prompt location: [JS-SCOPE-EX05](../../prompts/by-domain/01-javascript-and-async-programming.md#js-scope-ex05)
- Last verified: `2026-09-23`

#### Reasoning

Separate an unqualified assignment from an explicit property write.

#### Solution

In a sloppy classic script:

- top-level `record` is a global function binding and is normally reflected as a global-object property;
- `event` is a parameter binding local to each call;
- on the first call in a clean realm with an ordinary extensible global object, `lastEvent = event` creates a configurable property because `lastEvent` is unresolvable; later calls update it.
- `count` is a function-scoped local `var`.
- `globalThis.count = count` explicitly creates/updates a global-object property.
- the logs produce `"open"` and `1`.

With `"use strict"` or when loaded as an ES module, the first assignment throws `ReferenceError`; the count calculation/write and later logs are not reached.

After the sloppy version runs, `delete globalThis.lastEvent` explicitly deletes the normally configurable accidental-global property and returns `true`. Strict source containing `delete lastEvent` is an early `SyntaxError`. `delete` targets properties; it is not a way to remove the local `count` binding or any `let`/`const` binding.

Minimal repair preserving explicit global visibility:

```js
function record(event) {
  globalThis.lastEvent = event;
  const count = (globalThis.count || 0) + 1;
  globalThis.count = count;
}
```

Cleaner state-owning API:

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

In a real module, export `createRecorder` or one intentional recorder instance.

#### Complexity

Each `record` and `snapshot` call is `O(1)` time and state is `O(1)` space.

#### Alternative Approaches

Pass a mutable state object into `record` if dependency injection and external ownership better fit the integration.

#### Common Errors

- Calling the local `var count` global.
- Assuming strict mode merely stops global property creation but continues the function.
- Using `delete lastEvent` as a cleanup strategy.

### JS-SCOPE-EX06

- Status: `draft`
- Prompt location: [JS-SCOPE-EX06](../../prompts/by-domain/01-javascript-and-async-programming.md#js-scope-ex06)
- Last verified: `2026-09-23`

#### Reasoning

The nested `var result` belongs to the function scope, and all unbraced `case` clauses share one lexical CaseBlock.

#### Solution

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

The original function body is rejected before it can be called: the `var result` conflicts with lexical `result`, and duplicate `suffix` declarations conflict in the shared `switch` scope.

#### Complexity

`O(1)` time and `O(1)` additional space.

#### Alternative Approaches

A lookup table may be cleaner production code, but it intentionally bypasses the scope-repair objective of this exercise.

#### Common Errors

- Changing `var result` to a second `let result` inside the `if`, which shadows rather than updates the outer result.
- Fixing only the `if` conflict and missing the `switch`.
- Claiming only the selected `case` is parsed.

### JS-SCOPE-EX07

- Status: `draft`
- Prompt location: [JS-SCOPE-EX07](../../prompts/by-domain/01-javascript-and-async-programming.md#js-scope-ex07)
- Last verified: `2026-09-23`

#### Reasoning

Review correctness and ownership before style.

#### Solution

Ranked findings:

1. **High — correctness:** every callback shares the same `var index`; after the loop it equals `buttons.length`. If `active` is true, `buttons[index]` is normally `undefined` and `.id` throws `TypeError`.
2. **High — environment dependence:** `callbacks = []` creates an accidental global in a sloppy classic script and throws in strict/module code.
3. **Medium — ownership:** `active` and `callbacks` are shared globals with no documented lifecycle. Confirm whether external scripts rely on them.
4. **Low — maintainability:** declaration choices obscure which state should change.

If compatibility requires the original classic-script `active` global and a `callbacks` property created when `install` runs, an explicit minimal patch is:

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

The public property remains for compatibility and keeps its creation timing/configurability, but ownership is explicit and the shared loop binding is fixed.

Module-oriented target:

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

Tests:

- one and multiple buttons return their own IDs;
- disabled state returns `undefined`;
- repeated installation does not mix collections;
- strict-mode execution creates no unexpected global;
- decide and test whether later array mutation is live or snapshotted.

#### Complexity

Creation is `O(n)` time and `O(n)` space; each callback call is `O(1)`.

#### Alternative Approaches

Capture `const button = buttons[index]` per iteration if callback identity should follow the original button rather than the current array slot.

#### Common Errors

- Reporting only “use `let`.”
- Removing globals without checking the legacy contract.
- Treating `active` as definitely accidental when requirements are unknown.

### JS-SCOPE-EX08

- Status: `draft`
- Prompt location: [JS-SCOPE-EX08](../../prompts/by-domain/01-javascript-and-async-programming.md#js-scope-ex08)
- Last verified: `2026-09-23`

#### Reasoning

The declaration determines whether each callback gets a per-iteration binding. A second per-iteration binding chooses live versus snapshot value semantics.

#### Solution

Live values:

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

Snapshot values:

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

In both versions, `for (let ...)` creates a fresh `index` binding per iteration. The snapshot version also creates a per-iteration `value` binding; the live version reads the array slot when invoked.

Representative assertions:

```js
const values = ["a", "b", "c"];
const readers = createReaders(values);

console.assert(readers.length === 3);
console.assert(readers[0]().index === 0);
console.assert(readers[2]().value === "c");

values[0] = "changed";
// Live contract: readers[0]().value === "changed"
// Snapshot contract: readers[0]().value === "a"

console.assert(createReaders([]).length === 0);
```

#### Complexity

Creation is `O(n)` time and `O(n)` space. Each read is `O(1)`.

#### Alternative Approaches

`values.map((value, index) => () => ({ index, value }))` is idiomatic for the snapshot contract but excluded so the exercise exposes loop binding semantics.

#### Common Errors

- Using `var index` and capturing one shared binding.
- Claiming the live version snapshots `values[index]`.
- Leaving the live/snapshot contract implicit.

### JS-SCOPE-EX09

- Status: `draft`
- Prompt location: [JS-SCOPE-EX09](../../prompts/by-domain/01-javascript-and-async-programming.md#js-scope-ex09)
- Last verified: `2026-09-23`

#### Reasoning

Analyze each file in load order. Declaration instantiation happens before that file's evaluation, and one failed classic script does not retroactively undo a previously completed script.

#### Solution

Assume a clean browser realm and normal blocking external classic-script order.

1. `bootstrap.js` instantiates and evaluates:
   - `var mode` creates a global var binding and normally a non-configurable global-object property with value `"legacy"` after its initializer.
   - sloppy `sharedCount = 0` creates a configurable global-object property.
2. Before `widget.js` evaluates, its top-level lexical `let mode` conflicts with the existing global `var mode`/restricted global property. `GlobalDeclarationInstantiation` completes abruptly with `SyntaxError`, so the script never reaches Evaluation. This cross-Script failure is not formally an Early Error.
   - `"widget start"` does not log.
   - `makeHandlers` is not installed because the script does not evaluate.
3. `app.js` is a module:
   - its `var mode` is module-scoped and does not conflict with the classic-script global;
   - module instantiation/evaluation succeeds because the body of `start` is not executed merely by defining/exporting it;
   - `sharedCount` can resolve through the outer global environment because the property already exists;
   - `makeHandlers` remains unresolved and would throw `ReferenceError` when `start` reaches that call.

If another module imports and calls `start(nodes)`, `sharedCount` increments first and then the call to missing `makeHandlers` throws. There is no loop-callback output because no handlers are created.

Defects ranked:

1. **High:** classic-script global declaration collision prevents `widget.js` from running.
2. **High:** module depends on an undeclared, failed-to-install global `makeHandlers`.
3. **High:** intended callback loop would share one `var i`, so every callback would use `nodes.length`.
4. **Medium:** `sharedCount` is an accidental global with implicit ownership.
5. **Medium:** same spelling `mode` represents unrelated state across global and module environments.

Minimal mixed-loading repair:

```js
// bootstrap.js — classic
var mode = "legacy";
globalThis.sharedCount = 0;
```

```js
// widget.js — classic
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
// app.js — module
var mode = "module";

export function start(nodes) {
  globalThis.sharedCount += 1;
  return globalThis.makeHandlers(nodes);
}
```

This retains a legacy global contract explicitly. In a browser classic script, the top-level function declaration is available through the global object; production code should document and test that dependency.

Cleaner all-module target:

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

`bootstrap.js` should either become a module exporting its actual configuration or be removed if its state is obsolete.

#### Complexity

Handler creation is `O(n)` time and `O(n)` retained space; each handler call is `O(1)`.

#### Alternative Approaches

For a staged migration, expose exactly one documented namespace such as `globalThis.legacyApp` rather than several globals. That is still transitional state, not the final module design.

#### Common Errors

- Predicting `"widget start"` before the declaration-instantiation `SyntaxError`.
- Assuming the module's `var mode` overwrites `globalThis.mode`.
- Assuming `makeHandlers` exists because its source text was downloaded.
- Missing that `sharedCount` changes before the later call fails.
- Fixing the name collision but retaining the shared `var i` binding.
