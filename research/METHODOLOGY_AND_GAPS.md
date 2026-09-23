# Research Methodology, Findings & Gap Analysis

This is a convenience extract from the canonical [Master Question Inventory](MASTER_QUESTION_INVENTORY.md). If the two ever diverge, the canonical artifact wins.

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

