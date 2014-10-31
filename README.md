# Принципы написания однородного CSS-кода
_(based on https://github.com/necolas/idiomatic-css/tree/master/translations/ru-RU)_

Этот документ не закончен, и новые идеи всегда приветствуются. Пожалуйста, внесите свой вклад.

## Содержание

1. [Общие принципы](#general-principles)
2. [Методология](#metodology)
3. [Отступы](#whitespace)
4. [Препроцессоры] (#preprocessor)
5. [Форматирование](#format)
6. [Именование](#naming)
8. [Организация кода](#organization)

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
## 5. Препроцессоры:

* Ограничивайте вложенность одним уровнем. Пересмотрите все правила, в которых больше двух уровней вложенности. Это позволит избегать чрезмерной специфичности правил.  
* Всегда помещайте операторы (@extend, @include, ...) в первой строке блока объявлений.  

<a name="organization"></a>
## 6. Организация кода

Организация кода — важная часть любого проекта на CSS и ключевой элемент в большом проекте.

* Логически отделяйте различные части кода.  
* Используйте отдельные файлы (объединяемые на этапе сборки), чтобы разделить код обособленных компонентов.  
* При использовании препроцессора оформляйте часто используемый код в переменные, например, для типографики, цветов и т.д.  

<a name="metodology"></a>
7. Методология
* При написании кода и именовании стилей мы опираемся частично на [БЭМ](http://ru.bem.info/method/), частично на здраый смысл  
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

* Каскад допустим в исключительно контролируемых случаях, и не больше двух уровней. Таких, например, как формирование айтемов со ссылками внутри списка:  
```html
ul class="orderedList"
____li
________a
```

Классы "костыли" стартуют с нижнего прочерка
_clearFix
Модификация блока внутри чужого родителя также происходит НЕ с помощью каскада, но с помощью класса модификатора по правилу "костылей":
div class="footer"
____div class="headerBlock _footer__headerBlock"

7. Формирование и подключение файлов стилей
В HTML отдаем только один файл стилей style.css
Подключение остальных файлов через @import
Дабы избежать любые проблемы с каскадом, подключение происходит в порядке важности. Сначала подключаем файл с переменными и миксинами. После обнуляем все стили. Затем подключаем внешние CSS-фреймворки. После подключаем собственные UI и типографические фреймворки. Дальше подключаем общие файлы лайоута. Затем -- файлы конкретных блоков в связке с файлом адаптаций. И в самом конце -- костыли.
Пример:

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

8. Совместная работа наод одним проектом
Для того, чтобы исключить в принципе возможность конфликтов, блоки разносятся в отдельные файлы стилей. Имена файлов задаются методологией написания имен классов
Адаптация блоков также через подключение отдельного файла адаптаций
В исключительных ситуациях, когда над одним файлом стилей нужно работать одновременно двум и более кодерам, подключаем личный файл. По окончании работы мержим с основным
Для визуального контроля, личный файл стилей сопровождается ником разработчика в кавычках перед названием блока:
@import "(meksico)footer__menu"
