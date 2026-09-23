# 1. JavaScript & Async Programming — Exercise Prompts

> Status: `partial draft — section 1.1 only; calibration review pending`
>
> Keep the [solution file](../../solutions/by-domain/01-javascript-and-async-programming.md) closed until after an attempt.
>
> Sections 1.2–1.12 remain placeholders.

## 1.1. Execution Model, Declarations & Scope

Progression: **recall → prediction → explanation → debugging → code review → implementation → integrated challenge**.

### JS-SCOPE-EX01

**Rebuild the declaration matrix**

- Status: `draft`
- Domain: `JavaScript & Async Programming`
- Difficulty: `Junior | recall`
- Skills tested: `terminology, declaration lifecycle, production guidance`
- Related inventory IDs: `JS-01`, `JS-03`
- Solution location: [JS-SCOPE-EX01](../../solutions/by-domain/01-javascript-and-async-programming.md#js-scope-ex01)

#### Task

Without looking at the handbook, draw a table for:

- `var`;
- `let`;
- `const`;
- function declaration;
- function expression stored in `var`;
- function expression stored in `const`.

For each row record:

1. scope;
2. binding state before the declaration line;
3. reassignment rule;
4. same-scope redeclaration rule;
5. one production or interview note.

Then define **declaration**, **initialization**, **assignment**, **TDZ** and **early error** in one sentence each.

#### Constraints

- Maximum time: 8 minutes.
- Do not write “moved to the top.”
- Mark uncertain cells rather than looking them up.

#### Evaluation Checklist

- [ ] All requested rows and columns are present.
- [ ] Every term has a one-sentence definition.
- [ ] Uncertain cells were marked before checking.
- [ ] Production guidance and interview/legacy notes are separated.

### JS-SCOPE-EX02

**Predict values, errors and failure phase**

- Status: `draft`
- Domain: `JavaScript & Async Programming`
- Difficulty: `Junior → Mid | prediction`
- Skills tested: `hoisting, TDZ, shadowing, error classification`
- Related inventory IDs: `JS-01`, `JS-03`, `JS-04`
- Solution location: [JS-SCOPE-EX02](../../solutions/by-domain/01-javascript-and-async-programming.md#js-scope-ex02)

#### Task

Treat A–F as independent scripts. Before running anything, record:

- exact output up to the first failure;
- `undefined`, value or error class;
- whether the failure is an early error or occurs during evaluation;
- the binding state at each read.

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

#### Constraints

- Do not execute until all six predictions are written.
- After execution, explain every mismatch using bindings rather than a memorized slogan.

#### Evaluation Checklist

- [ ] A prediction exists for all six independent snippets.
- [ ] Every failure includes an error class and phase.
- [ ] Every read is justified with a binding state.
- [ ] Post-run mismatches are explained rather than merely corrected.

### JS-SCOPE-EX03

**Trace identifier resolution**

- Status: `draft`
- Domain: `JavaScript & Async Programming`
- Difficulty: `Mid | explanation`
- Skills tested: `Environment Records, lexical lookup, call stack`
- Related inventory IDs: `JS-02`
- Solution location: [JS-SCOPE-EX03](../../solutions/by-domain/01-javascript-and-async-programming.md#js-scope-ex03)

#### Task

For each marked read, list the Environment Records checked in order and identify the winning binding.

```js
const label = "global";

function build(prefix) {
  const label = `${prefix}:build`;

  return function (enabled) {
    if (enabled) {
      const suffix = "!";
      return label + suffix; // read 1: label; read 2: suffix
    }

    return label; // read 3
  };
}

function invoke(callback) {
  const label = "invoke";
  return callback(true);
}

const report = build("scope");
console.log(invoke(report));
```

Also draw the call stack at the moment `report` evaluates `return label + suffix`.

#### Constraints

- Distinguish the active caller from the lexical outer environment.
- Do not claim the block creates another function-call frame.

#### Evaluation Checklist

- [ ] Lookup order is explicit for every marked read.
- [ ] Lexical-environment and call-stack drawings are separate.
- [ ] Definition site and call site are both considered.
- [ ] Final output is stated only after the trace.

### JS-SCOPE-EX04

**Two timed interview explanations**

- Status: `draft`
- Domain: `JavaScript & Async Programming`
- Difficulty: `Junior → Mid | communication`
- Skills tested: `active recall, terminology, concise explanation`
- Related inventory IDs: `JS-01`, `JS-02`, `JS-03`
- Solution location: [JS-SCOPE-EX04](../../solutions/by-domain/01-javascript-and-async-programming.md#js-scope-ex04)

#### Task

Record two answers:

1. **45 seconds:** compare `var`, `let` and `const`.
2. **60 seconds:** explain execution context, Environment Records, scope chain, hoisting and TDZ as one coherent model.

For each answer use:

```text
definition → mental model → one example → one trap or production rule
```

#### Constraints

- No notes during the first recording.
- Do not use “the engine moves code.”
- Do not spend time on event-loop scheduling or full closure use cases.

#### Evaluation Checklist

- [ ] Conceptual correctness.
- [ ] Correct terminology recalled without prompting.
- [ ] One concrete example.
- [ ] Clear scope boundary and no unrelated detour.
- [ ] Fits the time box.

### JS-SCOPE-EX05

**Debug environment-dependent globals**

- Status: `draft`
- Domain: `JavaScript & Async Programming`
- Difficulty: `Mid | debugging`
- Skills tested: `strict mode, accidental globals, global object, host assumptions`
- Related inventory IDs: `JS-02`, `JS-22`
- Solution location: [JS-SCOPE-EX05](../../solutions/by-domain/01-javascript-and-async-programming.md#js-scope-ex05)

#### Task

A legacy analytics file is loaded as a classic browser script:

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

Answer:

1. In sloppy mode, classify `lastEvent`, the function-local `count` and `globalThis.count` as bindings and/or properties with an explicit owner.
2. What changes after adding `"use strict"`?
3. What changes if the same source is loaded as an ES module?
4. Which state should be local, returned or explicitly owned?
5. Provide the smallest repair and then a cleaner API.
6. After the sloppy version runs, predict `delete globalThis.lastEvent`. Contrast it with strict source containing `delete lastEvent`, and explain why `delete` is not local-variable cleanup.

#### Constraints

- Label browser classic-script and browser-module claims.
- Do not rely on DevTools console experiments.
- Preserve the visible counting behavior in the minimal repair.

#### Evaluation Checklist

- [ ] All three requested names have an owner classification.
- [ ] Sloppy, strict and module cases are addressed separately.
- [ ] Both repairs preserve or document observable behavior.
- [ ] The two deletion forms are analyzed by target and failure phase.

### JS-SCOPE-EX06

**Repair declaration conflicts**

- Status: `draft`
- Domain: `JavaScript & Async Programming`
- Difficulty: `Mid | debugging`
- Skills tested: `redeclaration, illegal shadowing, switch scope, early errors`
- Related inventory IDs: `JS-01`, `JS-04`
- Solution location: [JS-SCOPE-EX06](../../solutions/by-domain/01-javascript-and-async-programming.md#js-scope-ex06)

#### Task

Find every parse/declaration defect and repair it with the smallest scope change:

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

Then state whether any call to `format` can occur before the repair.

#### Constraints

- Preserve all intended return strings.
- Do not replace the entire function with a lookup table; this task is about scope.
- Explain why control-flow exclusivity does not remove declaration conflicts.

#### Evaluation Checklist

- [ ] Every declaration conflict is identified.
- [ ] Each change is minimal and justified.
- [ ] All intended return strings are preserved.
- [ ] The failure phase is explained.

### JS-SCOPE-EX07

**Scope-focused code review**

- Status: `draft`
- Domain: `JavaScript & Async Programming`
- Difficulty: `Mid → Senior | code review`
- Skills tested: `correctness, severity, global ownership, incremental refactor`
- Related inventory IDs: `JS-01`, `JS-02`, `JS-03`, `JS-22`
- Solution location: [JS-SCOPE-EX07](../../solutions/by-domain/01-javascript-and-async-programming.md#js-scope-ex07)

#### Task

Review this classic-script integration:

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

Produce:

1. severity-ranked review comments;
2. predicted behavior after `install` returns;
3. a minimal compatibility-preserving patch;
4. a module-oriented target design;
5. tests you would add before migrating the legacy integration.

#### Constraints

- Separate correctness defects from style preferences.
- State whether `active` is intentionally shared or merely global by accident; if unknown, ask for the contract.
- Avoid an unrelated rewrite.

#### Evaluation Checklist

- [ ] Comments are ranked by severity and category.
- [ ] Correctness, ownership and maintainability are all reviewed.
- [ ] Minimal patch and target design are separated.
- [ ] Tests cover both behavior and execution environment.

### JS-SCOPE-EX08

**Implement stable per-index callbacks**

- Status: `draft`
- Domain: `JavaScript & Async Programming`
- Difficulty: `Mid | implementation`
- Skills tested: `per-iteration bindings, declaration choice, testing`
- Related inventory IDs: `JS-01`, `JS-02`
- Solution location: [JS-SCOPE-EX08](../../solutions/by-domain/01-javascript-and-async-programming.md#js-scope-ex08)

#### Task

Implement:

```js
function createReaders(values) {
  // return one zero-argument function per item
}
```

Contract:

```js
const values = ["a", "b", "c"];
const readers = createReaders(values);

readers[0](); // { index: 0, value: "a" }
readers[2](); // { index: 2, value: "c" }
```

Choose and document one of these semantics:

- **live:** a reader observes a later replacement at `values[index]`;
- **snapshot:** a reader preserves the value present during creation.

#### Constraints

- Use a loop.
- No IIFE, `bind`, mutable global or array iteration helper.
- Use modern declarations.
- Add tests for empty input, three items and the chosen live/snapshot behavior.
- Explain the per-iteration binding.

#### Evaluation Checklist

- [ ] All contract examples and edge cases are tested.
- [ ] Live versus snapshot behavior is explicit.
- [ ] Declaration choices are justified.
- [ ] Time and space complexity are stated.

### JS-SCOPE-EX09

**Interview Challenge — scope migration packet**

- Status: `draft`
- Domain: `JavaScript & Async Programming`
- Difficulty: `Senior | integrated challenge`
- Skills tested: `prediction, environment labeling, debugging, review, implementation, communication`
- Related inventory IDs: `JS-01`, `JS-02`, `JS-03`, `JS-04`, `JS-22`
- Solution location: [JS-SCOPE-EX09](../../solutions/by-domain/01-javascript-and-async-programming.md#js-scope-ex09)

#### Task

A page is being migrated from classic scripts to modules.

```html
<script src="bootstrap.js"></script>
<script src="widget.js"></script>
<script type="module" src="app.js"></script>
```

```js
// bootstrap.js — classic script, sloppy mode
var mode = "legacy";
sharedCount = 0;
```

```js
// widget.js — classic script
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
// app.js — ES module
var mode = "module";

export function start(nodes) {
  sharedCount += 1;
  return makeHandlers(nodes);
}
```

Without executing it:

1. Determine whether each file completes declaration instantiation and evaluation.
2. List every output/error in actual order.
3. Identify which names are bindings, which are global-object properties and which are unavailable across the module boundary.
4. Find every correctness and ownership defect.
5. Design a minimal repair while retaining the three-file loading arrangement.
6. Design the cleaner all-module target.
7. Give a three-minute interview explanation of your reasoning.

#### Constraints

- State assumptions about a clean browser realm and normal external-script ordering.
- Do not add properties to `globalThis` in the all-module target.
- Keep functions/closure discussion limited to the scope consequences required here.
- Rank defects rather than listing them without severity.

#### Evaluation Checklist

- [ ] All three files are analyzed in load order.
- [ ] Outputs and failures are ordered and assigned a phase.
- [ ] Bindings, properties and cross-file visibility are classified.
- [ ] Defects are ranked rather than merely listed.
- [ ] Minimal repair and target architecture are separated.
- [ ] The explanation uses binding/environment terminology and stays within scope.
