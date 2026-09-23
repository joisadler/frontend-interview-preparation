# Этап 1 завершён — Curriculum

Сформирован curriculum, покрывающий все **510 question groups** утверждённого Master Question Inventory.

- Основная структура: **19 domains → sections → topics → subtopics**.
- Порядок внутри доменов: **Fundamentals → Professional/Mid → Advanced/Senior**.
- Современная база: React 19.3, Next.js 16 и TypeScript 6.
- Legacy-знания явно отделены от рекомендуемых production-подходов.
- Репозиторий, директории и файлы не создавались.

## Как читать curriculum

У материала будут четыре уровня глубины:

- **Core** — необходимо уверенно объяснять, писать и отлаживать.
- **Professional** — практические сценарии, trade-offs и production behavior.
- **Advanced** — architecture, performance, reliability и Senior-level judgment.
- **Survey / Legacy** — понимать назначение и ограничения, но не изучать внутренности непропорционально interview value.

DSA, UI coding и устные объяснения должны практиковаться параллельно основным доменам, а не только после завершения теории.

---

# 1. JavaScript & Async Programming

## 1.1. Execution Model, Declarations & Scope

- ECMAScript и host environment: browser/Node responsibilities.
- Execution contexts, call stack, lexical environments и scope chain.
- Global, function, block, lexical и module scope.
- `var`, `let`, `const`: declaration, initialization, assignment, redeclaration.
- Hoisting и TDZ; почему модель «код перемещается вверх» неточна.
- Shadowing и illegal shadowing.
- Strict mode, accidental globals и `delete`.

## 1.2. Values, Types, Equality & Coercion

- Primitive и object values; identity, mutation и shared references.
- Pass-by-value и передача object reference как значения.
- `typeof`, `null`, `undefined`, `Symbol`, `BigInt`.
- `NaN`, `Infinity`, `-0`, floating-point precision.
- Truthy/falsy и nullish values.
- `||`, `??`, optional chaining и short-circuiting.
- `==`, `===`, `Object.is`, SameValueZero.
- Explicit и implicit coercion; `ToPrimitive`, `valueOf`, `toString`.
- Output-prediction задачи на conversion и equality.

## 1.3. Functions, Closures & Functional Patterns

- Function declarations, expressions, named expressions и arrows.
- First-class и higher-order functions; callbacks.
- Parameters: default, rest, destructuring, `arguments`, arity.
- Closures: lexical capture, factories, encapsulation и memoization.
- Loop closure trap и удержание памяти.
- Pure functions, side effects и practical immutability.
- Currying, partial application, composition и pipelines.

## 1.4. `this`, Invocation & Object Model

- Default, implicit, explicit и constructor binding.
- Lost method context и lexical `this` в arrow functions.
- `call`, `apply`, `bind`.
- Пошаговая модель `new`.
- Object literals, factories, constructor functions и `Object.create`.
- Prototype, prototype chain, lookup и shadowing.
- `__proto__` как legacy accessor.
- Classes, inheritance, `super`, static и private fields.
- Own/inherited и enumerable/non-enumerable properties.
- Descriptors, getters и setters.
- `freeze`, `seal`, `preventExtensions`.
- Proxy/Reflect — survey depth.

## 1.5. Arrays, Transformations & Copying

- Dense и sparse arrays; holes против `undefined`.
- Mutating APIs: `push`, `splice`, `sort`, `reverse`.
- Non-mutating и copying APIs: `slice`, `concat`, `toSorted`, `toSpliced`, `toReversed`, `with`.
- `map`, `filter`, `reduce`, `forEach`, `find`, `some`, `every`.
- Comparator correctness, sort stability и multi-field sorting.
- Destructuring, rest и spread.
- Shallow copy, structural sharing и deep copy.
- `structuredClone`, cycles, transferables и limitations.
- JSON round-trip как недостаточный deep-clone mechanism.

## 1.6. Collections, Symbols & Iteration

- `Map` против object: keys, iteration, size и serialization.
- `Set` и deduplication.
- `WeakMap`, `WeakSet`, `WeakRef` и weak reachability.
- Symbols и well-known symbols.
- Iterable и iterator protocols.
- Custom iterables и generators.
- Async iterables как мост к streaming.

## 1.7. Modules, Errors & Serialization

- ESM imports/exports, module scope и static graph.
- Live bindings, cyclic imports, dynamic import и top-level await.
- Tree-shaking relationship.
- CommonJS — **legacy/interoperability knowledge**.
- ESM/CJS interop и dual-package issues.
- `try/catch/finally`, custom errors и `cause`.
- Error propagation и сохранение контекста.
- JSON limitations, replacer/reviver и schema validation.

## 1.8. Memory Management

- Reachability, roots и nondeterministic garbage collection.
- Closures и retained object graphs.
- Detached DOM, listeners, timers, subscriptions и caches.
- Object URL cleanup.
- Memory peak против настоящей утечки.
- Heap investigation как cross-reference к debugging.

## 1.9. Event Loop & Scheduling

- Call stack, host APIs и run-to-completion.
- Tasks, microtasks и rendering opportunity.
- Promise reactions, `queueMicrotask` и timers.
- Microtask draining и starvation.
- Output-prediction: sync → Promise → microtask → timer.
- Timer clamping, background throttling и drift.
- `requestAnimationFrame` и browser rendering schedule.

## 1.10. Promises & `async`/`await`

- Promise states, settlement и chaining.
- Returned-value flattening и thenable assimilation.
- Error propagation, `catch`, `finally`, unhandled rejection.
- `all`, `allSettled`, `race`, `any`.
- Sequential и parallel `await`.
- Accidental async waterfalls.
- Cancellation через `AbortController`.
- Race conditions, stale responses и latest-request-wins.

## 1.11. Async Coordination Patterns

- Debounce: leading, trailing, cancel и flush.
- Throttle и его отличие от debounce.
- Concurrency limiter и task queue.
- Retry eligibility, exponential backoff и jitter.
- Cancellation propagation.
- Result ordering, partial failure и retry storms.

## 1.12. JavaScript Implementation Practice

- Polyfills для `map`, `filter`, `reduce`, `bind`.
- Promise combinators.
- EventEmitter с корректной subscription lifecycle.
- Memoization и cache-key strategy.
- Flatten, groupBy, nested get/set.
- Deep clone с cycles и заранее оговорённым contract.
- Complexity, edge cases и самостоятельное тестирование.

---

# 2. TypeScript

## 2.1. Type-System Mental Model

- Static analysis против runtime behavior.
- Type erasure и intentionally unsound boundaries.
- Structural typing.
- Inference, contextual typing и widening.
- Literal types и preservation.
- `any`, `unknown`, `never`, `void`.

## 2.2. Object & Algebraic Types

- Union и intersection types.
- `type` против `interface`.
- Extension, intersection и declaration merging.
- Optional и readonly properties.
- Index signatures и `Record`.
- Tuple и literal-union modeling.

## 2.3. Narrowing & Exhaustiveness

- `typeof`, `instanceof`, `in` и equality narrowing.
- User-defined predicates и assertion functions.
- Discriminated unions.
- Exhaustive `switch` и `never` checks.
- Modeling states instead of incompatible boolean combinations.

## 2.4. Function Types & Generics

- Function signatures, callbacks и rest parameters.
- Overloads против unions и generics.
- Generic relationships между input и output.
- Constraints, defaults и dependent parameters.
- Avoiding useless or over-general generic parameters.

## 2.5. Type Transformations

- `keyof`, type-position `typeof`, indexed access.
- Mapped types и key remapping.
- Conditional types и distributivity.
- `infer`.
- Template-literal types — survey depth.
- Utility types и самостоятельная реализация representative utilities.
- `satisfies`, assertions и annotations.
- `as const` и const type parameters.

## 2.6. Classes, Enums & Legacy Constructs

- Access modifiers, abstract classes и `implements`.
- ECMAScript private fields против TypeScript `private`.
- Enums, literal unions и `as const` objects.
- `const enum` toolchain trade-offs.
- Namespaces и ambient declarations — преимущественно legacy/library knowledge.
- `.d.ts` и declaration merging.

## 2.7. Modules & Compiler Configuration

- ESM/CJS interop и module resolution.
- Package exports и type-only imports.
- `strict`, `strictNullChecks`, `noUncheckedIndexedAccess`.
- `exactOptionalPropertyTypes` и другие meaningful flags.
- Project references и incremental builds.
- Compiler-performance hotspots.
- TypeScript 6→7 migration concerns — перепроверять по актуальным release notes во время написания главы.

## 2.8. Sound Boundaries & Practical Type Design

- Variance, covariance, contravariance и bivariance — senior survey.
- API/JSON/storage data как `unknown`.
- Runtime schemas и generated types.
- Typed EventEmitter, reducer и API client.
- React props, events, refs и generic components.
- Discriminated component props.
- Readability и caller experience важнее type-level cleverness.

---

# 3. React

## 3.1. Component & Rendering Model

- Elements, components, DOM nodes и JSX transformation.
- Props, state, composition и one-way data flow.
- Render purity.
- Trigger → render → commit → browser paint.
- Reconciliation и Fiber mental model без низкоценной internal-field trivia.

## 3.2. Identity & State Updates

- Keys, sibling identity и проблемы array indexes.
- Position/type/key и preservation/reset of state.
- State as a snapshot.
- Update queues и batching.
- Replacement updates против functional updaters.
- Controlled и uncontrolled components.

## 3.3. Core Hooks

- Rules of Hooks и stable call order.
- `useState`: lazy initialization и immutable updates.
- `useReducer`: actions, transition modeling и reducer purity.
- `useRef`: DOM, mutable handles и render-independent values.
- Custom hooks: lifecycle ownership, inputs, outputs и cleanup.

## 3.4. Effects & Synchronization

- Effects как synchronization with external systems.
- Dependencies и exhaustive-deps reasoning.
- Cleanup before rerun и on unmount.
- Async cleanup, abort и subscription leaks.
- `useEffect`, `useLayoutEffect`, `useInsertionEffect`.
- Stale closures и подходящие решения.
- `useEffectEvent` для non-reactive effect logic.
- “You Might Not Need an Effect”.
- Effect loops и duplicated derived state.
- Strict Mode diagnostics.

## 3.5. DOM Integration & Escape Hatches

- Synthetic против native events.
- Portals: logical tree, physical DOM, event propagation.
- Focus, scroll locking и stacking contexts.
- Ref as prop в современном React.
- `useImperativeHandle`.
- `forwardRef` — **legacy/migration knowledge**.
- Error boundaries и ограничения того, что они ловят.

## 3.6. Context & External Stores

- Context lookup и propagation.
- Provider value identity и splitting.
- Context как dependency mechanism, а не автоматический global store.
- `useSyncExternalStore`.
- Snapshot stability, subscriptions, selectors и tearing.
- SSR snapshots.

## 3.7. Performance & React Compiler

- Render cost против commit cost.
- `memo`, `useMemo`, `useCallback`.
- Когда memoization ничего не улучшает.
- React Compiler и automatic memoization.
- Rules of React как prerequisite для compiler.
- Incremental compiler adoption.
- React Profiler и render-reason diagnosis.
- Large-list virtualization, overscan и accessibility trade-offs.

## 3.8. Suspense & Concurrent Rendering

- Suspense boundaries, fallback и reveal.
- Boundary placement и nested skeletons.
- `startTransition`, `useTransition`.
- `useDeferredValue`.
- `use()` с Promise и Context.
- Interruptible render и atomic commit.
- Purity и external-store consistency.
- Concurrent rendering не означает parallel JavaScript execution.

## 3.9. Actions & Optimistic UI

- Actions и progressive enhancement.
- `useActionState`.
- `useFormStatus`.
- Validation/error presentation.
- `useOptimistic`.
- Pending identity, rollback и server reconciliation.
- Duplicate submissions и out-of-order responses.

## 3.10. Server Rendering & Server Components

- React Server Components и Client Component boundary.
- RSC payload и serializable props.
- Secret/data-access boundaries.
- SSR, hydration и deterministic first render.
- Hydration mismatch diagnosis.
- Streaming SSR и selective hydration.
- Lazy loading и route/component code splitting.

## 3.11. Composition & Application APIs

- State colocation, lifting и derived state.
- Component API design: variants, composition, controlled/uncontrolled.
- Compound components и headless APIs.
- HOCs и render props — **legacy/interview knowledge**.
- Client routing, nested routes, loaders и route-level boundaries.

## 3.12. Legacy & Emerging React

- Class components, lifecycle methods и incremental migration.
- Activity.
- View Transitions.
- Fragment refs.
- Browser-only suspension и Trusted Types integration — current-awareness depth.
- Stable/canary/experimental channels.
- RSC security-patch discipline.

## 3.13. React Review & Debugging

- Stale closures и effect loops.
- State unexpectedly reset/preserved.
- Wrong row state because of keys.
- Controlled/uncontrolled warnings.
- Context-driven render storms.
- Suspense fallback flashing.
- Hydration mismatch.
- Review correctness, effects, accessibility, performance и testability.

---

# 4. Next.js

## 4.1. Router Foundations

- App Router как current baseline.
- Pages Router — **legacy/migration knowledge**.
- `page`, `layout`, `template`, `loading`, `error`, `not-found`.
- Route groups и private folders.
- Dynamic, catch-all и optional catch-all routes.
- Parallel и intercepted routes.
- Promised `params`/`searchParams` и current asynchronous request APIs.

## 4.2. Server & Client Components

- Server Components by default.
- `'use client'` как module-graph boundary.
- Boundary placement и interactive islands.
- RSC payload, initial HTML и hydration.
- Serializable props.
- Server-only/client-only modules.
- Accidental client-bundle expansion.

## 4.3. Data Fetching & Rendering Modes

- Fetch/database/service calls в Server Components.
- Parallel fetching и waterfall prevention.
- Static, dynamic и request-time rendering.
- Request-bound APIs.
- Static params.
- CSR/SSR/RSC consequences для SEO, caching и interactivity.

## 4.4. Next.js 16 Caching

- Runtime work by default и explicit caching.
- Request memoization против persistent cache.
- `use cache`, cache keys и user-data isolation.
- `cacheLife`, `cacheTag`.
- Cache Components и Partial Prerendering.
- Suspense как dynamic boundary.
- Revalidation и `updateTag`.
- Path/tag invalidation.
- Multi-layer stale-cache diagnosis.

## 4.5. Streaming & Navigation

- `loading.tsx` и nested Suspense.
- Static shell и streamed regions.
- Route prefetching.
- Client navigation и route cache.
- Scroll restoration.
- Chunk failures после новой deployment version.

## 4.6. Mutations & Backend Boundaries

- Server Actions и `'use server'`.
- Input validation, authentication и authorization.
- Pending/error/optimistic states.
- Route Handlers.
- Server Action против Route Handler против external service.
- HTTP methods, status codes, streaming и webhooks.
- Cache invalidation after mutation.

## 4.7. Auth, Proxy & Deployment

- `proxy.ts` как current request-interception API.
- `middleware.ts` — legacy terminology/runtime knowledge.
- Cookies, headers и secure route protection.
- UI redirects против настоящего server authorization.
- Node и edge-like runtimes.
- Adapters, self-hosting и multi-instance caches.
- Environment variables: build-time против runtime.

## 4.8. Metadata & Asset Optimization

- Static и dynamic metadata.
- Canonical URLs, robots, sitemap и social previews.
- Images, responsive sizing и LCP priority.
- Font optimization и layout stability.
- Script loading и third-party governance.

## 4.9. Tooling, Upgrade & Diagnosis

- Turbopack как current default pipeline.
- React Compiler integration.
- Codemods с обязательным review.
- Pages→App Router migration.
- RSC boundary failures.
- Stale caches и cross-user cache leakage.
- Logs, tracing, source maps и rollback.

---

# 5. HTML, DOM & Native Forms

## 5.1. Document Foundations

- Doctype, standards/quirks mode и parser recovery.
- Semantic structure и landmarks.
- Element categories, replaced и void elements.
- Attributes против DOM properties.
- `lang`, charset, viewport и document metadata.

## 5.2. Resource Loading, Media & SEO

- Classic, `async`, `defer` и module scripts.
- Preload, prefetch, preconnect и fetch priority.
- Responsive images: `picture`, `srcset`, `sizes`.
- Context-sensitive alternative text.
- Accessible audio/video, captions и transcripts.
- Structured data и crawlable content.

## 5.3. Native Forms

- Native submission, successful controls и `FormData`.
- Input types и Constraint Validation API.
- Labels, names, descriptions и errors.
- `autocomplete`, `fieldset`, `legend`.
- Button types и accidental submission.
- Client validation как UX, не security boundary.

## 5.4. Semantic Tables

- Caption, header cells и `scope`.
- Complex relationships.
- Responsive presentation без уничтожения table semantics.

## 5.5. DOM Model & Mutation

- Node types и tree relationships.
- NodeList против HTMLCollection; live против static.
- Querying, traversal, creation и removal.
- Safe text updates против HTML parsing.
- `DocumentFragment`.
- `<template>` и cloning.
- Native `dialog`, Popover и `inert` как progressive primitives.

## 5.6. DOM Events

- Capture → target → bubble.
- `target` против `currentTarget`.
- Delegation и dynamic children.
- `preventDefault`, propagation controls.
- Custom events и stable event contracts.
- MutationObserver.
- Listener options: passive, once, capture, signal.

## 5.7. Web Components

- Custom Elements lifecycle.
- Attributes против properties.
- Shadow DOM, slots и style isolation.
- Composed events.
- Framework interoperability.
- Accessibility и form integration limitations.
- Focused/survey depth rather than framework construction.

---

# 6. CSS

## 6.1. Cascade & Selectors

- Origins, importance, layers, specificity, scoping proximity и order.
- Inheritance.
- `!important` и specificity management.
- `:is`, `:where`, `:not`, `:has`.
- Pseudo-classes и pseudo-elements.

## 6.2. Box Generation, Flow & Sizing

- Box model и `box-sizing`.
- Normal flow и inner/outer display.
- Margin collapsing.
- Block formatting contexts и `flow-root`.
- Containment и `content-visibility`.
- Positioning и containing blocks.
- Stacking contexts.
- Absolute, relative, font-relative и viewport units.
- Intrinsic sizing и automatic minimum sizes.
- Overflow, clipping и scroll containers.

## 6.3. Flexbox & Grid

- Flex axes, basis, grow, shrink и alignment.
- Automatic min-size и wrapping traps.
- Grid tracks, lines, areas и placement.
- `fr`, `minmax`, `auto-fit`, `auto-fill`.
- Subgrid.
- Flexbox против Grid.
- Centering patterns и их assumptions.

## 6.4. Responsive & International Layout

- Mobile-first и content-driven breakpoints.
- `min`, `max`, `clamp`.
- Container queries.
- Logical properties, RTL и writing modes.
- Responsive media, `object-fit` и `aspect-ratio`.

## 6.5. Tokens, Themes & Typography

- Custom properties и inheritance.
- Semantic design tokens.
- Theme boundaries.
- Web fonts, FOIT/FOUT и subsetting.
- Metric-compatible fallbacks и layout stability.

## 6.6. Motion, Preferences & Rendering Cost

- Transitions, keyframes и transforms.
- Layout/paint/composite implications.
- `requestAnimationFrame`.
- `prefers-reduced-motion`.
- Forced colors и color scheme.
- Functional fallback without animation.

## 6.7. CSS Architecture & Debugging

- BEM, CSS Modules, CSS-in-JS, utility CSS и cascade layers.
- Current production choice by constraints, not fashion.
- Overflow, containing-block и stacking-context diagnosis.
- Computed styles, box model и minimal reproduction.
- Layout cost против paint/composite cost.

---

# 7. Accessibility

## 7.1. Foundations & Accessibility Tree

- Users и permanent/temporary/situational barriers.
- POUR и WCAG 2.2 levels.
- Semantic HTML first.
- DOM → accessibility tree.
- Accessible name, role, value, state и description.
- Hidden-content rules.

## 7.2. Keyboard, Focus & Semantics

- Natural tab order и visible focus.
- Avoiding positive `tabindex`.
- Roving tabindex.
- Dialog focus lifecycle и restoration.
- Button, link, checkbox, switch и toggle semantics.
- ARIA states/properties и invalid ARIA.
- Headings, landmarks и skip links.
- SPA route-change focus strategy.

## 7.3. Content, Forms & Visual Accessibility

- Alternative text для images, icons, SVG и charts.
- Form labels, descriptions и error summaries.
- Contrast и non-color cues.
- Zoom, reflow и text-spacing resilience.
- Reduced motion и flashing.
- Target size, touch и dragging alternatives.
- Hover-only content avoidance.

## 7.4. Dynamic Content & Widgets

- Live regions, status и alert announcements.
- Avoiding announcement spam.
- Dialog, tabs, menu, combobox, tree и grid patterns.
- Keyboard model, focus model и state communication.
- Prefer native/simple patterns when possible.

## 7.5. Testing & Delivery Workflow

- Screen-reader task testing.
- Keyboard-only workflow.
- Automated audits и их limitations.
- Zoom, reflow, forced colors и reduced-motion checks.
- Definition of done и regression prevention.
- Accessibility PR review и severity by user impact.

---

# 8. Browser Internals & Web APIs

## 8.1. Browser Architecture & Rendering

- Browser, renderer, network и GPU processes.
- Sandbox и process isolation.
- HTML parsing и incremental DOM construction.
- CSSOM и render tree.
- Style → layout → paint → raster/composite.

## 8.2. Main-Thread Scheduling

- Execution contexts и call stack.
- Event loop interaction with rendering.
- `requestAnimationFrame`.
- Long tasks и blocked interaction.
- `requestIdleCallback` и scheduler APIs — survey depth.
- Forced synchronous layout и read/write batching.

## 8.3. Browser Memory

- Detached nodes, listeners, timers и subscriptions.
- Unbounded caches.
- Object URLs.
- Retainer paths и confirmation of leaks.

## 8.4. Client Storage

- Cookies, localStorage, sessionStorage.
- IndexedDB и Cache API.
- Synchrony, capacity, queryability и lifetime.
- Quota, eviction и partitioning — senior survey.
- Sensitive-data constraints.

## 8.5. Fetch & Streams

- Request/Response, body consumption и cloning.
- HTTP error против rejected promise.
- Abort/cancellation.
- Readable, writable и transform streams.
- Backpressure и incremental processing.

## 8.6. Workers, Service Workers & PWA

- Web Workers, Shared Workers и transferables.
- CPU work против DOM work.
- Service Worker lifecycle.
- Cache-first, network-first и stale-while-revalidate.
- Offline fallback и versioning.
- PWA manifest, install и update UX.

## 8.7. Navigation & Page Lifecycle

- Location и History APIs.
- SPA deep links.
- Focus/scroll restoration.
- Visibility и background work.
- `pagehide`/`pageshow`.
- Back/forward cache и common blockers.

## 8.8. Observers & Integration APIs

- Intersection, Resize, Mutation и Performance observers.
- `postMessage` и BroadcastChannel.
- File, Clipboard, drag-and-drop и object URLs.
- Permissions, geolocation и notifications — survey depth.
- Cleanup и feedback-loop prevention.

## 8.9. Specialized Rendering & Compute

- SVG против Canvas против WebGL.
- Hit testing и accessibility implications.
- WebAssembly boundary и suitable CPU-heavy workloads.
- JS/Wasm data-transfer cost.
- Survey depth unless target role requires more.

---

# 9. HTTP, API Design & Real-Time Communication

## 9.1. Protocol Foundations

- Request/response anatomy.
- Methods, safety и idempotency.
- Status-code families и meaningful errors.
- Headers, MIME и content negotiation.
- HTTP/1.1, HTTP/2 и HTTP/3.
- DNS → TCP/QUIC → TLS → HTTP → CDN/origin.

## 9.2. Sessions & Credentials

- Cookies и server-side sessions.
- Bearer tokens.
- Expiration, refresh и logout.
- XSS/CSRF trade-offs.
- No universally correct token mechanism.

## 9.3. HTTP Caching & CDN

- Cache-Control, Expires, ETag и Last-Modified.
- Freshness против validation.
- `Vary`.
- Browser/private/shared caches.
- CDN и edge caching.
- Immutable assets.
- Personalized-response leakage и invalidation bugs.

## 9.4. Cross-Origin Requests

- Same-Origin Policy.
- Simple и preflighted CORS requests.
- Credentials и allowed origins.
- Preflight caching.
- Browser block против server/network failure.
- CORS не является authentication/authorization.

## 9.5. API Styles

- REST resource modeling.
- REST против GraphQL.
- RPC и generated clients.
- Backend-for-Frontend.
- Ownership, coupling, caching и error trade-offs.

## 9.6. Reliable Client–Server Interaction

- Fetch failure taxonomy и `Response.ok`.
- Timeout и abort.
- Offset против cursor pagination.
- Sorting, filtering и search contracts.
- Versioning и backward compatibility.
- Error envelopes и correlation IDs.
- Idempotency keys.
- Backoff, jitter, rate limits и `Retry-After`.
- Request deduplication и freshness.
- Optimistic updates, conflicts и server reconciliation.

## 9.7. Real-Time & Streaming

- Polling, long polling, SSE и WebSocket selection.
- Authentication, heartbeat и reconnect.
- Ordering, sequence IDs и duplicate suppression.
- Streaming responses и incremental UI.
- Multipart/chunked/resumable uploads.
- Presence и delivery states.
- Eventual-consistency UI.

---

# 10. Frontend Performance

## 10.1. Metrics & Measurement

- LCP, INP и CLS.
- TTFB, FCP, TBT и Long Tasks.
- Lab против field data.
- Lighthouse, CrUX и RUM.
- 75th percentile и segmentation.
- Performance APIs и production instrumentation.

## 10.2. Core Web Vital Diagnosis

- LCP phases: TTFB, discovery, download, render delay.
- INP: input delay, processing и presentation delay.
- CLS: unsized media, fonts и inserted content.
- Trace-based diagnosis instead of score chasing.

## 10.3. Critical Loading Path

- Network waterfall и request priority.
- Critical CSS и render-blocking resources.
- Browser/CDN caching.
- Responsive images и LCP priority.
- Font loading и layout stability.
- Third-party contention.

## 10.4. JavaScript Delivery Cost

- Download, decompress, parse, compile, execute.
- Hydration cost.
- Route/component code splitting.
- Tree shaking, minification и compression.
- Chunk waterfalls и over-splitting.
- Duplicate dependencies и bundle analysis.

## 10.5. Runtime Rendering & Animation

- Style, layout, paint и composite.
- Layout thrashing.
- Animation frame budgets.
- Transform/opacity where appropriate.
- Layer-promotion cost.
- Reduced-motion support.

## 10.6. Application Performance

- React render/commit profiling.
- Virtualization и incremental rendering.
- Workers и cooperative scheduling.
- Long-lived SPA memory growth.
- Production-like data and builds.

## 10.7. Data & Rendering Architecture

- Data waterfalls и parallel fetching.
- Request deduplication.
- Streaming.
- SSR/RSC/hydration trade-offs.
- Cacheability против personalization.

## 10.8. Performance Governance

- Route-level budgets.
- CI regression gates.
- Field-release comparison.
- Third-party ownership.
- Exception process и documented trade-offs.

---

# 11. Web Security, Authentication & Privacy

## 11.1. Browser Trust Boundaries

- Origin против site.
- Same-Origin Policy.
- CORS как response-reading permission.
- Authentication против authorization.
- Browser controls не заменяют server enforcement.

## 11.2. XSS & Injection Defense

- Reflected, stored и DOM XSS.
- Source → transformation → sink analysis.
- Contextual encoding.
- Safe DOM sinks.
- HTML sanitization.
- Trusted Types.
- CSP, nonces и hashes.
- Defense in depth.

## 11.3. CSRF & Cookie Security

- Ambient cookie sending.
- CSRF tokens и origin validation.
- SameSite.
- Secure, HttpOnly, Domain и Path.
- Unsafe state-changing GET requests.
- XSS interaction with CSRF defenses.

## 11.4. Authentication & Authorization

- Memory, web-storage и HttpOnly-cookie token trade-offs.
- OAuth/OIDC authorization code + PKCE.
- Access, ID и refresh tokens.
- RBAC и permission checks.
- Object-level и tenant authorization.
- UI hiding не защищает данные.
- Server enforcement for every sensitive operation.

## 11.5. Browser & Third-Party Defenses

- Clickjacking и `frame-ancestors`.
- Subresource Integrity.
- Unsafe URLs и open redirects.
- Secure `postMessage`.
- Prototype pollution.
- HSTS, Referrer Policy и Permissions Policy.
- COOP, COEP и CORP.

## 11.6. Application Trust & Privacy

- Client bundles cannot contain secrets.
- Secure file-upload boundaries.
- Server validation и isolated delivery.
- Privacy-aware telemetry и PII redaction.
- RSC/Server Action validation, authentication и authorization.
- Preventing sensitive data from entering serialized payloads.

---

# 12. State Management, Server Data & Forms

## 12.1. State Taxonomy & Ownership

- Local UI, shared client, server, URL, form и persistent state.
- Lifetime, owner и source of truth.
- Colocation и justified lifting.
- Derived values против mirrored state.
- URL as shareable navigation state.
- Loading, empty, error, partial, stale и success states.

## 12.2. Shared Client State

- Context против external store.
- Redux principles и unidirectional flow.
- Redux Toolkit, slices, Immer, selectors и middleware.
- Redux Toolkit, Zustand, Jotai, MobX и signals.
- Reducers и state machines.
- Normalized entities.
- Persistence, version migration и cross-tab synchronization.

## 12.3. Server-State Layers

- Server state как remotely owned and stale data.
- TanStack Query, SWR и RTK Query.
- Query identity, freshness и invalidation.
- Request deduplication и refetch policies.
- Optimistic mutation и rollback.
- SSR dehydration/hydration.
- Preventing request-cache leakage between users.

## 12.4. Forms

- Controlled против uncontrolled.
- Native forms и `FormData`.
- Client и authoritative server validation.
- Schema reuse.
- React Hook Form, Formik, TanStack Form и native Actions.
- Multi-step, dynamic и large forms.
- Async validation races.
- Draft persistence и idempotent submission.
- Accessible error summary и focus.

## 12.5. State & Form Review Practice

- Classify every value by owner and lifetime.
- Remove mirrored state.
- Diagnose wrong query keys.
- Make optimistic updates race-safe.
- Split expensive contexts.
- Review forms for accessibility, duplicate submission и failure recovery.

---

# 13. Testing

## 13.1. Strategy & Boundaries

- Unit, component, integration, contract и E2E.
- Pyramid/trophy as heuristics.
- Risk-based test selection.
- Observable behavior против implementation details.
- Feedback speed, fidelity, cost и flakiness.

## 13.2. Test Runner Fundamentals

- Jest/Vitest execution model.
- Assertions, setup и teardown.
- Mocks, spies, stubs и fakes.
- Fake timers, microtasks и deterministic time.
- Module isolation и mock leakage.
- Testing stable boundaries rather than every internal function.

## 13.3. React Testing

- Testing Library query priority.
- Role/name/label selectors.
- `userEvent`.
- Async queries и `waitFor`.
- Hooks, providers, router и store integration.
- Suspense, transitions и optimistic UI.
- Avoiding unjustified render-count assertions.

## 13.4. Network & Framework Testing

- MSW и Request/Response semantics.
- Success, slow, empty, error и malformed responses.
- Cancellation и response-order races.
- RSC/Actions/framework integration.
- Server Action authorization tests.
- API schemas и consumer-driven contracts.

## 13.5. Browser & E2E

- Playwright против Cypress.
- Stable selectors и web-first assertions.
- Fixtures и isolated test data.
- Page objects without hiding intent.
- Trace, video, screenshot и network diagnosis.
- Flaky-test classification и root-cause repair.

## 13.6. Specialized Techniques

- Visual regression.
- Automated и manual accessibility testing.
- Performance/Web Vitals testing.
- Snapshot-test boundaries.
- Coverage metrics.
- Mutation testing.
- Why high coverage does not guarantee useful assertions.

## 13.7. CI & Test Ownership

- Parallelism и sharding.
- Deterministic environments.
- Artifact retention.
- Retries as diagnostic signal.
- Quarantine with owner and deadline.
- Flake-rate tracking.
- Removing low-value tests.

---

# 14. Git, Packages, Build Tools & Delivery

## 14.1. Git Data Model & Recovery

- Working tree, index, commits и HEAD.
- Branches, merge и rebase.
- Reset, revert и restore.
- Stash и cherry-pick.
- Reflog recovery.
- `git bisect`.
- Shared-history safety.

## 14.2. Collaboration Workflows

- Semantic conflict resolution.
- Atomic commits и reviewable PRs.
- Merge/squash/rebase policies.
- Trunk-based development.
- GitFlow — **contextual/legacy**, not automatic modern default.
- Feature flags enabling short-lived branches.

## 14.3. Package Management

- dependencies, devDependencies, peer и optional dependencies.
- Semantic version ranges.
- Lockfiles и deterministic installs.
- npm, Yarn и pnpm architecture.
- Hoisting, phantom dependencies, PnP и pnpm links.
- Package exports, conditions и subpaths.
- ESM/CJS resolution.
- Supply-chain and reproducibility awareness.

## 14.4. Build Pipeline Mental Model

- Dependency graph.
- Resolve → parse → transform → emit.
- Loaders/transforms против plugins.
- Webpack, Vite, Rspack, esbuild и Turbopack.
- Babel, SWC и TypeScript compiler responsibilities.
- Transpilation против type checking.
- Browser targets и polyfill distinction.

## 14.5. Build Optimization & Debugging

- Tree shaking и `sideEffects`.
- Scope hoisting.
- Chunking и dynamic imports.
- Vendor/shared chunk trade-offs.
- HMR/Fast Refresh.
- Source maps и secure symbolication.
- Chunk-version mismatches after deployment.

## 14.6. Code-Quality Pipeline

- Linting, formatting, type checking и tests.
- Pre-commit feedback против CI authority.
- Configuration drift.
- Warnings/errors policy.
- Editor/CI parity.

## 14.7. Monorepos

- Workspaces и package boundaries.
- Internal versioning.
- Task graphs.
- Affected-only execution.
- Local/remote cache.
- Cache inputs и poisoning risks.
- Monorepo против distributed monolith.

## 14.8. CI/CD & Safe Delivery

- Install → checks → tests → build → security → deploy.
- Build once, promote same artifact.
- Environment parity.
- Feature flags.
- Canary, rolling и blue-green rollout.
- Health signals и rollback.
- Backward-compatible API/data changes.

---

# 15. Frontend Architecture & Design Patterns

## 15.1. Architectural Principles

- Separation of concerns.
- Cohesion и coupling.
- DRY as duplication of knowledge, not identical syntax.
- KISS и YAGNI.
- Pragmatic SOLID for components, hooks и services.
- Reversible против hard-to-reverse decisions.
- Maintainability, reliability, accessibility и performance as quality attributes.

## 15.2. Codebase Organization & Boundaries

- Layer-, feature- и domain-oriented organization.
- Vertical slices и hybrid structures.
- Component/module responsibilities.
- Public APIs и information hiding.
- Avoiding shared-folder dumping grounds.
- Dependency injection и composition roots.
- Monorepo против polyrepo.

## 15.3. Component Architecture & Design Systems

- Tokens → foundations → primitives → components → patterns.
- Semantic против raw tokens.
- Headless против styled components.
- Polymorphic component APIs.
- Controlled/uncontrolled contracts.
- Boolean-prop explosion.
- Versioning, migration и governance.

## 15.4. Reusable Patterns

- Observer и pub/sub.
- Strategy, factory, adapter и decorator.
- Command, state и reducer.
- Undo/redo.
- MVC, MVVM, Flux и unidirectional architecture.
- Legacy vocabulary separated from current recommendations.
- Using named patterns only when they clarify design.

## 15.5. State, Data & Rendering Architecture

- State ownership и data-access layer.
- Query/cache layer против global client store.
- BFF и client/server responsibility boundary.
- CSR, SSR, static, islands и RSC selection.
- Error boundaries, retries и graceful degradation.
- Partial failure, stale data и degraded modes.

## 15.6. Organization-Scale Architecture

- Modular monolith против microfrontends.
- Build-time, server-side и runtime integration.
- Routing, auth, shared state и dependency conflicts.
- Failure isolation.
- Internationalization, localization и RTL.
- Multi-tenancy и tenant isolation.
- Feature flags и experimentation.

## 15.7. Evolution & Governance

- Legacy migration и strangler pattern.
- Characterization tests и incremental modernization.
- ADRs и RFCs.
- Ownership и cross-team contracts.
- Versioning/deprecation.
- Architecture review without a central bottleneck.

---

# 16. UI Machine Coding

Все задания должны хранить условие отдельно от решения.

## 16.1. Interview Execution Method

- Clarify requirements и assumptions.
- Identify states, events и edge cases.
- Define data model и state ownership.
- Sketch component boundaries.
- Deliver a thin working vertical slice.
- Narrate decisions.
- Add accessibility, tests и performance proportionally.

## 16.2. Foundational Widgets

- Counter и todo list.
- Accordion.
- Tabs с keyboard navigation.
- Star rating.
- Stopwatch/progress/traffic-light state machine.
- Small game/grid/crossword с progressive requirements.

## 16.3. Composite & Overlay Widgets

- Modal/dialog с focus management.
- Tooltip и popover.
- Dropdown/menu.
- Carousel.
- OTP input.
- Controlled/uncontrolled APIs.
- Portal, outside click, Escape и restoration behavior.

## 16.4. Search, Lists & Data

- Debounced autocomplete с cancellation и cache.
- Pagination.
- Infinite scroll.
- Sortable/filterable/paginated data table.
- URL synchronization.
- Virtualization.
- Loading, empty, error и retry states.

## 16.5. Hierarchies, Forms & Commerce

- File explorer/tree.
- Nested comments.
- Toast notification queue.
- Multi-step form.
- Shopping cart/checkout.
- Normalized data и optimistic changes.
- Accessible state announcements.

## 16.6. Advanced Interactions

- File upload с progress/cancel/retry.
- Kanban и accessible drag-and-drop.
- Calendar/date picker.
- Realtime chat UI.
- Ordering, duplicates, temporary IDs и reconnection.
- Large-data and cross-device concerns.

## 16.7. Timed Practice Ladder

- 30 minutes: semantic working baseline.
- 60 minutes: async behavior, accessibility и edge cases.
- 90 minutes: tests, performance и extensions.
- Rebuild selected tasks without AI/autocomplete.
- Separate scoring for syntax recall, state modeling, correctness и explanation.

---

# 17. Data Structures & Algorithms

Каждый pattern изучается через:

**recognition → brute force → invariant → implementation → complexity → variants → testing → explanation.**

## 17.1. Complexity & Problem Solving

- Big-O time и space.
- Worst, average и amortized complexity.
- Input constraints.
- Hidden cost of JavaScript array/string operations.
- Explain brute force before optimization.
- Dry run и edge-case tests.

## 17.2. Arrays, Strings & Hashing

- Array/string transformations.
- Hash map и set selection.
- Frequency counter.
- Two Sum family.
- Sorting и custom comparators.
- Flatten nested arrays/objects.
- Unicode/code-point awareness where relevant.

## 17.3. Range & Pointer Patterns

- Two pointers.
- Fixed и variable sliding window.
- Prefix sums.
- Binary search и boundary variants.
- Search in answer space.
- Intervals: overlap, merge, insert и scheduling.

## 17.4. Stack, Queue & Linked Structures

- Stack и balanced delimiters.
- Monotonic stack.
- Queue/deque.
- Circular buffer.
- Linked-list reverse, merge и cycle detection.
- Pointer invariants.

## 17.5. Recursion, Trees & Graphs

- Recursion и backtracking.
- Tree DFS/BFS.
- Graph traversal.
- Connected components и cycles.
- Trie для prefix search.
- Topological ordering.
- DOM/tree traversal.
- Deep clone как graph traversal with cycles.

## 17.6. Selection, Caching, Scheduling & DP

- Top-K и heap.
- Priority queue.
- LRU cache.
- Memoization и basic dynamic programming.
- Async task scheduler/concurrency queue.
- Backpressure и ordered results.

## 17.7. Pattern Recognition Practice

- Mixed tasks without named pattern.
- Buggy-solution review.
- Complexity correction.
- Frontend variants: DOM tree, autocomplete trie, LRU, dependency graph.
- Spaced repetition based on recognition failures, not raw task count.

---

# 18. Frontend System Design

Каждый case study использует один process:

**Clarify → Requirements → Constraints → Data/API → Components → State → Rendering → Caching → Performance → Accessibility → Security → Resilience → Observability → Trade-offs → Evolution.**

## 18.1. Interview Foundations

- Functional и non-functional requirements.
- Actors, user flows и success metrics.
- Device, browser, localization и accessibility requirements.
- Data volume, latency и update frequency.
- Component-design против application-design round.
- Diagram selection и time management.

## 18.2. Reusable Building Blocks

- State ownership и state machines.
- API contracts, pagination и cancellation.
- CSR/SSR/static/streaming/RSC choices.
- Browser/CDN/application caches.
- Optimistic consistency.
- Virtualization и main-thread budgets.
- Offline/retry/error handling.
- Auth, privacy, telemetry и rollout.

## 18.3. Guided Product Cases

- Autocomplete/typeahead.
- Feed/infinite scrolling.
- Notifications/toasts.
- Image gallery/Pinterest grid.
- Shopping cart/checkout.
- Search results experience.
- Calendar/scheduling.

## 18.4. Data-Heavy, Realtime & Media Cases

- Large live data table/dashboard.
- Chat application.
- Large/resumable file upload.
- Email client.
- Video player/streaming UI.

## 18.5. Collaborative & Rich Editors

- Collaborative document editor.
- OT против CRDT at trade-off level.
- Figma/Canva-like canvas editor.
- Scene graph, hit testing и undo/redo.
- Browser code editor.
- Virtualized text, workers и running untrusted code.

## 18.6. Platform & Organization Cases

- Multi-tenant admin SaaS.
- Organization-wide component library.
- Microfrontend platform.
- Frontend monitoring/Web Vitals platform.
- Feature-flag и experimentation client.

## 18.7. Offline & Emerging Cases

- Offline-first PWA и synchronization.
- Outbox, conflicts, tombstones и quota.
- Streaming AI chat UI.
- Partial output, cancellation, citations и tool states.
- AI case remains supplementary; it does not replace core cases.

## 18.8. Practice Progression

- Guided worksheet.
- Same case from blank page.
- Thirty-minute timed design.
- Requirement change invalidating an earlier assumption.
- Compare two viable options.
- Five-minute architecture summary.
- Post-practice missed-requirement and weak-trade-off audit.

---

# 19. Debugging, Code Review & Interview Communication

## 19.1. Systematic Debugging

- Reproduce → minimize → hypothesize → test → verify.
- Expected против actual behavior.
- Observation против interpretation.
- One discriminating experiment at a time.
- Root cause против symptom.
- Thinking aloud without narrating every thought.

## 19.2. Diagnostic Tools

- Elements, Console, Sources и Network.
- Breakpoints, initiators и cache behavior.
- Performance traces.
- React Profiler.
- Heap snapshots и allocation profiles.
- Source maps и clean-profile reproduction.

## 19.3. Recurring Frontend Failures

- Stale closures и effect loops.
- State identity/reset bugs.
- Hydration mismatches.
- CORS, caching и request races.
- CSS overflow и stacking contexts.
- Out-of-order async UI.
- Cross-browser/device failures.
- Flaky tests и customer-only problems.

## 19.4. Production Diagnostics & Incidents

- Errors, releases, Web Vitals и network telemetry.
- Trace/correlation IDs.
- Sampling и privacy.
- Severity, impact и affected cohorts.
- Mitigation before perfect diagnosis.
- Feature disable, rollback и recovery verification.
- Blameless postmortem и owned corrective actions.

## 19.5. Code Review & Refactoring

- Correctness, edge cases и data flow.
- Naming, API shape и maintainability.
- Security, accessibility и performance.
- Tests and observability.
- Severity-ranked comments.
- Respectful actionable feedback.
- Characterization tests и incremental legacy refactoring.

## 19.6. Interview Communication

- 30–60 second concept explanation:
  definition → mental model → example → trap/trade-off.
- Think aloud, clarify constraints и state assumptions.
- Options → Criteria → Trade-off → Decision.
- Senior project stories: ownership, constraints, impact, failure, lessons.
- AI-assisted coding: generated output as untrusted draft.
- Independent verification of behavior, APIs, security и tests.

## 19.7. Integrated Practice

- Bug report diagnosis.
- Performance-trace exercise.
- Heap-leak lab.
- Hydration/race/CSS debugging packet.
- PR-review round.
- Legacy refactor in safe steps.
- Mock production incident.
- Timed explanation и architecture decision.

---

# Coverage Audit

Результат: **510/510 groups mapped, 0 unmapped, 0 removed**.

## Exact domain mapping

- **JavaScript — 60/60:** `JS-01–04,22 → 1.1`; `05–11,40 → 1.2`; `12–21 → 1.3`; `23–28,39 → 1.4`; `29–34 → 1.5`; `35–38 → 1.6`; `41–44 → 1.7`; `45 → 1.8`; `46–49 → 1.9`; `50–55 → 1.10`; `56–58 → 1.11`; `59–60 → 1.12`.
- **TypeScript — 28/28:** `TS-01–03 → 2.1`; `04,07–08 → 2.2`; `05–06 → 2.3`; `09–11 → 2.4`; `12–18 → 2.5`; `19–21 → 2.6`; `22–23,28 → 2.7`; `24–27 → 2.8`.
- **React — 48/48:** `RE-01–08 → 3.1–3.2`; `09–19,43 → 3.2–3.4`; `22–27 → 3.5–3.6`; `20–21,45–46 → 3.7`; `28–31,38–39 → 3.8`; `32–33 → 3.9`; `34–37 → 3.10`; `40–44 → 3.11–3.12`; `47 → 3.12`; `48 → 3.13`.
- **Next.js — 20/20:** `NX-01–03 → 4.1`; `04–05 → 4.2`; `06,14 → 4.3`; `07–09,15 → 4.4`; `10 → 4.5`; `11–12 → 4.6`; `13,18–19 → 4.7`; `16–17 → 4.8`; `20 → 4.9`.
- **HTML/DOM/forms — 25/25:** `HD-01–04 → 5.1`; `05–09,15 → 5.2`; `10–13 → 5.3`; `14 → 5.4`; `16–18 → 5.5`; `19–24 → 5.6`; `25 → 5.7`.
- **CSS — 28/28:** `CSS-01–03 → 6.1`; `04–12 → 6.2`; `13–18 → 6.3`; `19–21,24 → 6.4`; `22–23 → 6.5`; `25–26 → 6.6`; `27–28 → 6.7`.
- **Accessibility — 20/20:** `AX-01–03 → 7.1`; `04–07,11 → 7.2`; `09–10,12–14,17 → 7.3`; `15–16 → 7.4`; `08,18–20 → 7.5`.
- **Browser — 25/25:** `BR-01–04 → 8.1`; `05–08 → 8.2`; `09 → 8.3`; `10–11 → 8.4`; `12,25 → 8.5`; `13–16 → 8.6`; `17,24 → 8.7`; `18–21 → 8.8`; `22–23 → 8.9`.
- **HTTP/API/realtime — 27/27:** `NET-01–05 → 9.1`; `06 → 9.2`; `07–09 → 9.3`; `10 → 9.4`; `11–13 → 9.5`; `14–22 → 9.6`; `23–27 → 9.7`.
- **Performance — 24/24:** `PF-01–02,06–07 → 10.1`; `03–05 → 10.2`; `08–09,13–15 → 10.3`; `10–12 → 10.4`; `16–17 → 10.5`; `18–21 → 10.6`; `22–23 → 10.7`; `24 → 10.8`.
- **Security — 20/20:** `SEC-01–02 → 11.1`; `03–06 → 11.2`; `07–08 → 11.3`; `09–12,19 → 11.4`; `13–18 → 11.5`; `20 → 11.6`.
- **State/forms — 18/18:** `ST-01–02,10,18 → 12.1`; `03–06,11–13 → 12.2`; `07–09 → 12.3`; `14–17 → 12.4`.
- **Testing — 18/18:** `TEST-01–03 → 13.1`; `04 → 13.2`; `05,07 → 13.3`; `06,08,15 → 13.4`; `09–11 → 13.5`; `12–14,16–17 → 13.6`; `18 → 13.7`.
- **Tooling/delivery — 24/24:** `TOOL-01–06 → 14.1`; `07 → 14.2`; `08–13 → 14.3`; `14–16 → 14.4`; `17–20 → 14.5`; `21 → 14.6`; `22 → 14.7`; `23–24 → 14.8`.
- **Architecture — 25/25:** `ARCH-01,06–07 → 15.1`; `02–03,11,16 → 15.2`; `04–05 → 15.3`; `08–10,12 → 15.4`; `17–20 → 15.5`; `13–15,21–23 → 15.6`; `24–25 → 15.7`.
- **UI coding — 24/24:** `UI-01–03,08,23–24 → 16.2`; `04–06,09,16 → 16.3`; `07,10–12 → 16.4`; `13–15,17,21 → 16.5`; `18–20,22 → 16.6`.
- **DSA — 28/28:** `DSA-01,28 → 17.1`; `02–04,08,25 → 17.2`; `05–07,10,20 → 17.3`; `11–14 → 17.4`; `15–18,23–24,26 → 17.5`; `09,19,21–22,27 → 17.6`.
- **System Design — 24/24:** `SD-01–02 → 18.1`; `03–04,07,09–10,16–17 → 18.3`; `05–06,08,11–12 → 18.4`; `13–15 → 18.5`; `18,20–23 → 18.6`; `19,24 → 18.7`.
- **Engineering practice — 24/24:** `ENG-01 → 19.1`; `02–05 → 19.2`; `06–10,17–18 → 19.3`; `11–12 → 19.4`; `13–16,19 → 19.5`; `20–24 → 19.6`.

Некоторые groups намеренно покрываются в нескольких доменах. Например:

- event loop: JavaScript ↔ browser rendering;
- forms: HTML ↔ accessibility ↔ React ↔ security;
- caching: browser ↔ HTTP/CDN ↔ state libraries ↔ Next.js ↔ performance;
- memory: JavaScript reachability ↔ browser leaks ↔ production diagnostics;
- CORS/cookies: networking ↔ security;
- rendering pipeline: browser ↔ CSS ↔ performance.

Это cross-linking, а не дублирование ради объёма.

# Interview-Value Audit

## Материал с наибольшей глубиной

- JavaScript scope, closures, `this`, prototypes, event loop и Promises.
- TypeScript narrowing, generics и runtime boundaries.
- DOM events, CSS layout и accessibility.
- HTTP caching, CORS и API reliability.
- React state identity, effects, rendering и performance.
- Security boundaries.
- Debugging, code review и system-design reasoning.

## Survey-depth material

Следующие темы сохраняются ради realistic Senior coverage, но не должны отнимать объём у fundamentals:

- Proxy/Reflect и WeakRef.
- Template-literal types, variance и namespaces.
- Browser scheduler APIs и storage partitioning.
- Permissioned browser APIs.
- Canvas/WebGL/WebAssembly.
- Emerging React APIs.
- Specialized platform/system-design cases.
- AI-assisted coding и streaming AI UI.

## Legacy knowledge

Не преподаётся как новый production default:

- `var`, `arguments`, IIFE и constructor functions;
- CommonJS;
- TypeScript namespaces и некоторые enum patterns;
- class components и lifecycle methods;
- HOCs, render props и `forwardRef`;
- Next.js Pages Router и legacy middleware terminology;
- handwritten Redux boilerplate;
- Formik as a default choice;
- Create React App;
- Enzyme-style component testing;
- GitFlow без оправдывающих release constraints.

## Что сознательно не превращено в обязательные главы

- Внутренние поля Fiber и исходники React reconciler.
- Редкие specification algorithms.
- Все API каждой state/form/testing library.
- Exhaustive bundler/plugin configuration.
- Редкие Git plumbing commands.
- Продвинутое competitive programming.
- Глубокие WebGL/WebRTC/Node internals без соответствующей вакансии.

Role-specific направления — React Native, Angular/Vue/Svelte, глубокий Node/BFF, WebRTC и graphics-heavy frontend — следует подключать отдельными tracks под конкретную вакансию. Они не маскируются как уже покрытая часть этих 510 групп.

# Итог

Curriculum покрывает утверждённый inventory полностью:

| Layer | Groups covered |
|---|---:|
| Web platform, language, networking, performance, security | 257 |
| React ecosystem, state, testing and tooling | 128 |
| Architecture, coding, DSA, system design and engineering practice | 125 |
| **Total** | **510/510** |

Тем с практически нулевой interview value в обязательную траекторию не добавлено. Низкочастотные, но реалистичные темы сохранены с уменьшенной глубиной.

На этом **Этап 1 остановлен**. Репозиторий и файлы не создавались. Жду вашего review и явного разрешения перед Этапом 2.

