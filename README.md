<div dir="rtl">

<p align="center">
  <a href="https://github.com/kettanaito/naming-cheatsheet">
    <img src="./naming-cheatsheet.png" alt="Naming cheatsheet" />
  </a>
</p>

# قواعد نام گذاری توابع و متغیر‌ها

- [از زبان انگلیسی استفاده کنید](#english-language)
- [قاعده نام گذاری مشخص داشته باشید](#naming-convention)
- [از قانون S-I-D پیروی کنید](#s-i-d)
- [خلاصه نکنید](#avoid-contractions)
- [از تکرار دوری کنید](#avoid-context-duplication)
- [از طریق نام نتیجه را معلوم کنید](#reflect-the-expected-result)
- [نام گذاری توابع](#naming-functions)
  - [الگوی A / HC / LC](#ahclc-pattern)
    - [در نام از فعل استفاده کنید](#actions)
    - [نام باید عملکرد را مشخص کند](#context)
    - [پیشوندها](#prefixes)
- [از کلمات مفرد و جمع در نام استفاده کنید](#singular-and-plurals)

---

انتخاب نام کار پیچیده ای است و این راهنما قرار است کار را ساده تر کند.

دقت کنید ممکن است در زبان های مختلف این موضوع متفاوت باشد اما در این صفحه مثال ها با جاوااسکریپت نمایش داده شده است.


## از زبان انگلیسی استفاده کنید

از زبان انگلیسی برای نام گذاری متغیرها و تابع ها استفاده کنید.

</div>

```js
/* Bad */
const primerNombre = 'Gustavo'
const amigos = ['Kate', 'John']

/* Good */
const firstName = 'Gustavo'
const friends = ['Kate', 'John']
```

<div dir="rtl">

> چه بخواهیم و چه نخواهیم ، انگلیسی زبان غالب در برنامه نویسی است: نحو تمام زبان های برنامه نویسی به انگلیسی ، و همچنین مستندات و مطالب آموزشی بی شماری با این زبان نوشته شده است. با نوشتن کد خود به انگلیسی ، انسجام آن را به طرز چشمگیری افزایش می دهید.


## قاعده نام گذاری مشخص داشته باشید

یگی از قواعد نام گذاری را برای خود انتخاب کنید و طبق آن پیش بروید. از بین قواعدی مثل `camelCase`, `PascalCase`, `snake_case` و ... یکی را انتخاب کنید.

</div>

```js
/* Bad */
const page_count = 5
const shouldUpdate = true

/* Good */
const pageCount = 5
const shouldUpdate = true

/* Good as well */
const page_count = 5
const should_update = true
```

<div dir="rtl">

## از قانون S-I-D پیروی کنید

یک نام باید کوتاه، بصری و توصیفی باشد:

- **کوتاه یا Short**. نام باید کوتاه باشد تا در طولانی مدت به خاطر بماند
- **بصری یا Intuitive**. یک نام باید به صورت طبیعی قابل خواندن باشد و این موضوع باید برای همه این طور باشد
- **توصیفی یا Descriptive**. یک نام باید به کارآمد ترین روش با کاری که انجام می دهد مشخص شده باشد

</div>

```js
/* Bad */
const a = 5 // "a" could mean anything
const isPaginatable = a > 10 // "Paginatable" sounds extremely unnatural
const shouldPaginatize = a > 10 // Made up verbs are so much fun!

/* Good */
const postCount = 5
const hasPagination = postCount > 10
const shouldPaginate = postCount > 10 // alternatively
```

<div dir="rtl">

## خلاصه نکنید

از خلاصه کردن پرهیز کنید دلیل این موضوع هم این است که خلاصه کردن باعث کاهش خوانایی متن خواهد شد پس حتما در ارتباط با این موضوع پرهیز کنید.

</div>

```js
/* Bad */
const onItmClk = () => {}

/* Good */
const onItemClick = () => {}
```

<div dir="rtl">

## از تکرار دوری کنید

از تکرار جلوگیری کنید. مثلا مثل مثال زیر نام کلاس را در نام اعضا آن کلاس نبرید و استفاده نکنید.

</div>

```js
class MenuItem {
  /* Method name duplicates the context (which is "MenuItem") */
  handleMenuItemClick = (event) => { ... }

  /* Reads nicely as `MenuItem.handleClick()` */
  handleClick = (event) => { ... }
}
```

<div dir="rtl">

## از طریق نام نتیجه را معلوم کنید

یک نام باید نتیجه ای که بر می گرداند را دقیقا مشخص کند

</div>

```jsx
/* Bad */
const isEnabled = itemCount > 3
return <Button disabled={!isEnabled} />

/* Good */
const isDisabled = itemCount <= 3
return <Button disabled={isDisabled} />
```

---

<div dir="rtl">

# نام گذاری توابع

## الگوی A / HC / LC

یک الگوی مفید برای نام گذاری تابع ها وجود دارد:

</div>

```
prefix? + action (A) + high context (HC) + low context? (LC)
```

<div dir="rtl">

نحوه ی استفاده ی این الگو در جدول زیر آمده است.

</div>


| Name                   | Prefix   | Action (A) | High context (HC) | Low context (LC) |
| ---------------------- | -------- | ---------- | ----------------- | ---------------- |
| `getUser`              |          | `get`      | `User`            |                  |
| `getUserMessages`      |          | `get`      | `User`            | `Messages`       |
| `handleClickOutside`   |          | `handle`   | `Click`           | `Outside`        |
| `shouldDisplayMessage` | `should` | `Display`  | `Message`         |                  |

<div dir="rtl">

> **یادداشت:**  
> ترتیب انجام کارها بسیار مهم است مثلا `shouldUpdateComponent` در جایی استفاده می شود که به صورت دائمی آپدیت می شود ولی `shouldComponentUpdate` در جایی استفاده می شود که باید آپدیت کنید و این آپدیت توسط شما باید انجام شود.
> همیشه High context بر معنی نام یک متغیر تاثیر می گذارد.

---

## در نام از فعل استفاده کنید

مهم ترین بخشی را که تابع انجام می دهد را به عنوان فعل به کار ببرید و نام آن را نام تابع استفاده کنید.

### `get`

داده هایی که در همان لحظه خروجی خواهید گرفت.

</div>

```js
function getFruitCount() {
  return this.fruits.length
}
```

<div dir="rtl">

> همچنین [compose](#compose)  را مشاهده کنید.

### `set`

برای اعلان یک متغیر استفاده می شود

</div>

```js
let fruits = 0

function setFruits(nextFruits) {
  fruits = nextFruits
}

setFruits(5)
console.log(fruits) // 5
```

<div dir="rtl">

### `reset`

یک متغیر را به مقدار یا حالت اولیه خود بر می گرداند.

</div>

```js
const initialFruits = 5
let fruits = initialFruits
setFruits(10)
console.log(fruits) // 10

function resetFruits() {
  fruits = initialFruits
}

resetFruits()
console.log(fruits) // 5
```

<div dir="rtl">

### `fetch`

درخواست برای برخی از داده هایی، که یک مدتی  طول می کشد تا پاسخ داده شود (به عنوان مثال درخواست همگام سازی یا sync کردن).

</div>

```js
function fetchPosts(postCount) {
  return fetch('https://api.dev/posts', {...})
}
```

<div dir="rtl">

### `remove`

چیزی را از جایی حذف می کند.

به عنوان مثال ، اگر مجموعه ای از فیلترهای انتخاب شده در صفحه جستجو داشته باشید ، حذف یکی از این مجموعه ها با "removeFilter" است و "deleteFilter" اتفاق نمی افتد

</div>

```js
function removeFilter(filterName, filters) {
  return filters.filter((name) => name !== filterName)
}

const selectedFilters = ['price', 'availability', 'size']
removeFilter('price', selectedFilters)
```

<div dir="rtl">

> همچنین [delete](#delete) را مشاهده کنید.

### `delete`

چیزی که می خواهید کاملا پاک کنید.

فکر کنید یک سیستم مدیریت محتوا دارید وقتی روی کلید حذف پست می زنید عملیات `deletePost` انجام می شود و از `removePost` استفاده نمی شود.

</div>

```js
function deletePost(id) {
  return database.find({ id }).delete()
}
```

<div dir="rtl">

> همچنین [remove](#remove) را مشاهده کنید.

### `compose`

داده های جدیدی را از داده های موجود ایجاد می کند. بیشتر در رشته ها، شی ها یا تابع ها کاربرد دارد.

</div>

```js
function composePageUrl(pageName, pageId) {
  return (pageName.toLowerCase() + '-' + pageId)
}
```

<div dir="rtl">

> همچنین [get](#get) را مشاهده کنید.

### `handle`

Handles برای عمل ها به کار می رود. اغلب هنگام نام گذاری برای یک روش پاسخ گویی قابل استفاده است.

</div>

```js
function handleLinkClick() {
  console.log('Clicked a link!')
}

link.addEventListener('click', handleLinkClick)
```

---

<div dir="rtl">

## نام باید عملکرد را مشخص کند

نام یک تابع باید کار آن تابع را مشخص کند یا حداقل کاری را که قرار است انجام دهد را مشخص کند.

</div>

```js
/* A pure function operating with primitives */
function filter(list, predicate) {
  return list.filter(predicate)
}

/* Function operating exactly on posts */
function getRecentPosts(posts) {
  return filter(posts, (post) => post.date === Date.now())
}
```

<div dir="rtl">

> برخی از موارد در زبان های مختلف متفاوت است مثلا در جاوااسکریپت اپراتور filter روی آرایه ها عمل می کنند و نیازی به اضافه کردن fitlterArray ندارید.

--

## پیشوندها

پیشوندها به نام متغیرها معنای بهتری می دهند و معمولا در نام توابع استفاده نخواهند شد

### `is`

مشخصه یا حالتی از زمینه فعلی را توصیف می کند (معمولاً به صورت بولین).

</div>

```js
const color = 'blue'
const isBlue = color === 'blue' // characteristic
const isPresent = true // state

if (isBlue && isPresent) {
  console.log('Blue is present!')
}
```

<div dir="rtl">

### `has`

توصیف می کند که آیا این مقدار فعلی مقدار یا حالت خاصی می باشد یا نه (معمولاً به صورت بولین).

</div>

```js
/* Bad */
const isProductsExist = productsCount > 0
const areProductsPresent = productsCount > 0

/* Good */
const hasProducts = productsCount > 0
```

<div dir="rtl">

### `should`

یک جمله شرطی مثبت را همراه با یک عمل خاص منعکس می کند (معمولاً به صورت بولین).

</div>

```js
function shouldUpdateUrl(url, expectedUrl) {
  return url !== expectedUrl
}
```

<div dir="rtl">

### `min`/`max`

مقدار حداقل و حداکثر را مشخص کند هنگام توصیفات محدوده حتما محدودیت ها را مشخص کنید.

</div>

```js
/**
 * Renders a random amount of posts within
 * the given min/max boundaries.
 */
function renderPosts(posts, minPosts, maxPosts) {
  return posts.slice(0, randomBetween(minPosts, maxPosts))
}
```

<div dir="rtl">

### `prev`/`next`

این بخش حالت بعدی یا قبلی متغیر را نشان می دهد از آن در زمان انتقال حالت ها استفاده کنید.

</div>

```jsx
function fetchPosts() {
  const prevPosts = this.state.posts

  const fetchedPosts = fetch('...')
  const nextPosts = concat(prevPosts, fetchedPosts)

  this.setState({ posts: nextPosts })
}
```

<div dir="rtl">

## از کلمات مفرد و جمع در نام استفاده کنید

مانند پیشوندها نام متغیرها بسته به اینکه یک متغیر باشند و یک داده را بگیرند یا آرایه باشند و چندین داده را بگیرند باید جمع یا مفرد استفاده شود

</div>

```js
/* Bad */
const friends = 'Bob'
const friend = ['Bob', 'Tony', 'Tanya']

/* Good */
const friend = 'Bob'
const friends = ['Bob', 'Tony', 'Tanya']
```

