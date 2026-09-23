# 1. JavaScript & Async Programming — Questions

> Status: `partial draft — section 1.1 only; calibration review pending`
>
> Answers: [separate answer file](../answers/by-domain/01-javascript-and-async-programming.md)
>
> Sections 1.2–1.12 remain placeholders.

## 1.1. Execution Model, Declarations & Scope

Use these prompts for active recall. Do not open the answer file before making an attempt.

### JS-SCOPE-Q01

**Compare `var`, `let` and `const`.**

- Status: `draft`
- Domain: `JavaScript & Async Programming`
- Topic: `1.1. Execution Model, Declarations & Scope`
- Level: `Junior`
- Type: `conceptual | compare`
- Priority/frequency: `Core | F3`
- Related inventory IDs: `JS-01`
- Modern/legacy status: `modern guidance + legacy var knowledge`
- Answer location: [JS-SCOPE-Q01](../answers/by-domain/01-javascript-and-async-programming.md#js-scope-q01)
- Sources / last verified: `ECMAScript 2026, MDN | 2026-09-23`

#### Prompt

Compare the three declarations across scope, pre-declaration state, reassignment and redeclaration. Finish with the rule you would use in modern production code.

### JS-SCOPE-Q02

**Name the relevant scope boundaries.**

- Status: `draft`
- Domain: `JavaScript & Async Programming`
- Topic: `1.1. Execution Model, Declarations & Scope`
- Level: `Junior`
- Type: `conceptual | explain`
- Priority/frequency: `Core | F3`
- Related inventory IDs: `JS-02`
- Modern/legacy status: `modern core`
- Answer location: [JS-SCOPE-Q02](../answers/by-domain/01-javascript-and-async-programming.md#js-scope-q02)
- Sources / last verified: `ECMAScript 2026 | 2026-09-23`

#### Prompt

Explain global, function, block and module scope. Then explain why “lexical scope” is a rule for resolving names rather than just another equivalent boundary.

### JS-SCOPE-Q03

**Why are declaration, initialization and assignment different?**

- Status: `draft`
- Domain: `JavaScript & Async Programming`
- Topic: `1.1. Execution Model, Declarations & Scope`
- Level: `Junior`
- Type: `conceptual | why`
- Priority/frequency: `Core | F3`
- Related inventory IDs: `JS-01`, `JS-03`
- Modern/legacy status: `modern core`
- Answer location: [JS-SCOPE-Q03](../answers/by-domain/01-javascript-and-async-programming.md#js-scope-q03)
- Sources / last verified: `ECMAScript 2026 | 2026-09-23`

#### Prompt

Use `let count = 1; count = 2;` to identify declaration, binding creation, initialization and later assignment. Why does the distinction matter for TDZ and `const`?

### JS-SCOPE-Q04

**Predict binding-lifecycle results.**

- Status: `draft`
- Domain: `JavaScript & Async Programming`
- Topic: `1.1. Execution Model, Declarations & Scope`
- Level: `Junior`
- Type: `output`
- Priority/frequency: `Core | F3`
- Related inventory IDs: `JS-03`
- Modern/legacy status: `modern core + legacy var`
- Answer location: [JS-SCOPE-Q04](../answers/by-domain/01-javascript-and-async-programming.md#js-scope-q04)
- Sources / last verified: `ECMAScript 2026, MDN hoisting | 2026-09-23`

#### Prompt

Treat each snippet as an independent script. Predict the result and name the binding state at the read.

```js
console.log(a);
var a = 1;
```

```js
console.log(b);
let b = 1;
```

```js
console.log(typeof c);
const c = 1;
```

```js
console.log(typeof neverDeclared);
```

### JS-SCOPE-Q05

**Function declaration versus function expression timing.**

- Status: `draft`
- Domain: `JavaScript & Async Programming`
- Topic: `1.1. Execution Model, Declarations & Scope`
- Level: `Junior`
- Type: `compare | output`
- Priority/frequency: `Core | F3`
- Related inventory IDs: `JS-03`
- Modern/legacy status: `modern core + legacy var`
- Answer location: [JS-SCOPE-Q05](../answers/by-domain/01-javascript-and-async-programming.md#js-scope-q05)
- Sources / last verified: `ECMAScript 2026, MDN function declarations/expressions | 2026-09-23`

#### Prompt

For each independent snippet, say whether the call succeeds or throws. If it throws, name the error class and explain why.

```js
ready();
function ready() {}
```

```js
ready();
var ready = function () {};
```

```js
ready();
const ready = function () {};
```

### JS-SCOPE-Q06

**Shadowing or redeclaration?**

- Status: `draft`
- Domain: `JavaScript & Async Programming`
- Topic: `1.1. Execution Model, Declarations & Scope`
- Level: `Junior`
- Type: `conceptual | why`
- Priority/frequency: `Core | F2`
- Related inventory IDs: `JS-04`
- Modern/legacy status: `modern core + legacy var interaction`
- Answer location: [JS-SCOPE-Q06](../answers/by-domain/01-javascript-and-async-programming.md#js-scope-q06)
- Sources / last verified: `ECMAScript 2026, MDN let/var | 2026-09-23`

#### Prompt

Define shadowing and redeclaration. Why is the first snippet legal while the second is rejected?

```js
var mode = "outer";
{
  let mode = "inner";
}
```

```js
let mode = "outer";
{
  var mode = "inner";
}
```

### JS-SCOPE-Q07

**Debug an accidental global.**

- Status: `draft`
- Domain: `JavaScript & Async Programming`
- Topic: `1.1. Execution Model, Declarations & Scope`
- Level: `Junior`
- Type: `debugging`
- Priority/frequency: `Core | F2`
- Related inventory IDs: `JS-22`
- Modern/legacy status: `modern prevention + sloppy-script legacy`
- Answer location: [JS-SCOPE-Q07](../answers/by-domain/01-javascript-and-async-programming.md#js-scope-q07)
- Sources / last verified: `ECMAScript 2026, MDN strict mode | 2026-09-23`

#### Prompt

A classic browser script unexpectedly exposes `total` on `globalThis`:

```js
function update(items) {
  total = items.length;
}

update(["a", "b"]);
```

Explain the sloppy-script behavior, predict strict-mode behavior, repair the defect and name two preventive controls.

Then answer:

- after the sloppy version runs, what does `delete globalThis.total` operate on and what does it normally return?
- why can `delete` not remove a local `let`/`const` binding?
- what happens if strict source contains `delete total`?

### JS-SCOPE-Q08

**Execution context, Environment Record and call stack.**

- Status: `draft`
- Domain: `JavaScript & Async Programming`
- Topic: `1.1. Execution Model, Declarations & Scope`
- Level: `Mid`
- Type: `conceptual | explain`
- Priority/frequency: `Core | F3`
- Related inventory IDs: `JS-02`, `JS-03`
- Modern/legacy status: `modern core`
- Answer location: [JS-SCOPE-Q08](../answers/by-domain/01-javascript-and-async-programming.md#js-scope-q08)
- Sources / last verified: `ECMAScript 2026 execution contexts/environment records | 2026-09-23`

#### Prompt

Distinguish execution context, call stack, scope and Environment Record. Trace what changes when `outer()` calls `inner()`, and what changes when `inner()` enters an `if` block.

### JS-SCOPE-Q09

**Trace lexical resolution.**

- Status: `draft`
- Domain: `JavaScript & Async Programming`
- Topic: `1.1. Execution Model, Declarations & Scope`
- Level: `Mid`
- Type: `output | explain`
- Priority/frequency: `Core | F3`
- Related inventory IDs: `JS-02`
- Modern/legacy status: `modern core`
- Answer location: [JS-SCOPE-Q09](../answers/by-domain/01-javascript-and-async-programming.md#js-scope-q09)
- Sources / last verified: `ECMAScript 2026 identifier resolution | 2026-09-23`

#### Prompt

Predict the output, then list the Environment Records checked for the read of `name`.

```js
const name = "global";

function makeReader() {
  const name = "factory";
  return function () {
    return name;
  };
}

function run(reader) {
  const name = "caller";
  console.log(reader());
}

run(makeReader());
```

Why does the caller's binding not win?

### JS-SCOPE-Q10

**Why does a block not add a call-stack frame?**

- Status: `draft`
- Domain: `JavaScript & Async Programming`
- Topic: `1.1. Execution Model, Declarations & Scope`
- Level: `Mid`
- Type: `why | compare`
- Priority/frequency: `Professional | F2`
- Related inventory IDs: `JS-02`
- Modern/legacy status: `modern core`
- Answer location: [JS-SCOPE-Q10](../answers/by-domain/01-javascript-and-async-programming.md#js-scope-q10)
- Sources / last verified: `ECMAScript 2026 execution contexts | 2026-09-23`

#### Prompt

Compare entering `{ const value = 1; }` with calling `function f() { const value = 1; }`. What new specification state is needed in each case, and why is “one scope equals one stack frame” a broken model?

### JS-SCOPE-Q11

**Find every declaration defect.**

- Status: `draft`
- Domain: `JavaScript & Async Programming`
- Topic: `1.1. Execution Model, Declarations & Scope`
- Level: `Mid`
- Type: `find-the-bug | output`
- Priority/frequency: `Core | F2`
- Related inventory IDs: `JS-01`, `JS-04`
- Modern/legacy status: `modern core + legacy var interaction`
- Answer location: [JS-SCOPE-Q11](../answers/by-domain/01-javascript-and-async-programming.md#js-scope-q11)
- Sources / last verified: `ECMAScript 2026 declaration early errors | 2026-09-23`

#### Prompt

Classify each independent snippet as valid or an early error. For valid code, state which binding is read.

```js
function first() {
  let id = 1;
  {
    var id = 2;
  }
}
```

```js
function second() {
  var id = 1;
  {
    let id = 2;
    console.log(id);
  }
}
```

```js
const id = 1;
const id = 2;
```

If a snippet is an early error, does any preceding `console.log` in that parsed unit run?

### JS-SCOPE-Q12

**Classic browser script versus module globals.**

- Status: `draft`
- Domain: `JavaScript & Async Programming`
- Topic: `1.1. Execution Model, Declarations & Scope`
- Level: `Mid`
- Type: `compare | output`
- Priority/frequency: `Professional | F2`
- Related inventory IDs: `JS-02`, `JS-22`
- Modern/legacy status: `modern modules + classic-script interoperability`
- Answer location: [JS-SCOPE-Q12](../answers/by-domain/01-javascript-and-async-programming.md#js-scope-q12)
- Sources / last verified: `ECMAScript 2026 global environment, HTML Living Standard | 2026-09-23`

#### Prompt

Predict the two booleans first when loaded as a classic browser script, then as a browser ES module:

```js
var fromVar = 1;
let fromLet = 2;

console.log(globalThis.fromVar === 1);
console.log(globalThis.fromLet === 2);
```

Explain the Global Environment Record at a practical level. Do not use DevTools-console behavior as evidence.

### JS-SCOPE-Q13

**One loop binding or one per iteration?**

- Status: `draft`
- Domain: `JavaScript & Async Programming`
- Topic: `1.1. Execution Model, Declarations & Scope`
- Level: `Mid`
- Type: `output | why`
- Priority/frequency: `Core | F3`
- Related inventory IDs: `JS-01`, `JS-02`
- Modern/legacy status: `modern guidance + legacy var knowledge`
- Answer location: [JS-SCOPE-Q13](../answers/by-domain/01-javascript-and-async-programming.md#js-scope-q13)
- Sources / last verified: `ECMAScript 2026, MDN for/closures | 2026-09-23`

#### Prompt

Predict both arrays and explain the result using **bindings**, not “timing magic.”

```js
const withVar = [];
for (var i = 0; i < 3; i += 1) {
  withVar.push(() => i);
}

const withLet = [];
for (let j = 0; j < 3; j += 1) {
  withLet.push(() => j);
}

console.log(withVar.map((read) => read()));
console.log(withLet.map((read) => read()));
```

### JS-SCOPE-Q14

**Debug duplicate declarations in `switch`.**

- Status: `draft`
- Domain: `JavaScript & Async Programming`
- Topic: `1.1. Execution Model, Declarations & Scope`
- Level: `Mid`
- Type: `find-the-bug | debugging`
- Priority/frequency: `Professional | F2`
- Related inventory IDs: `JS-01`, `JS-04`
- Modern/legacy status: `modern core`
- Answer location: [JS-SCOPE-Q14](../answers/by-domain/01-javascript-and-async-programming.md#js-scope-q14)
- Sources / last verified: `ECMAScript 2026 block declarations, MDN let | 2026-09-23`

#### Prompt

Why is this function rejected as an Early Error, even though only one case runs? Repair it without moving `message` outside the cases.

```js
function label(status) {
  switch (status) {
    case "idle":
      const message = "Waiting";
      return message;
    case "done":
      const message = "Complete";
      return message;
    default:
      return "Unknown";
  }
}
```

### JS-SCOPE-Q15

**Review legacy scope-sensitive registration code.**

- Status: `draft`
- Domain: `JavaScript & Async Programming`
- Topic: `1.1. Execution Model, Declarations & Scope`
- Level: `Mid`
- Type: `code-review | refactoring`
- Priority/frequency: `Professional | F2`
- Related inventory IDs: `JS-01`, `JS-02`, `JS-22`
- Modern/legacy status: `legacy diagnosis → modern recommendation`
- Answer location: [JS-SCOPE-Q15](../answers/by-domain/01-javascript-and-async-programming.md#js-scope-q15)
- Sources / last verified: `ECMAScript 2026, MDN strict mode/closures | 2026-09-23`

#### Prompt

Review for correctness, global ownership and maintainability. Rank findings by severity; do not merely replace every `var` mechanically.

```js
function register(items) {
  handlers = {};

  for (var i = 0; i < items.length; i += 1) {
    handlers[i] = function () {
      return items[i];
    };
  }

  return handlers;
}
```

Propose a minimal safe repair and a cleaner module-oriented API.

### JS-SCOPE-Q16

**Explain hoisting precisely without over-teaching the specification.**

- Status: `draft`
- Domain: `JavaScript & Async Programming`
- Topic: `1.1. Execution Model, Declarations & Scope`
- Level: `Senior`
- Type: `conceptual | interview-communication`
- Priority/frequency: `Core | F3`
- Related inventory IDs: `JS-03`
- Modern/legacy status: `modern core + precise terminology`
- Answer location: [JS-SCOPE-Q16](../answers/by-domain/01-javascript-and-async-programming.md#js-scope-q16)
- Sources / last verified: `ECMAScript 2026 declaration instantiation, MDN hoisting | 2026-09-23`

#### Prompt

Give a 45–60 second answer that:

1. rejects physical source movement;
2. explains `var`, lexical declarations and function declarations;
3. uses no unnecessary abstract-operation trivia;
4. remains accurate enough for a Senior follow-up.

### JS-SCOPE-Q17

**Explain the browser Global Environment Record.**

- Status: `draft`
- Domain: `JavaScript & Async Programming`
- Topic: `1.1. Execution Model, Declarations & Scope`
- Level: `Senior`
- Type: `conceptual | explain`
- Priority/frequency: `Professional | F2`
- Related inventory IDs: `JS-02`, `JS-22`
- Modern/legacy status: `classic-script interoperability + modern module contrast`
- Answer location: [JS-SCOPE-Q17](../answers/by-domain/01-javascript-and-async-programming.md#js-scope-q17)
- Sources / last verified: `ECMAScript 2026 global environment, HTML Living Standard | 2026-09-23`

#### Prompt

Explain the Object Record and Declarative Record without implying that engines literally use two JavaScript objects. Include top-level `var`, function, `let`, `const`, modules and `globalThis`.

### JS-SCOPE-Q18

**Diagnose a production-only global collision.**

- Status: `draft`
- Domain: `JavaScript & Async Programming`
- Topic: `1.1. Execution Model, Declarations & Scope`
- Level: `Senior`
- Type: `practical-scenario | debugging`
- Priority/frequency: `Professional | F2`
- Related inventory IDs: `JS-02`, `JS-04`, `JS-22`
- Modern/legacy status: `legacy classic scripts → modern module boundary`
- Answer location: [JS-SCOPE-Q18](../answers/by-domain/01-javascript-and-async-programming.md#js-scope-q18)
- Sources / last verified: `ECMAScript 2026 GlobalDeclarationInstantiation | 2026-09-23`

#### Prompt

Development uses bundled modules and works. Production loads these independent classic scripts in order:

```html
<script src="app-config.js"></script>
<script src="vendor-widget.js"></script>
```

```js
// app-config.js
let config = { locale: "en" };
```

```js
// vendor-widget.js
console.log("vendor starts");
var config = { mode: "compact" };
```

What happens when the second script is instantiated? Does its log run? Give an immediate mitigation and a durable design fix.

### JS-SCOPE-Q19

**Review a cross-runtime top-level assumption.**

- Status: `draft`
- Domain: `JavaScript & Async Programming`
- Topic: `1.1. Execution Model, Declarations & Scope`
- Level: `Senior`
- Type: `code-review | trade-off`
- Priority/frequency: `Professional | F2`
- Related inventory IDs: `JS-02`, `JS-22`
- Modern/legacy status: `modern portability review`
- Answer location: [JS-SCOPE-Q19](../answers/by-domain/01-javascript-and-async-programming.md#js-scope-q19)
- Sources / last verified: `ECMAScript 2026, Node.js module wrapper | 2026-09-23`

#### Prompt

A library author expects this to work in a browser classic script, a browser module, Node.js ESM and Node.js CommonJS:

```js
var registry = { enabled: true };
console.log(globalThis.registry.enabled);
```

Review the assumption. If deliberate global exposure is required, what explicit contract would you use? If it is not required, what should the module expose instead?

### JS-SCOPE-Q20

**Implement a deliberate legacy-global bridge.**

- Status: `draft`
- Domain: `JavaScript & Async Programming`
- Topic: `1.1. Execution Model, Declarations & Scope`
- Level: `Senior`
- Type: `implementation | practical-scenario`
- Priority/frequency: `Professional | F2`
- Related inventory IDs: `JS-02`, `JS-22`
- Modern/legacy status: `legacy interoperability with explicit modern ownership`
- Answer location: [JS-SCOPE-Q20](../answers/by-domain/01-javascript-and-async-programming.md#js-scope-q20)
- Sources / last verified: `ECMAScript 2026 per-iteration environments | 2026-09-23`

#### Prompt

An application normally uses ES modules, but one legacy consumer requires a single property on an injected global-like object. Implement:

```js
const uninstall = installLegacyApi(root, api);
```

Contract:

- use the property name `frontendInterview`;
- reject installation when `root` already has its own property with that name;
- expose `api` through an explicit property write—never through an unresolved identifier;
- `uninstall()` deletes the property only if it still contains the exact installed `api`;
- return `true` only when cleanup deletes the property; otherwise return `false`;
- use `root`, not a hard-coded `window`, so the bridge is testable and host-neutral.

Explain why `delete root.frontendInterview` is appropriate here, why `delete` cannot remove a lexical binding, and why a normal module export remains the preferred production API.
