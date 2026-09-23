# Этап 0 завершён

Проведён web research, сформирован и нормализован Master Question Inventory.

- Никаких файлов, директорий или Git-репозитория не создано.
- Curriculum не проектировался.
- Учебные главы не писались.
- Итог: **510 нормализованных question groups**.
- Порядок ниже — только исследовательская taxonomy, а не будущая последовательность обучения.

## 1. Research methodology

Исследование выполнялось в пять проходов:

1. **Broad discovery** — крупные question banks, GitHub-репозитории и interview handbooks.
2. **Reality check** — официальные company guides и свежие candidate/interviewer reports.
3. **Domain deep dives** — отдельный поиск по TypeScript, accessibility, security, performance, browser internals, testing, tooling, system design и другим областям, которые хуже представлены в общих списках.
4. **2026 validation** — проверка устаревающих тем по официальным React, Next.js, TypeScript, W3C, MDN, OWASP и web.dev.
5. **Normalization**:
   - альтернативные формулировки объединялись;
   - самостоятельные underlying concepts сохранялись;
   - theoretical и implementation-варианты не сливались, если они проверяют разные навыки;
   - зеркала, переводы и явные копии считались одной source family.

Frequency — это частота **в независимых source families**, а не количество повторов в одном огромном репозитории:

- `F3` — встречается минимум в пяти независимых семьях источников;
- `F2` — встречается в двух–четырёх;
- `F1` — один достоверный источник либо gap, добавленный engineering analysis.

Уровень — основной ожидаемый уровень ответа, а не запрет спрашивать тему у других кандидатов:

- `J` — Junior/fundamental;
- `M` — Mid;
- `S` — Senior.

Типы:

- `C` — conceptual/API knowledge;
- `O` — output prediction;
- `I` — implementation/coding;
- `D` — debugging;
- `R` — code review/refactoring;
- `P` — performance;
- `A` — architecture/system design;
- `X` — practical scenario;
- `T` — trade-off discussion.

## 2. Масштаб корпуса

Я просмотрел или отфильтровал:

- **94 отдельных страницы, документов, репозитория и discussion threads**;
- **63 независимые source families** после удаления зеркал и производных материалов;
- крупные источники вместе заявляют **более 5,600 raw questions**, но это число нельзя честно считать уникальным: только один репозиторий заявляет 3,600+, JavaScript-банк — 1,000, real-experience collection — 568+, а GreatFrontEnd — 500+ ([3,600+ repository](https://github.com/sumitsingh4411/frontend-interview-questions), [1,000 JavaScript questions](https://github.com/sudheerj/javascript-interview-questions), [568 real questions](https://github.com/goswamikaushik/frontend-interview-mastery), [GreatFrontEnd 500+](https://www.greatfrontend.com/interviews/get-started)).
- Практически пригодная выборка составила приблизительно **2,350 явных prompts и alternate phrasings**.
- После normalization и gap analysis: **510 question groups**.

Это исследовательская выборка, а не полный scrape всех закрытых и динамических банков. Поэтому raw count — оценка, а 510 — проверяемое количество нормализованных групп ниже.

## 3. Типы исследованных источников

- Крупные open-source question banks и handbooks.
- Frontend-specific coding и machine-coding platforms.
- Официальные company interview guides.
- Реальные candidate reports 2024–2026.
- Материалы интервьюеров и engineering leads.
- Frontend System Design collections.
- Специализированные question banks: accessibility, security, CSS, testing, performance, Git, TypeScript.
- Официальные технические документы и release notes для проверки современности.
- Стандарты W3C, OWASP guidance и MDN/web.dev.

### Основные источники

**Общие question banks**

- [h5bp Front-end Developer Interview Questions](https://github.com/h5bp/front-end-developer-interview-questions)
- [Front End Interview Handbook 2026](https://github.com/yangshun/front-end-interview-handbook)
- [GreatFrontEnd question catalog](https://www.greatfrontend.com/interviews/get-started)
- [Sudheer JavaScript Interview Questions](https://github.com/sudheerj/javascript-interview-questions)
- [Sudheer React Interview Questions](https://github.com/sudheerj/reactjs-interview-questions/blob/master/README.md)
- [Frontend Interview Mastery — questions from reported interviews](https://github.com/goswamikaushik/frontend-interview-mastery)
- [Large multi-domain frontend question bank](https://github.com/sumitsingh4411/frontend-interview-questions)

**Coding и system design**

- [GreatFrontEnd JavaScript coding playbook](https://www.greatfrontend.com/front-end-interview-playbook/javascript)
- [GreatFrontEnd System Design Playbook](https://www.greatfrontend.com/front-end-system-design-playbook/introduction)
- [Machine Coding Round guide](https://www.greatfrontend.com/blog/machine-coding-round)
- [30 React machine-coding prompts](https://github.com/anuj-webdev/frontend-machine-coding-interview-questions-reactjs)
- [Frontend algorithm patterns](https://frontendinterviews.dev/frontend-algorithm-interview-questions)
- [Frontend system-design cases](https://github.com/goswamikaushik/frontend-interview-mastery/blob/main/real-interview-questions/system-design.md)

**Официальные company signals**

- [Amazon Front-End Engineer Interview Prep](https://www.amazon.jobs/content/en-gb/how-we-hire/fee-interview-prep)
- [Atlassian Engineering Interview Guide](https://www.atlassian.com/company/careers/resources/interviewing/engineering)
- [Atlassian Frontend Interview PDF](https://www.atlassian.com/dam/jcr%3Ac0aa929a-3391-4e9c-9202-3f3ba0eeb859/P30-P50-Frontend-Interview-Guide.pdf)
- [Canva hiring process](https://www.lifeatcanva.com/en/how-we-hire)
- [Stripe frontend team-screen guide](https://www.greatfrontend.com/static/guides/stripe-eng-team-screen-guide.pdf)
- [Stripe engineering hiring background](https://stripe.com/guides/atlas/scaling-eng)

Эти источники подтверждают, что реальные процессы комбинируют syntactically correct coding, тестирование, UI/component work, system design, accessibility, security, scalability и ясную коммуникацию — не только trivia или LeetCode.

**Свежие candidate/interviewer evidence**

- [Recent SDE-2 JavaScript questions](https://www.reddit.com/r/learnjavascript/comments/1vinp5g/10_javascript_questions_that_came_up_in_almost/)
- [Technical frontend assessments actually encountered](https://www.reddit.com/r/Frontend/comments/1g1gdfy/technical_frontend_interview_assessments_ive_faced/)
- [Real mid–senior React challenge](https://www.reddit.com/r/webdev/comments/1kq4i32/real_react_interview_for_midsenior_role/)
- [2025 senior frontend job-search report](https://www.reddit.com/r/cscareerquestions/comments/1p92cy3/2025_front_end_job_search_experience_offer/)
- [Senior frontend system-design difficulties](https://www.reddit.com/r/react/comments/1p1krkd/any_tips_on_senior_frontend_engineer_interview/)
- [Machine-coding reports](https://www.reddit.com/r/Frontend/comments/1mkwnrp/front_end_interview_machine_coding_round/)

**Accuracy и 2026 relevance**

- [React 19.3](https://react.dev/blog/2026/09/09/react-19-3)
- [React 19 Actions](https://react.dev/blog/2024/12/05/react-19)
- [React Compiler 1.0](https://react.dev/blog/2025/10/07/react-compiler-1)
- [Next.js 16](https://nextjs.org/blog/next-16)
- [Next.js Cache Components](https://nextjs.org/docs/app/getting-started/partial-prerendering)
- [TypeScript 6.0](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-6-0.html)
- [Current Core Web Vitals](https://web.dev/articles/vitals)
- [MDN Critical Rendering Path](https://developer.mozilla.org/en-US/docs/Web/Performance/Guides/Critical_rendering_path)
- [MDN CORS](https://developer.mozilla.org/en-US/docs/Web/HTTP/Guides/CORS)
- [WCAG 2.2](https://www.w3.org/TR/wcag/)
- [ARIA Authoring Practices](https://www.w3.org/WAI/ARIA/apg/)
- [Scott O’Hara’s accessibility interview questions](https://scottaohara.github.io/accessibility_interview_questions/)
- [OWASP XSS](https://cheatsheetseries.owasp.org/cheatsheets/Cross_Site_Scripting_Prevention_Cheat_Sheet.html), [CSRF](https://cheatsheetseries.owasp.org/cheatsheets/Cross-Site_Request_Forgery_Prevention_Cheat_Sheet.html) и [CSP](https://cheatsheetseries.owasp.org/cheatsheets/Content_Security_Policy_Cheat_Sheet.html)

## 4. Распределение

| Domain | Groups | % |
|---|---:|---:|
| JavaScript & async | 60 | 11.8% |
| TypeScript | 28 | 5.5% |
| React | 48 | 9.4% |
| Next.js | 20 | 3.9% |
| HTML, DOM & native forms | 25 | 4.9% |
| CSS | 28 | 5.5% |
| Accessibility | 20 | 3.9% |
| Browser internals & Web APIs | 25 | 4.9% |
| HTTP, API design & real-time | 27 | 5.3% |
| Performance | 24 | 4.7% |
| Security, auth & privacy | 20 | 3.9% |
| State, server data & forms | 18 | 3.5% |
| Testing | 18 | 3.5% |
| Git, packages, build & delivery | 24 | 4.7% |
| Architecture & design patterns | 25 | 4.9% |
| UI machine coding | 24 | 4.7% |
| Data structures & algorithms | 28 | 5.5% |
| Frontend System Design | 24 | 4.7% |
| Debugging, review & communication | 24 | 4.7% |
| **Total** | **510** | **100%** |

### Primary level

| Level | Groups | % |
|---|---:|---:|
| Junior/fundamental | 130 | 25.5% |
| Mid | 244 | 47.8% |
| Senior | 136 | 26.7% |

### Frequency

| Frequency | Groups | Meaning |
|---|---:|---|
| F3 | 146 | repeatedly present across ≥5 independent families |
| F2 | 242 | recurring across 2–4 families |
| F1 | 122 | narrower but credible, modern, or gap-added |
| **Total** | **510** | |

Question types overlap. Среди 510 групп: примерно 302 conceptual/API, 118 implementation, 96 debugging, 58 review/refactor, 71 performance-related, 95 architecture/system-design и 154 practical scenarios.

## 5. Основные выводы

1. **Fundamentals не становятся менее важными на Senior-уровне.** Closures, event loop, DOM events, CSS layout, HTTP и browser rendering регулярно используются как входная точка; seniority выявляется follow-up вопросами и trade-offs.

2. **Реально повторяются четыре технических формата:**
   - knowledge/output questions;
   - JavaScript или DSA coding;
   - UI machine coding;
   - frontend system design.

3. **Vanilla JavaScript и DOM нельзя заменить только React-подготовкой.** Официальные и candidate sources регулярно показывают DOM mutation, event handling, promises, data structures и небольшие framework-independent components.

4. **Mid → Senior differentiation — это diagnosis и judgment.** Профилирование, state ownership, failure handling, accessibility, security, deployment и migration важнее знания ещё одного hook.

5. **Frontend System Design не равен уменьшенному backend design.** Центральны rendering, client/server boundaries, state, API contracts, caching, offline/realtime behavior, accessibility, performance и resilience. Но отдельные компании всё равно могут расширять раунд до backend/API concerns.

6. **DSA остаётся реальным, но обычно полезнее practical subset:** arrays/strings, hash maps, trees, traversal, queues, intervals, caching, scheduling и complexity — вместо большого объёма редкого competitive programming.

7. **Популярные списки сильно недопредставляют** testing strategy, code review, debugging, observability, accessibility и production incidents.

8. **Старые React/Next материалы быстро портятся.** Актуальная база — React 19.3 и React Compiler; в Next.js 16 caching стал более явным и opt-in через Cache Components, поэтому старое описание «четырёх неизменных cache layers» нельзя безоговорочно преподавать как текущую модель ([React 19.3](https://react.dev/blog/2026/09/09/react-19-3), [Next.js 16](https://nextjs.org/blog/next-16)).

9. **AI-assisted coding — emerging format, а не универсальный стандарт.** Canva уже использует AI-assisted engineering interviews, но другие процессы по-прежнему требуют уверенно писать и отлаживать код без привычного IDE/AI окружения ([Canva process analysis](https://www.greatfrontend.com/interviews/company/canva/questions-guides), [Amazon FEE preparation](https://www.amazon.jobs/content/en-gb/how-we-hire/fee-interview-prep)).

## 6. Gap analysis

В inventory дополнительно внесены области, которые систематически терялись в generic lists:

- accessible name computation, focus restoration, live regions и реальные widget patterns;
- production debugging, heap snapshots, layout traces и source-map/telemetry workflow;
- flaky tests, visual regression, contract testing и тестирование accessibility;
- current React Actions, Compiler, `useEffectEvent`, Activity, View Transitions и Fragment refs;
- current Next.js Cache Components, `use cache`, deployment adapters и multi-instance invalidation;
- API idempotency, cancellation, race prevention, cursor pagination и retry storms;
- SSE vs WebSocket vs polling, reconnect, message ordering и offline reconciliation;
- package-manager resolution, peer dependencies, lockfiles и supply-chain concerns;
- design-system governance, monorepo/polyrepo и microfrontend failure isolation;
- internationalization, SEO, privacy-aware observability и multi-tenant concerns;
- code-review interviews и объяснение приоритетов замечаний;
- AI streaming UI и проверка AI-generated code.

Отдельные role-dependent спутники — React Native, Angular/Vue/Svelte depth, WebGL/WebRTC и глубокий Node/BFF — не развёрнуты в полноценные самостоятельные банки. Их разумно добавлять, когда определён target role.

# 7. Master Question Inventory

## A. JavaScript & async — 60

- JS-01 `[J/C/F3]` Сравните `var`, `let`, `const`: scope, redeclaration, initialization и assignment.
- JS-02 `[J/C/F3]` Объясните global, function, block, lexical и module scope.
- JS-03 `[J/C+O/F3]` Как работают hoisting и Temporal Dead Zone?
- JS-04 `[M/C+O/F2]` Что такое shadowing и illegal shadowing?
- JS-05 `[J/C/F3]` Primitive и object values: identity, mutation и reference sharing.
- JS-06 `[J/C+O/F3]` `typeof`, `null`, `undefined`, `Symbol`, `BigInt` и исторические oddities.
- JS-07 `[M/C+O/F2]` `NaN`, `Infinity`, `-0`, floating-point precision и безопасные сравнения.
- JS-08 `[J/C+O/F3]` Truthy/falsy, nullish values и defaulting.
- JS-09 `[J/C+O/F3]` `==`, `===`, `Object.is` и SameValueZero.
- JS-10 `[M/C+O/F3]` Implicit coercion, `ToPrimitive`, `valueOf` и `toString`.
- JS-11 `[J/C+O/F3]` Передаёт ли JavaScript значения или ссылки?
- JS-12 `[J/C+O/F3]` Function declaration, expression и named expression.
- JS-13 `[J/C+O/F3]` Arrow functions против regular functions.
- JS-14 `[J/C/F3]` First-class functions, callbacks и higher-order functions.
- JS-15 `[J/C+O+X/F3]` Closures: mental model, use cases, loop trap и retained memory.
- JS-16 `[M/C+O/F3]` Правила определения `this`.
- JS-17 `[M/C+I/F3]` `call`, `apply`, `bind` и preservation of context.
- JS-18 `[M/C+O/F2]` Что делает `new`; почему arrow function не constructor?
- JS-19 `[J/C+O/F2]` `arguments`, rest parameters, default parameters и arity.
- JS-20 `[M/C+I/F2]` Currying, partial application, composition и pipeline.
- JS-21 `[J/C+R/F2]` Pure functions, side effects и immutability.
- JS-22 `[M/C+O/F2]` Strict mode, accidental globals и `delete`.
- JS-23 `[J/C/F3]` Object literals, `Object.create`, constructors и factory functions.
- JS-24 `[M/C+O/F3]` Prototype, prototype chain, `__proto__` и lookup.
- JS-25 `[M/C+O/F3]` Classes, inheritance, `super`, static и private fields.
- JS-26 `[M/C+O/F2]` Own/inherited и enumerable/non-enumerable properties.
- JS-27 `[M/C+I/F2]` Property descriptors, getters и setters.
- JS-28 `[M/C/F2]` `freeze`, `seal`, `preventExtensions`: shallow guarantees.
- JS-29 `[J/C+R/F3]` Mutating и non-mutating array methods.
- JS-30 `[J/C+I/F3]` `map`, `filter`, `reduce`, `forEach`, `find`, `some`, `every`.
- JS-31 `[M/C+O/F2]` Sparse arrays, holes и copying behavior.
- JS-32 `[M/C+I+O/F3]` `sort`, comparator, stability и `toSorted`.
- JS-33 `[J/C+O/F3]` Destructuring, rest и spread.
- JS-34 `[M/C+I/F3]` Shallow copy, deep copy, cycles и `structuredClone`.
- JS-35 `[J/C+T/F3]` `Map` против plain object.
- JS-36 `[M/C+T/F2]` `Set`, `WeakMap`, `WeakSet`, `WeakRef`.
- JS-37 `[M/C/F2]` Symbols и well-known symbols.
- JS-38 `[M/C+I/F2]` Iterable protocol, iterators и generators.
- JS-39 `[S/C+I+T/F1]` Proxy и Reflect: interception и practical use cases.
- JS-40 `[J/C+O/F3]` Optional chaining, nullish coalescing и short-circuit evaluation.
- JS-41 `[M/C+T/F3]` ESM против CommonJS; CommonJS помечен как legacy/interoperability knowledge.
- JS-42 `[S/C+O/F2]` Live bindings, cyclic imports, dynamic import, top-level await и tree shaking.
- JS-43 `[J/C+I/F3]` `try/catch/finally`, throwing, custom errors и `cause`.
- JS-44 `[J/C+I/F2]` JSON serialization limitations и safe parsing.
- JS-45 `[M/C+D/F2]` Garbage collection, reachability и common memory leaks.
- JS-46 `[J/C+O/F3]` Event loop, call stack и host environment.
- JS-47 `[M/C+O/F3]` Tasks, microtasks и rendering opportunity.
- JS-48 `[M/O/F3]` Предскажите порядок `Promise`, `queueMicrotask`, timers и synchronous code.
- JS-49 `[M/C+D/F2]` Timer delay, clamping, drift и cleanup.
- JS-50 `[J/C+O/F3]` Promise states, chaining, thenables и assimilation.
- JS-51 `[M/C+O+D/F3]` Promise error propagation, `catch`, `finally`, unhandled rejection.
- JS-52 `[M/C+I/F3]` `all`, `allSettled`, `race`, `any`: semantics и selection.
- JS-53 `[M/C+O+I/F3]` `async/await`, sequencing, parallelism и error handling.
- JS-54 `[M/C+I/F2]` Cancellation через `AbortController`.
- JS-55 `[M/D+X/F3]` Race conditions и stale async responses.
- JS-56 `[M/C+I/F3]` Реализуйте debounce с leading/trailing/cancel.
- JS-57 `[M/C+I/F3]` Реализуйте throttle; сравните с debounce.
- JS-58 `[S/I+A/F2]` Concurrency limiter, task queue, retry/backoff/jitter.
- JS-59 `[M/I+R/F3]` Polyfills для array methods, `bind` и Promise combinators.
- JS-60 `[M/I+R/F3]` Utility family: deep clone, EventEmitter, memoize, flatten/groupBy/get/set.

## B. TypeScript — 28

- TS-01 `[J/C/F3]` Что TypeScript проверяет и что стирается runtime?
- TS-02 `[J/C+O/F3]` Type inference, widening, contextual typing и literal types.
- TS-03 `[J/C+T/F3]` `any`, `unknown`, `never`, `void`.
- TS-04 `[J/C/F3]` Union и intersection types.
- TS-05 `[M/C+I/F3]` Control-flow narrowing и built-in type guards.
- TS-06 `[M/C+I/F3]` Discriminated unions и exhaustive `never` checks.
- TS-07 `[J/C+T/F3]` `type` против `interface`.
- TS-08 `[J/C+R/F2]` Optional, readonly и index signatures.
- TS-09 `[M/C+T/F2]` Function overloads против union/generic signatures.
- TS-10 `[M/C+I/F3]` Generics и сохранение отношений между types.
- TS-11 `[M/C+I/F2]` Generic constraints, defaults и multiple parameters.
- TS-12 `[M/C+I/F3]` `keyof`, `typeof`, indexed access.
- TS-13 `[M/C+I/F2]` Mapped types и key remapping.
- TS-14 `[S/C+I/F2]` Conditional types, distributivity и `infer`.
- TS-15 `[S/C+I/F1]` Template-literal types.
- TS-16 `[M/C+I/F3]` Utility types и их самостоятельная реализация.
- TS-17 `[M/C+R/F2]` `satisfies` против annotation и assertion.
- TS-18 `[M/C+I/F2]` `as const` и const type parameters.
- TS-19 `[M/C+T/F2]` Classes, access modifiers, abstract, implements.
- TS-20 `[M/C+T/F2]` Enums против literal unions; `const enum` trade-offs.
- TS-21 `[S/C/F1]` Declaration merging, namespaces и ambient declarations.
- TS-22 `[S/C+D/F2]` ESM/CJS interoperability и module resolution.
- TS-23 `[M/C+R/F3]` `strict`, `noUncheckedIndexedAccess` и значимые compiler flags.
- TS-24 `[S/C/F1]` Variance, covariance, contravariance и bivariance.
- TS-25 `[S/I+A/F2]` Type-safe event emitter, reducer или API client.
- TS-26 `[M/I+R/F3]` Типизация React props, events, refs и generic components.
- TS-27 `[M/C+D/F2]` Почему API/JSON остаются `unknown`; runtime validation.
- TS-28 `[S/T+A/F1]` Schema-first types, generated types, compiler performance и TS 6→7 migration concerns.

## C. React — 48

React-specific современность сверялась с официальными React 19, 19.3 и Compiler release notes.

- RE-01 `[J/C/F3]` React elements, components и JSX transformation.
- RE-02 `[J/C/F3]` Props, state и one-way data flow.
- RE-03 `[M/C/F3]` Trigger → render → commit → browser paint.
- RE-04 `[M/C/F3]` Reconciliation и Fiber mental model.
- RE-05 `[J/C+O+D/F3]` Keys, identity и опасность array index.
- RE-06 `[J/C+O/F3]` State как snapshot и asynchronous-looking updates.
- RE-07 `[M/C+O+I/F3]` Batching, update queues и functional updater.
- RE-08 `[M/C+D/F3]` Preservation/reset of state через position, type и key.
- RE-09 `[J/C+T/F3]` Controlled и uncontrolled components.
- RE-10 `[J/C+R/F3]` Rules of Hooks и почему они существуют.
- RE-11 `[J/C+I/F3]` `useState`: initialization, updater и immutable changes.
- RE-12 `[M/C+I/F3]` `useReducer`: когда reducer полезнее state setters.
- RE-13 `[M/C+I/F3]` `useRef`: DOM, mutable values и render independence.
- RE-14 `[M/C+R/F3]` Effects как synchronization with external systems.
- RE-15 `[M/C+D/F3]` Dependencies, cleanup и async cleanup hazards.
- RE-16 `[M/D+R/F3]` Effect loops, duplicated derived state и “You Might Not Need an Effect”.
- RE-17 `[M/C+T/F2]` `useEffect`, `useLayoutEffect`, `useInsertionEffect`.
- RE-18 `[M/C+I/F3]` Custom hooks: API design и rules.
- RE-19 `[M/D+O/F3]` Stale closures; current `useEffectEvent` use case.
- RE-20 `[M/C+P+T/F3]` `memo`, `useMemo`, `useCallback`: когда они не помогают.
- RE-21 `[S/C+P+T/F2]` React Compiler и relationship с manual memoization.
- RE-22 `[M/C+P/F3]` Context propagation, value identity и provider splitting.
- RE-23 `[S/C+I/F2]` External stores и `useSyncExternalStore`.
- RE-24 `[M/C+I/F2]` Portals, stacking и event propagation.
- RE-25 `[J/C+O/F2]` Synthetic events и native events.
- RE-26 `[M/C+I/F2]` Refs, ref-as-prop, legacy `forwardRef`, imperative handles.
- RE-27 `[M/C+D/F3]` Error boundaries и что они не ловят.
- RE-28 `[M/C+A/F3]` Suspense boundaries и fallback architecture.
- RE-29 `[S/C+P/F2]` `startTransition`/`useTransition` и urgent updates.
- RE-30 `[M/C+P/F2]` `useDeferredValue`.
- RE-31 `[S/C/F2]` `use()` с Promise и Context.
- RE-32 `[M/C+I/F2]` Actions, `useActionState` и `useFormStatus`.
- RE-33 `[M/C+I+D/F2]` `useOptimistic`, rollback и reconciliation.
- RE-34 `[S/C+A+T/F2]` React Server Components и client boundaries.
- RE-35 `[M/C+D/F3]` Hydration и mismatch diagnosis.
- RE-36 `[S/C+A+P/F2]` Streaming SSR и selective hydration.
- RE-37 `[M/C+I+P/F3]` `lazy`, Suspense и code splitting.
- RE-38 `[S/C/F2]` Concurrent rendering, interruption и purity.
- RE-39 `[M/C+D/F3]` Strict Mode double invocation и impurity detection.
- RE-40 `[M/C/F2]` Class components и lifecycle methods — legacy interview knowledge.
- RE-41 `[M/C+T/F2]` HOCs, render props и compound components.
- RE-42 `[S/A+R/F3]` Reusable component API: composition, variants, controlled/uncontrolled.
- RE-43 `[M/A+R/F3]` State colocation, lifting и derived state.
- RE-44 `[M/C+A/F2]` Client routing, nested routes, loaders и route-level boundaries.
- RE-45 `[M/P+I/F3]` Large-list rendering и virtualization.
- RE-46 `[S/P+D/F3]` React Profiler и unnecessary-render diagnosis.
- RE-47 `[S/C+T/F1]` Activity, View Transitions и Fragment refs — emerging React 19.2/19.3.
- RE-48 `[S/R+D/F3]` Review React code for correctness, effects, a11y, performance и testability.

## D. Next.js — 20

Current модель сверялась с [Next.js 16](https://nextjs.org/blog/next-16) и [Cache Components](https://nextjs.org/docs/app/getting-started/partial-prerendering).

- NX-01 `[J/C+T/F3]` App Router против Pages Router; migration strategy.
- NX-02 `[J/C+I/F3]` Filesystem routes, layouts, templates и route groups.
- NX-03 `[M/C+I/F2]` Dynamic, catch-all, parallel и intercepted routes.
- NX-04 `[M/C+A/F3]` Server/Client Component boundary placement.
- NX-05 `[S/C/F2]` RSC payload, HTML и client hydration.
- NX-06 `[M/C+I/F3]` Data fetching внутри Server Components.
- NX-07 `[S/C+T/F2]` Next.js 16 runtime-by-default behavior и explicit caching.
- NX-08 `[S/C+I/F2]` `use cache`, `cacheLife`, `cacheTag`.
- NX-09 `[S/C+A+P/F2]` Cache Components и Partial Prerendering.
- NX-10 `[M/C+I+P/F3]` Suspense streaming и loading boundaries.
- NX-11 `[M/C+I+Security/F3]` Server Actions, validation и authorization.
- NX-12 `[M/C+I/F3]` Route Handlers против Server Actions и external API.
- NX-13 `[M/C+T/F2]` `proxy.ts`, legacy middleware и runtime boundary.
- NX-14 `[M/C+T/F3]` Static, dynamic и request-time rendering.
- NX-15 `[M/C+I/F3]` Revalidation, `updateTag` и stale-while-revalidate.
- NX-16 `[J/C+I/F2]` Metadata, SEO, social previews и dynamic metadata.
- NX-17 `[J/C+P/F2]` Image, font и script optimization.
- NX-18 `[M/C+A/F2]` Authentication, cookies, headers и protected routes.
- NX-19 `[S/A+D/F2]` Node/edge runtimes, adapters, multi-instance caches и deployment.
- NX-20 `[S/D+T/F1]` Turbopack, React Compiler, upgrades и production diagnostics.

## E. HTML, DOM & native forms — 25

- HD-01 `[J/C/F2]` Doctype, standards mode и browser error recovery.
- HD-02 `[J/C/F3]` Semantic elements и landmarks.
- HD-03 `[J/C/F2]` Inline, block, replaced и void elements.
- HD-04 `[J/C/F2]` `lang`, charset, viewport и important head metadata.
- HD-05 `[M/C+O+P/F3]` Classic, async, defer и module scripts.
- HD-06 `[M/C+P+T/F2]` Preload, prefetch, preconnect и fetch priority.
- HD-07 `[J/C+P/F2]` Responsive images: `picture`, `srcset`, `sizes`.
- HD-08 `[J/C+A11y/F3]` Context-sensitive `alt` и decorative images.
- HD-09 `[J/C+A11y/F1]` Accessible audio/video, captions и transcripts.
- HD-10 `[J/C+I/F3]` Native form submission и `FormData`.
- HD-11 `[J/C+I/F3]` Input types и Constraint Validation API.
- HD-12 `[J/C+A11y/F3]` Labels, names, autocomplete, fieldset и legend.
- HD-13 `[J/C+O/F3]` `button` types и default browser behavior.
- HD-14 `[J/C+A11y/F2]` Semantic tables, headers и captions.
- HD-15 `[M/C+T/F1]` SEO, structured data и document outline.
- HD-16 `[J/C/F3]` DOM tree, node types, NodeList и HTMLCollection.
- HD-17 `[J/C+I/F3]` Querying, traversal, creation и `DocumentFragment`.
- HD-18 `[M/C+I/F2]` `<template>`, cloning и declarative UI primitives.
- HD-19 `[J/C+O/F3]` Event capturing, target и bubbling.
- HD-20 `[M/C+I/F3]` Event delegation и dynamic children.
- HD-21 `[J/C+O/F3]` `preventDefault`, `stopPropagation`, `stopImmediatePropagation`.
- HD-22 `[M/C+I/F2]` Custom events и event contracts.
- HD-23 `[M/C+D/F2]` MutationObserver и DOM mutation diagnosis.
- HD-24 `[M/C+P/F2]` Passive/once/signal event listener options.
- HD-25 `[S/C+A+T/F2]` Custom Elements, Shadow DOM, slots и progressive enhancement.

## F. CSS — 28

CSS coverage подтверждался [GreatFrontEnd CSS bank](https://www.greatfrontend.com/questions/css-interview-questions) и scenario-oriented современным анализом layout/debugging.

- CSS-01 `[J/C+D/F3]` Cascade: origin, importance, layer, specificity, scope, order.
- CSS-02 `[J/C+O/F3]` Specificity calculation и `!important`.
- CSS-03 `[M/C+O/F2]` `:is`, `:where`, `:not`, `:has` и pseudo-elements.
- CSS-04 `[J/C+I/F3]` Box model и `box-sizing`.
- CSS-05 `[J/C/F3]` Normal flow и display types.
- CSS-06 `[M/C+D/F2]` Margin collapsing.
- CSS-07 `[M/C+D/F2]` Block formatting contexts и containment.
- CSS-08 `[J/C+D/F3]` Positioning и containing blocks.
- CSS-09 `[M/C+D/F3]` Stacking contexts и почему большой `z-index` не помогает.
- CSS-10 `[J/C+T/F3]` Absolute, relative, `%`, `em`, `rem`, viewport и dynamic units.
- CSS-11 `[M/C+D/F2]` Intrinsic sizing: min/max/fit-content.
- CSS-12 `[M/C+D/F2]` Overflow, scroll containers и clipping.
- CSS-13 `[J/C+I/F3]` Flex axes, grow, shrink и basis.
- CSS-14 `[M/C+D/F3]` Flex min-size, wrapping и alignment traps.
- CSS-15 `[J/C+I/F3]` Grid tracks, placement, `fr`, `minmax`, auto-fit/fill.
- CSS-16 `[M/C+I/F2]` Subgrid и nested layout.
- CSS-17 `[J/T+I/F3]` Flexbox против Grid.
- CSS-18 `[J/I+T/F3]` Способы centering и их assumptions.
- CSS-19 `[J/C+A/F3]` Mobile-first responsive design и media queries.
- CSS-20 `[M/C+A/F2]` Container queries.
- CSS-21 `[M/C+A11y/F2]` Logical properties, writing modes и RTL.
- CSS-22 `[M/C+A/F3]` Custom properties, design tokens и theming.
- CSS-23 `[M/C+P+A11y/F2]` Web fonts, fallback, FOIT/FOUT.
- CSS-24 `[J/C+I/F2]` `object-fit`, aspect ratio, backgrounds и responsive media.
- CSS-25 `[M/C+P/F3]` Transitions, keyframes, transforms и compositor-friendly properties.
- CSS-26 `[M/C+A11y/F2]` Reduced motion, forced colors и color scheme.
- CSS-27 `[S/T+A/F3]` BEM, CSS Modules, CSS-in-JS, utility CSS и cascade layers.
- CSS-28 `[S/D+P/F3]` Debug overflow/layout/stacking и distinguish layout/paint/composite costs.

## G. Accessibility — 20

- AX-01 `[J/C/F3]` Кто выигрывает от accessibility; POUR и WCAG levels.
- AX-02 `[J/C+R/F3]` Semantic HTML first; когда ARIA действительно нужна.
- AX-03 `[M/C+D/F3]` Accessibility tree и name/role/value/state.
- AX-04 `[J/C+X/F3]` Keyboard navigation, focus order и visible focus.
- AX-05 `[M/I+D/F3]` Modal focus trap, initial focus и restoration.
- AX-06 `[M/C+R/F3]` ARIA roles, states, properties и invalid ARIA.
- AX-07 `[M/C+T/F2]` Button, link, checkbox, switch и toggle button semantics.
- AX-08 `[M/C+X/F2]` Screen-reader testing и platform differences.
- AX-09 `[J/C+R/F3]` Alternative text для image, icon, SVG и chart.
- AX-10 `[J/C+I/F3]` Accessible form labels, instructions и errors.
- AX-11 `[J/C+R/F3]` Heading hierarchy, landmarks и skip links.
- AX-12 `[J/C+R/F3]` Contrast и почему одного цвета недостаточно.
- AX-13 `[M/C+D/F2]` Zoom, reflow, responsive text и text spacing.
- AX-14 `[M/C+R/F2]` Animation, flashing и `prefers-reduced-motion`.
- AX-15 `[M/C+I/F2]` Live regions и status/error announcements.
- AX-16 `[S/I+A/F2]` Accessible dialog, tabs, menu, combobox, tree и grid patterns.
- AX-17 `[M/C+X/F2]` Pointer targets, dragging alternatives и touch accessibility.
- AX-18 `[M/C+D/F3]` Automated audit против keyboard/screen-reader/manual testing.
- AX-19 `[S/A+X/F2]` Accessibility workflow, prioritization и regression prevention.
- AX-20 `[S/R+X/F2]` Review a custom component for semantic, keyboard, focus и announcement defects.

## H. Browser internals & Web APIs — 25

- BR-01 `[M/C/F2]` Browser processes, rendering process, compositor и sandbox.
- BR-02 `[J/C/F3]` HTML parsing и DOM construction.
- BR-03 `[M/C/F3]` CSSOM и render-tree construction.
- BR-04 `[M/C+P/F3]` Style, layout, paint и composite.
- BR-05 `[M/C+O/F3]` Execution contexts и call stack.
- BR-06 `[M/C+P/F3]` Event loop interaction with rendering и `requestAnimationFrame`.
- BR-07 `[S/C+T/F1]` `requestIdleCallback`, scheduler APIs и chunking work.
- BR-08 `[M/D+P/F3]` Forced synchronous layout и read/write batching.
- BR-09 `[M/D/F3]` Detached DOM nodes, listeners, timers и memory leaks.
- BR-10 `[J/C+T/F3]` Cookies, localStorage, sessionStorage, IndexedDB и Cache API.
- BR-11 `[S/C+T/F1]` Storage quota, eviction и partitioning.
- BR-12 `[M/C+I/F3]` Fetch, streams, body consumption и cancellation.
- BR-13 `[M/C+T/F3]` Web Workers, Shared Workers и transferable data.
- BR-14 `[M/C+A/F3]` Service Worker lifecycle и interception.
- BR-15 `[S/C+A/F2]` Cache-first, network-first, stale-while-revalidate и offline fallback.
- BR-16 `[M/C+A/F2]` PWA manifest, installation и update behavior.
- BR-17 `[M/C+I/F2]` History, location и SPA navigation.
- BR-18 `[M/C+I/F2]` Intersection, Resize, Mutation и Performance observers.
- BR-19 `[M/C+I+Security/F2]` `postMessage`, BroadcastChannel и multi-tab coordination.
- BR-20 `[M/C+I/F2]` Clipboard, File, drag-and-drop и object URLs.
- BR-21 `[M/C+T/F1]` Permissions, geolocation и notifications.
- BR-22 `[S/C+T/F1]` Canvas, SVG, WebGL и rendering choice.
- BR-23 `[S/C+T/F1]` WebAssembly boundary и suitable workloads.
- BR-24 `[S/C+D/P/F2]` Page Lifecycle, visibility и back/forward cache.
- BR-25 `[S/C+I/F2]` Streams, backpressure и incremental processing.

## I. HTTP, API design & real-time — 27

- NET-01 `[J/C/F3]` HTTP request/response, methods, safe и idempotent operations.
- NET-02 `[J/C+X/F3]` Status-code families и meaningful error handling.
- NET-03 `[J/C/F2]` Headers, MIME types и content negotiation.
- NET-04 `[M/C+T/F3]` HTTP/1.1, HTTP/2 и HTTP/3.
- NET-05 `[M/C/F3]` DNS, TCP, TLS и navigation request path.
- NET-06 `[J/C+T/F3]` Cookies, server sessions и bearer tokens.
- NET-07 `[M/C+P/F3]` Cache-Control, Expires, ETag и Last-Modified.
- NET-08 `[S/C+D/F2]` `Vary`, private/shared caches и invalidation bugs.
- NET-09 `[M/C+A+P/F3]` CDN и edge caching.
- NET-10 `[M/C+D+Security/F3]` CORS, preflight и credentialed requests.
- NET-11 `[M/C+A/F3]` REST resource modeling и HTTP semantics.
- NET-12 `[M/C+T/F3]` REST против GraphQL; over/under-fetching и cache implications.
- NET-13 `[S/C+A/F2]` RPC и Backend-for-Frontend.
- NET-14 `[M/C+D/F3]` Fetch errors, `Response.ok`, timeout и abort.
- NET-15 `[M/C+A/F3]` Offset против cursor pagination.
- NET-16 `[M/C+A/F2]` Sorting, filtering и search API contracts.
- NET-17 `[S/C+A/F2]` API versioning и backward compatibility.
- NET-18 `[M/C+A/F2]` Error envelopes, validation details и correlation IDs.
- NET-19 `[S/C+A/F2]` Idempotency keys и safe client retries.
- NET-20 `[M/C+I/F3]` Exponential backoff, jitter, rate limits и `Retry-After`.
- NET-21 `[M/C+A/F3]` Request deduplication, freshness и stale data.
- NET-22 `[M/C+D/F3]` Optimistic updates, conflicts и server reconciliation.
- NET-23 `[M/C+T/F3]` Polling, long polling, SSE и WebSocket selection.
- NET-24 `[S/C+A+D/F2]` WebSocket auth, heartbeat, reconnect, ordering и duplicates.
- NET-25 `[S/C+A/F2]` Streaming responses и incremental UI.
- NET-26 `[S/C+A+I/F2]` Multipart, chunked и resumable uploads.
- NET-27 `[S/A+X/F2]` Presence, delivery state и eventual consistency in realtime UI.

## J. Frontend performance — 24

Current metrics are LCP, INP и CLS, measured at the 75th percentile; FID is no longer a current Core Web Vital ([web.dev](https://web.dev/articles/vitals)).

- PF-01 `[M/C+P/F3]` Core Web Vitals: LCP, INP, CLS.
- PF-02 `[M/C+P/F3]` Lab против field data; Lighthouse, CrUX и RUM.
- PF-03 `[M/D+P/F3]` Diagnose a poor LCP.
- PF-04 `[S/D+P/F3]` Diagnose poor INP, long tasks и interaction phases.
- PF-05 `[M/D+P/F3]` Diagnose layout shifts.
- PF-06 `[M/C+P/F2]` TTFB, FCP, TBT и Long Tasks.
- PF-07 `[S/C+I/F2]` Performance APIs и production instrumentation.
- PF-08 `[M/D+P/F3]` Network waterfall, prioritization и preload misuse.
- PF-09 `[M/C+P/F3]` Critical CSS и render-blocking resources.
- PF-10 `[M/C+P/F3]` JavaScript download, parse, compile, execute и hydration cost.
- PF-11 `[M/I+P/F3]` Route/component code splitting и lazy loading.
- PF-12 `[M/C+P/F3]` Tree shaking, minification и compression.
- PF-13 `[M/C+P/F3]` Browser/CDN caching и immutable asset strategy.
- PF-14 `[M/C+P/F3]` Responsive images, formats и LCP image priority.
- PF-15 `[M/C+P/F2]` Font subsetting, preload и layout stability.
- PF-16 `[M/D+P/F3]` Layout, paint, compositing и layout thrashing.
- PF-17 `[M/C+P/F2]` Animation budgets и `requestAnimationFrame`.
- PF-18 `[S/D+P/F3]` React render/commit profiling.
- PF-19 `[M/I+P/F3]` Virtualization and incremental rendering.
- PF-20 `[S/C+P/F2]` Workers и cooperative scheduling.
- PF-21 `[S/D+P/F2]` Memory growth и long-lived SPA leaks.
- PF-22 `[S/A+P/F2]` Data waterfalls, parallel fetching и streaming.
- PF-23 `[S/A+P/F2]` SSR/RSC/hydration performance trade-offs.
- PF-24 `[S/A+P/F2]` Performance budgets, CI regression gates и third-party governance.

## K. Security, authentication & privacy — 20

- SEC-01 `[J/C/F3]` Origin против site; Same-Origin Policy.
- SEC-02 `[M/C+D/F3]` Почему CORS не authentication или authorization.
- SEC-03 `[M/C+X/F3]` Reflected, stored и DOM XSS.
- SEC-04 `[M/C+R/F3]` Contextual encoding, safe sinks и HTML sanitization.
- SEC-05 `[S/C+I/F2]` Trusted Types и dangerous DOM APIs.
- SEC-06 `[S/C+A/F3]` CSP, nonces, hashes и defense in depth.
- SEC-07 `[M/C+X/F3]` CSRF и automatic cookie sending.
- SEC-08 `[M/C+Security/F3]` Secure, HttpOnly, SameSite, Domain и Path.
- SEC-09 `[M/T+A/F3]` Token storage: memory, web storage и HttpOnly-cookie trade-offs.
- SEC-10 `[S/C+A/F2]` OAuth/OIDC authorization code + PKCE.
- SEC-11 `[J/C/F3]` Authentication против authorization.
- SEC-12 `[M/C+A/F3]` RBAC/permissions и server enforcement.
- SEC-13 `[M/C+X/F2]` Clickjacking и framing defenses.
- SEC-14 `[M/C+Security/F2]` Subresource Integrity и third-party scripts.
- SEC-15 `[M/C+R/F2]` Open redirects и unsafe URL schemes.
- SEC-16 `[M/C+R/F2]` Secure `postMessage` origin/source validation.
- SEC-17 `[S/C+D/F2]` Prototype pollution и unsafe object merging.
- SEC-18 `[S/C+A/F2]` Security headers: HSTS, Referrer/Permissions Policy, COOP/COEP/CORP.
- SEC-19 `[J/C+R/F3]` Почему client-side secrets и UI-only authorization не защищают данные.
- SEC-20 `[S/R+A/F1]` Secure file upload, telemetry privacy и RSC/Server Action trust boundaries.

## L. State, server data & forms — 18

- ST-01 `[M/C+A/F3]` Local UI, shared client, server, URL и form state.
- ST-02 `[M/A+R/F3]` Colocation, lifting, normalization и derived values.
- ST-03 `[M/T+A/F3]` Context против external store.
- ST-04 `[J/C/F3]` Redux flow и three principles.
- ST-05 `[M/C+I/F3]` Redux Toolkit slices, Immer, selectors и middleware.
- ST-06 `[M/T+A/F2]` Redux Toolkit, Zustand, Jotai, MobX и signals.
- ST-07 `[M/C+A/F3]` TanStack Query, SWR и RTK Query as server-state layers.
- ST-08 `[M/C+D/F3]` Query keys, freshness, invalidation, dedupe и refetch.
- ST-09 `[M/C+I+D/F3]` Optimistic mutation и rollback.
- ST-10 `[M/C+A/F2]` URL/query state как shareable source of truth.
- ST-11 `[S/C+A/F2]` Reducers и state machines for complex transitions.
- ST-12 `[M/C+A/F2]` Normalized entities и referential updates.
- ST-13 `[S/A+D/F2]` Persistence, hydration, version migration и cross-tab synchronization.
- ST-14 `[J/C+T/F3]` Controlled против uncontrolled forms.
- ST-15 `[M/C+A/F3]` Client/server validation и schema reuse.
- ST-16 `[M/T+A/F2]` React Hook Form, Formik, TanStack Form и native Actions.
- ST-17 `[S/A+P/F2]` Multi-step, dynamic и large-form architecture.
- ST-18 `[J/C+R/F3]` Loading, empty, error, partial и success states.

## M. Testing — 18

- TEST-01 `[J/C+T/F3]` Unit, component, integration и E2E boundaries.
- TEST-02 `[M/C+A/F3]` Testing pyramid/trophy и risk-based strategy.
- TEST-03 `[J/C+R/F3]` Observable behavior против implementation details.
- TEST-04 `[J/C+I/F3]` Jest/Vitest basics, spies, mocks и fake timers.
- TEST-05 `[M/I+R/F3]` Testing Library queries, `userEvent` и async UI.
- TEST-06 `[M/C+I/F3]` Network mocking with MSW.
- TEST-07 `[M/I+R/F2]` Testing hooks, context, router и shared stores.
- TEST-08 `[S/C+T/F1]` Testing RSC, Actions и framework integrations.
- TEST-09 `[M/T+A/F3]` Playwright против Cypress.
- TEST-10 `[M/I+R/F2]` Stable E2E selectors, fixtures и page objects.
- TEST-11 `[S/D+X/F3]` Diagnose flaky tests, leaked state и timing races.
- TEST-12 `[M/C+I/F2]` Visual regression testing.
- TEST-13 `[M/C+I/F3]` Automated accessibility testing и manual limits.
- TEST-14 `[S/C+I/F2]` Performance and Web Vitals testing.
- TEST-15 `[S/C+A/F2]` API contract и consumer-driven testing.
- TEST-16 `[M/T+R/F2]` Snapshot tests: useful boundaries и failure modes.
- TEST-17 `[M/C+T/F2]` Coverage metrics и mutation testing.
- TEST-18 `[S/A+D/F2]` CI sharding, retries, quarantine и test ownership.

## N. Git, packages, build tools & delivery — 24

- TOOL-01 `[J/C+I/F3]` Working tree, index/staging и commits.
- TOOL-02 `[J/C+T/F3]` Branching, merge и rebase.
- TOOL-03 `[J/C+X/F3]` Reset, revert и restore.
- TOOL-04 `[J/C+X/F2]` Stash и cherry-pick.
- TOOL-05 `[M/C+D/F2]` Reflog и recovery.
- TOOL-06 `[M/C+D/F2]` `git bisect` и regression localization.
- TOOL-07 `[M/T+A/F2]` Conflict resolution, PR history, trunk-based и GitFlow.
- TOOL-08 `[J/C/F3]` dependencies, devDependencies, peer и optional dependencies.
- TOOL-09 `[J/C+O/F3]` Semantic version ranges.
- TOOL-10 `[M/C+D/F3]` Lockfiles, deterministic installs и `npm ci`.
- TOOL-11 `[M/T/F2]` npm, Yarn и pnpm architecture.
- TOOL-12 `[M/C+D/F2]` Hoisting, phantom dependencies, PnP и pnpm links.
- TOOL-13 `[S/C+D/F2]` Package exports, conditions и ESM/CJS resolution.
- TOOL-14 `[M/C/F3]` Bundler dependency graph, loaders/transforms и plugins.
- TOOL-15 `[M/T+A/F3]` Webpack, Vite, Rspack, esbuild и Turbopack.
- TOOL-16 `[M/C+T/F3]` Babel, SWC и TypeScript compiler responsibilities.
- TOOL-17 `[M/C+D/F3]` Tree shaking, `sideEffects` и scope hoisting.
- TOOL-18 `[M/C+P/F3]` Chunking, dynamic import и shared/vendor code.
- TOOL-19 `[M/C+D/F2]` Hot Module Replacement.
- TOOL-20 `[M/C+D/F2]` Source maps и secure production debugging.
- TOOL-21 `[J/C+A/F3]` Linting, formatting, type checking и pre-commit gates.
- TOOL-22 `[S/T+A/F3]` Monorepo workspaces, task graphs и remote cache.
- TOOL-23 `[S/A+X/F2]` CI stages, artifact promotion и environment parity.
- TOOL-24 `[S/A+X/F2]` Feature flags, canary/blue-green rollout и rollback.

## O. Frontend architecture & design patterns — 25

- ARCH-01 `[J/C+R/F3]` Separation of concerns, cohesion и coupling.
- ARCH-02 `[M/A+T/F3]` Layer-, feature- и domain-oriented organization.
- ARCH-03 `[M/A+R/F3]` Component boundaries и public APIs.
- ARCH-04 `[S/A+T/F3]` Design-system layers: tokens → primitives → components → patterns.
- ARCH-05 `[M/A+T/F2]` Headless, styled и polymorphic components.
- ARCH-06 `[M/C+R/F2]` SOLID applied pragmatically to frontend.
- ARCH-07 `[J/C+T/F3]` DRY, KISS и YAGNI.
- ARCH-08 `[M/C+I/F3]` Observer/pub-sub pattern.
- ARCH-09 `[M/C+I/F2]` Strategy, factory, adapter и decorator.
- ARCH-10 `[M/C+I/F2]` Command, state и reducer patterns.
- ARCH-11 `[S/A+T/F2]` Dependency injection и service boundaries.
- ARCH-12 `[M/C+T/F2]` MVC, MVVM, Flux и unidirectional architecture.
- ARCH-13 `[S/A+T/F3]` Modular monolith против microfrontends.
- ARCH-14 `[S/A+T/F2]` Build-time, server-side и runtime MFE integration.
- ARCH-15 `[S/A+D/F2]` MFE routing, auth, shared state/dependencies и failure isolation.
- ARCH-16 `[S/A+T/F3]` Monorepo против polyrepo.
- ARCH-17 `[S/A+T/F2]` BFF и client/server responsibility boundary.
- ARCH-18 `[S/A+T/F3]` CSR, SSR, static, islands и RSC selection.
- ARCH-19 `[S/A+R/F3]` State and data-access architecture.
- ARCH-20 `[S/A+X/F3]` Error boundaries, retries и graceful degradation.
- ARCH-21 `[M/A+X/F2]` Internationalization, localization, RTL, dates и pluralization.
- ARCH-22 `[S/A+X/F2]` Multi-tenancy, roles и tenant configuration.
- ARCH-23 `[S/A+X/F2]` Feature flags, experimentation и configuration.
- ARCH-24 `[S/A+T/F2]` Legacy migration, strangler pattern и incremental modernization.
- ARCH-25 `[S/A+X/F2]` ADRs, RFCs, ownership, governance и cross-team contracts.

## P. UI machine coding — 24

Machine-coding sources consistently emphasise state modeling, component APIs, edge cases, accessibility, tests and communication—not только visual completeness.

- UI-01 `[J/I/F3]` Counter или todo list with clean state transitions.
- UI-02 `[J/I+A11y/F3]` Accordion.
- UI-03 `[J/I+A11y/F3]` Tabs with keyboard navigation.
- UI-04 `[M/I+A11y/F3]` Modal/dialog with focus management.
- UI-05 `[M/I+A11y/F2]` Tooltip или popover.
- UI-06 `[M/I+A11y/F3]` Dropdown/menu with outside click and keys.
- UI-07 `[M/I+D+P/F3]` Debounced autocomplete with cancellation and caching.
- UI-08 `[J/I+A11y/F3]` Star rating.
- UI-09 `[M/I+A11y/F3]` Carousel with autoplay and reduced-motion concerns.
- UI-10 `[M/I+P/F3]` Infinite scroll.
- UI-11 `[J/I/F3]` Pagination.
- UI-12 `[M/I+A+P/F3]` Sortable/filterable/paginated data table.
- UI-13 `[M/I+A/F3]` File explorer/tree view.
- UI-14 `[M/I+A/F2]` Nested comments.
- UI-15 `[M/I+A/F3]` Toast notification queue.
- UI-16 `[M/I+A11y/F2]` OTP input with paste/backspace behavior.
- UI-17 `[M/I+A/F3]` Multi-step form.
- UI-18 `[S/I+A/F2]` File upload with validation, progress, cancel и retry.
- UI-19 `[S/I+A/F2]` Kanban board and drag-and-drop.
- UI-20 `[S/I+A/F2]` Calendar/date picker.
- UI-21 `[M/I+A/F2]` Shopping cart/checkout.
- UI-22 `[S/I+A/F2]` Chat UI with pagination, delivery states и realtime updates.
- UI-23 `[J/I/F2]` Stopwatch, progress bars или traffic-light state machine.
- UI-24 `[M/I+R/F2]` Small game/grid/crossword task with progressive requirements.

## Q. Data structures & algorithms — 28

- DSA-01 `[J/C+I/F3]` Big-O time/space и input-constraint reasoning.
- DSA-02 `[J/I/F3]` Array/string transformation.
- DSA-03 `[J/C+I/F3]` Hash map и set selection.
- DSA-04 `[J/I/F3]` Frequency counter, deduplication и Two Sum family.
- DSA-05 `[M/I/F3]` Two pointers.
- DSA-06 `[M/I/F3]` Sliding window.
- DSA-07 `[M/I/F2]` Prefix sums.
- DSA-08 `[J/I/F3]` Sorting и custom comparators.
- DSA-09 `[M/I/F2]` Top-K and heap selection.
- DSA-10 `[M/I/F3]` Binary search and boundary variants.
- DSA-11 `[J/I/F3]` Stack and balanced delimiters.
- DSA-12 `[M/I/F2]` Monotonic stack.
- DSA-13 `[J/C+I/F2]` Queue/deque.
- DSA-14 `[M/I/F2]` Linked-list reversal, cycle и merge.
- DSA-15 `[M/I/F3]` Recursion и backtracking.
- DSA-16 `[M/I/F3]` Tree DFS/BFS.
- DSA-17 `[M/I/F2]` Graph traversal, cycle и connected components.
- DSA-18 `[M/I+X/F2]` Trie for autocomplete/prefix search.
- DSA-19 `[M/I/F2]` Priority queue и scheduling.
- DSA-20 `[M/I/F3]` Interval merge/overlap.
- DSA-21 `[M/I+A/F3]` LRU cache.
- DSA-22 `[M/I/F2]` Memoization и basic dynamic programming.
- DSA-23 `[S/I/F1]` Dependency graph/topological ordering.
- DSA-24 `[M/I+X/F3]` DOM/tree traversal without convenience selectors.
- DSA-25 `[M/I/F3]` Flatten nested arrays/objects.
- DSA-26 `[S/I/F2]` Deep clone as graph traversal with cycles.
- DSA-27 `[S/I+A/F2]` Task scheduler/concurrency queue.
- DSA-28 `[J/I+X/F3]` Explain brute force, optimization, tests и complexity aloud.

## R. Frontend System Design — 24

- SD-01 `[M/A+X/F3]` Clarify functional/non-functional requirements and scale.
- SD-02 `[M/A+T/F3]` Component-design round против application-design round.
- SD-03 `[M/A+P/F3]` Design autocomplete/typeahead.
- SD-04 `[M/A+P/F3]` Design feed/infinite scrolling.
- SD-05 `[S/A+P/F3]` Design large live data table/dashboard.
- SD-06 `[S/A+X/F3]` Design chat application.
- SD-07 `[M/A+X/F3]` Design notifications/toast system.
- SD-08 `[S/A+X/F3]` Design large/resumable file upload.
- SD-09 `[M/A+P/F2]` Design image gallery/Pinterest grid.
- SD-10 `[M/A+X/F2]` Design shopping cart and checkout frontend.
- SD-11 `[S/A+X/F2]` Design email client.
- SD-12 `[S/A+P/F2]` Design video player/streaming UI.
- SD-13 `[S/A+X/F3]` Design collaborative document editor.
- SD-14 `[S/A+P/F3]` Design Figma/Canva-like canvas editor.
- SD-15 `[S/A+X/F2]` Design browser code editor.
- SD-16 `[M/A+X/F2]` Design search results experience.
- SD-17 `[M/A+X/F2]` Design calendar/scheduling frontend.
- SD-18 `[S/A+X/F2]` Design multi-tenant admin SaaS.
- SD-19 `[S/A+X/F2]` Design offline-first PWA and sync.
- SD-20 `[S/A+T/F3]` Design organization-wide component library/design system.
- SD-21 `[S/A+T/F2]` Design microfrontend platform.
- SD-22 `[S/A+P/F2]` Design frontend monitoring/Web Vitals platform.
- SD-23 `[S/A+X/F2]` Design feature-flag and experimentation client.
- SD-24 `[S/A+X/F1]` Design streaming AI chat UI with partial output, cancellation, citations and tool states.

## S. Debugging, code review & interview communication — 24

- ENG-01 `[J/D+X/F3]` Reproduce, minimize, form hypothesis, test and verify.
- ENG-02 `[J/D/F3]` Use Elements, Console, Sources и Network panels.
- ENG-03 `[M/D+P/F3]` Read a Performance trace.
- ENG-04 `[M/D+P/F3]` Use React Profiler and render reasons.
- ENG-05 `[S/D/F2]` Heap snapshots, allocation profiles и leak confirmation.
- ENG-06 `[M/D+R/F3]` Diagnose stale closures, effect loops и state reset.
- ENG-07 `[M/D/F3]` Diagnose hydration mismatch.
- ENG-08 `[M/D/F3]` Diagnose CORS, caching и request race failures.
- ENG-09 `[M/D/F3]` Diagnose CSS overflow, containing block и stacking-context bugs.
- ENG-10 `[M/D+X/F3]` Abort stale requests and prevent out-of-order UI.
- ENG-11 `[S/A+D/F2]` Production telemetry: errors, Web Vitals, network, releases и trace IDs.
- ENG-12 `[S/D+X/F3]` Incident triage, mitigation, rollback и postmortem.
- ENG-13 `[M/R/F3]` Review correctness, edge cases и data flow.
- ENG-14 `[M/R/F3]` Review naming, API shape, maintainability и complexity.
- ENG-15 `[S/R/F3]` Prioritize security, accessibility, performance и test comments.
- ENG-16 `[S/R+T/F2]` Refactor legacy code incrementally without unsafe rewrite.
- ENG-17 `[M/D+X/F2]` Diagnose cross-browser/device-only failure.
- ENG-18 `[S/D+X/F2]` Diagnose flaky tests or non-reproducible customer issue.
- ENG-19 `[M/R+X/F2]` Give actionable, respectful PR feedback with severity.
- ENG-20 `[J/X/F3]` Explain a concept accurately in 30–60 seconds.
- ENG-21 `[J/X/F3]` Think aloud, clarify constraints и state assumptions.
- ENG-22 `[M/T+X/F3]` Present Options → Criteria → Trade-off → Decision.
- ENG-23 `[S/X/F3]` Explain ownership, impact, metrics, failure и lessons from a past project.
- ENG-24 `[S/R+X/F1]` Use AI in a coding round while independently verifying behavior, security, tests and generated assumptions.

## 8. Research limitations

- Frequency отражает публичные источники, а не внутреннюю статистику всех компаний.
- Несколько крупнейших банков имеют коммерческие или динамические разделы, поэтому raw totals нельзя воспроизвести полностью.
- Candidate reports дают ценный reality signal, но один рассказ не доказывает company-wide process.
- SEO-oriented “2026 question lists” использовались только как discovery layer; current technical claims проверялись по primary documentation.
- Framework-specific глубина зависит от вакансии. Inventory намеренно React-heavy, но фундаментальные web topics остаются framework-independent.
- F1 не означает «неважно»: туда входят современные, senior и production-oriented темы, которые редко попадают в generic lists.

На этом **Этап 0 остановлен**. Curriculum, repository skeleton и учебные материалы не создавались.

