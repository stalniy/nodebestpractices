[✔]: assets/images/checkbox-small-blue.png

# Кращі практики в Node.js

<h1 align="center">
  <img src="assets/images/banner-2.jpg" alt="Кращі практики на Node.js">
</h1>

<br/>

<div align="center">
  <img src="https://img.shields.io/badge/⚙%20Item%20count%20-%2082%20Best%20Practices-blue.svg" alt="83 items"> <img src="https://img.shields.io/badge/%F0%9F%93%85%20Last%20update%20-%20Apr%2013%202019-green.svg" alt="Останні зміни: April 13, 2019"> <img src="https://img.shields.io/badge/ %E2%9C%94%20Updated%20For%20Version%20-%20Node%2010.15.3%20LTS-brightgreen.svg" alt="Змінено під Node 10.15.3 LTS">
</div>

<br/>

[![nodepractices](/assets/images/twitter-s.png)](https://twitter.com/nodepractices/) **Підписуйся на нас в Twitter!** [**@nodepractices**](https://twitter.com/nodepractices/)

<br/>

Читати на іншій мові: [![CN](/assets/flags/CN.png)**CN**](/README.chinese.md), [![BR](/assets/flags/BR.png)**BR**](/README.brazilian-portuguese.md) [(![ES](/assets/flags/ES.png)**ES**, ![FR](/assets/flags/FR.png)**FR**, ![HE](/assets/flags/HE.png)**HE**, ![KR](/assets/flags/KR.png)**KR**, ![RU](/assets/flags/RU.png)**RU**, ![TR](/assets/flags/TR.png)**TR** в розробці!)](#translations) та [![UA](/assets/flags/UA.png)**UA** в розробці](/README.ukrainian.md)

<br/>

###### Створено і підтримується нашим [Керівним комітетом](#steering-committee) та іншими [Співучасниками](#collaborators)

# Останні нововведення та інші новини

- **Нововведення:** 4.4: [Уникайте тестових фікстур, використовуйте дані в кожному тесті окремо](https://github.com/i0natan/nodebestpractices#4-testing-and-overall-quality-practices)

- **Нововведення:** 6.25: [Не публікуйте секрети в npm реєстр](/sections/security/avoid_publishing_secrets.md)

- **Новий переклад:** ![BR](/assets/flags/BR.png) [бразильська та португальська](/README.brazilian-portuguese.md) версії від тепер доступні, велика подяка [Marcelo Melo](https://github.com/marcelosdm)! ❤️

<br/><br/>

# Вітаємо! 3 Основні Речі, які Варто Знати для Початку:

**1. Ви читаєте цілу купу найкращих Node.js статей -** цей репозиторій є збіркою найбільш рейтингового контенту кращих практик в Node.js, та контенту написаного небайдужими співучасниками репозиторію

**2. Це найбільша збірка і вона збільшується щотижня -** наразі, тут більше 80 кращих практик, рекомендацій по написанню кода та архітектурних порад. Нові задачі та запити на зміни (pull requests) створюються щодні для того, щоб тримати це онлайн зібрання в актуальному стані. Ми були раді побачити і Ваш внесок в нашу спільну роботу, будь то виправлення помилок в коді, допомога з перекладом, чи феноменальні нові ідеї та поради. Дивіться наші [рекомендації по написанню тут](/.operations/writing-guidelines.ukrainian.md)

**3. Більшість рекомендацій мають додаткову інформацію -** більшість пунктів мають **🔗Читати детальніше** посилання, де наведена більш детальна інформація, з прикладами коду та цитатами з популярних блогів

<br/><br/>

## Зміст

1.  [Структура проекту (5)](#1-project-structure-practices)
2.  [Обробка помилок (11) ](#2-error-handling-practices)
3.  [Стиль написання коду (12) ](#3-code-style-practices)
4.  [Тестування та якість коду (11) ](#4-testing-and-overall-quality-practices)
5.  [Запуск онлайн (Production) (18) ](#5-going-to-production-practices)
6.  [Безпека (25)](#6-security-best-practices)
7.  [Продуктивність (1) (В процесі розробки ✍️)](#7-performance-best-practices)

<br/><br/>

# `1. Структура проекту`

## ![✔] 1.1 Структуруйте своє рішення по компонентах

**TL;DR:** Найбільша пастка при побудові великих додатків - це робота з великою кодовою базою із сотнями залежностей - такий моноліт сповільнює розробників при реалізації нового функціоналу. Натомість, розбивайте код по компонентах, кожен з яких лежить в окремій папці або виділено місцю в коді та тримайте кожен компонент малим та простим. Перейдіть за 'Читати детальніше' посиланням наведеним нижче, щоб побачити приклади правильної структури проекту

**Інакше:** Коли програмістам, які створють новий функціонал, тяжко зрозуміти на що впливають їхні зміни в коді і бояться поламати залежний компонент - релізи стають більш повільними та ризикованішими. Також набагато важче масштабуватись, якщо бізнес логіка не розбита на окремі одиниці

🔗 [**Читати детальніше: струтуруйте по компонентах**](/sections/projectstructre/breakintcomponents.md)

<br/><br/>

## ![✔] 1.2 Розбивайте компоненти на шари, тримай Express в своїх межах

**TL;DR:** Кожен компонент повинен складатись з 'шарів' - окрема логіка під роботу з HTTP, бізнес логіку та доступ до данних. Це не лише встановлює прозоре розділення відповідальностей, але й також суттєво спрощує мокування і тестування системи. Хоча це і дуже поширений підхід, розробники API як правило змішують шари, прокидуючи об'єкти з рівня HTTP (Express req, res) в бізнес логіку та шар доступу до данних - це робить Ваш додаток залежним від абстрацій Express і обмежує використання інших шарів за межами Express

**Інакше:** Додаток, що містить змішані між собою шари практично не можливо тестувати, перевикористовувати в CRON задачах та інших середовищах, що базуються на не Express

🔗 [**Читати детальніше: Розбивайте додаток на шари**](/sections/projectstructre/createlayers.md)

<br/><br/>

## ![✔] 1.3 Загорніть загальні утиліти в npm пакети

**TL;DR:** У великому додатку In a large app, що становить велику кодову базу, утиліти на зразок логера, шифрування, тощо, повинні бути завернуті у Ваш власний код і бути доступними як приватні npm пакети. Це дозвлояє перевикористовувати їх між багатьма проектами

**Інакше:** Вам доведеться перевинаходити власний інструмент для керування залежностями та релізами

🔗 [**Читати детальніше: Загорніть загальні утиліти в npm пакети**](/sections/projectstructre/wraputilities.md)

<br/><br/>

## ![✔] 1.4 Розділяйте Express 'app' та 'server'

**TL;DR:** Уникайте поганої звичку створювати весь [Express](https://expressjs.com/) `app` в одному великому файлі - розділіть 'Express' визначення як мінімум на 2 файли: створення API (app.js) та доступ по мережі (WWW). Для більш кращої структури зробіть, щоб кожен компонент міг вносити зміни в API (наприклад, додавати обробники запитів)

**Інакше:** Ваш API буде доступний лише для тестування через HTTP виклики (повільніші тести, для яких набагато важче генерувати звіт про покриття). Скоріше всього це не дуже велике задоволення підтримувати сотні строчок коду в одному файлі

🔗 [**Читати детальніше: розділяйте Express 'app' та 'server'**](/sections/projectstructre/separateexpress.md)

<br/><br/>

## ![✔] 1.5 Використовуйте безпечну та ієрархічну конфігурацію, що підтримує змінні середовища

**TL;DR:** Бездоганне налаштування конфігурації повинно відповідати таким вимогам: (а) значення можуть бути отримані з файла або змінних середовища (б) секрети знаходяться за межами закоміченого коду (в) конфігурація є ієрархічною, що дозволяє її легко знайти. [rc](https://www.npmjs.com/package/rc), [nconf](https://www.npmjs.com/package/nconf) та [config](https://www.npmjs.com/package/config) є бібліотеками, що задовільняють майже всі з вище наведених побажань

**Інакше:** Якщо не задовільнити одну із вище наведених вимог, то команда розробників або операційних розробників (devops) рано чи пізно застряне. Можливо обидві команди застрянуть

🔗 [**Читати детальніше: Використовуйте безпечну та ієрархічну конфігурацію, що підтримує змінні середовища**](/sections/projectstructre/configguide.md)

<br/><br/><br/>

<p align="right"><a href="#table-of-contents">⬆ Повернутись на початок</a></p>

# `2. Обробка помилок`

## ![✔] 2.1 Використовуйте Async-Await або Promise для обробки асинхронних помилок

**TL;DR:** Обробка асинхронних помилок за допомогою callback функцій - це мабуть найкоротший шлях до хаосу (так називаємий "callback hell"). Найкраще, що Ви можете зробити - це використати Promise або Async-Await, ці інструменти точно змешать розмір та покращать читабельність коду.

**Інакше:** Node.js callback стиль, `function(err, response)`, є багатообіцяючим шляхом до важко підтримуваного коду через змішування логіки обробки помилок та бізнес логіки, збиткової вкладеності та дивних практик програмування

🔗 [**Читати детальніше: уникайте використання callback стилю**](/sections/errorhandling/asyncerrorhandling.md)

<br/><br/>

## ![✔] 2.2 Використовуйте вбудований Error конструктор

**TL;DR:** Багато хто викидує помилки рядком (прим. `string`) або спеціальним типом – це ускладнює їх обробку, особливо при використанні в інших модулях. Якщо Ви відхиляєте (прим. reject) Promise або викидуєте помилку – використовуйте вбудований `Error` конструктор, який збільшить узгодженість та запобіжить втраті інформації ()

**Інакше:** Коректна обробка помилок може стати ще більшою проблемою, якщо нема впевненості в якому вигляді помилка буде викинута. Навіть гірше, якщо не використовувати `Error` конструктор можна втратити критичну для розуміння покилки інформацію таку як зворотній стек викликів!

🔗 [**Читати детальніше: Використовуйте вбудований Error конструктор**](/sections/errorhandling/useonlythebuiltinerror.md)

<br/><br/>

## ![✔] 2.3 Розділяйте помилки на операційні та помилки програміста

**TL;DR:** Операційні помилки (н/д, API отримав некоретні дані) відносяться до очікуваних, в цьому випадку вплив помилки зрозумілий і вона може бути коректно оброблена. З іншої сторони, помилки програміста (н/д, спроба прочитати невизначену змінну) відносяться до неочікуваних, зазвичай у таких випадках треба коректно (прим. gracefull) перезапустити додаток.

**Інакше:** Можна перезапускати додаток щоразу як виникає помилка, але для чого змушувати ~5000 онлайн користувачів чекати через незначну, очікувану, операційну помилку? Зворотній бік також не ідеальний – тримати додаток запущеним під час неочікуваної помилки (помилки програміста) може призвести до непередбачуваної поведінки. Розділяючи цих 2 випадки дозволяє діяти тактично та застосовувати розумний підхід оперичаючись на джерело винекнення помилки

🔗 [**Читати детальніше: операційні помилки і помилки прогргаміста**](/sections/errorhandling/operationalvsprogrammererror.md)

<br/><br/>

## ![✔] 2.4 Обробляйте помилки централізовано, не в Express middleware

**TL;DR:** Обробка помилок, як наприклад відправка email адміну або логування, повинна бути інкапсульовано в спеціально виділених централізованих об'єктах, які використовуються по всьому додатку (н/д, Express middleware, cron задачі, unit тестування)

**Інакше:** Якщо не обробляти помилки в одному місці, то це призведе до дублювання коду та скоріше всього до того, що деякі помилки будуть не оброблені.

🔗 [**Читати детальніше: обробляйте помилки централізовано**](/sections/errorhandling/centralizedhandling.md)

<br/><br/>

## ![✔] 2.5 Документуйте API помилки використовуючи Swagger або GraphQL

**TL;DR:** Описуйте помилки, які можуть виникнути у відповідь на API запит, щоб клієнти могли обробити їх коректно, і запобігти падіння своєї програми. Для REST API, це зазвичай робиться за допомогою Swagger. Якщо Ви використовуєте GraphQL, Ви можете використати описати це за допомогою схеми або коментарів.

**Інакше:** API клієнт може просто впасти і перезапуститись лише через те, що отримав помилку яку не може зрозуміти. Примітка: клієнтом Вашого API можете бути Ви самі (дуже поширено в мікросервісній архітектурі)

🔗 [**Читати детальніше: документуйте API помилки використовуючи Swagger або GraphQL**](/sections/errorhandling/documentingusingswagger.md)

<br/><br/>

## ![✔] 2.6 Перезапускайте процес поступово (в оригіналі gracefully) коли щось пішло не так

**TL;DR:** Коли виникає невідома помилка (помилка програміста, дивіться пункт 2.3), стан програми стає невизначеним. Стандартна практика рекомендую обережно (в оригіналі carefully) перезапустити процес використовуючи програми для керування процесами на зразок [Forever](https://www.npmjs.com/package/forever) або [PM2](http://pm2.keymetrics.io/)

**Інакше:** Коли виникає невідома помилка, якийсь об'єкт може мати некоретний стан (наприклад, event emitter, який використовується глобально і не викидує більше події через внутрішню помилку) і всі наступні запити можуть закінчуватись помилкою або повертати дуже дивні результати

🔗 [**Читати детальніше: перезапускайте процес**](/sections/errorhandling/shuttingtheprocess.md)

<br/><br/>

## ![✔] 2.7 Використовуйте надійний (в оригіналі mature) логер для підвищення відслідковування помилок

**TL;DR:** Набір надійних інструментів, для логування таких як [Winston](https://www.npmjs.com/package/winston), [Bunyan](https://github.com/trentm/node-bunyan) або [Log4js](http://stritti.github.io/log4js/), пришвидшить знаходження та покращить розуміння помилок. Так що забудьте про console.log

**Інакше:** Перегляд неструктурованих логів, створених за допомогою console.log, без інструментів, що дозволяють проводити пошук або гідного переглядача логів, займе Вас на роботі до пізньої години

🔗 [**Читати детальніше: використовуйте надійний логер**](/sections/errorhandling/usematurelogger.md)

<br/><br/>

## ![✔] 2.8 Тестуйте ситуації, що призводять до помилок за допомогою улюбленого тестового фреймворка

**TL;DR:** За допомогою автоматизованих інструменті або вручну, переконайтесь, що Ваш код не лише задовільняє позитивний сценарій, але й також коректно себе веде та повертає очікувані помилки під час негативного сценарію. Тестові фреймворки на зразок Mocha та Chai можуть допомогти в цьому (дивіться приклади в "Gist вікні")

**Інакше:** Без тестування, автоматичного або ручного, Ви не можете покладатись на те, що код верне коректні помилки. Без виразних помилок – не може йти мови ні про яку обробку помилок

🔗 [**Читати детальніше: тестуйте ситуації, що призводять до помилок**](/sections/errorhandling/testingerrorflows.md)

<br/><br/>

## ![✔] 2.9 Виявляйте помилки та час простою за допомогою APM продуктів

**TL;DR:** Продукти для моніторинг та перформансу (так звані APM) активно оцінюють Ваш код або API, щоб потім автоматично повідомляти про помилки, падіння та повільні частини, що були пропущені

**Інакше:** Ви можете витратити багато зусиль на вимірювання продуктивності API та часу простою, можливо Ви навіть ніколи не будете знати, яка частина Вашого коду найповільніша в реальних сценаріях і як це впливає на UX

🔗 [**Читати детальніше: використовуйте APM продукти**](/sections/errorhandling/apmproducts.md)

<br/><br/>

## ![✔] 2.10 Ловіть необроблені відхилення (в оригіналі rejection) Promise

**TL;DR:** Будь-яка помилка викинута всередині Promise ланцюжка буде тихо проковтнута та відхилена, якщо програміст не обробить її спеціально. Навіть якщо Ваш код підписаний на `process.uncaughtException` подію! Виправте це підписавшись на подію `process.unhandledRejection`

**Інакше:** Ви ніколи не будете знати, що у Вашій програмі є помилки.

🔗 [**Читати детальніше: ловіть необроблені відхилення Promise**](/sections/errorhandling/catchunhandledpromiserejection.md)

<br/><br/>

## ![✔] 2.11 Викидуйте помилку як можна раніше, валідуйте аргументи використовуючи спеціалізовану бібліотеку

**TL;DR:** Перевіряйте вхідні дані в API, щоб уникнути неприємних багів, які набагато важче відслідкувати пізніше. Валідація зазвичай є рутинною роботою, але за умови якщо Ви не використовуєте бібліотеку на зразок Joi

**Інакше:** Розглянемо ситуаці: Ваша функція очікує числовий аргумент “Discount”, але викликаюча сторона забула передати його, пізніше, Ваш код перевіряє чи Discount!=0 (допустима знижка повинна бути більше нуля) та дозволяє користувачу насолоджуватись знижкою. Що ж за неприємна помилка? Ви її бачите?

🔗 [**Читати детальніше: Викидуйте помилку як можна раніше**](/sections/errorhandling/failfast.md)

<br/><br/><br/>

<p align="right"><a href="#table-of-contents">⬆ Повернутись на початок</a></p>

# `3. Стиль написання коду`

## ![✔] 3.1 Використовуйте ESLint

**TL;DR:** [ESLint](https://eslint.org) є де-факто статнадртом для перевірки помилок і виправлення форматування коду. Він не лише ідентифікує проблеми з відступами, а й також допомогає знайти серйозні анти-патерни в коді, як наприклад, викидування некласифікованих помилок. І хоча ESLint може автоматично виправити форматування, інші інструменти на зразок [prettier](https://www.npmjs.com/package/prettier) та [beautify](https://www.npmjs.com/package/js-beautify) справляються з проблемами форматування набагато краще (звісно ж їх можна використовувати у зв'язці з ESLint).

**Інакше:** Програмісти будуть зайняті постійними суперечками про відступи і довжину строки, ще вони будуть витрачати час на створення власного код стилю.

🔗 [**Читати детальніше: Використовуйте ESLint та Prettier**](/sections/codestylepractices/eslint_prettier.md)

<br/><br/>

## ![✔] 3.2 ESLint плагіни під Node.js

**TL;DR:** Поверх стандартних ESLint правил для JavaScript, також підключіть плагіни специфічні для Node.js, такі як [eslint-plugin-node](https://www.npmjs.com/package/eslint-plugin-node), [eslint-plugin-mocha](https://www.npmjs.com/package/eslint-plugin-mocha) і [eslint-plugin-node-security](https://www.npmjs.com/package/eslint-plugin-security)

**Інакше:** Багато Node.js анти-патернів можуть глибоко закріпитись у Вашому коді. Наприклад, програмісти можуть підключити Node.js модуль передавши змінну в `require` (ось так `require(variableAsPath)`) і це може дозволити атакуючій стороні виконати довільний JS скрипт. Node.js лінтери можуть ідентифікувати та попередити такі патерни

<br/><br/>

## ![✔] 3.3 Відкривайте фігурну дужку для початку кодового блоку на тій самій строці

**TL;DR:** Відкриваюча фігурна дужка для блоку повинна бути на тій самі строці, що й відкриваючий вираз

### Приклад Коду

```javascript
// Так робіть
function someFunction() {
  // код тут
}

// Уникайте робити так
function someFunction()
{
  // код тут
}
```

**Інакше:** Якщо не слідувати такому підходу, то можна наткнутись на неочікувані результати, як описано на StackOverflow:

🔗 [**Читати детальніше:** "Чому результати відрізняються в залежності від того де стоїть фігурна дужка?" (StackOverflow)](https://stackoverflow.com/questions/3641519/why-does-a-results-vary-based-on-curly-brace-placement)

<br/><br/>

## ![✔] 3.4 Не забувайте про крапку з комою

**TL;DR:** Хоча це і не було одностайно походжено, всеодно рекомендується ставити крапку з комою вкінці кожного виразу (в оригіналі statement). Це зробить Ваш код більш читабельним і прозорим для інших програмістів

**Інакше:** Як Ви вже знаєте з попередньої секції, JavaScript інтерпретатор автоматично додає крапку з комою вкінці кожного виразу (в оригіналі statement), якщо її не знаходить - це може призводити до неочікуваних результатів

### Приклад Коду

```javascript
// Так робіть
const count = 2;
(function doSomething() {
  // тут щось надзвичайне
}());

// Уникайте робити так — викине помилку
const count = 2 // інтерпретатор пробує виконати 2(), але 2 не є функцією
(function doSomething() {
  // тут щось надзвичайне
}())
```

<br/><br/>

## ![✔] 3.5 Давайте функціям імена

**TL;DR:** Давайте функціям всім функціям імена, включаючи замикання і колбеки. Уникайте використання анонімних функцій. Це Вам дуже допоможе під час відладки Node.js додатку. Завдяки іменам, Ви легко зрозумієте, куди дивитесь під час аналізу знімка пам'яті (в оригіналі "memory snapshot")

**Інакше:** Відладка помилок, на системі якою користуються клієнти, за допомогою знімка пам'яті може стати справжнім викликом, якщо Ви помітите, що збільшення пам'яті відбувається в анонімній функції

<br/><br/>

## ![✔] 3.6 Використовуйте домовленості про іменування змінних, констант, функцій та класів

**TL;DR:** Використовуйте **_lowerCamelCase_** коли іменуєте константи, змінні, функції і **_UpperCamelCase_** (перша літера велика) коли іменуєте класи. Це допоможе швидко відрізняти змінні та функції від класів для яких треба інстанціювати екземпляр. Використовуйте зрозумілі імена, але старайтесь, щоб вони були короткими

**Інакше:** Javascript - це єдина мова в світі, що дозволяє викликати конструктор (клас) напряму без інстанціювання екземпляра. В результаті, класи і функції конструктори відрізняються тим що називаються з великої букви

### Приклад Коду

```javascript
// для класів використовуємо UpperCamelCase
class SomeClassExample {}

// для констант використовуйє ключове слово const і lowerCamelCase ім'я
const config = {
  key: 'value'
};

// для змінних та функцій використовуємо імена в lowerCamelCase
let someVariableExample = 'value';
function doSomething() {}
```

<br/><br/>

## ![✔] 3.7 Надавайте перевагу const, а не let. Забудьте про var

**TL;DR:** `const` дозволяє задати значення змінної лише при ініціалізації і їй не можна змінити значення. Надавши перевагу `const` Ви більше не зможете використовувати одну й ту саму змінну для різних сценаріїв і це зробить код зрозумілішим. Використовуйте `let`, якщо змінну треба перевизначити, наприклад у `for` циклі. Інший дуже важливий аспект при використанні `let` і `const` - це те, що вони визначають змінну лише у області видимості блока, в якому змінна була створена. Натомість `var` доступна у всьому скоупі функції, незалежно від того створена вона в блоці чи на початку функції, тому [`var` не повинен використовуватись в ES6](https://hackernoon.com/why-you-shouldnt-use-var-anymore-f109a58b9b70). Тепер ми маємо `const` і `let`

**Інакше:** Відладжувати код зі змінними, які постійно змінюються набагато тяжче

🔗 [**Читати детальніше: JavaScript ES6+: var, let чи const?** ](https://medium.com/javascript-scene/javascript-es6-var-let-or-const-ba58b8dcde75)

<br/><br/>

## ![✔] 3.8 Підключайте модулі на початку, не у функціях

**TL;DR:** Підключайте модулі на початку кожного файлу, перед і за межами будь-якої функції. Цей простий підхід не лише допоможе швидко і легко бачити всі залежності файлу, але й допоможе уникнути потенційних проблем

**Інакше:** Підключення модулів відбувається синхронно самим Node.js. Якщо воно відбувається всередині функції, то може заблокувати більш критичні запити. Також, якщо підключаємий модуль (або одна із його залежностей) викине помилку і закрешить сервер, то дізнатись про це хотілося б якомога раніше. Цього точно дуже важко досягти, якщо підключати модуль всередині функції

<br/><br/>

## ![✔] 3.9 Підключайте модуль як папку, а не файл

**TL;DR:** Коли розробляєш модуль або бібліотеку в папці, додай index.js файл, який виконуватиме функцію публічного інтерфейсу для Nodejs модуля.
Це допоможе пізніше внести зміни, не порушуючи зворотню сумісність

**Інакше:** Зміна внутрішньої структури папок або перейменування файлів може порушити зворотню сумісність з клієнтами

### Приклад Коду

```javascript
// Do
module.exports.SMSProvider = require('./SMSProvider');
module.exports.SMSNumberResolver = require('./SMSNumberResolver');

// Avoid
module.exports.SMSProvider = require('./SMSProvider/SMSProvider.js');
module.exports.SMSNumberResolver = require('./SMSNumberResolver/SMSNumberResolver.js');
```

<br/><br/>

## ![✔] 3.10 Використовуйте оператор `===`

**TL;DR:** Надавайте перевагу строгому оператору рівності `===`, а не більш слабкому абстрактному оператору `==`. `==` порівнює 2 змінні після приведення їх до одного сумісного типу. Натомість оператор `===` не робить приведення типів, а натомість переконується, що змінні мають однаковий тип

**Інакше:** Порівняння нерівних змінних може повернути true, якщо використовувати `==`

### Приклад Коду

```javascript
'' == '0'           // false
0 == ''             // true
0 == '0'            // true

false == 'false'    // false
false == '0'        // true

false == undefined  // false
false == null       // false
null == undefined   // true

' \t\r\n ' == 0     // true
```

Всі вирази вище повернуть false, якщо використати `===`

<br/><br/>

## ![✔] 3.11 Використовуйте Async Await, уникайте callback

**TL;DR:** Node 8 LTS повністю підтримує Async-await. Це новий спосіб для роботи з асинхронним кодом, що витіснив Promise-и та callback-и. Async-await не є блокуючим, проте дозволяє писати асинхронний код так, щоб він виглядав як синхронний. Найкращий подарунок, який Ви можете зробити для свого коду - це використати async-await, що дозволяє писати код більш компактно і робить його більш зрозумілим, наприклад, try-catch

**Інакше:** Обробка асинхронних помилок з використанням callback стилю ймовірно найкоротший шлях до безладу (в оригіналі hell) - цей стиль змушує перевіряти помилки скрізь по коду, мати справу з глибокою вкладеністю та ускладнює розуміння коду

🔗[**Читати детальніше:** async await 1.0](https://github.com/yortus/asyncawait)

<br/><br/>

## ![✔] 3.12 Використовуйте стрілочні функції (=>)

**TL;DR:** Хоча і рекомендується використовувати async-await і уникати функцій-параметрів, іноді приходиться мати справу із старішими інтерфейсами, що працюють з Promise або callback-ами. В таких випадках - стрілочні функції роблять код компактнішим і зберігають лексичний контекст корневої функції (тобто `this`)

**Інакше:** Код написаний з ES5 функціями більш незграбний і схильний до помилок

🔗 [**Читати детальніше: Настав час Стрілочних функцій**](https://medium.com/javascript-scene/familiarity-bias-is-holding-you-back-its-time-to-embrace-arrow-functions-3d37e1a9bb75)

<br/><br/><br/>

<p align="right"><a href="#table-of-contents">⬆ Повернутись на початок</a></p>

# `4. Testing And Overall Quality Practices`

## ![✔] 4.1 At the very least, write API (component) testing

**TL;DR:** Most projects just don't have any automated testing due to short timetables or often the 'testing project' ran out of control and was abandoned. For that reason, prioritize and start with API testing which is the easiest way to write and provides more coverage than unit testing (you may even craft API tests without code using tools like [Postman](https://www.getpostman.com/). Afterward, should you have more resources and time, continue with advanced test types like unit testing, DB testing, performance testing, etc

**Otherwise:** You may spend long days on writing unit tests to find out that you got only 20% system coverage

<br/><br/>

## ![✔] 4.2 Include 3 parts in each test name

**TL;DR:** Make the test speak at the requirements level so it's self explanatory also to QA engineers and developers who are not familiar with the code internals. State in the test name what is being tested (unit under test), under what circumstances and what is the expected result

**Otherwise:** A deployment just failed, a test named “Add product” failed. Does this tell you what exactly is malfunctioning?

🔗 [**Read More: Include 3 parts in each test name**](/sections/testingandquality/3-parts-in-name.md)

<br/><br/>

## ![✔] 4.3 Detect code issues with a linter

**TL;DR:** Use a code linter to check basic quality and detect anti-patterns early. Run it before any test and add it as a pre-commit git-hook to minimize the time needed to review and correct any issue. Also check [Section 3](https://github.com/i0natan/nodebestpractices#3-code-style-practices) on Code Style Practices

**Otherwise:** You may let pass some anti-pattern and possible vulnerable code to your production environment.

<br/><br/>

## ![✔] 4.4 Avoid global test fixtures and seeds, add data per-test

**TL;DR:** To prevent tests coupling and easily reason about the test flow, each test should add and act on its own set of DB rows. Whenever a test needs to pull or assume the existence of some DB data - it must explicitly add that data and avoid mutating any other records

**Otherwise:** Consider a scenario where deployment is aborted due to failing tests, team is now going to spend precious investigation time that ends in a sad conclusion: the system works well, the tests however interfere with each other and break the build

🔗 [**Read More: Avoid global test fixtures**](/sections/testingandquality/avoid-global-test-fixture.md)

<br/><br/>



## ![✔] 4.5 Constantly inspect for vulnerable dependencies

**TL;DR:** Even the most reputable dependencies such as Express have known vulnerabilities. This can get easily tamed using community and commercial tools such as 🔗 [npm audit](https://docs.npmjs.com/cli/audit) and 🔗 [snyk.io](https://snyk.io) that can be invoked from your CI on every build

**Otherwise:** Keeping your code clean from vulnerabilities without dedicated tools will require to constantly follow online publications about new threats. Quite tedious

<br/><br/>

## ![✔] 4.6 Tag your tests

**TL;DR:** Different tests must run on different scenarios: quick smoke, IO-less, tests should run when a developer saves or commits a file, full end-to-end tests usually run when a new pull request is submitted, etc. This can be achieved by tagging tests with keywords like #cold #api #sanity so you can grep with your testing harness and invoke the desired subset. For example, this is how you would invoke only the sanity test group with [Mocha](https://mochajs.org/): mocha --grep 'sanity'

**Otherwise:** Running all the tests, including tests that perform dozens of DB queries, any time a developer makes a small change can be extremely slow and keeps developers away from running tests

<br/><br/>

## ![✔] 4.7 Check your test coverage, it helps to identify wrong test patterns

**TL;DR:** Code coverage tools like [Istanbul/NYC ](https://github.com/gotwarlost/istanbul)are great for 3 reasons: it comes for free (no effort is required to benefit this reports), it helps to identify a decrease in testing coverage, and last but not least it highlights testing mismatches: by looking at colored code coverage reports you may notice, for example, code areas that are never tested like catch clauses (meaning that tests only invoke the happy paths and not how the app behaves on errors). Set it to fail builds if the coverage falls under a certain threshold

**Otherwise:** There won't be any automated metric telling you when a large portion of your code is not covered by testing

<br/><br/>

## ![✔] 4.8 Inspect for outdated packages

**TL;DR:** Use your preferred tool (e.g. 'npm outdated' or [npm-check-updates](https://www.npmjs.com/package/npm-check-updates) to detect installed packages which are outdated, inject this check into your CI pipeline and even make a build fail in a severe scenario. For example, a severe scenario might be when an installed package is 5 patch commits behind (e.g. local version is 1.3.1 and repository version is 1.3.8) or it is tagged as deprecated by its author - kill the build and prevent deploying this version

**Otherwise:** Your production will run packages that have been explicitly tagged by their author as risky

<br/><br/>

## ![✔] 4.9 Use docker-compose for e2e testing

**TL;DR:** End to end (e2e) testing which includes live data used to be the weakest link of the CI process as it depends on multiple heavy services like DB. Docker-compose turns this problem into a breeze by crafting production-like environment using a simple text file and easy commands. It allows crafting all the dependent services, DB and isolated network for e2e testing. Last but not least, it can keep a stateless environment that is invoked before each test suite and dies right after

**Otherwise:** Without docker-compose teams must maintain a testing DB for each testing environment including developers' machines, keep all those DBs in sync so test results won't vary across environments

<br/><br/>

## ![✔] 4.10 Refactor regularly using static analysis tools

**TL;DR:** Using static analysis tools helps by giving objective ways to improve code quality and keeps your code maintainable. You can add static analysis tools to your CI build to fail when it finds code smells. Its main selling points over plain linting are the ability to inspect quality in the context of multiple files (e.g. detect duplications), perform advanced analysis (e.g. code complexity) and follow the history and progress of code issues. Two examples of tools you can use are [Sonarqube](https://www.sonarqube.org/) (2,600+ [stars](https://github.com/SonarSource/sonarqube)) and [Code Climate](https://codeclimate.com/) (1,500+ [stars](https://github.com/codeclimate/codeclimate)).

**Otherwise:** With poor code quality, bugs and performance will always be an issue that no shiny new library or state of the art features can fix

🔗 [**Read More: Refactoring!**](/sections/testingandquality/refactoring.md)

<br/><br/>

## ![✔] 4.11 Carefully choose your CI platform (Jenkins vs CircleCI vs Travis vs Rest of the world)

**TL;DR:** Your continuous integration platform (CICD) will host all the quality tools (e.g test, lint) so it should come with a vibrant ecosystem of plugins. [Jenkins](https://jenkins.io/) used to be the default for many projects as it has the biggest community along with a very powerful platform at the price of complex setup that demands a steep learning curve. Nowadays, it has become much easier to set up a CI solution using SaaS tools like [CircleCI](https://circleci.com) and others. These tools allow crafting a flexible CI pipeline without the burden of managing the whole infrastructure. Eventually, it's a trade-off between robustness and speed - choose your side carefully

**Otherwise:** Choosing some niche vendor might get you blocked once you need some advanced customization. On the other hand, going with Jenkins might burn precious time on infrastructure setup

🔗 [**Read More: Choosing CI platform**](/sections/testingandquality/citools.md)

<br/><br/><br/>


<p align="right"><a href="#table-of-contents">⬆ Return to top</a></p>

# `5. Going To Production Practices`

## ![✔] 5.1. Monitoring!

**TL;DR:** Monitoring is a game of finding out issues before customers do – obviously this should be assigned unprecedented importance. The market is overwhelmed with offers thus consider starting with defining the basic metrics you must follow (my suggestions inside), then go over additional fancy features and choose the solution that ticks all boxes. Click ‘The Gist’ below for an overview of the solutions

**Otherwise:** Failure === disappointed customers. Simple

🔗 [**Read More: Monitoring!**](/sections/production/monitoring.md)

<br/><br/>

## ![✔] 5.2. Increase transparency using smart logging

**TL;DR:** Logs can be a dumb warehouse of debug statements or the enabler of a beautiful dashboard that tells the story of your app. Plan your logging platform from day 1: how logs are collected, stored and analyzed to ensure that the desired information (e.g. error rate, following an entire transaction through services and servers, etc) can really be extracted

**Otherwise:** You end up with a black box that is hard to reason about, then you start re-writing all logging statements to add additional information

🔗 [**Read More: Increase transparency using smart logging**](/sections/production/smartlogging.md)

<br/><br/>

## ![✔] 5.3. Delegate anything possible (e.g. gzip, SSL) to a reverse proxy

**TL;DR:** Node is awfully bad at doing CPU intensive tasks like gzipping, SSL termination, etc. You should use ‘real’ middleware services like nginx, HAproxy or cloud vendor services instead

**Otherwise:** Your poor single thread will stay busy doing infrastructural tasks instead of dealing with your application core and performance will degrade accordingly

🔗 [**Read More: Delegate anything possible (e.g. gzip, SSL) to a reverse proxy**](/sections/production/delegatetoproxy.md)

<br/><br/>

## ![✔] 5.4. Lock dependencies

**TL;DR:** Your code must be identical across all environments, but amazingly npm lets dependencies drift across environments by default – when you install packages at various environments it tries to fetch packages’ latest patch version. Overcome this by using npm config files, .npmrc, that tell each environment to save the exact (not the latest) version of each package. Alternatively, for finer grained control use `npm shrinkwrap`. \*Update: as of NPM5, dependencies are locked by default. The new package manager in town, Yarn, also got us covered by default

**Otherwise:** QA will thoroughly test the code and approve a version that will behave differently in production. Even worse, different servers in the same production cluster might run different code

🔗 [**Read More: Lock dependencies**](/sections/production/lockdependencies.md)

<br/><br/>

## ![✔] 5.5. Guard process uptime using the right tool

**TL;DR:** The process must go on and get restarted upon failures. For simple scenarios, process management tools like PM2 might be enough but in today's ‘dockerized’ world, cluster management tools should be considered as well

**Otherwise:** Running dozens of instances without a clear strategy and too many tools together (cluster management, docker, PM2) might lead to DevOps chaos

🔗 [**Read More: Guard process uptime using the right tool**](/sections/production/guardprocess.md)

<br/><br/>

## ![✔] 5.6. Utilize all CPU cores

**TL;DR:** At its basic form, a Node app runs on a single CPU core while all others are left idling. It’s your duty to replicate the Node process and utilize all CPUs – For small-medium apps you may use Node Cluster or PM2. For a larger app consider replicating the process using some Docker cluster (e.g. K8S, ECS) or deployment scripts that are based on Linux init system (e.g. systemd)

**Otherwise:** Your app will likely utilize only 25% of its available resources(!) or even less. Note that a typical server has 4 CPU cores or more, naive deployment of Node.js utilizes only 1 (even using PaaS services like AWS beanstalk!)

🔗 [**Read More: Utilize all CPU cores**](/sections/production/utilizecpu.md)

<br/><br/>

## ![✔] 5.7. Create a ‘maintenance endpoint’

**TL;DR:** Expose a set of system-related information, like memory usage and REPL, etc in a secured API. Although it’s highly recommended to rely on standard and battle-tests tools, some valuable information and operations are easier done using code

**Otherwise:** You’ll find that you’re performing many “diagnostic deploys” – shipping code to production only to extract some information for diagnostic purposes

🔗 [**Read More: Create a ‘maintenance endpoint’**](/sections/production/createmaintenanceendpoint.md)

<br/><br/>

## ![✔] 5.8. Discover errors and downtime using APM products

**TL;DR:** Application monitoring and performance products (a.k.a APM) proactively gauge codebase and API so they can auto-magically go beyond traditional monitoring and measure the overall user-experience across services and tiers. For example, some APM products can highlight a transaction that loads too slow on the end-users side while suggesting the root cause

**Otherwise:** You might spend great effort on measuring API performance and downtimes, probably you’ll never be aware which is your slowest code parts under real-world scenario and how these affect the UX

🔗 [**Read More: Discover errors and downtime using APM products**](/sections/production/apmproducts.md)

<br/><br/>

## ![✔] 5.9. Make your code production-ready

**TL;DR:** Code with the end in mind, plan for production from day 1. This sounds a bit vague so I’ve compiled a few development tips that are closely related to production maintenance (click Gist below)

**Otherwise:** A world champion IT/DevOps guy won’t save a system that is badly written

🔗 [**Read More: Make your code production-ready**](/sections/production/productioncode.md)

<br/><br/>

## ![✔] 5.10. Measure and guard the memory usage

**TL;DR:** Node.js has controversial relationships with memory: the v8 engine has soft limits on memory usage (1.4GB) and there are known paths to leak memory in Node’s code – thus watching Node’s process memory is a must. In small apps, you may gauge memory periodically using shell commands but in medium-large apps consider baking your memory watch into a robust monitoring system

**Otherwise:** Your process memory might leak a hundred megabytes a day like how it happened at [Walmart](https://www.joyent.com/blog/walmart-node-js-memory-leak)

🔗 [**Read More: Measure and guard the memory usage**](/sections/production/measurememory.md)

<br/><br/>

## ![✔] 5.11. Get your frontend assets out of Node

**TL;DR:** Serve frontend content using dedicated middleware (nginx, S3, CDN) because Node performance really gets hurt when dealing with many static files due to its single-threaded model

**Otherwise:** Your single Node thread will be busy streaming hundreds of html/images/angular/react files instead of allocating all its resources for the task it was born for – serving dynamic content

🔗 [**Read More: Get your frontend assets out of Node**](/sections/production/frontendout.md)

<br/><br/>

## ![✔] 5.12. Be stateless, kill your servers almost every day

**TL;DR:** Store any type of data (e.g. user sessions, cache, uploaded files) within external data stores. Consider ‘killing’ your servers periodically or use ‘serverless’ platform (e.g. AWS Lambda) that explicitly enforces a stateless behavior

**Otherwise:** Failure at a given server will result in application downtime instead of just killing a faulty machine. Moreover, scaling-out elasticity will get more challenging due to the reliance on a specific server

🔗 [**Read More: Be stateless, kill your Servers almost every day**](/sections/production/bestateless.md)

<br/><br/>

## ![✔] 5.13. Use tools that automatically detect vulnerabilities

**TL;DR:** Even the most reputable dependencies such as Express have known vulnerabilities (from time to time) that can put a system at risk. This can be easily tamed using community and commercial tools that constantly check for vulnerabilities and warn (locally or at GitHub), some can even patch them immediately

**Otherwise:** Keeping your code clean from vulnerabilities without dedicated tools will require you to constantly follow online publications about new threats. Quite tedious

🔗 [**Read More: Use tools that automatically detect vulnerabilities**](/sections/production/detectvulnerabilities.md)

<br/><br/>

## ![✔] 5.14. Assign a transaction id to each log statement

**TL;DR:** Assign the same identifier, transaction-id: {some value}, to each log entry within a single request. Then when inspecting errors in logs, easily conclude what happened before and after. Unfortunately, this is not easy to achieve in Node due to its async nature, see code examples inside

**Otherwise:** Looking at a production error log without the context – what happened before – makes it much harder and slower to reason about the issue

🔗 [**Read More: Assign ‘TransactionId’ to each log statement**](/sections/production/assigntransactionid.md)

<br/><br/>

## ![✔] 5.15. Set NODE_ENV=production

**TL;DR:** Set the environment variable NODE_ENV to ‘production’ or ‘development’ to flag whether production optimizations should get activated – many npm packages determine the current environment and optimize their code for production

**Otherwise:** Omitting this simple property might greatly degrade performance. For example, when using Express for server-side rendering omitting `NODE_ENV` makes it slower by a factor of three!

🔗 [**Read More: Set NODE_ENV=production**](/sections/production/setnodeenv.md)

<br/><br/>

## ![✔] 5.16. Design automated, atomic and zero-downtime deployments

**TL;DR:** Research shows that teams who perform many deployments lower the probability of severe production issues. Fast and automated deployments that don’t require risky manual steps and service downtime significantly improve the deployment process. You should probably achieve this using Docker combined with CI tools as they became the industry standard for streamlined deployment

**Otherwise:** Long deployments -> production downtime & human-related error -> team unconfident in making deployment -> fewer deployments and features

<br/><br/>

## ![✔] 5.17. Use an LTS release of Node.js

**TL;DR:** Ensure you are using an LTS version of Node.js to receive critical bug fixes, security updates and performance improvements

**Otherwise:** Newly discovered bugs or vulnerabilities could be used to exploit an application running in production, and your application may become unsupported by various modules and harder to maintain

🔗 [**Read More: Use an LTS release of Node.js**](/sections/production/LTSrelease.md)

<br/><br/>

## ![✔] 5.18. Don't route logs within the app

**TL;DR:** Log destinations should not be hard-coded by developers within the application code, but instead should be defined by the execution environment the application runs in. Developers should write logs to `stdout` using a logger utility and then let the execution environment (container, server, etc.) pipe the `stdout` stream to the appropriate destination (i.e. Splunk, Graylog, ElasticSearch, etc.).

**Otherwise:** Application handling log routing === hard to scale, loss of logs, poor separation of concerns

🔗 [**Read More: Log Routing**](/sections/production/logrouting.md)

<br/><br/><br/>

<p align="right"><a href="#table-of-contents">⬆ Return to top</a></p>

# `6. Security Best Practices`

<div align="center">
<img src="https://img.shields.io/badge/OWASP%20Threats-Top%2010-green.svg" alt="54 items"/>
</div>

## ![✔] 6.1. Embrace linter security rules

<a href="https://www.owasp.org/index.php/Top_10-2017_A1-Injection" target="_blank"><img src="https://img.shields.io/badge/%E2%9C%94%20OWASP%20Threats%20-%20A1:Injection%20-green.svg" alt=""/></a> <a href="https://www.owasp.org/index.php/Top_10-2017_A7-Cross-Site_Scripting_(XSS)" target="_blank"><img src="https://img.shields.io/badge/%E2%9C%94%20OWASP%20Threats%20-%20XSS%20-green.svg" alt=""/></a>

**TL;DR:** Make use of security-related linter plugins such as [eslint-plugin-security](https://github.com/nodesecurity/eslint-plugin-security) to catch security vulnerabilities and issues as early as possible, preferably while they're being coded. This can help catching security weaknesses like using eval, invoking a child process or importing a module with a string literal (e.g. user input). Click 'Read more' below to see code examples that will get caught by a security linter

**Otherwise:** What could have been a straightforward security weakness during development becomes a major issue in production. Also, the project may not follow consistent code security practices, leading to vulnerabilities being introduced, or sensitive secrets committed into remote repositories

🔗 [**Read More: Lint rules**](/sections/security/lintrules.md)

<br/><br/>

## ![✔] 6.2. Limit concurrent requests using a middleware

<a href="https://www.owasp.org/index.php/Denial_of_Service" target="_blank"><img src="https://img.shields.io/badge/%E2%9C%94%20OWASP%20Threats%20-%20DDOS%20-green.svg" alt=""/></a>

**TL;DR:** DOS attacks are very popular and relatively easy to conduct. Implement rate limiting using an external service such as cloud load balancers, cloud firewalls, nginx, [rate-limiter-flexible](https://www.npmjs.com/package/rate-limiter-flexible) package, or (for smaller and less critical apps) a rate-limiting middleware (e.g. [express-rate-limit](https://www.npmjs.com/package/express-rate-limit))

**Otherwise:** An application could be subject to an attack resulting in a denial of service where real users receive a degraded or unavailable service.

🔗 [**Read More: Implement rate limiting**](/sections/security/limitrequests.md)

<br/><br/>

## ![✔] 6.3 Extract secrets from config files or use packages to encrypt them

<a href="https://www.owasp.org/index.php/Top_10-2017_A6-Security_Misconfiguration" target="_blank"><img src="https://img.shields.io/badge/%E2%9C%94%20OWASP%20Threats%20-%20A6:Security%20Misconfiguration%20-green.svg" alt=""/></a> <a href="https://www.owasp.org/index.php/Top_10-2017_A3-Sensitive_Data_Exposure" target="_blank"><img src="https://img.shields.io/badge/%E2%9C%94%20OWASP%20Threats%20-%20A3:Sensitive%20Data%20Exposure%20-green.svg" alt=""/></a>

**TL;DR:** Never store plain-text secrets in configuration files or source code. Instead, make use of secret-management systems like Vault products, Kubernetes/Docker Secrets, or using environment variables. As a last resort, secrets stored in source control must be encrypted and managed (rolling keys, expiring, auditing, etc). Make use of pre-commit/push hooks to prevent committing secrets accidentally

**Otherwise:** Source control, even for private repositories, can mistakenly be made public, at which point all secrets are exposed. Access to source control for an external party will inadvertently provide access to related systems (databases, apis, services, etc).

🔗 [**Read More: Secret management**](/sections/security/secretmanagement.md)

<br/><br/>

## ![✔] 6.4. Prevent query injection vulnerabilities with ORM/ODM libraries

<a href="https://www.owasp.org/index.php/Top_10-2017_A1-Injection" target="_blank"><img src="https://img.shields.io/badge/%E2%9C%94%20OWASP%20Threats%20-%20A1:Injection%20-green.svg" alt=""/></a>

**TL;DR:** To prevent SQL/NoSQL injection and other malicious attacks, always make use of an ORM/ODM or a database library that escapes data or supports named or indexed parameterized queries, and takes care of validating user input for expected types. Never just use JavaScript template strings or string concatenation to inject values into queries as this opens your application to a wide spectrum of vulnerabilities. All the reputable Node.js data access libraries (e.g. [Sequelize](https://github.com/sequelize/sequelize), [Knex](https://github.com/tgriesser/knex), [mongoose](https://github.com/Automattic/mongoose)) have built-in protection against injection attacks.

**Otherwise:** Unvalidated or unsanitized user input could lead to operator injection when working with MongoDB for NoSQL, and not using a proper sanitization system or ORM will easily allow SQL injection attacks, creating a giant vulnerability.

🔗 [**Read More: Query injection prevention using ORM/ODM libraries**](/sections/security/ormodmusage.md)

<br/><br/>

## ![✔] 6.5. Collection of generic security best practices

**TL;DR:** This is a collection of security advice that is not related directly to Node.js - the Node implementation is not much different than any other language. Click read more to skim through.

🔗 [**Read More: Common security best practices**](/sections/security/commonsecuritybestpractices.md)

<br/><br/>

## ![✔] 6.6. Adjust the HTTP response headers for enhanced security

<a href="https://www.owasp.org/index.php/Top_10-2017_A6-Security_Misconfiguration" target="_blank"><img src="https://img.shields.io/badge/%E2%9C%94%20OWASP%20Threats%20-%20A6:Security%20Misconfiguration%20-green.svg" alt=""/></a>

**TL;DR:** Your application should be using secure headers to prevent attackers from using common attacks like cross-site scripting (XSS), clickjacking and other malicious attacks. These can be configured easily using modules like [helmet](https://www.npmjs.com/package/helmet).

**Otherwise:** Attackers could perform direct attacks on your application's users, leading to huge security vulnerabilities

🔗 [**Read More: Using secure headers in your application**](/sections/security/secureheaders.md)

<br/><br/>

## ![✔] 6.7. Constantly and automatically inspect for vulnerable dependencies

<a href="https://www.owasp.org/index.php/Top_10-2017_A9-Using_Components_with_Known_Vulnerabilities" target="_blank"><img src="https://img.shields.io/badge/%E2%9C%94%20OWASP%20Threats%20-%20A9:Known%20Vulnerabilities%20-green.svg" alt=""/></a>

**TL;DR:** With the npm ecosystem it is common to have many dependencies for a project. Dependencies should always be kept in check as new vulnerabilities are found. Use tools like [npm audit](https://docs.npmjs.com/cli/audit) or [snyk](https://snyk.io/) to track, monitor and patch vulnerable dependencies. Integrate these tools with your CI setup so you catch a vulnerable dependency before it makes it to production.

**Otherwise:** An attacker could detect your web framework and attack all its known vulnerabilities.

🔗 [**Read More: Dependency security**](/sections/security/dependencysecurity.md)

<br/><br/>

## ![✔] 6.8. Avoid using the Node.js crypto library for handling passwords, use Bcrypt

<a href="https://www.owasp.org/index.php/Top_10-2017_A2-Broken_Authentication" target="_blank"><img src="https://img.shields.io/badge/%E2%9C%94%20OWASP%20Threats%20-%20A9:Broken%20Authentication%20-green.svg" alt=""/></a>

**TL;DR:** Passwords or secrets (API keys) should be stored using a secure hash + salt function like `bcrypt`, that should be a preferred choice over its JavaScript implementation due to performance and security reasons.

**Otherwise:** Passwords or secrets that are persisted without using a secure function are vulnerable to brute forcing and dictionary attacks that will lead to their disclosure eventually.

🔗 [**Read More: Use Bcrypt**](/sections/security/bcryptpasswords.md)

<br/><br/>

## ![✔] 6.9. Escape HTML, JS and CSS output

<a href="https://www.owasp.org/index.php/Top_10-2017_A7-Cross-Site_Scripting_(XSS)" target="_blank"><img src="https://img.shields.io/badge/%E2%9C%94%20OWASP%20Threats%20-%20A7:XSS%20-green.svg" alt=""/></a>

**TL;DR:** Untrusted data that is sent down to the browser might get executed instead of just being displayed, this is commonly referred as a cross-site-scripting (XSS) attack. Mitigate this by using dedicated libraries that explicitly mark the data as pure content that should never get executed (i.e. encoding, escaping)

**Otherwise:** An attacker might store malicious JavaScript code in your DB which will then be sent as-is to the poor clients

🔗 [**Read More: Escape output**](/sections/security/escape-output.md)

<br/><br/>

## ![✔] 6.10. Validate incoming JSON schemas

<a href="https://www.owasp.org/index.php/Top_10-2017_A7-Cross-Site_Scripting_(XSS)" target="_blank"><img src="https://img.shields.io/badge/%E2%9C%94%20OWASP%20Threats%20-%20A7: XSS%20-green.svg" alt=""/></a> <a href="https://www.owasp.org/index.php/Top_10-2017_A8-Insecure_Deserialization" target="_blank"><img src="https://img.shields.io/badge/%E2%9C%94%20OWASP%20Threats%20-%20A8:Insecured%20Deserialization%20-green.svg" alt=""/></a>

**TL;DR:** Validate the incoming requests' body payload and ensure it meets expectations, fail fast if it doesn't. To avoid tedious validation coding within each route you may use lightweight JSON-based validation schemas such as [jsonschema](https://www.npmjs.com/package/jsonschema) or [joi](https://www.npmjs.com/package/joi)

**Otherwise:** Your generosity and permissive approach greatly increases the attack surface and encourages the attacker to try out many inputs until they find some combination to crash the application

🔗 [**Read More: Validate incoming JSON schemas**](/sections/security/validation.md)

<br/><br/>

## ![✔] 6.11. Support blacklisting JWTs

<a href="https://www.owasp.org/index.php/Top_10-2017_A2-Broken_Authentication" target="_blank"><img src="https://img.shields.io/badge/%E2%9C%94%20OWASP%20Threats%20-%20A9:Broken%20Authentication%20-green.svg" alt=""/></a>

**TL;DR:** When using JSON Web Tokens (for example, with [Passport.js](https://github.com/jaredhanson/passport)), by default there's no mechanism to revoke access from issued tokens. Once you discover some malicious user activity, there's no way to stop them from accessing the system as long as they hold a valid token. Mitigate this by implementing a blacklist of untrusted tokens that are validated on each request.

**Otherwise:** Expired, or misplaced tokens could be used maliciously by a third party to access an application and impersonate the owner of the token.

🔗 [**Read More: Blacklist JSON Web Tokens**](/sections/security/expirejwt.md)

<br/><br/>

## ![✔] 6.12. Prevent brute-force attacks against authorization

<a href="https://www.owasp.org/index.php/Top_10-2017_A2-Broken_Authentication" target="_blank"><img src="https://img.shields.io/badge/%E2%9C%94%20OWASP%20Threats%20-%20A9:Broken%20Authentication%20-green.svg" alt=""/></a>

**TL;DR:** A simple and powerful technique is to limit authorization attempts using two metrics:

1. The first is number of consecutive failed attempts by the same user unique ID/name and IP address.
2. The second is number of failed attempts from an IP address over some long period of time. For example, block an IP address if it makes 100 failed attempts in one day.

**Otherwise:** An attacker can issue unlimited automated password attempts to gain access to privileged accounts on an application

🔗 [**Read More: Login rate limiting**](/sections/security/login-rate-limit.md)

<br/><br/>

## ![✔] 6.13. Run Node.js as non-root user

<a href="https://www.owasp.org/index.php/Top_10-2017_A5-Broken_Access_Control" target="_blank"><img src="https://img.shields.io/badge/%E2%9C%94%20OWASP%20Threats%20-%20A5:Broken%20Access%20Access%20Control-green.svg" alt=""/></a>

**TL;DR:** There is a common scenario where Node.js runs as a root user with unlimited permissions. For example, this is the default behaviour in Docker containers. It's recommended to create a non-root user and either bake it into the Docker image (examples given below) or run the process on this user's behalf by invoking the container with the flag "-u username"

**Otherwise:** An attacker who manages to run a script on the server gets unlimited power over the local machine (e.g. change iptable and re-route traffic to his server)

🔗 [**Read More: Run Node.js as non-root user**](/sections/security/non-root-user.md)

<br/><br/>

## ![✔] 6.14. Limit payload size using a reverse-proxy or a middleware

<a href="https://www.owasp.org/index.php/Top_10-2017_A8-Insecure_Deserialization" target="_blank"><img src="https://img.shields.io/badge/%E2%9C%94%20OWASP%20Threats%20-%20A8:Insecured%20Deserialization%20-green.svg" alt=""/></a> <a href="https://www.owasp.org/index.php/Top_10-2017_A1-Injection" target="_blank"><img src="https://img.shields.io/badge/%E2%9C%94%20OWASP%20Threats%20-%20DDOS%20-green.svg" alt=""/></a>

**TL;DR:** The bigger the body payload is, the harder your single thread works in processing it. This is an opportunity for attackers to bring servers to their knees without tremendous amount of requests (DOS/DDOS attacks). Mitigate this limiting the body size of incoming requests on the edge (e.g. firewall, ELB) or by configuring [express body parser](https://github.com/expressjs/body-parser) to accept only small-size payloads

**Otherwise:** Your application will have to deal with large requests, unable to process the other important work it has to accomplish, leading to performance implications and vulnerability towards DOS attacks

🔗 [**Read More: Limit payload size**](/sections/security/requestpayloadsizelimit.md)

<br/><br/>

## ![✔] 6.15. Avoid JavaScript eval statements

<a href="https://www.owasp.org/index.php/Top_10-2017_A7-Cross-Site_Scripting_(XSS)" target="_blank"><img src="https://img.shields.io/badge/%E2%9C%94%20OWASP%20Threats%20-%20A7:XSS%20-green.svg" alt=""/></a> <a href="https://www.owasp.org/index.php/Top_10-2017_A1-Injection" target="_blank"><img src="https://img.shields.io/badge/%E2%9C%94%20OWASP%20Threats%20-%20A1:Injection%20-green.svg" alt=""/></a> <a href="https://www.owasp.org/index.php/Top_10-2017_A4-XML_External_Entities_(XXE)" target="_blank"><img src="https://img.shields.io/badge/%E2%9C%94%20OWASP%20Threats%20-%20A4:External%20Entities%20-green.svg" alt=""/></a>

**TL;DR:** `eval` is evil as it allows executing custom JavaScript code during run time. This is not just a performance concern but also an important security concern due to malicious JavaScript code that may be sourced from user input. Another language feature that should be avoided is `new Function` constructor. `setTimeout` and `setInterval` should never be passed dynamic JavaScript code either.

**Otherwise:** Malicious JavaScript code finds a way into text passed into `eval` or other real-time evaluating JavaScript language functions, and will gain complete access to JavaScript permissions on the page. This vulnerability is often manifested as an XSS attack.

🔗 [**Read More: Avoid JavaScript eval statements**](/sections/security/avoideval.md)

<br/><br/>

## ![✔] 6.16. Prevent evil RegEx from overloading your single thread execution

<a href="https://www.owasp.org/index.php/Denial_of_Service" target="_blank"><img src="https://img.shields.io/badge/%E2%9C%94%20OWASP%20Threats%20-%20DDOS%20-green.svg" alt=""/></a>

**TL;DR:** Regular Expressions, while being handy, pose a real threat to JavaScript applications at large, and the Node.js platform in particular. A user input for text to match might require an outstanding amount of CPU cycles to process. RegEx processing might be inefficient to an extent that a single request that validates 10 words can block the entire event loop for 6 seconds and set the CPU on 🔥. For that reason, prefer third-party validation packages like [validator.js](https://github.com/chriso/validator.js) instead of writing your own Regex patterns, or make use of [safe-regex](https://github.com/substack/safe-regex) to detect vulnerable regex patterns

**Otherwise:** Poorly written regexes could be susceptible to Regular Expression DoS attacks that will block the event loop completely. For example, the popular `moment` package was found vulnerable with malicious RegEx usage in November of 2017

🔗 [**Read More: Prevent malicious RegEx**](/sections/security/regex.md)

<br/><br/>

## ![✔] 6.17. Avoid module loading using a variable

<a href="https://www.owasp.org/index.php/Top_10-2017_A7-Cross-Site_Scripting_(XSS)" target="_blank"><img src="https://img.shields.io/badge/%E2%9C%94%20OWASP%20Threats%20-%20A7:XSS%20-green.svg" alt=""/></a> <a href="https://www.owasp.org/index.php/Top_10-2017_A1-Injection" target="_blank"><img src="https://img.shields.io/badge/%E2%9C%94%20OWASP%20Threats%20-%20A1:Injection%20-green.svg" alt=""/></a> <a href="https://www.owasp.org/index.php/Top_10-2017_A4-XML_External_Entities_(XXE)" target="_blank"><img src="https://img.shields.io/badge/%E2%9C%94%20OWASP%20Threats%20-%20A4:External%20Entities%20-green.svg" alt=""/></a>

**TL;DR:** Avoid requiring/importing another file with a path that was given as parameter due to the concern that it could have originated from user input. This rule can be extended for accessing files in general (i.e. `fs.readFile()`) or other sensitive resource access with dynamic variables originating from user input. [Eslint-plugin-security](https://www.npmjs.com/package/eslint-plugin-security) linter can catch such patterns and warn early enough

**Otherwise:** Malicious user input could find its way to a parameter that is used to require tampered files, for example, a previously uploaded file on the filesystem, or access already existing system files.

🔗 [**Read More: Safe module loading**](/sections/security/safemoduleloading.md)

<br/><br/>

## ![✔] 6.18. Run unsafe code in a sandbox

<a href="https://www.owasp.org/index.php/Top_10-2017_A7-Cross-Site_Scripting_(XSS)" target="_blank"><img src="https://img.shields.io/badge/%E2%9C%94%20OWASP%20Threats%20-%20A7:XSS%20-green.svg" alt=""/></a> <a href="https://www.owasp.org/index.php/Top_10-2017_A1-Injection" target="_blank"><img src="https://img.shields.io/badge/%E2%9C%94%20OWASP%20Threats%20-%20A1:Injection%20-green.svg" alt=""/></a> <a href="https://www.owasp.org/index.php/Top_10-2017_A4-XML_External_Entities_(XXE)" target="_blank"><img src="https://img.shields.io/badge/%E2%9C%94%20OWASP%20Threats%20-%20A4:External%20Entities%20-green.svg" alt=""/></a>

**TL;DR:** When tasked to run external code that is given at run-time (e.g. plugin), use any sort of 'sandbox' execution environment that isolates and guards the main code against the plugin. This can be achieved using a dedicated process (e.g. `cluster.fork()`), serverless environment or dedicated npm packages that act as a sandbox

**Otherwise:** A plugin can attack through an endless variety of options like infinite loops, memory overloading, and access to sensitive process environment variables

🔗 [**Read More: Run unsafe code in a sandbox**](/sections/security/sandbox.md)

<br/><br/>

## ![✔] 6.19. Take extra care when working with child processes

<a href="https://www.owasp.org/index.php/Top_10-2017_A7-Cross-Site_Scripting_(XSS)" target="_blank"><img src="https://img.shields.io/badge/%E2%9C%94%20OWASP%20Threats%20-%20A7:XSS%20-green.svg" alt=""/></a> <a href="https://www.owasp.org/index.php/Top_10-2017_A1-Injection" target="_blank"><img src="https://img.shields.io/badge/%E2%9C%94%20OWASP%20Threats%20-%20A1:Injection%20-green.svg" alt=""/></a> <a href="https://www.owasp.org/index.php/Top_10-2017_A4-XML_External_Entities_(XXE)" target="_blank"><img src="https://img.shields.io/badge/%E2%9C%94%20OWASP%20Threats%20-%20A4:External%20Entities%20-green.svg" alt=""/></a>

**TL;DR:** Avoid using child processes when possible and validate and sanitize input to mitigate shell injection attacks if you still have to. Prefer using `child_process.execFile` which by definition will only execute a single command with a set of attributes and will not allow shell parameter expansion.

**Otherwise:** Naive use of child processes could result in remote command execution or shell injection attacks due to malicious user input passed to an unsanitized system command.

🔗 [**Read More: Be cautious when working with child processes**](/sections/security/childprocesses.md)

<br/><br/>

## ![✔] 6.20. Hide error details from clients

<a href="https://www.owasp.org/index.php/Top_10-2017_A6-Security_Misconfiguration" target="_blank"><img src="https://img.shields.io/badge/%E2%9C%94%20OWASP%20Threats%20-%20A6:Security%20Misconfiguration%20-green.svg" alt=""/></a>

**TL;DR:** An integrated express error handler hides the error details by default. However, great are the chances that you implement your own error handling logic with custom Error objects (considered by many as a best practice). If you do so, ensure not to return the entire Error object to the client, which might contain some sensitive application details

**Otherwise:** Sensitive application details such as server file paths, third party modules in use, and other internal workflows of the application which could be exploited by an attacker, could be leaked from information found in a stack trace

🔗 [**Read More: Hide error details from client**](/sections/security/hideerrors.md)

<br/><br/>

## ![✔] 6.21. Configure 2FA for npm or Yarn

<a href="https://www.owasp.org/index.php/Top_10-2017_A6-Security_Misconfiguration" target="_blank"><img src="https://img.shields.io/badge/%E2%9C%94%20OWASP%20Threats%20-%20A6:Security%20Misconfiguration%20-green.svg" alt=""/></a>

**TL;DR:** Any step in the development chain should be protected with MFA (multi-factor authentication), npm/Yarn are a sweet opportunity for attackers who can get their hands on some developer's password. Using developer credentials, attackers can inject malicious code into libraries that are widely installed across projects and services. Maybe even across the web if published in public. Enabling 2-factor-authentication in npm leaves almost zero chances for attackers to alter your package code.

**Otherwise:** [Have you heard about the eslint developer who's password was hijacked?](https://medium.com/@oprearocks/eslint-backdoor-what-it-is-and-how-to-fix-the-issue-221f58f1a8c8)

<br/><br/>

## ![✔] 6.22. Modify session middleware settings

<a href="https://www.owasp.org/index.php/Top_10-2017_A6-Security_Misconfiguration" target="_blank"><img src="https://img.shields.io/badge/%E2%9C%94%20OWASP%20Threats%20-%20A6:Security%20Misconfiguration%20-green.svg" alt=""/></a>

**TL;DR:** Each web framework and technology has its known weaknesses - telling an attacker which web framework we use is a great help for them. Using the default settings for session middlewares can expose your app to module- and framework-specific hijacking attacks in a similar way to the `X-Powered-By` header. Try hiding anything that identifies and reveals your tech stack (E.g. Node.js, express)

**Otherwise:** Cookies could be sent over insecure connections, and an attacker might use session identification to identify the underlying framework of the web application, as well as module-specific vulnerabilities

🔗 [**Read More: Cookie and session security**](/sections/security/sessions.md)

<br/><br/>

## ![✔] 6.23. Avoid DOS attacks by explicitly setting when a process should crash

<a href="https://www.owasp.org/index.php/Denial_of_Service" target="_blank"><img src="https://img.shields.io/badge/%E2%9C%94%20OWASP%20Threats%20-%20DDOS%20-green.svg" alt=""/></a>

**TL;DR:** The Node process will crash when errors are not handled. Many best practices even recommend to exit even though an error was caught and got handled. Express, for example, will crash on any asynchronous error - unless you wrap routes with a catch clause. This opens a very sweet attack spot for attackers who recognize what input makes the process crash and repeatedly send the same request. There's no instant remedy for this but a few techniques can mitigate the pain: Alert with critical severity anytime a process crashes due to an unhandled error, validate the input and avoid crashing the process due to invalid user input, wrap all routes with a catch and consider not to crash when an error originated within a request (as opposed to what happens globally)

**Otherwise:** This is just an educated guess: given many Node.js applications, if we try passing an empty JSON body to all POST requests - a handful of applications will crash. At that point, we can just repeat sending the same request to take down the applications with ease

<br/><br/>

## ![✔] 6.24. Prevent unsafe redirects

<a href="https://www.owasp.org/index.php/Top_10-2017_A1-Injection" target="_blank"><img src="https://img.shields.io/badge/%E2%9C%94%20OWASP%20Threats%20-%20A1:Injection%20-green.svg" alt=""/></a>

**TL;DR:** Redirects that do not validate user input can enable attackers to launch phishing scams, steal user credentials, and perform other malicious actions.

**Otherwise:** If an attacker discovers that you are not validating external, user-supplied input, they may exploit this vulnerability by posting specially-crafted links on forums, social media, and other public places to get users to click it.

🔗 [**Read More: Prevent unsafe redirects**](/sections/security/saferedirects.md)

<br/><br/>

## ![✔] 6.25. Avoid publishing secrets to the npm registry

<a href="https://www.owasp.org/index.php/Top_10-2017_A6-Security_Misconfiguration" target="_blank"><img src="https://img.shields.io/badge/%E2%9C%94%20OWASP%20Threats%20-%20A6:Security%20Misconfiguration%20-green.svg" alt=""/></a>

**TL;DR:** Precautions should be taken to avoid the risk of accidentally publishing secrets to public npm registries. An `.npmignore` file can be used to blacklist specific files or folders, or the `files` array in `package.json` can act as a whitelist.

**Otherwise:** Your project's API keys, passwords or other secrets are open to be abused by anyone who comes across them, which may result in financial loss, impersonation, and other risks.

🔗 [**Read More: Avoid publishing secrets**](/sections/security/avoid_publishing_secrets.md)
<br/><br/><br/>

<p align="right"><a href="#table-of-contents">⬆ Return to top</a></p>

# `7. Performance Best Practices`

## Our contributors are working on this section. [Would you like to join?](https://github.com/i0natan/nodebestpractices/issues/256)

## ![✔] 7.1. Prefer native JS methods over user-land utils like Lodash

 **TL;DR:** It's often more penalising to use utility libraries like `lodash` and `underscore` over native methods as it leads to unneeded dependencies and slower performance.
 Bear in mind that with the introduction of the new V8 engine alongside the new ES standards, native methods were improved in such a way that it's now about 50% more performant than utility libraries.

**Otherwise:** You'll have to maintain less performant projects where you could have simply used what was **already** available or dealt with a few more lines in exchange of a few more files.

🔗 [**Read More: Native over user land utils**](/sections/performance/nativeoverutil.md)

<br/><br/><br/>

# Milestones

To maintain this guide and keep it up to date, we are constantly updating and improving the guidelines and best practices with the help of the community. You can follow our [milestones](https://github.com/i0natan/nodebestpractices/milestones) and join the working groups if you want to contribute to this project

<br/>

## Translations

All translations are contributed by the community. We will be happy to get any help with either completed, ongoing or new translations!

### Completed translations

- ![BR](/assets/flags/BR.png) [Brazilian Portuguese](/README.brazilian-portuguese.md) - Courtesy of [Marcelo Melo](https://github.com/marcelosdm)
- ![CN](/assets/flags/CN.png) [Chinese](README.chinese.md) - Courtesy of [Matt Jin](https://github.com/mattjin)

### Translations in progress

- ![FR](/assets/flags/FR.png) [French](https://github.com/gaspaonrocks/nodebestpractices/blob/french-translation/README.french.md) ([Discussion](https://github.com/i0natan/nodebestpractices/issues/129))
- ![HE](/assets/flags/HE.png) Hebrew ([Discussion](https://github.com/i0natan/nodebestpractices/issues/156))
- ![KR](/assets/flags/KR.png) [Korean](README.korean.md) - Courtesy of [Sangbeom Han](https://github.com/uronly14me) ([Discussion](https://github.com/i0natan/nodebestpractices/issues/94))
- ![RU](/assets/flags/RU.png) [Russian](https://github.com/i0natan/nodebestpractices/blob/russian-translation/README.russian.md) ([Discussion](https://github.com/i0natan/nodebestpractices/issues/105))
- ![ES](/assets/flags/ES.png) [Spanish](https://github.com/i0natan/nodebestpractices/blob/spanish-translation/README.spanish.md) ([Discussion](https://github.com/i0natan/nodebestpractices/issues/95))
- ![TR](/assets/flags/TR.png) Turkish ([Discussion](https://github.com/i0natan/nodebestpractices/issues/139))

<br/><br/>

## Steering Committee

Meet the steering committee members - the people who work together to provide guidance and future direction to the project. In addition, each member of the committee leads a project tracked under our [Github projects](https://github.com/i0natan/nodebestpractices/projects).

<img align="left" width="100" height="100" src="assets/images/members/yoni.png">

[Yoni Goldberg](https://github.com/i0natan)
<a href="https://twitter.com/goldbergyoni"><img src="assets/images/twitter-s.png" width="16" height="16"></img></a>
<a href="https://goldbergyoni.com"><img src="assets/images/www.png" width="16" height="16"></img></a>

Independent Node.js consultant who works with customers in USA, Europe, and Israel on building large scale scalable Node applications. Many of the best practices above were first published at [goldbergyoni.com](https://goldbergyoni.com). Reach Yoni at @goldbergyoni or me@goldbergyoni.com

<br/>

<img align="left" width="100" height="100" src="assets/images/members/bruno.png">

[Bruno Scheufler](https://github.com/BrunoScheufler)
<a href="https://brunoscheufler.com/"><img src="assets/images/www.png" width="16" height="16"></img></a>

💻 full-stack web engineer, Node.js & GraphQL enthusiast

<br/>

<img align="left" width="100" height="100" src="assets/images/members/kyle.png">

[Kyle Martin](https://github.com/js-kyle)
<a href="https://twitter.com/kylemartin_93"><img src="assets/images/twitter-s.png" width="16" height="16"></img></a>
<a href="https://www.linkedin.com/in/kylemartinnz"><img src="assets/images/linkedin.png" width="16" height="16"></img></a>

Full Stack Developer & Site Reliability Engineer based in New Zealand, interested in web application security, and architecting and building Node.js applications to perform at global scale.

<br/>

<img align="left" width="100" height="100" src="assets/images/members/sagir.png">

[Sagir Khan](https://github.com/sagirk)
<a href="https://twitter.com/sagir_k"><img src="assets/images/twitter-s.png" width="16" height="16"></img></a>
<a href="https://sagirk.com"><img src="assets/images/www.png" width="16" height="16"></img></a>
<a href="https://linkedin.com/in/sagirk"><img src="assets/images/linkedin.png" width="16" height="16"></img></a>

Deep specialist in JavaScript and its ecosystem — React, Node.js, MongoDB, pretty much anything that involves using JavaScript/JSON in any layer of the system — building products using the web platform for the world’s most recognized brands. Individual Member of the Node.js Foundation, collaborating on the Community Committee's Website Redesign Initiative.

<br/>

## Collaborators

Thank you to all our collaborators! 🙏

Our collaborators are members who are contributing to the repository on a reguar basis, through suggesting new best practices, triaging issues, reviewing pull requests and more. If you are interested in helping us guide thousands of people to craft better Node.js applications, please read our [contributor guidelines](/.operations/CONTRIBUTING.md) 🎉

| <a href="https://github.com/idori" target="_blank"><img src="assets/images/members/ido.png" width="75" height="75"></a> | <a href="https://github.com/TheHollidayInn" target="_blank"><img src="assets/images/members/keith.png" width="75" height="75"></a> |
| :--: | :--: |
| [Ido Richter (Founder)](https://github.com/idori) | [Keith Holliday](https://github.com/TheHollidayInn) |

### Past collaborators

| <a href="https://github.com/refack" target="_blank"><img src="assets/images/members/refael.png" width="50" height="50"></a> |
| :--: |
| [Refael Ackermann](https://github.com/refack) |

<br/>

## Thank You Notes

We appreciate any contribution, from a single word fix to a new best practice. Below is a list of everyone who contributed to this project. A 🌻 marks a successful pull request and a ⭐ marks an approved new best practice.

### Flowers

🌻 [Kevin Rambaud](https://github.com/kevinrambaud),
🌻 [Michael Fine](https://github.com/mfine15),
🌻 [Shreya Dahal](https://github.com/squgeim),
🌻 [ChangJoo Park](https://github.com/ChangJoo-Park),
🌻 [Matheus Cruz Rocha](https://github.com/matheusrocha89),
🌻 [Yog Mehta](https://github.com/BitYog),
🌻 [Kudakwashe Paradzayi](https://github.com/kudapara),
🌻 [t1st3](https://github.com/t1st3),
🌻 [mulijordan1976](https://github.com/mulijordan1976),
🌻 [Matan Kushner](https://github.com/matchai),
🌻 [Fabio Hiroki](https://github.com/fabiothiroki),
🌻 [James Sumners](https://github.com/jsumners),
🌻 [Chandan Rai](https://github.com/crowchirp),
🌻 [Dan Gamble](https://github.com/dan-gamble),
🌻 [PJ Trainor](https://github.com/trainorpj),
🌻 [Remek Ambroziak](https://github.com/reod),
🌻 [Yoni Jah](https://github.com/yonjah),
🌻 [Misha Khokhlov](https://github.com/hazolsky),
🌻 [Evgeny Orekhov](https://github.com/EvgenyOrekhov),
🌻 [Gediminas Petrikas](https://github.com/gediminasml),
🌻 [Isaac Halvorson](https://github.com/hisaac),
🌻 [Vedran Karačić](https://github.com/vkaracic),
🌻 [lallenlowe](https://github.com/lallenlowe),
🌻 [Nathan Wells](https://github.com/nwwells),
🌻 [Paulo Vítor S Reis](https://github.com/paulovitin),
🌻 [syzer](https://github.com/syzer),
🌻 [David Sancho](https://github.com/davesnx),
🌻 [Robert Manolea](https://github.com/pupix),
🌻 [Xavier Ho](https://github.com/spaxe),
🌻 [Aaron Arney](https://github.com/ocularrhythm),
🌻 [Jan Charles Maghirang Adona](https://github.com/septa97),
🌻 [Allen Fang](https://github.com/AllenFang),
🌻 [Leonardo Villela](https://github.com/leonardovillela),
🌻 [Michal Zalecki](https://github.com/MichalZalecki)
🌻 [Chris Nicola](https://github.com/chrisnicola),
🌻 [Alejandro Corredor](https://github.com/aecorredor),
🌻 [Ye Min Htut](https://github.com/ymhtut),
🌻 [cwar](https://github.com/cwar),
🌻 [Yuwei](https://github.com/keyfoxth),
🌻 [Utkarsh Bhatt](https://github.com/utkarshbhatt12),
🌻 [Duarte Mendes](https://github.com/duartemendes),
🌻 [Sagir Khan](https://github.com/sagirk),
🌻 [Jason Kim](https://github.com/serv),
🌻 [Mitja O.](https://github.com/Max101),
🌻 [Sandro Miguel Marques](https://github.com/SandroMiguel),
🌻 [Gabe Kuslansky](https://github.com/GabeKuslansky),
🌻 [Ron Gross](https://github.com/ripper234),
🌻 [Valeri Karpov](https://github.com/vkarpov15)
🌻 [Sergio](https://github.com/imsergiobernal),
🌻 [Duarte Mendes](https://github.com/duartemendes),
🌻 [Nikola Telkedzhiev](https://github.com/ntelkedzhiev),
🌻 [Vitor Godoy](https://github.com/vitordagamagodoy),
🌻 [Manish Saraan](https://github.com/manishsaraan),
🌻 [Sangbeom Han](https://github.com/uronly14me),
🌻 [blackmatch](https://github.com/blackmatch),
🌻 [Joe Reeve](https://github.com/ISNIT0),
🌻 [Marcelo Melo](https://github.com/marcelosdm),
🌻 [Ryan Busby](https://github.com/BusbyActual),
🌻 [Iman Mohamadi](https://github.com/ImanMh),
🌻 [Remek Ambroziak](https://github.com/reod),
🌻 [Sergii Paryzhskyi](https://github.com/HeeL),
🌻 [Kapil Patel](https://github.com/kapilepatel),
🌻 [迷渡](https://github.com/justjavac),
🌻 [Hozefa](https://github.com/hozefaj),
🌻 [Ethan](https://github.com/el-ethan),
🌻 [Sam](https://github.com/milkdeliver),
🌻 [Arlind](https://github.com/ArlindXh),
🌻 [Teddy Toussaint](https://github.com/ttous),
🌻 [Lewis](https://github.com/LewisArdern),
🌻 [DouglasMV](https://github.com/DouglasMV),
🌻 [Corey Cleary](https://github.com/coreyc),
🌻 [Mehmet Perk](https://github.com/mperk),
🌻 [Ryan Ouyang](https://github.com/ryanouyang),
🌻 [Gabriel Lidenor](https://github.com/GabrielLidenor),
🌻 [Roman](https://github.com/animir),
🌻 [Francozeira](https://github.com/Francozeira)

### Stars

⭐ [Kyle Martin](https://github.com/js-kyle),
⭐ [Keith Holliday](https://github.com/TheHollidayInn),
⭐ [Corey Cleary](https://github.com/coreyc),
⭐ [Maximilian Berkmann](https://github.com/Berkmann18),
⭐ [DouglasMV](https://github.com/DouglasMV),
⭐ [Marcelo Melo](https://github.com/marcelosdm),
⭐ [Mehmet Perk](https://github.com/mperk),
⭐ [Ryan Ouyang](https://github.com/ryanouyang)

<br/><br/><br/>
