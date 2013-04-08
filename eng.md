# A simple (and very rough) responsive table solution

There are a lot of very clever responsive table solutions available now.

There are solutions that [flip the table][1] on [it’s side][2], [convert it to
a pie chart][3], [gradually reduce the columns][4], [allow users to determine
columns][5], and even allow [partial scrolling across the table][6]. All of
them are very clever.

However, there are concerns about many of them: 
1. Some of them would be hard to implement in the real world – especially 
those that rely on the `::before` pseudo-element selectors to generate table 
headers.
2. Some of them may not work for all types of table data – like the pie 
chart solution.
3. Some of them many confuse the end users – like the disappearing column 
solution.

Would you like to see a super-simple solution for responsive tables – that
needs no JavaScript and just a few lines of CSS? Take a look:

## Solution 1: Super simple

All you need to do is add a wrapping div around the table.

    <div class="table-container">
      <table>
        ...
      <table>
    </div>

And then add some simple rules:

    .table-container
    {
      width: 100%;
      overflow-y: auto;
      _overflow: auto;
      margin: 0 0 1em;
    }

[Here is demo 1][7]

## Solution 2: Adding scrollbars for iOS

If you look at the demo above on an iOS device, like an iPhone, you will see
that there are no scrollbars present. While users can swipe the table to
scroll, this is not immediately obvious. We can fix that by adding some
additional CSS.

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

[Here is demo 2][8]

## Solution 3: Scrollbars for everyone

If you want to force all browsers and devices to display scrollbars, there are
a range of JQuery options available:
* [jScrollPane][9]
* [Custom content scroller][10]
* [jScroller][11]
* [Tiny Scroller][12]

## Solution 4: Adding a gradient

Did you notice that the table looks "cut off" at the right edge? to give this
a "fade in" look, you could add a `linear-gradient`. To do this successfully
(so that it will work well at any screen size or when the user scrolls) we
will add two new elements to the markup.

    <div class="table-container-outer">
      <div class="table-container-fade"></div>
        <div class="table-container">
          <table>
            ...
          <table>
        </div>
      </div>
    </div>

And then some additional CSS

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

[Here is demo 4][13]

So there you have it, a few simple (and very rough) responsive table options.
What do you think?


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