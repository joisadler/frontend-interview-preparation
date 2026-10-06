# 1.2. Значения, типы, равенство и преобразование типов (Values, Types, Equality & Coercion)

> Статус: `approved by user on 2026-10-06 — Stage 4, цикл 1.2 завершён`
>
> Связанные inventory IDs: `JS-05`, `JS-06`, `JS-07`, `JS-08`, `JS-09`, `JS-10`, `JS-11`, `JS-40`
>
> Последняя содержательная проверка: `2026-10-01`
>
> Проверка примеров: output-prediction и граничные числовые примеры выполнены в Node.js; намеренно ошибочные примеры подписаны.

Эта глава отвечает на один большой вопрос: **что именно находится в переменной и что JavaScript делает с этим значением, когда мы копируем, сравниваем или используем его не в том типе?**

Из него вырастают почти все типичные ловушки темы:

- почему `const`-объект можно изменить;
- почему два одинаково выглядящих объекта не равны;
- почему функция может изменить переданный объект, но не переназначить переменную вызывающего кода;
- почему `0 || 10` и `0 ?? 10` дают разные результаты;
- почему `NaN !== NaN`, а `new Set([NaN, NaN]).size === 1`;
- почему `0.1 + 0.2 !== 0.3`;
- почему оператор `+` иногда складывает, а иногда склеивает строки.

Мы начнём со значений и identity, затем перейдём к проверке типов и особым числам. После этого разберём boolean-контексты, defaulting и optional chaining. Только когда эта база будет готова, сравним четыре семантики равенства и построим практическую модель coercion.

Полные темы копирования массивов и deep copy остаются в 1.5, well-known symbols и протоколы итерации — в 1.6, свойства и прототипы — в 1.4. Здесь берём ровно столько, сколько нужно для identity, shared references и преобразования объектов в примитивы.

## Как читать эту главу

```text
value и type
  → primitive или object
    → immutability, identity, mutation, reassignment
      → shared references и pass-by-value
        → typeof, absence и special numeric values
          → truthy / falsy / nullish
            → short-circuit и optional chaining
              → equality semantics
                → explicit / implicit coercion
                  → ToPrimitive и output prediction
```

### Два прохода

**🎯 Первый проход — интервью-ядро.** Прочитайте вопросы 1–5, 7, 9–16 и 18. Этого достаточно, чтобы восстановить primitives/objects, identity, pass-by-value, `typeof`, `NaN`, truthy/falsy, `||`/`??`, optional chaining, `===`, `Object.is`, coercion и оператор `+`.

**🔬 Второй проход — точность.** Вопросы 6, 8 и 17 уточняют `Symbol`/`BigInt`, сравнение floating-point чисел, SameValueZero, `ToPrimitive` и порядок `valueOf()`/`toString()`. Эти детали полезны для Mid/Senior follow-up, но не должны заслонять рабочие правила.

Блоки `🔬 Точная деталь` можно пропустить при первом чтении. Блок `🧓 Legacy` означает знание для старого кода или интервью, а не рекомендацию использовать такое поведение в новой реализации.

## Ментальная модель

Сначала вся тема в девяти строках:

1. В JavaScript **тип есть у значения**, а переменная хранит текущее значение и может позже получить значение другого типа.
2. Primitive value — самостоятельное неизменяемое значение; object value имеет identity и изменяемое содержимое.
3. Присваивание всегда копирует значение. Для объекта копируется значение, позволяющее обратиться к тому же object identity.
4. Поэтому две переменные могут разделять один объект, а shallow copy разрывает только верхнюю ссылку.
5. JavaScript передаёт аргументы **по значению (pass-by-value)** — в том числе значение object reference.
6. Boolean-контекст делит значения на truthy и falsy; nullish — более узкая группа: только `null` и `undefined`.
7. `===`, `Object.is` и SameValueZero не выполняют общий deep comparison объектов: для objects важна identity.
8. Coercion сначала может превратить object в primitive, а затем — primitive в нужный контексту тип.
9. У `+` две роли: после `ToPrimitive` он выбирает string concatenation либо numeric addition.

Три полезные аналогии:

- **Primitive как напечатанное число на карточке:** копия карточки несёт то же значение, но карточку нельзя «изменить изнутри» — можно только заменить её другой.
- **Object identity как общий документ по одной ссылке:** два человека могут открыть один документ; правка видна обоим, но создание копии верхней страницы не копирует вложенные приложения.
- **Coercion как переходник:** контекст просит значение нужной формы. Иногда переходник очевиден (`Number("42")`), иногда язык подключает его скрыто (`"5" * 2`).

Аналогии помогают помнить поведение, но спецификация не требует хранить object reference как видимый адрес памяти и не превращает primitives в реальные бумажные карточки.

---

## Связное объяснение в формате вопросов и ответов

### 🎯 1. Что такое значение и где у него тип?

**Значение (value)** — данные, с которыми работает программа: `42`, `"hello"`, `null`, `1n`, объект пользователя или функция. **Тип (type)** описывает набор возможных значений и правила операций над ними.

В JavaScript тип относится к текущему значению, а не навсегда к имени переменной:

```js
let result = 42;
console.log(typeof result); // "number"

result = "done";
console.log(typeof result); // "string"
```

Это не значит, что «переменная сама стала строковой коробкой». Привязка `result` сначала хранила number value, затем получила string value. Статическая система TypeScript может отдельно ограничить допустимые присваивания, но runtime JavaScript видит реальные значения.

#### Какие категории значений есть в JavaScript?

На уровне языка удобно начать с двух групп:

| Группа | Значения |
|---|---|
| Primitive values | `undefined`, `null`, `boolean`, `number`, `bigint`, `string`, `symbol` |
| Object values | обычные объекты, массивы, функции, даты, регулярные выражения и другие objects |

Функция — object value с внутренней способностью быть вызванной. Поэтому `typeof function () {}` возвращает специальную строку `"function"`, хотя функция остаётся объектом в более широкой классификации языка.

#### Тип значения и возможность переназначить переменную — разные оси

```js
const count = 1;
// count = 2; // TypeError: assignment to constant variable
```

`count` хранит primitive number value. Запрет появился не потому, что number неизменяем, а потому, что `const` запрещает переназначить binding.

```js
let user = { name: "Ada" };
user = { name: "Grace" };
```

`user` хранит object value, а `let` разрешает заменить его другим object value. Тип значения не определяет, можно ли переназначать binding; это определяет форма объявления.

### 🎯 2. Чем primitive value отличается от object value?

Главные различия для этой темы — **неизменяемость значения** и **identity**.

#### Primitives неизменяемы

**Неизменяемость (immutability)** primitive означает: само primitive value нельзя изменить изнутри. Операция создаёт другое значение.

```js
let text = "cat";
text.toUpperCase();

console.log(text); // "cat"

text = text.toUpperCase();
console.log(text); // "CAT"
```

Метод `toUpperCase()` не меняет исходную строку. Он возвращает новую строку. Чтобы `text` показывал новое значение, binding нужно переназначить.

Попытка записать символ внутрь строки тоже не меняет string value:

```js
"use strict";

const code = "cat";
// code[0] = "b"; // TypeError в strict mode; строка остаётся "cat"
```

Число, boolean, `null`, `undefined`, `bigint` и `symbol` так же не имеют изменяемых внутренних полей, доступных как у обычного объекта.

#### Objects имеют identity

У object value есть **идентичность (identity)**: конкретный объект остаётся тем же объектом, даже когда его содержимое меняется.

```js
const user = { name: "Ada" };
const sameUser = user;

user.name = "Grace";

console.log(sameUser.name); // "Grace"
console.log(user === sameUser); // true
```

`user` и `sameUser` содержат копии одного и того же значения, которое ведёт к одному object identity. Мы не создали второго пользователя.

Два отдельно созданных объекта имеют разную identity, даже если их свойства выглядят одинаково:

```js
console.log({ id: 1 } === { id: 1 }); // false
console.log([1, 2] === [1, 2]);       // false
```

Оператор не выполняет deep comparison содержимого. Он спрашивает: «Это один и тот же object value?»

<details>
<summary>🔬 Точная деталь: «reference» — полезная модель, но не отдельный language type</summary>

В разговорной речи objects называют «reference types». Для интервью безопаснее сказать:

> Object value имеет identity, а переменная содержит значение, через которое код обращается к этому объекту.

Спецификация не добавляет в список ECMAScript language types отдельный тип `Reference` для пользовательских значений. Reference Record существует как внутренний specification type для операций вроде доступа к переменной или свойству, но это не значение, которое можно получить через `typeof` или сохранить в массив.

Фраза «переменная хранит ссылку» остаётся хорошей практической моделью, если не превращать её в утверждение о видимом адресе памяти.

</details>

### 🎯 3. Чем mutation отличается от reassignment и почему появляется shared state?

- **Переназначение (reassignment)** меняет значение в binding.
- **Мутация (mutation)** меняет состояние уже существующего объекта.

```js
let profile = { theme: "light" };

profile.theme = "dark";          // mutation: тот же object identity
profile = { theme: "contrast" }; // reassignment: другой object value
```

`const` запрещает только второй шаг:

```js
const settings = { compact: false };

settings.compact = true; // допустимая mutation
// settings = {};        // TypeError: reassignment запрещён
```

#### Shared references

**Разделяемая ссылка (shared reference)** возникает, когда несколько bindings ведут к одному объекту:

```js
const defaults = { nested: { retries: 2 } };
const requestOptions = defaults;

requestOptions.nested.retries = 5;
console.log(defaults.nested.retries); // 5
```

Это не особое копирование «по ссылке». Обычное присваивание скопировало object value, и обе копии обозначают один identity.

Аналогия с общим документом полезна здесь: два ярлыка открывают один файл. Переименование одного ярлыка не меняет другой binding, но редактирование самого файла видно через оба ярлыка.

#### Где помогает shallow copy?

**Поверхностная копия (shallow copy)** создаёт новый внешний объект, но вложенные object values остаются общими:

```js
const defaults = {
  theme: "light",
  network: { retries: 2 },
};

const options = { ...defaults };

console.log(options === defaults); // false
console.log(options.network === defaults.network); // true

options.theme = "dark";
options.network.retries = 5;

console.log(defaults.theme); // "light"
console.log(defaults.network.retries); // 5
```

Spread решил sharing на верхнем уровне, но не скопировал вложенный `network`. Полная тема shallow/deep copy, `structuredClone` и cycles будет в 1.5. Для 1.2 достаточно правила:

> Новый внешний объект не означает новый object graph.

### 🎯 4. JavaScript передаёт объекты по значению или по ссылке?

Короткий точный ответ: **JavaScript передаёт аргументы по значению (pass-by-value)**. Если аргумент — object value, параметр получает копию значения, которое ведёт к тому же объекту.

```js
function update(user) {
  user.name = "Grace";       // mutation общего объекта
  user = { name: "Lin" };    // reassignment только локального параметра
}

const original = { name: "Ada" };
update(original);

console.log(original); // { name: "Grace" }
```

Пошагово:

1. Binding `original` содержит object value.
2. При вызове это значение копируется в новый локальный binding параметра `user`.
3. Оба значения обозначают один object identity, поэтому `user.name = ...` меняет общий объект.
4. `user = ...` заменяет только значение локального binding `user`.
5. Binding `original` вызывающего кода не переназначается.

#### Почему это не pass-by-reference?

При настоящей передаче переменной по ссылке функция могла бы переназначить binding вызывающего кода. Здесь не может:

```js
function replace(value) {
  value = { replaced: true };
}

let item = { replaced: false };
replace(item);

console.log(item.replaced); // false
```

Поэтому фраза «primitives передаются по value, objects — по reference» создаёт неправильную модель. Лучше сказать:

> Всё передаётся по value. Для object argument скопированное значение сохраняет доступ к тому же object identity.

Если функция должна «заменить значение у вызывающего кода», она обычно возвращает новое значение, а вызывающий код явно присваивает его:

```js
function replace(value) {
  return { ...value, replaced: true };
}

item = replace(item);
```

### 🎯 5. Что показывает `typeof` и где он вводит в заблуждение?

`typeof` возвращает строку с грубой runtime-классификацией значения:

| Значение | `typeof` |
|---|---|
| `undefined` | `"undefined"` |
| `null` | `"object"` — историческая ошибка |
| `true` | `"boolean"` |
| `42`, `NaN`, `Infinity` | `"number"` |
| `42n` | `"bigint"` |
| `"hello"` | `"string"` |
| `Symbol("id")` | `"symbol"` |
| `function () {}` | `"function"` |
| массив, дата, regexp, обычный объект | `"object"` |

```js
typeof NaN;          // "number"
typeof [];           // "object"
typeof null;         // "object"
typeof (() => {});   // "function"
```

`typeof` хорошо отвечает на вопрос «primitive какого базового вида передо мной?» и умеет отдельно узнавать callable objects. Но он не различает массив, дату и обычный объект.

Для точной проверки нужен подходящий контракту инструмент:

```js
Array.isArray(value);
value === null;
Number.isNaN(value);
```

Проверка класса через `instanceof` имеет отдельные ограничения, включая разные realms, и относится к объектной модели из 1.4.

#### Почему `typeof null === "object"`?

Это историческая несовместимость, сохранённая ради web compatibility. `null` — отдельный primitive value, а не object. В первой реализации JavaScript его внутреннее представление пересеклось с меткой objects; исправление позже сломало бы существующий код.

Правило для интервью:

> Список primitives определяет семантику; `typeof` — оператор с историческими особенностями, а не идеальная функция `getExactType`.

#### `undefined` и `null`

Оба значения часто обозначают отсутствие, но их происхождение и контракт обычно различаются:

- `undefined` часто появляется как «значение не было предоставлено»: отсутствующий аргумент, отсутствующее свойство, `let value;`, функция без явного `return`;
- `null` обычно записывают намеренно как «значения сейчас нет» или «результат отсутствует» по контракту API.

```js
function findUser() {
  return null; // намеренно: пользователь не найден
}

const config = {};
console.log(config.timeout); // undefined: свойства нет
```

Это соглашение, а не автоматическая гарантия языка. В реальном API нужно документировать, может ли поле быть missing, `undefined`, `null` или несколькими вариантами сразу.

#### Проверка необъявленного identifier

У `typeof` есть специальное поведение:

```js
typeof neverDeclared; // "undefined"
```

Обычное чтение `neverDeclared` дало бы `ReferenceError`, но `typeof` позволяет проверить действительно необъявленное имя. При этом результат не отличает его от объявленной переменной со значением `undefined`:

```js
let declared;

typeof declared;      // "undefined"
typeof neverDeclared; // "undefined"
```

Для свойств объекта это вообще не проверка существования. Если важно отличить отсутствующее собственное свойство от существующего со значением `undefined`, используйте `Object.hasOwn(object, key)`.

Связь с 1.1: `typeof` **не обходит TDZ**:

```js
// Намеренно ошибочный пример: чтение binding в TDZ.
typeof later; // ReferenceError
let later;
```

### 🔬 6. Зачем нужны `Symbol` и `BigInt`?

Оба — primitive types, но решают разные задачи.

#### `Symbol`: уникальное primitive value

Каждый обычный вызов `Symbol(description)` создаёт новое уникальное значение:

```js
const first = Symbol("id");
const second = Symbol("id");

console.log(first === second); // false
console.log(typeof first);     // "symbol"
```

Описание помогает отладке, но не определяет identity. Symbols могут быть property keys и помогают избежать случайного совпадения строковых имён:

```js
const cacheKey = Symbol("cache");
const record = { [cacheKey]: "ready" };

console.log(record[cacheKey]); // "ready"
```

`Symbol.for("key")` — отдельный API глобального symbol registry: повторный вызов с тем же ключом возвращает тот же Symbol. Well-known symbols вроде `Symbol.iterator` будут подробно рассмотрены в 1.6.

Для строкового представления Symbol используйте явный `String(symbol)`:

```js
const token = Symbol("token");

String(token); // "Symbol(token)"
// `${token}`; // TypeError: implicit string coercion Symbol запрещена
```

#### `BigInt`: целые числа произвольной величины

`BigInt` хранит целые числа за пределами safe integer range у `Number`:

```js
const exact = 9_007_199_254_740_993n;

typeof exact; // "bigint"
```

BigInt не является «более точным Number для всего». Он не хранит дроби:

```js
5n / 2n; // 2n — дробная часть отбрасывается к нулю
```

Большинство арифметических операций не разрешает смешивать `BigInt` и `Number`:

```js
// Намеренно ошибочный пример: mixed numeric types.
1n + 1; // TypeError
```

Сначала нужно принять явное решение о типе результата:

```js
1n + BigInt(1); // 2n
Number(1n) + 1; // 2, но большое BigInt может потерять точность
```

Сравнения имеют свои правила:

```js
0n === 0; // false: разные types
0n == 0;  // true: loose equality допускает математическое сравнение
1n < 2;   // true: relational comparison умеет сравнить значения
```

Production-правило: внутри одной арифметической модели держите один numeric type. Используйте `BigInt` для целых значений, которые могут выйти за safe integer range, а не для обычных дробных вычислений.

### 🎯 7. Что особенного в `NaN`, `Infinity` и `-0`?

Все три относятся к типу `number`:

```js
typeof NaN;       // "number"
typeof Infinity;  // "number"
typeof -0;        // "number"
```

#### `NaN`

`NaN` означает, что числовая операция не дала осмысленного number result. Например:

```js
Number("not a number"); // NaN
0 / 0;                  // NaN
```

`NaN` распространяется по многим вычислениям:

```js
NaN + 10; // NaN
```

Главная ловушка:

```js
NaN === NaN; // false
NaN !== NaN; // true
```

Проверяйте его через `Number.isNaN()`:

```js
Number.isNaN(NaN);     // true
Number.isNaN("hello"); // false
```

Глобальная функция `isNaN()` сначала выполняет number coercion:

```js
isNaN("hello"); // true: Number("hello") → NaN
isNaN("");      // false: Number("") → 0
```

Поэтому она отвечает на запутанный вопрос «станет ли аргумент `NaN` после преобразования к Number?», а не «является ли значение самим `NaN`». В новом коде почти всегда нужен `Number.isNaN()`.

#### `Infinity` и `-Infinity`

Это числовые значения для положительной и отрицательной бесконечности:

```js
1 / 0;  // Infinity
-1 / 0; // -Infinity

Infinity + 1;        // Infinity
Infinity - Infinity; // NaN
```

Если внешний ввод должен быть обычным конечным числом, одной проверки `!Number.isNaN(value)` недостаточно: `Infinity` не является `NaN`. Используйте `Number.isFinite(value)`.

```js
Number.isFinite(42);       // true
Number.isFinite(Infinity); // false
Number.isFinite("42");    // false, без coercion
```

Глобальная `isFinite()` тоже выполняет coercion, поэтому для валидации типизированного значения обычно хуже.

#### `-0`

IEEE 754 хранит положительный и отрицательный zero:

```js
0 === -0;          // true
Object.is(0, -0);  // false
1 / 0;             // Infinity
1 / -0;            // -Infinity
```

В большинстве бизнес-задач sign zero не важен. Он становится наблюдаемым в отдельных математических вычислениях, визуализации направлений и API, где знак предельного значения несёт смысл. Не нужно заменять каждый `===` на `Object.is`; сначала определите требования.

### 🔬 8. Почему `0.1 + 0.2 !== 0.3` и как сравнивать дроби?

JavaScript `Number` использует 64-bit binary floating-point формат IEEE 754. Некоторые простые десятичные дроби не имеют конечного двоичного представления, поэтому сохраняются ближайшим доступным значением:

```js
0.1 + 0.2;         // 0.30000000000000004
0.1 + 0.2 === 0.3; // false
```

Это не «ошибка JavaScript» в смысле неправильной реализации. Это ограничение конечного floating-point представления, знакомое многим языкам.

#### Почему одного `Number.EPSILON` недостаточно?

`Number.EPSILON` — расстояние между `1` и следующим representable number. Оно полезно около величины `1`, но абсолютная точность меняется вместе с масштабом числа.

Плохое универсальное правило:

```js
Math.abs(a - b) < Number.EPSILON;
```

Оно может быть слишком строгим для больших значений и слишком щедрым или бессмысленным для требований конкретного домена.

Практическая функция сочетает absolute tolerance для чисел около нуля и relative tolerance для масштаба:

```js
function nearlyEqual(
  left,
  right,
  { relativeTolerance = 1e-12, absoluteTolerance = Number.EPSILON } = {},
) {
  if (left === right) {
    return true; // одинаковые finite values, zero и одинаковая Infinity
  }

  if (!Number.isFinite(left) || !Number.isFinite(right)) {
    return false;
  }

  const difference = Math.abs(left - right);
  const scale = Math.max(Math.abs(left), Math.abs(right));

  return difference <= Math.max(
    absoluteTolerance,
    relativeTolerance * scale,
  );
}
```

Числа `1e-12` и `Number.EPSILON` здесь не универсальная истина. Допуски должны идти из требований: пиксели, физические измерения, проценты и научные расчёты имеют разные допустимые ошибки.

#### Как безопаснее работать с деньгами?

Для fixed-scale валютной суммы часто храните integer minor units:

```js
const priceInCents = 1_099;
const quantity = 3;
const totalInCents = priceInCents * quantity; // 3297
```

Но нужен явный контракт:

- какая валюта и сколько у неё minor units;
- когда и как округлять налоги, скидки и распределения;
- остаются ли integers внутри `Number.isSafeInteger()`;
- как сериализуется и валидируется значение на границе API.

Если суммы могут выйти за safe integer range, рассмотрите `BigInt` для integer minor units. Если нужны точные decimal rules с дробным масштабом, процентами и регуляторным округлением, используйте согласованный backend contract и проверенную decimal/fixed-point библиотеку. Не округляйте каждую промежуточную операцию «на глаз» через `toFixed()` — он возвращает строку и не определяет вашу бизнес-политику округления.

### 🎯 9. Что такое truthy, falsy и nullish values?

В boolean-контексте JavaScript выполняет преобразование к boolean. **Falsy** values дают `false`; остальные values — **truthy**.

Полный практический список falsy values:

| Falsy value | Замечание |
|---|---|
| `false` | boolean false |
| `0`, `-0` | оба знака zero |
| `0n` | BigInt zero |
| `NaN` | invalid number result |
| `""` | пустая строка |
| `null` | намеренное отсутствие |
| `undefined` | отсутствие значения |

```js
Boolean(0);          // false
Boolean("0");        // true
Boolean([]);         // true
Boolean({});         // true
Boolean("false");    // true
```

Objects всегда truthy, даже пустой array и wrapper вокруг false:

```js
Boolean(new Boolean(false)); // true: это object
```

**Nullish values** — только `null` и `undefined`. Это не синоним falsy:

```text
falsy   = false, 0, -0, 0n, NaN, "", null, undefined
nullish =                              null, undefined
```

Различие важно для defaults: `0`, `false` и `""` часто являются валидными данными, а не отсутствием.

### 🎯 10. Что значит short-circuit evaluation и что возвращают `||`, `&&`, `??`?

**Короткое замыкание вычисления (short-circuit evaluation)** означает: правый operand вычисляется только тогда, когда он нужен для результата.

Важно: логические операторы возвращают один из operands, а не обязательно boolean.

#### `||`: первое truthy или последнее значение

```js
"Ada" || "Anonymous"; // "Ada"
"" || "Anonymous";    // "Anonymous"
0 || 10;              // 10
```

Если левый operand truthy, `||` возвращает его и не вычисляет правый. Иначе вычисляет и возвращает правый.

```js
let calls = 0;

function fallback() {
  calls += 1;
  return "default";
}

"ready" || fallback();
console.log(calls); // 0
```

`||` подходит, когда **любое falsy значение действительно означает отсутствие или отказ**. Например, выбрать первый непустой label. Для числового zero, `false` или пустой строки как валидных данных он часто неверен.

#### `&&`: первое falsy или последнее значение

```js
true && "render"; // "render"
0 && expensive(); // 0; expensive() не вызывается
```

`&&` полезен для условного вычисления, но длинные цепочки могут скрывать бизнес-условие. В production-коде иногда ясный `if` лучше компактности.

#### `??`: правый operand только для nullish

```js
0 ?? 10;          // 0
false ?? true;    // false
"" ?? "default"; // ""
null ?? "default";      // "default"
undefined ?? "default"; // "default"
```

Поэтому для default value вопрос звучит так:

```text
||  → считать отсутствием любое falsy?
??  → считать отсутствием только null / undefined?
```

Реальный bug:

```js
function normalizeSettings(input) {
  return {
    retries: input.retries || 3,
    animations: input.animations || true,
  };
}

normalizeSettings({ retries: 0, animations: false });
// Ошибка: { retries: 3, animations: true }
```

Исправление:

```js
function normalizeSettings(input) {
  return {
    retries: input.retries ?? 3,
    animations: input.animations ?? true,
  };
}
```

<details>
<summary>🔬 Точная деталь: смешивание <code>??</code> с <code>||</code>/<code>&amp;&amp;</code></summary>

JavaScript запрещает смешивать `??` с `||` или `&&` в одной цепочке без явных parentheses:

```js
// Намеренно ошибочный пример: SyntaxError.
const value = left ?? middle || fallback;
```

Нужно обозначить intended grouping:

```js
const firstValue = (left ?? middle) || fallback;
// или
const secondValue = left ?? (middle || fallback);
```

Это не просто вопрос precedence: синтаксический запрет заставляет автора сделать неоднозначное намерение видимым.

</details>

Операторы `||=` и `??=` применяют те же критерии к условному присваиванию. Используйте их только если mutation binding/property соответствует контракту.

### 🎯 11. Что делает optional chaining и где прекращается защита?

**Опциональная цепочка (optional chaining)** `?.` останавливает непрерывную цепочку доступа, если значение слева равно `null` или `undefined`, и возвращает `undefined` вместо ошибки.

```js
const city = user?.address?.city;
const firstItem = response?.items?.[0];
const result = callbacks.onDone?.();
```

Это не «подавить любую ошибку». `?.` проверяет только конкретное значение слева на nullish.

#### Trap 1: каждый потенциально отсутствующий шаг должен быть защищён

```js
const user = { profile: null };

user?.profile.name;  // TypeError: profile существует как null,
                     // а перед .name нет ?.
user?.profile?.name; // undefined
```

В выражении `base?.a.b` short-circuit первого `?.` распространяется по непрерывной цепочке, если `base` nullish. Но если `base` существует и `a` равен nullish, обычный `.b` всё равно бросит ошибку.

#### Trap 2: grouping разрывает continuous chain

```js
const data = null;

data?.a.b;       // undefined: вся непрерывная цепочка остановлена на data
(data?.a).b;     // TypeError: результат undefined, затем отдельный .b
```

Parentheses здесь логически создают промежуточный результат и следующий обычный доступ.

#### Trap 3: optional call проверяет отсутствие, но не callability

```js
const api = { onDone: "not a function" };

api.onDone?.(); // TypeError: свойство существует, но не callable
```

Также важно различать:

```js
api?.onDone();  // проверяет api; существующий api без onDone даст TypeError
api.onDone?.(); // проверяет onDone; undefined вернёт undefined
```

#### Trap 4: root identifier всё равно должен разрешиться

```js
// Намеренно ошибочный пример: identifier не объявлен.
undeclaredRoot?.value; // ReferenceError
```

Optional chaining не заменяет `typeof undeclaredRoot` и не обходит TDZ.

#### Trap 5: short-circuit пропускает side effects только внутри цепочки

```js
let index = 0;
const items = null;

items?.[index++];
console.log(index); // 0
```

Computed key не вычисляется, потому что цепочка остановилась. Это полезно, но скрытые side effects внутри property access обычно ухудшают читаемость.

#### Trap 6: не все позиции синтаксически допустимы

Optional chain нельзя использовать как assignment target; `new` и tagged template имеют отдельные запреты:

```js
// Намеренно ошибочные примеры: SyntaxError.
user?.name = "Ada";
new Constructor?.();
tag?.`text`;
```

#### Что `?.` не ловит?

- исключение getter-а;
- ошибку внутри реально вызванной функции;
- неверный тип существующего метода;
- отсутствие обязательных данных, которое должно считаться ошибкой контракта.

Production guidance: используйте `?.` для действительно optional границ. Если поле обязано существовать, явная ошибка или validation часто полезнее тихого `undefined`.

### 🎯 12. Какие семантики равенства есть в JavaScript?

Для интервью удобно сравнивать четыре алгоритма:

| Семантика | Доступ | Coercion | `NaN` с `NaN` | `+0` с `-0` | Objects |
|---|---|---:|---:|---:|---|
| Loose equality | `==` | да | false | true | одна identity после возможного ToPrimitive |
| Strict equality | `===` | нет | false | true | одна identity |
| SameValue | `Object.is()` | нет | true | false | одна identity |
| SameValueZero | built-ins | нет | true | true | одна identity |

#### `===`: современный default

Strict equality не преобразует разные types:

```js
0 === "0";          // false
null === undefined; // false
```

Для одинаковых primitive types сравниваются значения с особыми number rules. Для objects — identity:

```js
const first = { id: 1 };
const alias = first;

first === alias;       // true
first === { id: 1 };   // false
```

#### `Object.is()`: SameValue

`Object.is()` совпадает с `===` в большинстве обычных случаев, но меняет два numeric edge cases:

```js
Object.is(NaN, NaN); // true
Object.is(0, -0);    // false
```

Используйте его, когда эти различия соответствуют нужной семантике. Это не deep equality.

#### SameValueZero

SameValueZero считает `NaN` равным самому себе, но не различает signs of zero:

```js
[NaN].includes(NaN); // true
new Set([NaN, NaN]).size; // 1
```

Эту семантику используют:

- `Array.prototype.includes()` и `TypedArray.prototype.includes()`;
- keys в `Map`;
- values в `Set`.

Для контраста `indexOf()` использует strict-equality-like comparison и не находит `NaN`:

```js
[NaN].indexOf(NaN); // -1
```

Практическая карта:

```text
обычное сравнение в приложении → ===
нужно NaN == NaN и различать signed zero → Object.is
поиск/ключи built-in коллекций → знать SameValueZero
структурное сравнение objects → отдельный доменный алгоритм, не один из этих operators
```

### 🎯 13. Когда `==` преобразует типы и можно ли его использовать осознанно?

**Нестрогое равенство (loose equality)** пытается привести operands к совместимой форме по конкретному алгоритму. Оно не означает «сравнить после простого `Number()` для всего».

Примеры:

```js
"5" == 5;            // true
false == 0;          // true
null == undefined;   // true
null == 0;           // false
0n == 0;             // true
```

Практическая модель для common cases:

1. Одинаковые types сравниваются почти как `===`.
2. `null` loosely equal только `undefined` (и редкой web-legacy экзотике `document.all`).
3. Boolean превращается в Number: `false → 0`, `true → 1`.
4. String рядом с Number преобразуется к Number.
5. Object рядом с primitive проходит `ToPrimitive`, затем сравнение продолжается.
6. Symbol не превращается автоматически в другую primitive category для равенства.

#### Осознанный `value == null`

Один распространённый намеренный шаблон:

```js
if (value == null) {
  // value — null или undefined
}
```

Он компактен и точно использует специальное правило `null`/`undefined`. Но команда должна считать такой exception читаемым и закрепить его linting convention. Если неоднозначность нежелательна, пишите явно:

```js
if (value === null || value === undefined) {
  // ...
}
```

Production guidance: используйте `===` по умолчанию. `==` оставляйте для редкого осознанного контракта, а не для случайного удобства.

<details>
<summary>🧓 Legacy: <code>document.all</code></summary>

Браузеры сохраняют необычное поведение `document.all` ради совместимости: он falsy, `typeof document.all === "undefined"` и он loosely equal `null`/`undefined`, хотя технически это специальный host object.

Это нужно узнавать как web-legacy oddity, но нельзя использовать как production pattern или переносить на обычные objects.

</details>

### 🎯 14. Что такое explicit и implicit coercion?

**Преобразование типов (type coercion)** — получение значения другого типа по правилам языка.

- **Явное преобразование (explicit coercion)** прямо видно в коде: `Boolean(value)`, `Number(text)`, `String(id)`.
- **Неявное преобразование (implicit coercion)** запускает оператор или контекст: `if (value)`, `"5" * 2`, `value == 0`.

Explicit не автоматически безопасно, а implicit не автоматически плохо. Важнее, очевиден ли контракт и обработаны ли ошибки.

#### Преобразование к boolean

```js
Boolean("");   // false
Boolean("0");  // true
Boolean(0);    // false
Boolean([]);   // true
```

`Boolean(value)` и `!!value` дают один primitive boolean. В коде `Boolean()` обычно яснее при преобразовании данных; `!!` часто встречается как короткая идиома.

Boolean coercion не вызывает `valueOf()` или `toString()` у object. Любой обычный object truthy независимо от содержимого.

#### Преобразование к Number

| Input | `Number(input)` |
|---|---:|
| `undefined` | `NaN` |
| `null` | `0` |
| `true` / `false` | `1` / `0` |
| `"42"` | `42` |
| `""` или whitespace-only string | `0` |
| `"42px"` | `NaN` |
| `1n` | `1`, с риском потери точности для больших BigInt |
| `Symbol()` | `TypeError` |

```js
Number(" 42 "); // 42
Number("");     // 0
Number("42px"); // NaN
```

Unary plus обычно выполняет такое же number coercion, но не принимает BigInt:

```js
+"42"; // 42
// +1n; // TypeError
```

Для пользовательского ввода сначала определите, разрешены ли empty string, whitespace, decimal format, signs и `Infinity`. Слепой `Number(input)` может принять больше, чем разрешает ваш продукт.

#### Преобразование к String

```js
String(null);        // "null"
String(undefined);   // "undefined"
String(42);          // "42"
String(1n);          // "1"
String(Symbol("x")); // "Symbol(x)"
```

`String(value)` полезен именно тем, что намерение видно и Symbol обрабатывается безопасно. Не используйте `"" + value` как универсальную функцию преобразования: operator `+` сначала делает primitive coercion и может вести себя иначе для объектов и Symbols.

### 🎯 15. Почему оператор `+` особенно опасен для mental model?

У binary `+` две роли:

1. string concatenation;
2. numeric addition для двух Numbers или двух BigInts.

Упрощённый алгоритм:

```text
left  → ToPrimitive
right → ToPrimitive
если хотя бы один primitive — String → оба к String → concatenation
иначе оба к numeric type
  два Number → number addition
  два BigInt → bigint addition
  смесь Number / BigInt → TypeError
```

Примеры:

```js
1 + 2;          // 3
"1" + 2;        // "12"
1 + "2";        // "12"
true + 1;       // 2
null + 1;       // 1
undefined + 1;  // NaN
1n + 2n;        // 3n
"1" + 2n;       // "12"
// 1n + 2;      // TypeError
```

Порядок и grouping важны:

```js
1 + 2 + "3"; // "33": сначала 3, затем concatenation
"1" + 2 + 3; // "123": после первой строки дальше concatenation
```

Другие arithmetic operators обычно требуют numeric coercion:

```js
"5" - 2; // 3
"5" * 2; // 10
"5" / 2; // 2.5
```

Это одна из причин не использовать implicit coercion как форматирование данных. Явное `Number(input)` или `String(value)` делает boundary видимой.

### 🎯 16. Как работают сравнения `<`, `>`, `<=`, `>=` с разными типами?

Relational comparison — не `==` с другим знаком. Он сначала получает primitive values. Если оба primitives — strings, выполняется лексикографическое сравнение последовательностей UTF-16 code units. Иначе используется numeric comparison с правилами для Number/BigInt.

```js
"2" < "10"; // false: сравниваются строки, "2" идёт после "1"
"2" < 10;   // true: string преобразуется к number
2n < 2.5;   // true: relational comparison разрешает Number/BigInt
```

Знаменитая ловушка показывает, что equality и ordering идут разными путями:

```js
null == 0;  // false
null > 0;   // false
null >= 0;  // true
```

Для `>=` relational comparison приводит `null` к `0`; для `==` специальное правило `null` не считает его равным number zero.

С `NaN` ordering не даёт обычного порядка:

```js
NaN < 1;  // false
NaN > 1;  // false
NaN === NaN; // false
```

Production guidance:

- normalise данные на границе системы;
- не смешивайте numeric strings и numbers глубоко внутри бизнес-логики;
- для сортировки явно документируйте comparator и поведение invalid values;
- не выводите смысл из одной проверки вроде `value >= 0`, если `value` мог быть `null` или string.

### 🔬 17. Как `ToPrimitive`, `valueOf()` и `toString()` связаны с coercion?

Когда оператору нужен primitive, а он получает object, запускается абстрактная операция **`ToPrimitive`**.

Практическая модель:

1. Если у object есть метод `[Symbol.toPrimitive]`, он получает hint `"string"`, `"number"` или `"default"`.
2. Иначе язык пробует обычные методы в порядке, зависящем от hint.
3. Результат должен быть primitive; возвращённый object не завершает преобразование.
4. Полученный primitive затем может пройти `ToString`, `ToNumber` или другую операцию контекста.

| Контекст | Hint / обычный порядок |
|---|---|
| string coercion | `"string"`: `toString()` → `valueOf()` |
| number coercion | `"number"`: `valueOf()` → `toString()` |
| binary `+`, object в `==` | `"default"`: обычно как number; `Date` — особый string-like case |

#### Обычный object

```js
const amount = {
  valueOf() {
    return 7;
  },
  toString() {
    return "seven";
  },
};

Number(amount); // 7: number hint → valueOf first
String(amount); // "seven": string hint → toString first
amount + 1;     // 8: default hint, valueOf returns 7
```

#### `[Symbol.toPrimitive]` имеет приоритет

```js
const value = {
  [Symbol.toPrimitive](hint) {
    if (hint === "number") return 10;
    if (hint === "string") return "ten";
    return 20;
  },
};

+value;         // 10
String(value);  // "ten"
value + 1;      // 21
```

Если `[Symbol.toPrimitive]` возвращает object, возникает `TypeError`.

#### Почему `[] == ![]` даёт `true`?

Это умеренно полезная interview-проверка модели, но плохой production style:

```js
[] == ![]; // true
```

Разбор:

1. `[]` — truthy object, поэтому `![]` даёт `false`.
2. В loose equality boolean `false` превращается в number `0`.
3. Левый array рядом с primitive проходит `ToPrimitive`: пустой array через `toString()` даёт `""`.
4. `""` рядом с number превращается в `0`.
5. `0 == 0` → `true`.

Ценность puzzle — проверить pipeline. В реальном коде не нужно писать выражения, правильность которых зависит от пяти скрытых шагов.

### 🎯 18. Как системно решать output-prediction задачи на values и coercion?

Не пытайтесь помнить все puzzles как отдельные факты. Для каждого оператора задайте один и тот же набор вопросов.

#### Шаг 1. Выпишите исходные types и object identities

```js
const a = [];
const b = a;
const c = [];
```

Здесь `a`/`b` разделяют identity, `c` — другой object.

#### Шаг 2. Назовите оператор и его equality/coercion semantics

- `===` → без coercion;
- `Object.is` → SameValue;
- `includes` / `Set` / `Map` → SameValueZero;
- `==` → IsLooselyEqual;
- `+` → ToPrimitive, затем string либо numeric branch;
- `<`/`>=` → relational comparison;
- `||` → falsy;
- `??` / `?.` → nullish.

#### Шаг 3. Если участвует object, выполните `ToPrimitive`

Проверьте `[Symbol.toPrimitive]`, затем соответствующий порядок `valueOf()`/`toString()`.

#### Шаг 4. Выполните primitive conversion

Запишите промежуточные values явно:

```text
false → 0
""    → 0 в number context
[]    → "" через ToPrimitive
```

#### Шаг 5. Только теперь примените оператор

Не перескакивайте сразу к ответу. Например:

```js
const left = [1];
const result = left + 2;
```

```text
[1] → ToPrimitive → "1"
"1" + 2 → string branch
result → "12"
```

#### Шаг 6. Назовите production-вывод

Хороший интервью-ответ заканчивается не puzzle, а инженерным правилом: normalize boundaries, используйте `===`, выбирайте `??` для nullish default, не полагайтесь на скрытую object coercion.

---

## Краткий справочник

### Primitives и objects

| Вопрос | Primitive | Object |
|---|---|---|
| Внутреннее изменение | значение immutable | состояние часто mutable |
| Identity | сравнение по primitive value и алгоритму | сравнение по identity |
| Присваивание | копируется primitive value | копируется value, обозначающее тот же object |
| `const` | нельзя переназначить binding | нельзя переназначить binding; object всё ещё может мутировать |

### Absence и defaults

| Проверка | Критерий |
|---|---|
| `if (value)` | truthy/falsy |
| `value || fallback` | fallback для любого falsy |
| `value ?? fallback` | fallback только для `null`/`undefined` |
| `value?.property` | stop только для `null`/`undefined` слева |

### Equality

| Нужно | Инструмент |
|---|---|
| обычное сравнение без coercion | `===` |
| считать `NaN` равным себе и различить signed zero | `Object.is()` |
| понять `includes`, `Set`, `Map` | SameValueZero |
| намеренно проверить `null` или `undefined` вместе | `value == null` по командной convention либо явные `===` |
| сравнить object content | отдельный доменный comparator |

## Типичные ошибки

1. **«Тип принадлежит переменной навсегда».** Runtime type принадлежит текущему value.
2. **«`const` делает object immutable».** Он запрещает reassignment binding.
3. **«Spread полностью копирует object».** Это shallow copy; nested objects могут оставаться общими.
4. **«Objects передаются by reference».** Аргумент передаётся by value; copied object value обозначает тот же identity.
5. **«`typeof null` доказывает, что null — object».** Это historical oddity оператора.
6. **«`typeof x === "undefined"` всегда означает, что variable не объявлена».** Объявленный `undefined` выглядит так же; TDZ бросает ошибку.
7. **«`isNaN` проверяет именно NaN».** Глобальная функция сначала coerces; `Number.isNaN` не coerces.
8. **«Любая ошибка floating point исправляется Number.EPSILON».** Tolerance зависит от масштаба и домена.
9. **«Все objects truthy, кроме пустых».** Пустые array/object тоже truthy.
10. **«`||` и `??` взаимозаменяемы».** Первый реагирует на все falsy, второй — только на nullish.
11. **«Optional chaining ловит любую ошибку дальше».** Он защищает конкретную непрерывную nullish chain.
12. **«`Object.is` — deep equality».** Для objects он по-прежнему сравнивает identity.
13. **«`==` просто приводит обе стороны к Number».** Алгоритм имеет отдельные ветви для nullish, booleans, strings, BigInt и objects.
14. **«`+` всегда складывает».** После ToPrimitive string operand выбирает concatenation.

## Ловушки на интервью

### Primitive immutability против reassignment

Строка не меняется от `toUpperCase()`, но binding `let` можно переназначить новой строкой. Object может мутировать даже через `const`.

### Shared mutation после shallow copy

Сначала сравните outer identity, затем отдельно identity каждого nested object.

### `NaN`, signed zero и разные equality algorithms

```js
NaN === NaN;              // false
Object.is(NaN, NaN);      // true
0 === -0;                 // true
Object.is(0, -0);         // false
[NaN].includes(NaN);      // true
```

### Defaulting сохраняет или уничтожает валидные falsy values

Проверьте `0`, `false`, `""` и `NaN` отдельно. `??` сохраняет их все.

### Optional chain заканчивается раньше, чем кажется

`(object?.a).b` уже не одна непрерывная chain. `object?.method()` и `object.method?.()` защищают разные значения.

### Object equality

Два literal objects никогда не становятся одной identity только потому, что их keys/values одинаковы.

### Coercion puzzle

Разбирайте `[] == ![]` только через промежуточные steps и сразу отмечайте: это проверка mental model, не production recommendation.

## Production guidance

| Ситуация | Рекомендация |
|---|---|
| Обычное equality | `===`; выберите отдельный comparator для domain objects |
| Missing default | `??`, если `0`/`false`/`""` валидны |
| Optional data | `?.` только на действительно optional boundary |
| External numeric input | явный parse/validation; отклонить `NaN` и unwanted infinities |
| Floating comparison | domain tolerance; absolute + relative where appropriate |
| Money | integer minor units или проверенная decimal model + explicit rounding |
| Shared objects | документировать mutation; копировать нужные уровни, а не надеяться на spread |
| Big integers | единая BigInt model; не смешивать арифметику с Number |
| Coercion | explicit at boundaries; implicit only when idiom очевиден |

---

## Вопросы для активного воспроизведения

Эталонные ответы находятся в отдельном файле. Сначала ответьте вслух или письменно без подсказки.

### Базовый уровень (Junior)

- [`JS-VALUES-Q01`](../../question-bank/by-domain/01-javascript-and-async-programming.md#js-values-q01) — primitives, objects и type of value.
- [`JS-VALUES-Q02`](../../question-bank/by-domain/01-javascript-and-async-programming.md#js-values-q02) — immutability, mutation и reassignment.
- [`JS-VALUES-Q03`](../../question-bank/by-domain/01-javascript-and-async-programming.md#js-values-q03) — pass-by-value object argument.
- [`JS-VALUES-Q04`](../../question-bank/by-domain/01-javascript-and-async-programming.md#js-values-q04) — `typeof`, `null`, `undefined` и TDZ.
- [`JS-VALUES-Q05`](../../question-bank/by-domain/01-javascript-and-async-programming.md#js-values-q05) — `Symbol` и `BigInt`.
- [`JS-VALUES-Q06`](../../question-bank/by-domain/01-javascript-and-async-programming.md#js-values-q06) — `NaN`, infinities и `-0`.
- [`JS-VALUES-Q07`](../../question-bank/by-domain/01-javascript-and-async-programming.md#js-values-q07) — truthy, falsy и nullish.
- [`JS-VALUES-Q08`](../../question-bank/by-domain/01-javascript-and-async-programming.md#js-values-q08) — `||`, `??` и defaults.

### Средний уровень (Mid)

- [`JS-VALUES-Q09`](../../question-bank/by-domain/01-javascript-and-async-programming.md#js-values-q09) — short-circuit и side effects.
- [`JS-VALUES-Q10`](../../question-bank/by-domain/01-javascript-and-async-programming.md#js-values-q10) — optional chaining traps.
- [`JS-VALUES-Q11`](../../question-bank/by-domain/01-javascript-and-async-programming.md#js-values-q11) — equality semantics matrix.
- [`JS-VALUES-Q12`](../../question-bank/by-domain/01-javascript-and-async-programming.md#js-values-q12) — object identity и shallow copy.
- [`JS-VALUES-Q13`](../../question-bank/by-domain/01-javascript-and-async-programming.md#js-values-q13) — `Number.isNaN()` против `isNaN()`.
- [`JS-VALUES-Q14`](../../question-bank/by-domain/01-javascript-and-async-programming.md#js-values-q14) — floating-point и money bug.
- [`JS-VALUES-Q15`](../../question-bank/by-domain/01-javascript-and-async-programming.md#js-values-q15) — explicit conversion table.
- [`JS-VALUES-Q16`](../../question-bank/by-domain/01-javascript-and-async-programming.md#js-values-q16) — output prediction для `+`.
- [`JS-VALUES-Q17`](../../question-bank/by-domain/01-javascript-and-async-programming.md#js-values-q17) — relational comparison с coercion.
- [`JS-VALUES-Q18`](../../question-bank/by-domain/01-javascript-and-async-programming.md#js-values-q18) — `ToPrimitive`, `valueOf()` и `toString()`.

### Продвинутый уровень (Senior)

- [`JS-VALUES-Q19`](../../question-bank/by-domain/01-javascript-and-async-programming.md#js-values-q19) — policy для `==` в code review.
- [`JS-VALUES-Q20`](../../question-bank/by-domain/01-javascript-and-async-programming.md#js-values-q20) — SameValueZero в коллекциях.
- [`JS-VALUES-Q21`](../../question-bank/by-domain/01-javascript-and-async-programming.md#js-values-q21) — ревью shared mutation.
- [`JS-VALUES-Q22`](../../question-bank/by-domain/01-javascript-and-async-programming.md#js-values-q22) — validation numeric pipeline.
- [`JS-VALUES-Q23`](../../question-bank/by-domain/01-javascript-and-async-programming.md#js-values-q23) — реализация scale-aware comparison.
- [`JS-VALUES-Q24`](../../question-bank/by-domain/01-javascript-and-async-programming.md#js-values-q24) — integrated coercion challenge.

## Как объяснить тему на интервью за 30–60 секунд

### Primitives, objects и `const`

> В JavaScript type принадлежит value. Primitives — `undefined`, `null`, boolean, number, bigint, string и symbol — immutable: операция создаёт новое primitive value. Objects имеют identity и обычно mutable state. `const` фиксирует binding, а не object, поэтому `const user = {}` можно мутировать, но нельзя переназначить. При присваивании object value копируется значение, ведущее к той же identity, поэтому возможна shared mutation.

### Pass-by-value

> JavaScript передаёт аргументы по value. Когда аргумент object, параметр получает копию object value, которая указывает на тот же object identity. Поэтому mutation через параметр видна вызывающему коду, но reassignment параметра не меняет binding вызывающей функции. Именно поэтому JavaScript неточно называть pass-by-reference.

### `===`, `Object.is` и SameValueZero

> Для обычного кода default — `===`: без coercion, objects сравниваются по identity, `NaN` не равен себе, а `+0` и `-0` равны. `Object.is` использует SameValue: считает `NaN` равным себе и различает signed zero. SameValueZero тоже считает `NaN` равным себе, но объединяет zero; его используют `includes`, `Set` и `Map`.

### `||`, `??` и optional chaining

> `||` возвращает fallback для любого falsy value, поэтому может потерять валидные `0`, `false` и empty string. `??` использует fallback только для `null` или `undefined`. Optional chaining тоже реагирует только на nullish и останавливает одну непрерывную chain. Grouping может её разорвать, а существующий, но не callable method всё равно даст `TypeError`.

### Coercion и `+`

> Coercion бывает explicit и implicit. Если operator получает object там, где нужен primitive, сначала работает `ToPrimitive`: приоритет у `Symbol.toPrimitive`, затем порядок `valueOf`/`toString` зависит от hint. Binary `+` после этого выбирает string concatenation, если хотя бы один primitive — string; иначе выполняет Number или BigInt addition. Поэтому я нормализую types на system boundaries и не строю production logic на скрытых цепочках coercion.

## Упражнения

Открывайте только файл с условиями; решения хранятся отдельно.

1. [`JS-VALUES-EX01`](../../exercises/prompts/by-domain/01-javascript-and-async-programming.md#js-values-ex01) — восстановить карту values, `typeof` и falsy.
2. [`JS-VALUES-EX02`](../../exercises/prompts/by-domain/01-javascript-and-async-programming.md#js-values-ex02) — предсказать values, types, equality и coercion errors.
3. [`JS-VALUES-EX03`](../../exercises/prompts/by-domain/01-javascript-and-async-programming.md#js-values-ex03) — объяснить pass-by-value через bindings.
4. [`JS-VALUES-EX04`](../../exercises/prompts/by-domain/01-javascript-and-async-programming.md#js-values-ex04) — исправить defaulting и optional chaining.
5. [`JS-VALUES-EX05`](../../exercises/prompts/by-domain/01-javascript-and-async-programming.md#js-values-ex05) — отладить numeric validation и money calculation.
6. [`JS-VALUES-EX06`](../../exercises/prompts/by-domain/01-javascript-and-async-programming.md#js-values-ex06) — провести code review shared defaults и shallow copy.
7. [`JS-VALUES-EX07`](../../exercises/prompts/by-domain/01-javascript-and-async-programming.md#js-values-ex07) — разобрать coercion puzzle через `ToPrimitive`.
8. [`JS-VALUES-EX08`](../../exercises/prompts/by-domain/01-javascript-and-async-programming.md#js-values-ex08) — реализовать typed normalization boundary.
9. [`JS-VALUES-EX09`](../../exercises/prompts/by-domain/01-javascript-and-async-programming.md#js-values-ex09) — реализовать domain-aware equality и дедупликацию.
10. [`JS-VALUES-EX10`](../../exercises/prompts/by-domain/01-javascript-and-async-programming.md#js-values-ex10) — стабилизировать checkout boundary в integrated interview challenge.

## Интервью-челлендж

Выполните [`JS-VALUES-EX10`](../../exercises/prompts/by-domain/01-javascript-and-async-programming.md#js-values-ex10), не запуская код до полного прогноза.

Нужно будет:

1. нарисовать object identities и shared nested references;
2. назвать equality semantics каждой операции;
3. проследить short-circuit и optional chain;
4. разложить implicit coercion на `ToPrimitive` и последующие conversions;
5. найти data-validation и money bugs;
6. предложить production-safe boundary и объяснить решение за три минуты.

Отдельно оценивайте conceptual understanding, terminology recall, точность outputs, исправление кода и ясность объяснения.

## Чек-лист готовности

### Объяснить

- [ ] Я различаю type of value и mutability/reassignment binding.
- [ ] Я объясняю primitive immutability, object identity и shared references.
- [ ] Я могу точно сказать, почему JavaScript pass-by-value.
- [ ] Я объясняю `typeof null` как historical oddity, а не type truth.
- [ ] Я сравниваю `===`, `Object.is` и SameValueZero за 30–60 секунд.
- [ ] Я описываю practical `ToPrimitive` pipeline.

### Узнать и предсказать

- [ ] Я предсказываю mutation после alias и shallow copy.
- [ ] Я узнаю все falsy и отличаю их от nullish.
- [ ] Я предсказываю `||`, `&&`, `??` и `?.` с short-circuit side effects.
- [ ] Я различаю `NaN`, infinities и signed zero.
- [ ] Я решаю output tasks на `==`, `===`, `Object.is`, `includes` и `+` пошагово.

### Реализовать

- [ ] Я нормализую external input явно и проверяю `NaN`/Infinity.
- [ ] Я выбираю integer/decimal model и rounding contract для денег.
- [ ] Я реализую scale-aware floating comparison с domain tolerances.
- [ ] Я копирую именно нужные уровни object graph.

### Отладить

- [ ] Я нахожу потерю валидных falsy values из-за `||`.
- [ ] Я нахожу разрыв optional chain и неверный optional call.
- [ ] Я отличаю shared mutation от reassignment.
- [ ] Я трассирую `ToPrimitive`, `valueOf()` и `toString()` перед operator result.

### Провести ревью кода

- [ ] Я отделяю correctness bug от stylistic preference в вопросах coercion.
- [ ] Я проверяю equality semantics, ownership mutable objects и input boundaries.
- [ ] Я не предлагаю JSON/deep clone или `Object.is` как универсальное решение.
- [ ] Я документирую intentional `== null`, если команда допускает этот pattern.

## Связанные inventory IDs

| Inventory ID | Покрытие в этой главе |
|---|---|
| `JS-05` | primitives/objects, immutability, identity, mutation, reassignment, shared references и shallow copy boundary |
| `JS-06` | `typeof`, historical `null`, `undefined`, undeclared identifiers, TDZ link, `Symbol`, `BigInt` |
| `JS-07` | `NaN`, `Number.isNaN`, infinities, `-0`, floating precision, tolerances и money guidance |
| `JS-08` | truthy/falsy, nullish, boolean contexts и defaulting |
| `JS-09` | `==`, `===`, `Object.is`, SameValueZero и object identity |
| `JS-10` | explicit/implicit coercion, `+`, relational comparison, `ToPrimitive`, hooks и output prediction |
| `JS-11` | pass-by-value и object reference as copied value |
| `JS-40` | short-circuit, `||`, `??`, optional chaining и traps |

Ограниченные cross-references:

- `JS-01`: `const` упомянут только для отделения immutable binding от mutable object; declaration lifecycle остаётся в 1.1.
- `JS-21`: practical immutability используется как следствие identity, но pure functions и functional patterns остаются в 1.3.
- `JS-34`: shallow copy показан только для shared identity; deep copy и `structuredClone` остаются в 1.5.
- `JS-37`: базовый `Symbol` нужен как primitive и coercion hook; well-known symbols остаются в 1.6.

## Источники

Первичные и авторитетные источники:

- [ECMAScript 2026 — ECMAScript Language Types](https://tc39.es/ecma262/2026/multipage/ecmascript-data-types-and-values.html#sec-ecmascript-language-types)
- [ECMAScript 2026 — `ToPrimitive` and `OrdinaryToPrimitive`](https://tc39.es/ecma262/2026/multipage/abstract-operations.html#sec-toprimitive)
- [ECMAScript 2026 — `ToBoolean`](https://tc39.es/ecma262/2026/multipage/abstract-operations.html#sec-toboolean)
- [ECMAScript 2026 — Testing and Comparison Operations](https://tc39.es/ecma262/2026/multipage/abstract-operations.html#sec-testing-and-comparison-operations)
- [ECMAScript 2026 — Addition operator](https://tc39.es/ecma262/2026/multipage/ecmascript-language-expressions.html#sec-addition-operator-plus)
- [MDN — JavaScript data types and data structures](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Data_structures)
- [MDN — `typeof`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/typeof)
- [MDN — `BigInt`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/BigInt)
- [MDN — `NaN` and `Number.isNaN()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number/isNaN)
- [MDN — `Number.EPSILON`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number/EPSILON)
- [MDN — Equality comparisons and sameness](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Equality_comparisons_and_sameness)
- [MDN — Nullish coalescing](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Nullish_coalescing)
- [MDN — Optional chaining](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Optional_chaining)
- [MDN — Addition](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Addition)
- [MDN — `Symbol.toPrimitive`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Symbol/toPrimitive)

Дата проверки источников: **2026-10-01**.
