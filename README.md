# Общие стандарты верстки и написания однородного CSS-кода

Этот документ не закончен, и новые идеи всегда приветствуются. Пожалуйста, внесите свой вклад.

## Содержание

1. [Общие принципы](#general-principles)
2. [Отступы](#whitespace)
3. [Форматирование](#format)
4. [Именование](#naming)
5. [Препроцессоры](#preprocessor)
6. [Организация кода](#organization)
7. [Методология](#metodology)
8. [Формирование и подключение файлов стилей](#file-include)
9. [Нелинейная верстка](#nonlinearly)
10. [Совместная работа наод одним проектом](#team)
11. [Карта верстки](#markup-map)
12. [Прочее](#other)
13. [Источники](#sources)

<a name="general-principles"></a>
## 1. Общие принципы

> «Вы сослужите проекту хорошую службу, если будете осознавать, что написание
> кода только для себя — Плохая Идея™. Если тысячи людей используют ваш код, то
> пишите его максимально ясным и не делайте что-то только потому, что
> спецификация языка допускает это». — Idan Gazit

* Весь код в любом проекте должен выглядеть так, будто его создал один человек,
  вне зависимости от того, сколько людей на самом деле принимали участие.
* Строго соблюдайте соглашения.
* В сомнительных случаях используйте общепринятый подход.

<a name="whitespace"></a>
## 2. Отступы

Для всего проекта должен применяться единый стиль отступов. Всегда будьте последовательны в использовании отступов и применяйте их для повышения читабельности кода.

* _Никогда_ не смешивайте пробелы и табуляцию.
* В наших проектах мы используем табуляцию в 4 пробела  

> Совет: настройте редактор кода так, чтобы он отображал невидимые символы. 
> Это позволит избегать случайных пробелов в конце строк или в пустых строках и легче отслеживать изменения в коде.

<a name="format"></a>
## 3. Форматирование

Выбранный формат записи кода должен гарантировать, что код легко читается; что его легко комментировать; должен минимизировать шанс случайного внесения ошибки; и в результате обеспечивать удобство чтения сообщений внутри системы управления версиями.

1. При создании правила для нескольких селекторов помещайте каждый селектор на отдельной строке.  
2. Перед открывающей скобкой ставьте один пробел (*).  
3. Внутри блока объявлений помещайте каждое объявление на отдельной строке.  
4. Добавляйте один уровень отступов перед каждым объявлением.  
5. Ставьте пробел после двоеточия внутри объявления.  
6. Всегда ставьте точку с запятой после последнего объявления в блоке (*)  
7. Ставьте закрывающую скобку на одной вертикальной линии с первым символом в селекторе (*).  
8. Разделяйте правила пустой строкой.  
9. Последовательно используйте двойные и одинарные кавычки. Двойные -- до открытия блока стилей, одинарные -- внутри.

_Пример разделения пустой строкой_
```css
.selector-1,  
.selector-2,  
.selector-3 {  
    -webkit-box-sizing: border-box;  
    -moz-box-sizing: border-box;  
    box-sizing: border-box;  
    display: block;  
    color: #333;  
    background: #fff;  
}
```

_Пример применения кавычек_
```css
a [type="attr"] {  
	content: ''.  
}
```

_(*) -- за исключением работы в конкретных препроцессорах_

<a name="naming"></a>
## 4. Именование

Вы не компилятор и не компрессор кода, поэтому ведите себя соответственно.
Используйте понятные и осмысленные имена для классов в HTML. Выберите ясный и последовательный шаблон именования, который будет удобен как для HTML, так и для CSS.

```css
/* Пример кода с плохими именами */

.s-scr {
    overflow: auto;
}

.cb {
    background: #000;
}
```

```css
/* Пример лучшего подхода к именованию */

.isScrollable {
    overflow: auto;
}

.columnBody {
    background: #000;
}
```

<a name="preprocessor"></a>
## 5. Препроцессоры

* Ограничивайте вложенность одним уровнем. Пересмотрите все правила, в которых больше двух уровней вложенности. Это позволит избегать чрезмерной специфичности правил.  
* Всегда помещайте операторы (@extend, @include, ...) в первой строке блока объявлений.  

<a name="organization"></a>
## 6. Организация кода

Организация кода — важная часть любого проекта на CSS и ключевой элемент в большом проекте.

* Логически отделяйте различные части кода.  
* Используйте отдельные файлы (объединяемые на этапе сборки), чтобы разделить код обособленных компонентов.  
* При использовании препроцессора оформляйте часто используемый код в переменные, например, для типографики, цветов и т.д.  

<a name="metodology"></a>
## 7. Методология
* При написании кода и именовании стилей мы опираемся на [БЭМ](http://ru.bem.info/method/), и частично на здравый смысл  
* Именование двухсловных классов через 'camelCase'  
* Для избежания проблем, которые всегда сопровождают каскадное написание CSS, каскад выносится в имя стилей  
* Спуск по каскаду через двойное подчеркивание:

Плохо:
```css
.header
	.header .search
		.header .search .input
		.header .search .button
```

Хорошо:
```css
.header
.header__search
.header__search__input
.header__search__button
```

* Каскад допустим в исключительно контролируемых случаях, и не больше двух уровней. Таких, например, как формирование айтемов со ссылками внутри списка, которые не имеют смысла в отрыве от родителя:  
```html
<ul class="orderedList">
	<li>
		<a>
```

* Классы "костыли" стартуют с нижнего прочерка:
```css
._clearFix
```

* Модификация блока внутри чужого родителя также происходит НЕ с помощью каскада, но с помощью класса модификатора по правилу "костылей":
```html
<div class="footer">
	<div class="headerBlock _headerBlock_footer">
```

<a name="file-include"></a>
## 8. Формирование и подключение файлов стилей

1. В HTML отдаем только один файл стилей style.css  
2. Подключение остальных файлов через '@import'  
3. Дабы избежать проблемы с каскадом, подключение происходит в порядке важности. Сначала подключаем файл с переменными и миксинами. После обнуляем все стили. Затем подключаем внешние CSS-фреймворки. После подключаем собственные UI и типографические фреймворки. Дальше подключаем общие файлы лайоута. Затем -- файлы конкретных блоков в связке с файлом адаптаций. И в самом конце -- костыли.  

Пример:
```css
@import "_sprite"  
@import "_variables"  
@import "_functions"  
@import "_normalize"  
@import "bootstrap"  
@import "userInterface"  
@import "layout"  
  
@import "header"  
@import "header__nav"  
  
@import "contactsInfo"  
  
@import "verticalMenu"  
  
  
@import "footer"  
@import "footer__menu"  
@import "footer__menu__adaptive"  
```

<a name="nonlinearly"></a>
## 9. Нелинейная верстка

Проекты, которые живут и изменяются прямо в процессе разработки, имеют свойство преподносить проблемы там, где их меньше всего ждешь. Одним из конкретных примеров такой проблемы может быть ситуация, где попапы оказываются под слоем 'OVERLAY' или внутри блока со свойством 'overflow:hidden'. Произойти это может после очередной ротации дизайна. Принципиальным решением этой проблемы может быть вынос попапов на уровень BODY


<a name="team"></a>
## 10. Совместная работа над одним проектом

* Чтобы исключить в принципе возможность конфликтов, блоки разносятся в отдельные файлы стилей. Имена файлов задаются методологией написания имен классов
* Адаптация блоков также через подключение отдельного файла адаптаций
```css
@import "footer"  
@import "footer_adaptive"  
```
* В исключительных ситуациях, когда над одним файлом стилей нужно работать одновременно двум и более кодерам, подключаем личный файл. По окончании работы мержим с основным
* Для визуального контроля, личный файл стилей сопровождается ником разработчика в кавычках перед названием блока:
```css
@import "(meksico)footer__menu"  
```

<a name="markup-map"></a>
## 11. Алгоритм разработки верстки

Генеральная проблема постоянно развивающихся проектов — это то, что сайт начинает жить своей жизнью. Добавляются новые страницы, старые видоизменяются и этот поток изменений — постоянен. Рано или поздно, без должной проработки абстракций, проект начинает упираться в потолок, заданный логикой кодера. Которая, в свою очередь, привязана к контексту. Поэтому критически важно дать фундамент будущей верстки, не ограничивающей, но поддерживающей проект.

Опытным путем было найденно решение, позволяющее намного мягче входить в поток изменений. Первое, и самое главное его условие, это концепция БЭМа. Блок внутри блока — это отдельная абстракция, которая не должна иметь контекстной зависимости от верхнего уровня. Второе — карта верстки. [Пример карты](https://github.com/trinetixHTML/Developments/blob/master/markupMapExample/markup_map.mail.ru.txt) на [шаблоне проекта mail.ru](https://github.com/trinetixHTML/Developments/blob/master/markupMapExample/markup_map.mail.ru.png)

Для правильной проработки абстракций, мы принимаем к работе следующй алгоритм:

1. Перед началом работы, создается карта верстки  
> Карта представляет собой набор классов и вложенностей, полностью чистых от технический деталей. Это скелет, который в дальнейшем обрастет телом  

2. Группой кодеров, или техлидом, проводится первичная ревизия карты верстки  
> Вносятся поправки, выделяются общие сущности, составляется будущая файловая структура проекта  
  
3. Карта верстки делится между участниками команды проекта  
  
4. Финальная ревизия верстки техлидом


<a name="other"></a>
## 12. Прочее
* Подключение шрифтов через слеш, без указания HTTP или HTTPS

```html
<link href="//fonts.googleapis.com/css?family=Lobster" rel="stylesheet" type="text/css">
```
<a name="sources"></a>
## 13. Источники
1. _Based on https://github.com/necolas/idiomatic-css/tree/master/translations/ru-RU_
2. _БЭМ http://ru.bem.info/method/_
