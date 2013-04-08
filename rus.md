# Простой (и довольно грубый) способ создания адаптивных таблиц

В настоящее время существует множество способов создания адаптивных таблиц.

Есть варианты с [переворачиванием таблицы][1] [набок][2],
[превращением ее в круговую диаграмму][3],
[постепенным сужением столбцов][4],
[возможностью задания столбцов пользователем][5] и даже с
[частичным прокруткой внутри таблицы][6]. Все эти решения хороши, но тем не 
менее не лишены недостатков:

1. Некоторые сложно реализовать в реальных условиях, особенно если в них
используются псевдоэлементы `::before` для генерации заголовков таблицы.
2. Некоторые из них (например, круговую диаграмму) можно использовать только для
определенных типов табличных данных.
3. Другие же решения могут сбить с толку конечного пользователя, 
в частности — решение с пропадающими столбцами.

Хотите увидеть суперпростой способ сделать таблицу адаптивной? Способ,
содержащий всего лишь пару строк CSS и не требующий JavaScript? Взгляните:

## Способ 1: Суперпростой

Все, что вам нужно сделать - обернуть таблицу в `div`:

    <div class="table-container">
      <table>
        ...
      <table>
    </div>

И потом добавить простые стили:

    .table-container
    {
      width: 100%;
      overflow-y: auto;
      _overflow: auto;
      margin: 0 0 1em;
    }

[Демо 1][7]

## Способ 2: Добавление скроллбаров для iOS

Если вы откроете вышеуказанное демо на iOS-устройстве, например, на iPhone,
то увидите, что там нет скроллбаров. И хотя пользователи могут сдвигать
таблицу для прокрутки, это не так уж и очевидно. Мы можем исправить этот
недостаток добавлением следующего CSS:

    .table-container::-webkit-scrollbar
    {
      -webkit-appearance: none;
      width: 14px;
      height: 14px;
    }

    .table-container::-webkit-scrollbar-thumb
    {
      border-radius: 8px;
      border: 3px solid #fff;
      background-color: rgba(0, 0, 0, .3);
    }

[Демо 2][8]

## Способ 3: Скроллбары для всех

Если вы хотите заставить все браузеры и устройства отображать скроллбары, то
для этого существует целый ряд решений на jQuery:

* [jScrollPane][9]
* [Custom content scroller][10]
* [jScroller][11]
* [Tiny Scroller][12]

## Способ 4: Добавление градиента

Вы заметили, что таблица выглядит «обрезанной» с правого края? Для придания
ему эффекта «растворения» вы можете использовать `linear-gradient`. Чтобы
все хорошо работало на экране любого размера или во время прокрутки
пользователем, мы добавим в разметку два новых элемента:

    <div class="table-container-outer">
      <div class="table-container-fade"></div>
        <div class="table-container">
          <table>
            ...
          <table>
        </div>
      </div>
    </div>

И CSS:

    .table-container-outer { position: relative; }

    .table-container-fade
    {
      position: absolute;
      right: 0;
      width: 30px;
      height: 100%;
      background-image: -webkit-linear-gradient(0deg, rgba(255,255,255,.5), #fff);
      background-image: -moz-linear-gradient(0deg, rgba(255,255,255,.5), #fff);
      background-image: -ms-linear-gradient(0deg, rgba(255,255,255,.5), #fff);
      background-image: -o-linear-gradient(0deg, rgba(255,255,255,.5), #fff);
      background-image: linear-gradient(0deg, rgba(255,255,255,.5), #fff);
    }

[Демо 4][13]

Итак, вот они, несколько простых (и довольно грубых) решений для создания
адаптивных таблиц.

Что думаете?


[1]:  http://css-tricks.com/examples/ResponsiveTables/responsive.php
[2]:  http://www.mobifreaks.com/wp-content/demos/Responsive-and-SEO-Friendly-Data-Tables/
[3]:  http://jsbin.com/emexa4
[4]:  http://www.irishstu.com/stublog/wp-content/uploads/2011/12/table-childs.html
[5]:  http://filamentgroup.com/examples/rwd-table-patterns/
[6]:  http://www.zurb.com/playground/playground/responsive-tables/index.html

[7]:  demo1.html
[8]:  demo2.html

[9]:  http://jscrollpane.kelvinluck.com/index.html
[10]: http://manos.malihu.gr/jquery-custom-content-scroller/
[11]: http://www.myjqueryplugins.com/jquery-plugin/jscrollbar
[12]: http://baijs.nl/tinyscrollbar/

[13]: demo4.html