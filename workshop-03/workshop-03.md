[repo]: https://github.com/umass-cs-326/Workshop3

# Workshop 03: HTML and Bootstrap

# Introduction

Developers write website GUIs using HTML and CSS. As we discussed in
class, these technologies are becoming increasingly difficult to use
directly.  Websites must work across different browsers
(Chrome/Safari/Internet Explorer), operating systems
(Windows/Mac/Linux), and devices (desktop/smartphone/tablet). Managing
this complexity can be quite difficult!

In this class, you will use [Bootstrap](http://getbootstrap.com) to write your
website GUI. Bootstrap provides you with useful HTML and CSS primitives for
writing website GUIs that work across desktop, tablet, and mobile. Wikipedia
summarizes Bootstrap quite well:

> Bootstrap is a free and open-source collection of tools for creating websites
> and web applications. It contains HTML- and CSS-based design templates for
> typography, forms, buttons, navigation and other interface components, as well
> as optional JavaScript extensions. It aims to ease the development of dynamic
> websites and web applications.

In this workshop, you will use Bootstrap to write basic, non-interactive website
GUIs. By the end of the workshop, you should have a decent idea of what is
possible using Bootstrap, and how to apply Bootstrap to your group project.

Specifically, you will:

* Learn about HTML
* Learn about CSS
* Learn how to use Bootstrap
* Write the next Facebook in Bootstrap!
  * ...OK, that's an overstatement. We're going to create a rough version of Facebook's layout.

We will not have time to cover the following topics, but we encourage students
to explore them on their own:

* [Responsive design](https://en.wikipedia.org/wiki/Responsive_web_design)
* Compatibility with ancient web browsers (IE8, IE7, etc)
  * These web browsers are [becoming increasingly irrelevant](http://gs.statcounter.com/#desktop-browser_version_partially_combined-ww-monthly-201412-201512).

# Part 0: Initial setup

To get started you need to fork the [GitHub repository for this workshop][repo]. To do that click on the "**Fork**" button, it is on the upper right-hand part of the github page next to "**Unwatch**" and "**Star**". The repository contains the version of Bootstrap we will be using (v3.3.6) and a basic script that runs a local web server:

![Forking the Workshop](../images/fork.png)

Clone the repository into your **class folder**, `cd`, into it, and run the following command to install a basic web server:

```
npm install
```

This command will create a `node_modules` folder, which you should leave alone.
It contains the web server.

Run the following command to start the local web server, which will let you
view the HTML you produce in a web browser:

```
npm run serve
```

*Note: If you have a firewall installed, you will need to approve Node.js to
open port 8080 on the network. Most firewalls will ask you immediately.*

Navigate your web browser to [http://localhost:8080/](http://localhost:8080/), which should look something like this:

![Server Listing](../images/server-listing.png)

**Keep that console window open for the entirety of the workshop.** When you close that window, the web server stops! Open a second console window and navigate to the workshop git repository directory so you can run other commands while the server runs.

# Part 1: Hello, Bootstrap!

Let's get familiar with Bootstrap by writing a simple "Hello World!" webpage.

This workshop's git repository has the following directories:

* `css/`: A folder to put CSS files into. Currently contains a few Bootstrap CSS
files. You can add new CSS files to this directory, but *do not modify the
Bootstrap CSS files.* We will describe how to customize the look of Bootstrap
the proper way.
* `fonts/`: Bootstrap contains a number of [Glyphicons](http://getbootstrap.com/components/#glyphicons)
that you are free to use in your website. The `fonts` directory contains
[web font](https://en.wikipedia.org/wiki/Web_typography) files containing these
Glyphs. Since Bootstrap works on every browser, it maintains these fonts in
several formats. *Do not modify these files.*
* `img/`: A folder to put your images into.
* `js/`: Contains Bootstrap's JavaScript dependencies.

You will put all HTML files into the root of the repository.

Create the file `helloworld.html` in the root of the repository, and put the
following HTML into it:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <!-- The above 3 meta tags *must* come first in the head;
	     any other head content must come *after* these tags -->
    <title>Bootstrap 101 Template</title>

    <!-- Bootstrap's CSS -->
    <link href="css/bootstrap.min.css" rel="stylesheet">
  </head>
  <body>
    <!-- All of your HTML will go between here.... -->
    <h1>Hello, world!</h1>

    <!-- ...and here. -->
    <!-- jQuery (necessary for Bootstrap's JavaScript plugins) -->
    <script src="js/jquery.min.js"></script>
    <!-- Include all compiled plugins (below),
	     or include individual files as needed -->
    <script src="js/bootstrap.min.js"></script>
  </body>
</html>
```

You will use this same boilerplate code for all of your Bootstrap projects.

Navigate to http://localhost:8080/helloworld.html, and you should see the
following:

![Hello Bootstrap](../images/hello_bootstrap.png)

**Add `helloworld.html` to Git, commit it, and push to GitHub**


## A walk through `helloworld.html`, aka "what are those tags for?"

*tl;dr: Bootstrap handles all of this stuff so you can focus on making cool websites.*

Most of the HTML here is pretty standard
(e.g. the
[`html` tag](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/html),
[`head` tag](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/head),
[`body` tag](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/body),
etc)...  but some of the elements are confusing. Let's discuss them
now!

The following is
a [document type declaration](https://en.wikipedia.org/wiki/Document_type_declaration):

```html
<!DOCTYPE html>
```

Roughly, these tell the web browser how to interpret the document. The
web has gone through many iterations, and so older documents on the
web are displayed slightly differently than newer ones. This doctype
is
the
[HTML5 doctype](https://en.wikipedia.org/wiki/Document_type_declaration#HTML5_DTD-less_DOCTYPE),
which is what you should generally use on all of your websites.

The template contains a block of `meta` tags, which are somewhat interesting:

```html
<meta charset="utf-8">
<meta http-equiv="X-UA-Compatible" content="IE=edge">
<meta name="viewport" content="width=device-width, initial-scale=1">
```

The first line tells the browser to interpret the rest of the document
from that point as `utf-8`, which is a character
encoding.
[Character encodings are a rabbit hole](https://en.wikipedia.org/wiki/Character_encoding),
but, at a high level, it tells the browser how to translate the
low-level bits of the document into language characters. Without this
tag, the web server would have to tell the browser what character
encoding to use. If it didn't, the web browser would likely assume
ASCII, which means fun emojis like 👍  won't display properly. *tl;dr:
You generally want utf-8 at all times.*

The second line tells Internet Explorer to use its new Edge rendering
engine if available, which is much more standards compliant than its
older rendering engines. On certain versions of IE, this tag is
required to enable new browser features.

The third line is for mobile browsers; it tells the browser to render
the page at the width of the device's screen, and to start the page
view at the standard zoom level. Otherwise, the browser may render the
website with a different width (e.g. thinner or larger), or may use a
different zoom level when it loads your website.

Finally, Bootstrap puts its `script` tags as the last items in the `body` of the
HTML file, which seems unusual if you have ever written HTML before. These tags
pull in the JavaScript files that Bootstrap relies on. We will cover these tags
later when we start covering JavaScript:

```html
<body>
  <!-- snip -->
  <!-- jQuery (necessary for Bootstrap's JavaScript plugins) -->
  <script src="js/jquery.min.js"></script>
  <!-- Include all compiled plugins (below),
       or include individual files as needed -->
  <script src="js/bootstrap.min.js"></script>
</body>
```

Most HTML guides specify that `script` tags be added to the `head` of the
document. However, if Bootstrap did that, the web browser would wait until both
`jquery.min.js` and `bootstrap.min.js` downloaded and initialized before
displaying the `body` of the webpage. On a mobile connection, this could
translate into a multi-second wait.

By putting these tags into the `body`, the web browser will display all of the
content in the HTML document *before* the `script` tags while the `script` tags
load. This is now standard practice on most websites.

[There are more modern ways to do this](http://stackoverflow.com/a/24070373),
but Bootstrap uses this method because it is compatible with the most web
browsers.

# Part 2: Facebook in Bootstrap

Many of you are likely familiar with Facebook. In this part of the workshop, you
will recreate Facebook's desktop interface using HTML, CSS, and Bootstrap.
Facebook's desktop interface looks like this:

![Facebook](../images/facebook.png)

**For grading purposes, we are going to have you write git commits at particular
points in the workshop with specific messages.** We will look at your website
at those commits, and check that it is correct. If you do not commit your code
when the guide tells you to, or if you use a different commit message, we will
have trouble grading your submission.

Let's dive in!

## Step 00: Basic Bootstrap template

Create a file called `facebook.html` in the root of the workshop repository with
the standard Bootstrap boilerplate we used for the Hello World example, except
with a modified `title`:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <!-- The above 3 meta tags *must* come first in the head;
		 any other head content must come *after* these tags -->
    <title>Facebook</title>

    <!-- Bootstrap's CSS -->
    <link href="css/bootstrap.min.css" rel="stylesheet">
  </head>
  <body>
    <!-- Our Facebook layout will go here. -->

    <!-- jQuery (necessary for Bootstrap's JavaScript plugins) -->
    <script src="js/jquery.min.js"></script>
    <!-- Include all compiled plugins (below),
		 or include individual files as needed -->
    <script src="js/bootstrap.min.js"></script>
  </body>
</html>
```

Don't commit anything to Git just yet; we're going to do a bit more first!

## Step 01: Facebook at the Macro Level

Now that we have a template, it's time to work on the layout of our Facebook
clone! But... Facebook's desktop interface is quite cluttered. You may not know
where to begin.

At this point, it's important to look at the big picture. Ignore the details;
what are the *top-level content panes* on the webpage? If we can create those
properly, then we can start filling in the details of each. HTML
documents are *trees*, so you should be able to edit the content of each
content pane independently.

In other words, if you establish these content panes correctly, the size and
contents of one content pane will not impact the others.

To answer my own question, there are five top-level content panes:

![Facebook Content Panes](../images/facebook_content_panes.png)

Facebook uses a three-column layout, with a top navigation bar and a chat dock
in the corner. What we want to do now is create HTML for each of these using
Bootstrap.

Bootstrap has two primary documentation pages for creating the layout of a
website:

- [CSS Guide](http://getbootstrap.com/css/): Documents many of the CSS classes
available within Bootstrap, which you can use to style / format your GUI.
- [Component Guide](http://getbootstrap.com/components/): Documents the
components/widgets in Bootstrap. The line between *components* and *simple CSS
classes* is murky at best; many components are simply CSS classes you apply to
HTML elements. You'll likely check both of these pages regularly when designing
a website.

We will refer to content in both of these as you build your Facebook clone.

### Basic Navbar

The component guide contains a section on how
to
[create a navigation bar](http://getbootstrap.com/components/#navbar),
which is absolutely *perfect* for the Facebook navigation bar.

In your template, add an *empty* Bootstrap navigation bar to the `body` of the
page. It should go *before* the `script` tags:

```html
<nav class="navbar navbar-default">
  NAVBAR
</nav>
```

[The `nav` HTML tag](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/nav)
is intended for a content pane with links to other parts of the site.
`navbar` and `navbar-default` are Bootstrap CSS classes, which transform the
ordinary HTML tag into a Bootstrap navigation bar. HTML tags can have an
arbitrary number of CSS classes applied to them. Later on, we'll define our
own classes to customize our site further.

Now, if you
refresh
[http://localhost:8080/facebook.html](http://localhost:8080/facebook.html),
you'll see a faint gray outline of a navigation bar:

![Navbar Outline](../images/navbar_outline.png)

You may be tempted to fill in the navbar with buttons and such, and figure out
how to make it Facebook blue... but *do not do that just yet*. When implementing
a webpage layout, the top-level structure of a webpage is the most important
detail to think through and get right. It quickly becomes frustrating if you try
to change/fix the top-level structure of a fully-developed webpage, which
typically contains hundreds of lines of HTML!

### Three Columns

With the navbar in place, we can tackle creating the main three columns.
Bootstrap has a handy [grid system](http://getbootstrap.com/css/#grid), which
lets you place HTML elements in rows and columns. You will use this grid system
regularly in your layouts.

The grid documentation contains many details, but the most important facts are:

* A grid contains a list of rows.
* Each row has 12 columns.
* Each grid cell can span 1 or more columns, can be specified for a particular
  screen size, and can begin at a particular column.
  * For this tutorial, we are targeting *medium*-size screens, so we will
    only use `col-md-*` CSS classes.
  * Bootstrap lets you make *responsive* designs that adapt to different screen
    sizes. You can define columns that span different numbers of columns for
    different screen sizes, and can define columns that only display for
    particular screen sizes. We will not cover this in this workshop, but
    understanding how this works is crucial for writing mobile websites in
    Bootstrap.
* Each row is as tall as the largest cell within it, and expands to fill the width
  of the HTML element that contains it.
* You can nest grids within grids by defining rows within cells.

We'll cover each of these points (and more!) as we make grids for the Facebook
layout.

For the Facebook three-column layout, we can make one row with three cells:
one for the left sidebar, one for the main feed, and one for the right sidebar.
We just need to decide how many columns each cell spans!

To visualize the solution, here's the Facebook layout with the Bootstrap
grid columns overlaid on top:

![Facebook Grid](../images/facebook_grid.png)

*Remember: The Bootstrap grid system is always 12 columns wide, each
column is equal in size, and the columns expand to fill the width of
the HTML element that contains it.*

The left sidebar is *roughly* 2 columns wide, the feed 7, and the right sidebar 3.
Now, we can add a simple, one-row grid to the `body` of our Facebook clone.
Add this just below the navbar:

```html
<!-- The container for our grid. The outermost grid must be placed within
     a `container` or `container-fluid` class. (Meaning: If you nest a grid
     within a grid, you should not define another `container`)
     What's the difference between these two types of container? There's a
     good answer here: http://stackoverflow.com/a/22263969 -->
<div class="container">
  <!-- The row that contains the three main columns of the website. -->
  <div class="row">
    <!-- Left sidebar: A cell that spans 2 columns -->
    <div class="col-md-2">
      Left Sidebar
    </div>
    <!-- Main feed: A cell that spans 7 columns -->
    <div class="col-md-7">
      Main Feed
    </div>
    <!-- Right sidebar: A cell that spans 3 columns -->
    <div class="col-md-3">
      Right Sidebar
    </div>
  </div>
</div>
```

Now, our Facebook clone looks like the following:

![Facebook Clone](../images/facebook_clone_macro.png)

Those look like the correct proportions!

If you resize your browser window to make it wider or narrower, you'll notice
that the width of the grid changes slightly. [The `container` that we nested
our grid inside has several fixed widths, depending on the width of the
browser window.](http://stackoverflow.com/a/22263969) This is part of
Bootstrap's *responsive design*, which we encourage you to read more about
if you are interested.

Also, note that your Facebook layout looks weird when the browser gets
too thin. We will not address this limitation in this workshop, but there
are two solutions to this problem: 1) [Disabling Bootstrap's responsiveness](http://getbootstrap.com/getting-started/#disable-responsive),
or 2) Adding in extra Bootstrap CSS classes so the layout looks good on smaller screens.

### Chat Popup

The final main content pane on the Facebook page is the chat popup menu. This
menu docks at the bottom of the screen, and sits *on top* of the content on the
right. How can we re-create this popup using Bootstrap?

[The CSS `position` property](https://developer.mozilla.org/en-US/docs/Web/CSS/position)
tells the browser how to render an HTML element and its children (i.e. nested elements).

We can position the chat menu using the `absolute` position, which instructs the
browser to display the element at a specific location relative to the browser
window. To ensure that the chat menu covers contents on the page, we can set the
CSS property [`z-index`](https://developer.mozilla.org/en-US/docs/Web/CSS/z-index)
to a large value. Elements with a larger `z-index` always cover elements with
a lower `z-index`.

The next question: How do we tell the browser how wide the chat menu is?
Up until now, all of our HTML elements have a width that is relative to the size
of the browser window. For example, the width of the navigation bar and the main grid depends
on the width of the `container` class, which depends on the size of the browser window. *This is a good thing.* Our layout will
display well on desktop devices with a variety of screen sizes.

Often, new web developers are tempted to micromanage every pixel on their
webpages by defining pixel widths, heights, and offsets on all of their HTML
elements. This is a *bad idea*. HTML layouts produced using this technique are:

* **Unmaintainable**: The HTML/CSS will be cluttered with specific pixel offsets.
  Adding additional content panes or altering the layout would be a
  considerable undertaking, as all of the pixel values affect one another.
* **Inflexible**: Bootstrap is designed so that your webpage can look good on
  many screen sizes. Using specific pixel counts restricts your webpage to
  looking good on only one screen size.
* **Non-portable**: Web browsers differ slightly in how they display webpages.
  It's common that one browser will add a single extra pixel of padding
  between elements over another browser due to a [rounding error](https://en.wikipedia.org/wiki/Round-off_error).
  You cannot count on pixel-precise behavior across browsers.

However, there are exceptions to every rule. The chat menu is a *small* floating
menu, and its contents do not vary much in width. In particular, it contains a
fixed-width online indicator, text indicating how many people are online (which
will be at most 8 + log 10(# online friends) characters wide), and two
fixed-width buttons. We cannot rely on this content being a specific width,
but we can reasonably assume that it won't exceed a certain width.

The Facebook chat popup itself is ~300 pixels wide, which gives the content
plenty of room to grow if the person has many friends online:

![Facebook Chat Menu](../images/facebook_chat_menu.png)

With that discussion out of the way, we're going to add a `div` element for the
chat menu to the HTML. Before we can do that, however, we need to add a CSS
file so we can define custom CSS stylings for our website.

Create an empty file at `css/facebook.css`, and add the following HTML to
`facebook.html` within the `head` tag, just after the `link` tag for
`bootstrap.min.css`:

```css
<!-- Custom CSS -->
<link href="css/facebook.css" rel="stylesheet">
```

Now, our webpage will load and apply `facebook.css` when you view it.

Open `facebook.css`, and add a CSS rule for the chat menu:

```css
.chat-popup {
  width: 300px;
  position: absolute;
  bottom: 0px;
  right: 20px;
}
```

*Note: CSS classes typically use all lowercase letters with dashes
in-between words. You don't need to follow this convention, but the
rest of the web typically does.*

The above is a *CSS rule*. A *CSS rule* contains a *selector* and a *declaration
block*. The syntax is as follows:

```css
SELECTOR {
  DECLARATION BLOCK
}
```

Our rule uses a [CSS class selector](https://developer.mozilla.org/en-US/docs/Web/CSS/Class_selectors),
which means "apply these properties to elements with the class `chat-popup`".
Class selectors are written using a period (`.`) before the target class.

CSS rules can change the look and position of elements on the webpage, and are
how Bootstrap components work. The CSS rule above is only concerned with the
*position* of the chat menu. The value for `bottom` and `right`, when `position`
is set to `fixed`, means:
"Display this element 0 pixels from the bottom, and 30 pixels from the right".

Add the following HTML to the `body` of your page, after the `container` div
containing the grid:

```html
<div class="chat-popup">
  CHAT MENU
</div>
```

Navigate to http://localhost:8080/facebook.html, and you should see the
following:

![Facebook Clone Chat Menu](../images/facebook_clone_chat_menu.png)

That looks about right!

**`add` `facebook.html` and `css/facebook.css` to Git, `commit` your
changes with the commit message `fb1`, and `push` the changes to
GitHub.**

## Step 02: Scrolling Behavior

Next, we need to check how our layout responds when we have enough content
to trigger scrolling. On Facebook, the main feed is larger than the browser
window's height. The user scrolls down the feed to see content hiding
off-screen. As the user does this, the chat menu and top menu follows along.

*Note: Facebook also makes the right sidebar follow as you scroll so you look
at trending content and advertisements, but it scrolls in an odd manner. We
will not cover this behavior in this workshop. Our right sidebar will not
"stick" to the side of the browser window.*

Let's see how our current layout responds to content in the main feed.
Add a *really tall* `div` element to the main feed's `div`, like so:

```html
<div class="col-md-7">
  Main Feed
  <div style="height: 99999px;">

  </div>
</div>
```

The `style` attribute can be specified on any HTML element. It lets you specify
CSS stylings within the HTML. You should avoid using the `style` attribute,
as it clutters your HTML with styling information. You should use HTML to
organize the structure of your webpage (i.e. the HTML tree), and CSS to
customize the look given that structure.

In this example, we are adding this element *temporarily* to investigate
scrolling behavior, so we are justified in using `style`.

Navigate
to
[http://localhost:8080/facebook.html](http://localhost:8080/facebook.html) and
try scrolling... and...  you'll discover there are some problems:

![Facebook Lone Scroll Issue](../images/facebook_clone_scroll_issue.png)

The chat menu and navigation bar should stay "attached" to the browser window
as you scroll, but they don't. Why is that?

### Chat Menu

We used `position: absolute;` to place the menu, which places the menu relative
to the browser window. However, the menu does not stay in place when you scroll!
(It does, however, stay in place when you resize the window to make it longer.
Weird, right?)

Instead, we need to use `position: fixed;`, which *fixes* the element relative
to the user's current view of the webpage. Fix the CSS for the `chat-popup`
class, and reload the page:

![Facebook Clone Chat Menu Scroll Fixed](../images/facebook_clone_chat_menu_scroll_fixed.gif)

Much better!

The [link we posted earlier](https://developer.mozilla.org/en-US/docs/Web/CSS/position)
mentions these differences, but it's much easier to understand when you see it
in-person. (Also, full disclosure: we made this mistake ourselves when creating
this assignment.)

### Navigation Menu

Considering the chat menu solution, you may be tempted to make the `nav` element
absolutely placed, and call it a day. You can certainly fix the problem that
way, but it's much easier to use [Bootstrap's built-in CSS class that does it
for you](http://getbootstrap.com/components/#navbar-fixed-top).

Add the `navbar-fixed-top` CSS class to your `nav` element, and reload the page.
The navigation bar is now docked at the top... but it's also covering the three
main columns!

![Facebook Clone Navbar](../images/facebook_clone_navbar_covering.png)

To fix this, we can simply *offset* the content of the `body` by a particular
pixel amount. Add the following to `facebook.css`:

```css
body {
  padding-top: 60px;
}
```

This CSS rule uses a [*type selector*](https://developer.mozilla.org/en-US/docs/Web/CSS/Type_selectors),
which applies the rule to all elements of the specified type.
This particular CSS rule applies its properties to *every `body` element on the
webpage*. Now, the browser will add 60 pixels worth of padding above the `body`
element. Since the navbar and chat content panels are placed relative
to the browser's viewport (effectively *floating* above the webpage), they are
not impacted by this change.

We chose 60 pixels for the offset because the
[Bootstrap example code for a fixed navbar](http://getbootstrap.com/getting-started/#examples-navbars)
uses a similar value. The navbar is apparently ~50 pixels high by default, and
we can rely on this value remaining constant.

Now, all is well!

![Facebook Clone Scrolling](../images/facebook_clone_scrolling_ok.png)

**`commit` your changes with the commit message `fb2`, and `push` the changes to GitHub.**

## Step 03: The Navigation Bar

With a solid page structure in place, we can start adding buttons and content
to flesh out the layout.

Facebook's navigation bar looks like the following:

![Facebook Navbar](../images/facebook_navbar.png)

Notice that one half of the navigation bar is *left-aligned* (the logo + search
box), and the other half is *right-aligned*, with empty space pooling in the
middle.

Bootstrap's [default example for a navigation bar](http://getbootstrap.com/components/#navbar-default)
uses the same basic design. We can repurpose this
sample code to imitate Facebook's navigation bar. In addition, we can use
Bootstrap's [Glyphicons](http://getbootstrap.com/components/#glyphicons)
to imitate all of Facebook's icons.

First, let's empty out the sample code from that link into its essentials, and
modify it to use a "home" glyphicon for the brand logo:

```html
<nav class="navbar navbar-fixed-top navbar-default">
  <!-- ".container-fluid" expands to fill the entire browser view's width.
       ".container" will use the same width as the ".container" in the body,
       which contains the three columns of content.

       We want ".container" here so the navbar is the same width as the content.

       Confused? Try switching between the two container classes once you have a
       complete navbar to see the difference. -->
  <div class="container">
    <!-- This code is only active when viewing the site on mobile. We will not
         cover responsive design, but we'll leave this in, as it's part of the
         example code.-->
    <div class="navbar-header">
      <button type="button" class="navbar-toggle collapsed" data-toggle="collapse"
		      data-target="#bs-example-navbar-collapse-1" aria-expanded="false">
        <span class="sr-only">Toggle navigation</span>
        <span class="icon-bar"></span>
        <span class="icon-bar"></span>
        <span class="icon-bar"></span>
      </button>
      <!-- Use a "home" glyphicon as a logo. -->
      <a class="navbar-brand" href="#">
        <!-- This is how you display a glyphicon. -->
        <span class="glyphicon glyphicon-home"></span>
      </a>
    </div>

    <!-- On mobile, this div is hidden by default. The user hits the button
         in the `navbar-header` to see the content of the div.
         On desktop, this div is visible all of the time. -->
    <div class="collapse navbar-collapse" id="bs-example-navbar-collapse-1">
      <form class="navbar-form navbar-left" role="search">
        <!-- Left-aligned items. -->
      </form>
      <ul class="nav navbar-nav navbar-right">
        <!-- Right-aligned items. -->
      </ul>
    </div><!-- /.navbar-collapse -->
  </div><!-- /.container -->
</nav>
```

Now, your navigation bar will have a house icon in the corner, instead of the
Facebook logo.

Next, let's add in the search bar. The example code already had one in there,
but it didn't look quite right. [Bootstrap's documentation has an example
input field with an attached button](http://getbootstrap.com/components/#input-groups-buttons).
We can use this code, and modify the button to display the "search" Glyphicon.

Modify the `form` element to include the search bar:

```html
<form class="navbar-form navbar-left" role="search">
  <!-- Left-aligned items. -->
  <div class="input-group">
    <input type="text" class="form-control" placeholder="Search Facebook">
    <span class="input-group-btn">
      <button type="submit" class="btn btn-default">
        <span class="glyphicon glyphicon-search"></span>
      </button>
    </span>
  </div>
</form>
```

Next, the right-hand side of the navigation bar has 7 different buttons spread
among 4 button groups (the picture + name are a single button). The final button
is a dropdown.

[Bootstrap has support for button groups](http://getbootstrap.com/components/#btn-groups-single),
including [various types of dropdown buttons](http://getbootstrap.com/components/#btn-dropdowns-single)
and putting [multiple button groups into a single toolbar](http://getbootstrap.com/components/#btn-groups-toolbar).
We can use the sample code from the Bootstrap guide to craft the buttons we need.

The original navbar example code used a `ul` element for the right hand side
of the navbar, which is an *unordered list*. Typically, `ul` is used to make
bulleted lists. Modern websites abuse it to place many different HTML elements
side-by-side, since you can eliminate the bullet point and change the behavior
of `ul` via CSS.

`ul` is not an appropriate element for the right-hand-side of our navigation
bar, since we'll be using a button toolbar to group things together.

Change the `ul` element above into a `div`, like so:

```html
<div class="nav navbar-nav navbar-right">
  <!-- Right-aligned items -->
  <div class="btn-toolbar pull-right" role="toolbar">
    <div class="btn-group" role="group">
      <button type="button" class="btn btn-default">
        John
      </button>
    </div>
    <div class="btn-group" role="group">
      <button type="button" class="btn btn-default">
        Home
      </button>
    </div>
    <div class="btn-group" role="group">
        <button type="button" class="btn btn-default">
          <span class="glyphicon glyphicon-user"></span>
        </button>
        <button type="button" class="btn btn-default">
          <span class="glyphicon glyphicon-comment"></span>
        </button>
        <button type="button" class="btn btn-default">
          <span class="glyphicon glyphicon-globe"></span>
        </button>
    </div>
    <div class="btn-group" role="group">
      <button type="button" class="btn btn-default">
        <span class="glyphicon glyphicon-lock"></span>
      </button>
      <div class="btn-group" role="group">
        <button type="button" class="btn btn-default dropdown-toggle"
			    data-toggle="dropdown">
          <span class="caret"></span>
        </button>
        <ul class="dropdown-menu">
          <li><a href="#">Log out...</a></li>
        </ul>
      </div>
    </div>
  </div>
</div>
```

Notice that the above HTML is entirely composed of Bootstrap sample code. All we
did was replace the text of the buttons with different text or a Glyphicon.

Now if you look at the navbar, it'll look mostly right... but there's an issue
with how the buttons display! They are bunched up toward the top of the screen:

![Facebook Clone Button Issue](../images/facebook_clone_button_issue.png)

Ideally, we'd like these to be vertically aligned within the navbar. The
Bootstrap documentation [discusses this issue](http://getbootstrap.com/components/#navbar-buttons),
and has a solution:

> Add the `.navbar-btn` class to `<button>` elements not residing in a `<form>`
> to vertically center them in the navbar.

Apply this fix to *every `button` element in the navbar* (except for the search
  button -- since that's within a `form`!), and the navbar will look as you'd expect:

![Facebook Clone Button Fixed](../images/facebook_clone_button_fixed.png)

When you get a notification, friend request, or message, Facebook adds a number
beside the appropriate button in the navigation bar. Bootstrap supports this
functionality; [it calls these numbers "badges"](http://getbootstrap.com/components/#badges).

Add badges to the notification, friend request, and message buttons:

```html
<div class="btn-group" role="group">
  <button type="button" class="btn btn-default">
    <span class="glyphicon glyphicon-user"></span>
    <span class="badge">5</span>
  </button>
  <button type="button" class="btn btn-default">
    <span class="glyphicon glyphicon-comment"></span>
    <span class="badge">1</span>
  </button>
  <button type="button" class="btn btn-default">
    <span class="glyphicon glyphicon-globe"></span>
    <span class="badge">3</span>
  </button>
</div>
```

Next, the search bar is a little too small. Facebook uses a 395px wide search
bar. We can create a CSS class for the search bar, and make it 395 pixels wide.

Add the following to `facebook.css`:

```css
.fb-search {
  width: 395px;
}
```

Add the `fb-search` class to the `input` tag for the search bar and... it
doesn't do anything! Why is this?

If you are using Google Chrome, you can right-click the search bar, and click on
*Inspect* to open up Chrome's developer tools. It will show you that Chrome
is ignoring our `width` setting, since it is set already in the Bootstrap
class `form-control`:

![Facebook Search Size Failure](../images/facebook_search_size_increase_fail.png)

We can tell the web browser to make `fb-search`'s `width` setting override
`form-control`'s by marking it `!important`. Using `!important` is
generally not recommended, as it makes your CSS hard to debug, but sometimes it
cannot be avoided. In this case, we do not want to modify Bootstrap, yet we want
to change its behavior for this one case.

You use `!important` on individual properties, like so:

```css
.fb-search {
  width: 395px !important;
}
```

Now, your navigation bar should look like the following:

![Facebook Clone Navbar Badges](../images/facebook_clone_navbar_badges.png)

The navbar is now complete! Later, we'll revisit the navbar to make it look more
like Facebook.

**`commit` your changes with the commit message `fb3`, and `push` the changes to GitHub.**

## Step 04: The Left Sidebar

The left sidebar of Facebook contains a laundry list of destinations:

![Facebook Left Sidebar](../images/facebook_left_sidebar.png)

We'll emulate a truncated version of this list in Bootstrap that omits the
specific groups and pages that I belong to.

We could implement this list using a Bootstrap grid, but there's an
easier solution built into Bootstrap.

Notice that the **News Feed** item in the list is **bolded**. The user can only
be in one of these destinations at once, which will populate the Main Feed
section of the site. The active destination is bolded.

Bootstrap provides this functionality via [pills](http://getbootstrap.com/components/#nav-pills).
While pills look *visually* different from Facebook's sidebar, the concept
behind the UI control is the same.

Like before, we'll use the closest Glyphicon for each of the icons in the list:

```html
<!-- Left sidebar: A cell that spans 2 columns -->
<div class="col-md-2">
  <ul class="nav nav-pills nav-stacked">
    <li role="presentation"><a href="#">John Vilk</a></li>
    <li role="presentation">
      <a href="#"><span class="glyphicon glyphicon-pencil"></span>
	  Edit Profile</a>
    </li>
    <!-- List items that are just text are not indented, and look like the
         Facebook section labels. -->
    <li role="presentation">FAVORITES</li>
    <!-- The class "active" highlights this item in the list -->
    <li role="presentation" class="active">
      <a href="#"><span class="glyphicon glyphicon-list-alt"></span>
	  News Feed</a>
    </li>
    <!-- We can use badges in pills to add numbers beside them. -->
    <li role="presentation">
      <a href="#">
        <span class="glyphicon glyphicon-comment"></span> Messages
		<span class="badge">7</span>
      </a>
    </li>
    <li role="presentation">
      <a href="#"><span class="glyphicon glyphicon-calendar"></span>
	  Events</a>
    </li>
    <li role="presentation">
      <a href="#"><span class="glyphicon glyphicon-picture"></span>
	  Photos</a>
    </li>
    <li role="presentation">
      <a href="#"><span class="glyphicon glyphicon-gift"></span>
	  Gifts</a>
    </li>
    <!-- "Saved" also has a number beside it. -->
    <li role="presentation">
      <a href="#">
        <span class="glyphicon glyphicon-bookmark"></span>
		Saved
		<span class="badge">2</span>
      </a>
    </li>
    <li role="presentation">
      <a href="#"><span class="glyphicon glyphicon-tags"></span>
	  Sale Groups</a>
    </li>
    <li role="presentation">PAGES</li>
    <li role="presentation">
      <a href="#"><span class="glyphicon glyphicon-plus"></span>
	  Create Page</a>
    </li>
    <li role="presentation">
      <a href="#"><span class="glyphicon glyphicon-signal"></span>
	  Create Ad</a>
    </li>
    <li role="presentation">GROUPS</li>
    <li role="presentation">
      <a href="#"><span class="glyphicon glyphicon-plus"></span>
	  Create Group</a>
    </li>
    <li role="presentation">
      <a href="#"><span class="glyphicon glyphicon-user"></span>
	  New Groups</a>
    </li>
    <li role="presentation">FRIENDS</li>
    <li role="presentation">
      <a href="#"><span class="glyphicon glyphicon-pushpin"></span>
	  Amherst, MA</a>
    </li>
  </ul>
</div>
```

Notice how we use `#` as the target of the [anchor (`a`) elements](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/a).
Anchor tags are used to link to a webpage, e.g.:

```html
<a href="https://google.com">Click here to go to Google!</a>
```

... will look like this: [Click here to go to Google!](https://google.com/).

Using `#` as the target of an anchor prevents the webpage from loading a new
page when the user clicks the link. If the user clicks the link, the webpage
will change the URL of the page from `http://localhost:8080/facebook.html` to
`http://localhost:8080/facebook.html#`, but will not do anything else. You can
also add arbitrary text after the `#`, e.g. `#groups`, and the browser will
rewrite the URL to `http://localhost:8080/facebook.html#groups`.

Ordinarily, these URLs are used to link to particular sections of a webpage.
For example, the link `http://getbootstrap.com/css/#type` will bring your browser
to the *Typography* section of the Bootstrap documentation. If you clicked that
same link on the `http://getbootstrap.com/css/` page, it would merely scroll
your browser to the *Typography* section without reloading the webpage.

If the section doesn't exist,
e.g. `http://getbootstrap.com/css/#flying_pigs`, the `#` part of the
link does nothing. In the next workshop, we'll explore how you can
exploit this behavior to make portions of a dynamic website
*linkable*, like this Google.com easter egg which is not a specific
*section* of Google.com:

[https://www.google.com/#q=a+long+time+ago+in+a+galaxy+far+far+away](https://www.google.com/#q=a+long+time+ago+in+a+galaxy+far+far+away)

Now, your left sidebar should look quite nice:

![Facebook Clone Left Sidebar](../images/facebook_clone_left_sidebar.png)

Since that was rather straightforward, you do not have to commit your changes
just yet. Proceed to the next step.

## Step 05: The Right Menu

The right sidebar contains birthday information, trending events, and
advertisements:

![Facebook Right Sidebar](../images/facebook_right_sidebar.png)

*Mmm... Pita Pockets... (This course is not affiliated with Pita Pockets.)*

This sidebar can be recreated using a grid. As we discussed earlier, you can nest
grids *within grids*. Every nested grid has its own 12 columns, which expand to
fill the width of the element containing it. Since the right sidebar is so
small, every column is quite tiny!

We can make a grid with one column of 12-column-wide cells, and nest content
inside it. Initially, you may be tempted to create the rows in the grid like so:

![Facebok Right Sidebar Annotated Wrong](../images/facebook_right_sidebar_annotated_wrong.png)

This grid configuration *will* work, and will produce the intended visuals.
However, this structure betrays the structure of the *information* contained in
the sidebar. The "trending" widget should be contained within one element,
as should the "suggested pages" widget.

If you structure your HTML according to the information displayed, you will
be able to:

* Apply custom CSS styles to specific widgets without impacting other sidebar
  components.
* Make the content of the widget *dynamic*, as we'll discuss in the
  next workshop.
* Easily identify what HTML belongs to the "Trending" widget in a large HTML
  document.

Thus, instead, we will structure the sidebar grid like so:

![Facebook Right Sidebar Annotated](../images/facebook_right_sidebar_annotated.png)

Now, you can flesh out your right sidebar with a skeleton:

```html
<!-- Right sidebar: A cell that spans 3 columns -->
<div class="col-md-3">
  <!-- Nested grid! Like the outer grid, it's just a sequence of rows. -->
  <!-- Ticker -->
  <div class="row">
    Ticker widget
  </div>
  <!-- Birthday -->
  <div class="row">
    Birthday widget
  </div>
  <!-- Trending -->
  <div class="row">
    Trending widget
  </div>
  <!-- Suggested pages -->
  <div class="row">
    Suggested pages widget
  </div>
</div>
```

The *ticker widget* is the little download icon in the top-right corner of the sidebar.
Clicking it expands the ticker. For this workshop, we will not cover the
expanding functionality, and will just make it a static link using the `download-alt` glyphicon.

By default, HTML elements display from left to right, but we want the ticker button
to display all of the way to the right. Bootstrap has a [helper CSS class called
`pull-right`](http://getbootstrap.com/css/#helper-classes-floats) that we can
apply to items within grids. Thus, specify the ticker like so:

```html
<!-- Ticker. -->
<div class="row">
  <div class="col-md-12">
    <a href="#" class="pull-right">
      <span class="glyphicon glyphicon-download-alt"></span>
    </a>
  </div>
</div>
```

*Note that we do not add `pull-right` to the table cell. We apply it to the element within the table cell.*

The *birthday widget* is fairly easy; use a glyphicon birthday cake and some
text within a 12-column-wide cell:

```html
<!-- Birthday -->
<div class="row">
  <div class="col-md-12">
    <span class="glyphicon glyphicon-gift"></span>
	<a href="#">Zak</a> and <a href="#">1 other</a>
  </div>
</div>
```

The *trending widget* is the most complex widget on this sidebar. We can use
another Bootstrap grid for its internal structure:

```html
<!-- Trending -->
<div class="row">
  <div class="col-md-12">
    <div class="row">
      <div class="col-md-12">
        Buttons
      </div>
    </div>
    <div class="row">
      News content.
    </div>
  </div>
</div>
```

The widget has a sequence of buttons, of which one is active at a time. Can you
recall a Bootstrap component that works in this manner?

We can use Bootstrap's [pills component](http://getbootstrap.com/components/#nav-pills)
once more. They are visually different from Facebook's buttons, but that can
be overcome later using CSS.

Since the widget header contains a "TRENDING" label along with the buttons, we
can use a nested row with two cells: one for the label, and one for the pills.
On Facebook, the TRENDING label is roughly 1/4 of the width of the sidebar, but
Bootstrap's elements are generally larger, so we can allocate it 1/3 of the 12 columns
(4) and the rest of the columns to the buttons:

```html
<!-- Trending -->
<div class="row">
  <div class="col-md-12">
    <div class="row">
      <div class="col-md-4">
        TRENDING
      </div>
      <div class="col-md-8">
        <ul class="nav nav-pills">
          <li role="presentation" class="active">
            <a href="#"><span class="glyphicon glyphicon-flash"></span></a>
          </li>
          <li role="presentation"><a href="#">
			  <span class="glyphicon glyphicon-tower"></span>
			  </a></li>
          <li role="presentation"><a href="#">
			  <span class="glyphicon glyphicon-sunglasses"></span>
			  </a></li>
          <li role="presentation"><a href="#">
			  <span class="glyphicon glyphicon-record"></span>
			  </a></li>
          <li role="presentation"><a href="#">
			  <span class="glyphicon glyphicon-facetime-video"></span>
			  </a></li>
        </ul>
      </div>
    </div>
  </div>
</div>
```

The result is structured roughly correctly, but is too wide to fit into the
sidebar!

![Facebook Right Sidebar Trending Wrong](../images/facebook_right_sidebar_trending_wrong.png)

Right-clicking a pill item and clicking *Inspect* in Chrome shows that
Bootstrap adds a lot of *padding* to the anchor elements (the `a` elements) within the
pills:

![Facebook Right Sidebar Trending Padding](../images/facebook_right_sidebar_trending_padding.png)

Now might be a good time for you to read up on the [CSS box model](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Box_Model/Introduction_to_the_CSS_box_model),
which defines what the content/padding/border/margin areas are.

We can alter the padding ourselves via CSS. While we could define a custom CSS
class and apply it to each link in the trending widget, there's a much
easier way!

We can use a CSS [*descendent selector*](https://developer.mozilla.org/en-US/docs/Web/CSS/Descendant_selectors)
to apply stylings to particular elements that are contained within other
elements. In particular, we want to alter the padding of `a` elements within
`ul` elements with the `nav` class within the trending widget. Add the class `fb-trending` to the
12-column-wide cell containing the entire trending widget, and then add the
following CSS rule to `facebook.css`:

```css
/* Style applies to a elements within ul elements with class nav within
   an element with class fb-trending */
.fb-trending ul.nav a {
  padding-left: 5px;
  padding-right: 5px;
  padding-top: 2px;
  padding-bottom: 2px;
}
```

*Note: Above, we combined type and class selectors when we specified `ul.nav`. This means "select `ul` elements with class `nav`."*

Now, the trending header looks a little closer to Facebook's:

![Facebook Right Sidebar Buttons Fixed](../images/facebook_right_sidebar_buttons_fixed.png)

Next, the buttons should be right-aligned. Do you remember how to do this? Add
the `pull-right` CSS class to the `ul` element containing the buttons, and they
will line up starting from the right-hand-side of the sidebar.

Now, you may notice that the TRENDING label isn't aligned with the buttons. In HTML/CSS,
[vertically aligning content is hard to do.](http://phrogz.net/css/vertical-align/)
In this example, we know that the pills are a particular height because 1) the
glyphicons are a particular size, and 2) we set the padding to a specific
amount. They are always 24 pixels high. Text, like "TRENDING", is vertically
aligned to the middle of a line of text. The height of a line of text is
controlled via the `line-height` CSS properly.

We can set the `line-height` for this element to `24px`, which will result in
text that happens to be vertically aligned with our 24 pixel high buttons.
Add the class `fb-trending-title` to the `col-md-4` containing the "TRENDING"
text, then add the following CSS rule to `facebook.css`:

```css
.fb-trending-title {
  line-height: 24px;
}
```

*Note: It's unfortunate that we had to do this. Now, if you change the height of the buttons, you'll need to manually fix this "magic value" to fix alignment.*

Now, TRENDING should be vertically aligned:

![Facebook Right Sidebar Trending Buttons Fixed](../images/facebook_right_sidebar_trending_buttons_fixed.png)

We can use CSS to add a top and bottom border around these buttons, like on
Facebook. We only want to apply the border to the first row of the `fb-trending`
`div`, which contains the buttons.

We can do this using a [*child selector*](https://developer.mozilla.org/en-US/docs/Web/CSS/Child_selectors)
and [CSS *pseudo-classes*.](https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-classes).
The child selector is similar to the descendent selector, except it only applies
to elements that are *direct* children. You can remember this by thinking of
family tries: a child is a
direct descendent of two people, and anyone below a person is that person's descendent.

*Pseudo-classes* are harder to summarize; we recommend you take a look at
[Mozilla Development Network's](https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-classes)
article for more information. The [`:first-child` pseudo-class](https://developer.mozilla.org/en-US/docs/Web/CSS/:first-child)
applies to targets that are the first child.

Putting it all together, we can target first-born `row` elements to `fb-trending`
with the selector `.fb-trending > .row:first-child`, add a top and bottom
border, add a little bit of padding between the buttons and the border, and
add margin space between the border and the content above/below the border:

```css
.fb-trending > .row:first-child {
  border-top: 1px solid lightgrey;
  border-bottom: 1px solid lightgrey;
  /* Padding is the whitespace between the content of fb-trending and its
     border */
  padding-top: 5px;
  padding-bottom: 5px;
  /* Margin is the whitespace between the border and adjacent elements */
  margin-top: 5px;
  margin-bottom: 5px;
}
```

*Confused about border/padding/margin? [Read more about the CSS box model.](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Box_Model/Introduction_to_the_CSS_box_model)*

Your border should look like this:

![Facebook Right Sidebar Trending Border](../images/facebook_right_sidebar_trending_border.png)

Next, we tackle the content of the trending widget!

The contents of the trending widget could be expressed as a grid:

![Facebook Right Sidebar Trending Contents Grid](../images/facebook_right_sidebar_trending_contents_grid.png)

However, a grid is ill-suited for this list. The cell containing the lightning
bolt is more than 1 column wide, but less than 2 columns wide. A grid
would create excess whitespace between the lightning bolt and the news item, and
would look like this:

![Facebook Right Sidebar Trending Contents Padding](../images/facebook_right_sidebar_trending_contents_padding.png)

Bootstrap has a better option called a [media object](http://getbootstrap.com/components/#media).
Each media object can have some type of arbitrarily-sized media to the
left, and text to the right. The text can contain a header, but that is
optional.

The media objects can be [in a list](http://getbootstrap.com/components/#media-list),
which is perfect for the trending widget.
For this list, we want the lightning bolts on the left, and the news item
on the right. Adapt the sample code for the media list for our news items:

```html
<div class="row">
  <div class="col-md-12">
    <ul class="media-list">
      <li class="media">
        <div class="media-left media-top">
          <span class="glyphicon glyphicon-flash"></span>
        </div>
        <div class="media-body">
          <a href="#">George Lucas</a>: Filmmaker Criticizes New
			  "Star Wars" Film and Direction of Franchise Under
			  Disney
        </div>
      </li>
      <li class="media">
        <div class="media-left media-top">
          <span class="glyphicon glyphicon-flash"></span>
        </div>
        <div class="media-body">
          <a href="#">Super Smash Bros.</a>: Game Glitch Allows
			  Players to Control 8 Characters With 1 Controller
        </div>
      </li>
      <li class="media">
        <div class="media-left media-top">
          <span class="glyphicon glyphicon-flash"></span>
        </div>
        <div class="media-body">
          <a href="#">Tuukka Rask</a>: Boston Bruins Player
			  Debuts Goalie Mask for Winter Classic
        </div>
      </li>
      <li class="media">
        <div class="media-left media-top">
          <span class="caret"></span>
        </div>
        <div class="media-body">
          <a href="#">See More</a>
        </div>
      </li>
    </ul>
  </div>
</div>
```

*Note: For the "See More" icon, we use Bootstrap's [caret](http://getbootstrap.com/css/#helper-classes-carets), which is not a Glyphicon.*

The result looks great!

![Facebook Right Sidebar Media List](../images/facebook_right_sidebar_media_list.png)

Recall that Facebook's widget is more compressed, with less whitespace between
items. Where is the extra whitespace between list items coming from? Using
Chrome's developer tools once again, we can *Inspect* the list, which uncovers
that the `media` class adds margin space to the top of list items:

![Facebook Right Sidebar Trending Content Padding](../images/facebook_right_sidebar_trending_content_padding.png)

A quick CSS rule can fix that issue:

```css
.fb-trending .media {
  margin-top: 5px;
}
```

Also, add a final CSS rule to create a bottom border for the entire trending
widget:

```css
.fb-trending {
  border-bottom: 1px solid lightgrey;
}
```

Now, the trending widget is complete! Your right sidebar should now look like
this:

![Facebook Right Sidebar Post Trending Progress](../images/facebook_right_sidebar_post_trending_progress.png)

There's one final widget to tackle: The *Suggested Pages* widget.

![Facebook Right Sidebar Suggested Pages](../images/facebook_right_sidebar_suggested_pages.png)

We could put everything into a grid cell, but notice how everything below
"Suggested Pages" is left-aligned. There is no fancy formatting. We can lump
all of that in a single grid cell, and use HTML line breaks (`<br>`) to put
content onto new lines. Line breaks are generally useful when you need to
add a line between [inline HTML elements](https://developer.mozilla.org/en-US/docs/Web/HTML/Inline_elements),
which typically flow like text. ([Block-level elements](https://developer.mozilla.org/en-US/docs/Web/HTML/Block-level_elements)
are the other side of the coin; they typically exist on their own lines.)

First, download
this
[image of falafel](http://choicesaintlouis.com/wp-content/uploads/2015/08/Falafel-Mediterranean.jpg),
and add it to your repository as `img/falafel.jpg`:

![Falafel](../images/falafel.jpg)

Then, add the following HTML for the "Suggested Pages" widget:

```html
<!-- Suggested Pages -->
<div class="row">
  <div class="col-md-12">
    <div class="row">
      <div class="col-md-8">
        SUGGESTED PAGES
      </div>
      <div class="col-md-4">
        <a href="#" class="pull-right">See All</a>
      </div>
    </div>
    <div class="row">
      <div class="col-md-12">
        <img src="img/falafel.jpg" width="100%" />
        <br><a href="#">Pita Pocket's</a>
        <br> Mediterranean Restaurant · 301 likes
        <br><button type="button" class="btn btn-default">
		<span class="glyphicon glyphicon-thumbs-up">
		</span> Like Page</button>
      </div>
    </div>
  </div>
</div>
```

*Note that all of the tags we used within the column are [inline elements](https://developer.mozilla.org/en-US/docs/Web/HTML/Inline_elements#Elements).
That's why `<br>` works so well for this widget.*

The end result looks pretty nice, but we need some whitespace between the
trending widget and the suggested pages widget; that border is a little too
close:

![Facebook Right Sidebar Suggested Pages](../images/facebook_right_sidebar_suggested_pages_clone.png)

Modify your `.fb-trending` rule in `facebook.css` by adding the property
`margin-bottom: 5px;`. This will add space between the trending widget's bottom
border and the suggested pages widget. (Astute readers who read up on the box
model may note that we could have added 5px of `padding-top` or `margin-top` to
the suggested pages widget instead.)

Your final right sidebar should look like this:

![Facebook Clone Right Sidebar Final](../images/facebook_clone_right_sidebar_final.png)

**`add` `img/falafel.jpg` to your Git repository, `commit` your
changes with message `fb5`, and `push` your changes to GitHub.** Note
that this changeset includes both the left and right sidebar!

## Step 06: The Chat Menu

The chat menu is quite simple looking:

![Facebook Chat menu](../images/facebook_chat_menu.png)

We can recreate this with a Bootstrap grid with two cells: One for
left-aligned content (the online indicator & text), and the second for
right-aligned content (the buttons).

Note that the chat menu is floating, and is thus outside of the `container` we
defined for the `body`. Bootstrap requires that grids be placed
inside an element with class `container` or `container-fluid`.

`container` is one of four fixed widths depending on the size of your screen.
[This table](http://getbootstrap.com/css/#grid-options) contains a listing of
container widths. For example, if your browser window is < 1200 pixels wide,
but greater than 992 pixels wide, `container` will have a total width of
`970 px`. We used `container` on the `body` of the webpage; notice how the
webpage does not change its width when you make subtle changes to the browser
window's width.

`container-fluid` always expands to fill the width of the element that contains
it. We did not use `container-fluid` on the `body` of our webpage, since the
width of our content would expand to fit the entire browser window; Facebook
does not exhibit this behavior, and has whitespace to the sides when the
browser window is sufficiently wide.

The chat menu is floating above the page, and its grid should expand to fill
the width of the chat menu. Thus, we put its grid into a `container-fluid`
container, and divide up its columns between the left and right-aligned items:

```html
<div class="chat-popup">
  <div class="container-fluid">
    <div class="row">
      <div class="col-md-8">
        Left
      </div>
      <div class="col-md-4">
        Right
      </div>
    </div>
  </div>
</div>
```

The chat menu will now look like this, ignoring the drop shadow that my Mac
puts on all of my desktop windows:

![Facebook Clone Chat Menu](../images/facebook_clone_chat_menu_1.png)

The left side can just contain the text "● Chat (32)", with "●" having the color
green. (There are many [Unicode symbols](http://unicode-table.com/en/) that you
can use in your website since your HTML contains a `meta` tag that marks your
HTML document's character set as Unicode with 8-bit code units -- aka `utf-8`. :) )

To color "●" green, we can encapsulate it inside of a [`span` tag](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/span)
with a class applied to it. You should use `span` tags whenever you need to
style inline content (i.e. content that is part of a line of items).
MDN has a great writeup about [inline elements](https://developer.mozilla.org/en-US/docs/Web/HTML/Inline_elements) like `span`, and how they differ from [block-level elements](https://developer.mozilla.org/en-US/docs/Web/HTML/Block-level_elements)
like `div`.

Define a CSS rule that styles things green:

```css
.green {
  color: green;
}
```

Then, add the text to the left-hand-side of the chat menu!

```html
<div class="col-md-8">
  <span class="green">●</span> Chat (32)
</div>
```

The right-hand-side of the menu is comprised of multiple buttons. Unlike the
buttons in the navigation bar, these buttons are quite small. [Bootstrap has button
sizes](http://getbootstrap.com/components/#btn-dropdowns-sizing), so we can
define a group of *extra small* buttons for the right-hand-side:

```html
<div class="col-md-4">
  <div class="btn-group pull-right" role="group">
    <button type="button" class="btn btn-xs">
      <span class="glyphicon glyphicon-pencil"></span>
    </button>
    <button type="button" class="btn btn-xs">
      <span class="glyphicon glyphicon-asterisk"></span>
    </button>
  </div>
</div>
```

Your chat menu should look like this now (ignoring the drop shadow again):

![Facebook Clone Chat Menu](../images/facebook_clone_chat_menu_2.png)

Facebook's chat menu has a border with rounded edges. CSS supports these through
the [border-radius](https://developer.mozilla.org/en-US/docs/Web/CSS/border-radius)
attribute. The chat menu should have a border on the top, left, and right sides
only, and rounded corners on the top left and top right.

Rather than define separate top, left, and right borders, we can define a
border for all sides with `border` and remove it from the bottom by setting
`border-bottom` to `none`. Modify your `chat-popup` CSS rule from before to
include the border properties:

```css
.chat-popup {
  width: 300px;
  position: fixed;
  bottom: 0px;
  right: 20px;
  /* Applies the given border style to all sides. */
  border: 1px solid #000;
  /* Removes the border on the bottom. */
  border-bottom: none;
  border-top-left-radius: 3px;
  border-top-right-radius: 3px;
}
```


Your final chat menu should look like the following:

![Facebook Clone Chat Menu Final](../images/facebook_clone_chat_menu_final.png)

Since that wasn't too difficult, don't commit your changes just yet. We're going
to tackle the main feed next!

## Step 07: The Feed

The feed contains a status update entry form at the top, like this:

![Facebook Status Update Entry](../images/facebook_status_update_entry.png)

...and a list of Facebook status updates following, like this:

![Facebook Status Update](../images/facebook_vaguebook_msg.png)

Notice how everything in the main feed is surrounded by a border. Bootstrap
provides a [panel component](http://getbootstrap.com/components/#panels)
that surrounds content by a box. These panels expand to fill the width of
the HTML element you place them in, so we can place them together in the
main feed without using a grid.

Insert the following skeleton for the main feed:

```html
<!-- Main feed: A cell that spans 7 columns -->
<div class="col-md-7">
  <!-- Status update entry -->
  <div class="panel panel-default">
    <div class="panel-body">
      Status update entry
    </div>
  </div>
  <!-- Status update #1 -->
  <div class="panel panel-default">
    <div class="panel-body">
      Status update #1
    </div>
  </div>
</div>
```

The main feed will now look like this:

![Facebook Clone Main Feed Skeleton](../images/facebook_clone_main_feed_skeleton.png)

The top of the status update entry has three buttons (Update Status, Add
Photos/Video, and Create Photo Album), and only one is active at once.
We can use Bootstrap's [pills](http://getbootstrap.com/components/#nav-pills) once again:

```html
<div class="panel panel-default">
  <div class="panel-body">
    <ul class="nav nav-pills">
      <li role="presentation" class="active">
        <a href="#"><span class="glyphicon glyphicon-pencil">
		</span> <strong>Update Status</strong></a>
      </li>
      <li role="presentation">
        <a href="#"><span class="glyphicon glyphicon-picture"></span>
		<strong>Add Photos/Video</strong></a>
      </li>
      <li role="presentation">
        <a href="#"><span class="glyphicon glyphicon-th"></span>
		<strong>Create Photo Album</strong></a>
      </li>
    </ul>
  </div>
</div>
```

For the input box with picture to the left, we can use Bootstrap's [media object](http://getbootstrap.com/components/#media) again.

The status update input box lets the user input multiple lines of text. There's
only one HTML element that provides this functionality:
[`textarea`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/textarea).

Add the following after the pills:

```html
<div class="media">
  <div class="media-left media-top">
    PIC
  </div>
  <div class="media-body">
    <div class="form-group">
      <!-- rows="2" means "display the textarea as 2 rows high". The user can
           enter more than 2 rows of text. -->
      <textarea class="form-control" rows="2"
	  placeholder="What's on your mind?">
	  </textarea>
    </div>
  </div>
</div>
```

Notice that we didn't make a grid inside of the status update entry. Like
Bootstrap panels, the pills and the media object expand to fill the width of
the status update entry, so they will appear on separate lines. Adding a grid
wouldn't harm anything, though, and would result in the same visual look.

The bottom part of the status update entry contains buttons on the left, and
buttons on the right. We can re-create this using a grid row, with one cell
pulled right. Add the following just after the media object:

```html
<div class="row">
  <div class="col-md-6">
    <div class="btn-group" role="group">
      <button type="button" class="btn btn-default">
        <span class="glyphicon glyphicon-camera"></span>
      </button>
      <button type="button" class="btn btn-default">
        <span class="glyphicon glyphicon-user"></span>
      </button>
      <button type="button" class="btn btn-default">
        <span className="glyphicon glyphicon-heart">
        </span>
      </button>
      <button type="button" class="btn btn-default">
        <span class="glyphicon glyphicon-pushpin"></span>
      </button>
    </div>
  </div>
  <div class="col-md-6">
    <div class="pull-right">
      <button type="button" class="btn btn-default">
        <span class="glyphicon glyphicon-user"></span>
		Friends <span class="caret"></span>
      </button>
      <button type="button" class="btn btn-default">
        Post
      </button>
    </div>
  </div>
</div>
```

The status update entry will now look like this:

![Facebook Clone Status Update](../images/facebook_clone_status_update_1.png)

The little triangle in the corner of the `textarea` lets the user resize the
textarea, which is not something we want. We can solve this with CSS. The [`resize` CSS property](https://developer.mozilla.org/en-US/docs/Web/CSS/resize)
dictates the `textarea`'s resizeability.

The border should also be moved off of the `textarea` and onto the element
containing it. The `textarea` also has a shadow that should be removed.

Add the `fb-status-update-entry` class to the `panel` containing the entire
status update entry. Now we can use CSS to solve our problems:

```css
.fb-status-update-entry textarea {
  resize: none;
  /* Needs to be !important, since Bootstrap sets this elsewhere. */
  box-shadow: none !important;
  border: none;
}
.fb-status-update-entry .media {
  border-top: 1px solid lightgrey;
  border-bottom: 1px solid lightgrey;
  /* Adds whitespace between bottom border and buttons */
  margin-bottom: 10px;
  /* Adds whitespace between top of media object and top border. */
  padding-top: 5px;
}
```


The status update entry form is now complete!

![Facebook Clone Status Update](../images/facebook_clone_status_update_2.png)

A status update itself has a more complicated structure:

![Facebook Clone Status Update](../images/facebook_vaguebook_msg.png)

We can reuse many of the Bootstrap components we've already described
earlier.

First, we can use a [grid](http://getbootstrap.com/css/#grid) for the top of the status update, with a [media object](http://getbootstrap.com/components/#media)
for the picture / post time/date information. Note that we'll have to use
`pull-right` on the cell containing the down arrow, so it appears on the right
side of the status update:

```html
<!-- Status update #1 -->
<div class="panel panel-default">
  <div class="panel-body">
    <!-- Post metadata -->
    <div class="row">
      <div class="col-md-10">
        <div class="media">
          <div class="media-left media-top">
            PIC
          </div>
          <div class="media-body">
            <a href="#">Someone</a>
            <br> Yesterday at 3:48pm · Austin, TX ·
			<span class="glyphicon glyphicon-user"></span>
          </div>
        </div>
      </div>
      <div class="col-md-2">
        <span class="caret pull-right"></span>
      </div>
    </div>
    <!-- Post content -->
    <div class="row">
      <div class="col-md-12">
        ugh.
      </div>
    </div>
  </div>
</div>
```

For Like/Comment/Share, we could use a [button group](http://getbootstrap.com/components/#btn-groups)... but on Facebook, they
look more like regular links. A better option is an [inline list](http://getbootstrap.com/css/#type-lists); we can make an inline list of
links:

```html
<div class="row">
  <div class="col-md-12">
    <ul class="list-inline">
      <li>
      <a href="#"><span class="glyphicon glyphicon-thumbs-up">
		  </span> Like</a>
      </li>
      <li>
      <a href="#"><span class="glyphicon glyphicon-comment">
		  </span> Comment</a>
      </li>
      <li>
      <a href="#"><span class="glyphicon glyphicon-share-alt">
		  </span> Share</a>
      </li>
    </ul>
  </div>
</div>
```

The content below the Like/Comment/Share links has a different background.
Bootstrap panels can [have a footer](http://getbootstrap.com/components/#panels-footer)
with a different background (by default, a similar shade of grey).

The "Like" information can be a simple grid row, and the comments section
can be a [media object list](http://getbootstrap.com/components/#media-list).
The "Comment" field can be media object with an [input group with multiple buttons](http://getbootstrap.com/components/#input-groups-buttons-multiple).

Put all of that together, and we get the following `panel-footer` `div`,
which you should place after the `panel-body` `div`:

```html
<div class="panel-footer">
  <div class="row">
    <div class="col-md-12">
      <a href="#">13 people</a> like this
    </div>
  </div>
  <ul class="media-list">
    <li class="media">
      <div class="media-left media-top">
        PIC
      </div>
      <div class="media-body">
        <a href="#">Someone Else</a> hope everything is ok!
        <br><a href="#">Like</a> · <a href="#">Reply</a> · 20 hrs
      </div>
    </li>
    <li class="media">
      <div class="media-left media-top">
        PIC
      </div>
      <div class="media-body">
        <a href="#">Another Person</a> sending hugs your way
        <br><a href="#">Like</a> · <a href="#">Reply</a> · 20 hrs
      </div>
    </li>
    <li class="media">
      <div class="media-left media-top">
        PIC
      </div>
      <div class="media-body">
        <div class="input-group">
          <input type="text" class="form-control"
			     placeholder="Write a comment...">
          <span class="input-group-btn">
            <button class="btn btn-default" type="button">
              <span class="glyphicon glyphicon-camera"></span>
            </button>
            <button class="btn btn-default" type="button">
              <span className="glyphicon glyphicon-heart">
              </span>
            </button>
          </span>
        </div>
      </div>
    </li>
  </ul>
</div>
```

The status update is nearly complete, but is missing two separators:

1. between the update text and the buttons
2. between the "Like" count and the comments

![Facebook Main Status](../images/facebook_clone_main_status_update_1.png)

![Facebook Vague Message](facebook_vaguebook_msg.png)

We could accomplish this with a border, but an even easier solution is to use
two [`hr` elements](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/hr).

Add an `<hr>` element between the `row` containing the status update tet, and
the `row` containing the button groups. It does not need to be placed inside
of a grid row. Add the second `<hr>` element between the `row` that contains
the like count, and the `media-list`.

Your status update should now look like this:

![Facebook Clone Status Update](../images/facebook_clone_status_update_hr.png)

The size of the `hr` elements is spot-on, but the color is too light and it
adds too much whitespace. We can customize this behavior using CSS.

Add the class `fb-status-update` to the `panel` `div` containing the status
update, and then add the following CSS rule:

```css
.fb-status-update hr {
  margin-top: 5px;
  margin-bottom: 5px;
  /* The color of `hr` is set by its top border color.
     Yeah, it's weird. */
  border-top: 1px solid lightgray;
}
```


The borders now look much better:

![Facebook Clone Status Update Fixed](../images/facebook_clone_status_update_hr_fixed.png)

Now, there's too much whitespace between the Like/Comment/Share links and
the Like counter. If you use Chrome's *Inspect* tool, you'll see that
it comes from the bottom margin on the `list-inline` class, and the bottom
padding on the `panel-body` class.

Reign those in using these two CSS rules:

```css
.fb-status-update .list-inline {
  margin-bottom: 0px;
}

.fb-status-update .panel-body {
  padding-bottom: 5px;
}
```

Now, the status update looks great!

![Facebook Clone Status Update](../images/facebook_clone_status_update_done.png)

We could mock up several different types of Facebook posts (e.g. pictures,
videos, events...), but this workshop is already getting a bit long.
Consider the main feed complete!

**`commit` your changes with the commit message `fb7`, and `push` it to
GitHub`.**

## Step 08: Styling

Your Facebook looks kindof like Facebook, but the colors are quite different:

![Facebook no style](../images/facebook_clone_no_style.png)

![Facebook](../images/facebook.png)

We can improve upon this with a few CSS changes.

First, make the background Facebook gray by modifying our `body` CSS rule
to change the `background-color`:

```css
body {
  padding-top: 60px;
  /* I figured out the background color using Chrome's Inspect tool. */
  background-color: #e9eaed;
}
```

Now, take a look at Facebook... and you'll notice some problems.

This background change highlights some issues with the right sidebar, which
should:

* Have a white background. Right now, it has a gray background.
* Have a small, light gray border. It currently has no border.
* Use gray-colored text. Currently, the text is black.
* Birthday: The present should be white with a red background and round corners.
* Trending: Active pills should be light blue in color with no background, non-active pills should be gray.
* Trending: The lightning bolts next to news items should be light blue.

But we can fix all of these problems with the power of CSS!

Add the `fb-right-sidebar` class to the `col-md-3` `div` containing the right
sidebar, then add the following CSS rules:

```css
/* Fix background, text, and border of right sidebar. */
.fb-right-sidebar {
  /* Gray text. This is the same color Facebook uses. */
  color: #9197a3;
  border: 1px solid lightgrey;
  background-color: white;
  padding-bottom: 10px;
}
/* Make the birthday icon look more Facebookey.
   It would be better practice to add a custom class to the birthday widget, but
   I'm doing this to make the workshop a little faster. */
.fb-right-sidebar .glyphicon-gift {
  color: white;
  background-color: red;
  /* Sets padding at 2px on all sides at once */
  padding: 2px;
  /* Sets the border radius to 2px for each corner. */
  border-radius: 2px;
}
/* Customize the look of non-active pills in trending widget */
.fb-trending > .row:first-child li a {
  /* Tells the element to inherit the color from its parent. Remember that
     we set 'color' for the entire right sidebar to gray! */
  color: inherit;
}

/* Customize the look of active pills in trending widget */
.fb-trending > .row:first-child li.active a {
  background-color: transparent;
  /* Same color as the lightning bolt */
  color: #5990ff;
}
/* Apply a light-blue color to flash icons *only* in the content
   section of the trending widget. */
.fb-trending > .row:nth-child(2) .glyphicon-flash {
  color: #5990ff;
}
```

*Note: Above, we use the [nth-child](https://developer.mozilla.org/en-US/docs/Web/CSS/:nth-child) pseudo-class. Above, we use it to select the second child `row` of `fb-trending`*

Now, things are getting closer:

![facebook clone background](../images/facebook_clone_background.png)

![facebook](../images/facebook.png)

Notice how most of the links on Facebook have a dark blue color, and have bolded
text. We can recreate that on our webpage with a single CSS rule!

```css
/* Makes links dark blue, even if they have been visited. (By default, the
   browser will change the look of visited links.) */
a,
a:visited {
  /* The color Facebook uses. */
  color: #3b5998;
  font-weight: bold;
}
```

*Notice how the above CSS selector had a comma (`,`) in it. Commas lets you apply
a rule to multiple selectors. The above rule says "Bold and color `a` elements
on the page, and [`a` elements with the `:visited` pseudo-class](https://developer.mozilla.org/en-US/docs/Web/CSS/:visited)".*

What's next?

![Facebook Clone Link Fix](../images/facebook_clone_link_fix.png)

How about making the navbar blue and changing the style of its buttons?
Facebook buttons are a dark blue, unless they contain a badge indicating
pending notifications:

![Facebook Navbar Buttons](../images/facebook_navbar_buttons.png)

Recall that we added badges to some of our navbar buttons with the following
code:

```html
<button type="button" class="btn btn-default navbar-btn">
  <span class="glyphicon glyphicon-user"></span>
  <span class="badge">5</span>
</button>
```

We cannot easily identify which buttons in our navbar have badges or not
using CSS. Badges are a *child* of the button, and there are no CSS selectors
that let you style parent elements with a particular child.

Thus, we need a new CSS class! Add the `fb-notifications` class to all three of
the navbar `button`s we have with badges, and then add the following CSS to
`facebook.css`:

```css
/* Blue background */
.navbar {
  background-color: #3a5795;
}

/* Make house logo white, even if the user hovers over it */
.navbar .navbar-brand,
.navbar .navbar-brand:hover {
  color: white;
}

/* Remove the background color and border of all navbar buttons. Make their
   color dark blue, like Facebook. */
.navbar button {
  background-color: transparent;
  border: none;
  color: #2e467c;
}

/* Make buttons slightly darker when the user hovers over it, like Facebook
  does. */
.navbar button:hover {
  background-color: transparent;
  color: #22345c;
  border: none;
}

/* Make the button white if clicked on, and remain white after clicking.
   Facebook normally opens up a menu when you do this.
   :active = user is currently interacting with the button.
   :focus = user is currently interacting or has just interacted with the
   button.
   :active:focus = both at the same time
   We have to override all of these combinations, since Bootstrap has separate
   rules for them.*/
.navbar button:active,
.navbar button:focus,
.navbar button:active:focus {
  background-color: transparent;
  color: white;
  border: none;
  /* Removes halo and shadow on button when clicked. */
  outline: none;
  box-shadow: none;
}

/* Search button style -- overrides the above two rules for the search
   button */
.navbar form button,
.navbar form button:hover,
.navbar form button:focus,
.navbar form button:active,
.navbar form button:active:focus {
  background-color: lightgrey;
  color: black;
  /* Make it a bit wider. */
  width: 50px;
  /* Make the border's curve more gentle */
  border-top-right-radius: 10px;
  border-bottom-right-radius: 10px;
  /* Apply a light-grey border color. You can specify colors as names, rgb
     triplets, or hex numbers. */
  border-top: 1px solid rgb(204, 204, 204);
  border-bottom: 1px solid rgb(204, 204, 204);
  border-right: 1px solid rgb(204, 204, 204);
  /* Removes halo and shadow on button when clicked. */
  outline: none;
  box-shadow: none;
}

/* Navbar button style when the button has notifications.
   Apply same style when the user is hovering the mouse over the button. */
button.fb-notifications,
button.fb-notifications:hover {
  color: white;
}

/* Make the Bootstrap badges more Facebook-style in the navbar */
.navbar .badge {
  background-color: red;
  color: white;
  border-radius: 3px;
  padding-left: 4px;
  padding-right: 4px;
  border: 1px solid black;
  /* Offset the badge a bit so it hovers over the glyphicon. */
  right: 8px;
  top: -10px;
}

/* Make the "John" and "Home" buttons white. Would probably be cleaner
   using a CSS class! */
.navbar .navbar-right > .btn-toolbar > .btn-group:first-child button,
.navbar .navbar-right > .btn-toolbar > .btn-group:nth-child(2) button
{
  color: white;
}

/* Make the "John" and "Home" buttons have a dark blue background when
   hovered over. */
.navbar .navbar-right > .btn-toolbar > .btn-group:first-child button:hover,
.navbar .navbar-right > .btn-toolbar > .btn-group:nth-child(2) button:hover
{
  background-color: #2e467c;
}
```

Now your navbar should look *very* Facebook-ey:

![Facebook Clone Navbar Final](../images/facebook_clone_navbar_done.png)

The left sidebar looks very different from Facebook's:

![facebook clone left sidebar](../images/facebook_clone_left_sidebar_2.png)

![facebook left sidebar](../images/facebook_left_sidebar.png)

First, add the `pull-right` class to the `badge`s beside "Messages" and "Saved".
That will make those badges appear on the right-hand-side of the listing. Then,
add the `fb-left-sidebar` class to the `div` containing the left sidebar so
we can easily style this sidebar in isolation.

The following differences are quite apparent:

* The items are spaced out too much in our list, and should be aligned with
  the titles of their sections.
  * If you view the items using Chrome's *Inspect* tool, you'll see this is
    caused by padding on the `a` element.
* We forgot to add in a space between the *Event* glyphicon and the "Event" text.
  * Whoops. You can fix that in the HTML by adding a space between those two elements. We goofed. :)
* The font color should be black, not blue.
* The badges should not have a background, and should have a dark gray font.
* Section titles should have a dark gray font.
* The "active" pill should have black, bolded text with no background.
* When the mouse hovers over an item in the list, it should have a darker gray
  background.

We can easily make these changes via CSS:

```css
/* Remove padding between list elements, align list items all of the way to the
   left, and make text non-bolded & black. */
.fb-left-sidebar .nav > li > a {
  padding-top: 2px;
  padding-bottom: 2px;
  padding-left: 0px;
  color: black;
  font-weight: normal;
}

/* Make list items have a darker gray background when the mouse hovers
   over them. */
.fb-left-sidebar .nav > li > a:hover,
.fb-left-sidebar .nav > li.active > a:hover {
  /* This is the color Facebook uses */
  background-color: #dcdee3;
  color: black;
}

/* Override Bootstrap's default style, which changes the color/bgcolor of
   list items when you click on them. */
.fb-left-sidebar .nav > li > a:active,
.fb-left-sidebar .nav > li > a:focus,
.fb-left-sidebar .nav > li > a:active:focus,
.fb-left-sidebar .nav > li.active > a:active,
.fb-left-sidebar .nav > li.active > a:focus,
.fb-left-sidebar .nav > li.active > a:active:focus {
  background-color: transparent;
  color: black;
}

/* Make the badges have no background, a dark gray color, and normal font
   weight (removes bold). */
.fb-left-sidebar .badge {
  background-color: transparent;
  /* The same color as Facebook */
  color: #4e5665;
  font-weight: normal;
}

/* Color all text items in the left sidebar this color gray. */
.fb-left-sidebar {
  /* I got this color from Facebook */
  color: #9197a3;
}


/* The active pill should be bolded w/ no background. */
.fb-left-sidebar .nav > li.active > a {
  font-weight: bold;
  background-color: transparent;
}
```

The left sidebar looks much more like Facebook's now:

![Facebook Clone Left Sidebar](../images/facebook_clone_left_sidebar_3.png)
![Facebook Left Sidebar](images/facebook_left_sidebar.png)

We could go on to apply similar changes to the main feed, but we'll stop
here; you probably get the idea by now.

Your Facebook clone should now look like this:

![Facebook Clone Final](../images/facebook_clone_final.png)

**`commit` your changes with commit message `fb8` and `push` them to GitHub.**

## Part 2 Conclusion

You did it! You built Facebook! (...well, kind of...)

You learned about:

* Basic HTML, including the difference between [inline elements](https://developer.mozilla.org/en-US/docs/Web/HTML/Inline_elements) and [block-level elements](https://developer.mozilla.org/en-US/docs/Web/HTML/Block-level_elements)
* The [CSS box model](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Box_Model/Introduction_to_the_CSS_box_model)
* CSS [selectors](https://developer.mozilla.org/en-US/docs/Web/Guide/CSS/Getting_started/Selectors), [pseudo-classes](https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-classes), and [rules](https://developer.mozilla.org/en-US/docs/Web/CSS/Syntax#CSS_rulesets).
* How to use Bootstrap.
* How to examine webpages using the [Chrome Web Inspector](https://developers.google.com/web/tools/chrome-devtools/iterate/inspect-styles/basics) in the Chrome Dev Tools.
* How to customize the look of Bootstrap for your application using CSS.

Now you should be ready to try using Bootstrap yourself!

# Part 4: Submission

You must submit the URL of your Workshop3 GitHub repository to
Moodle. Visit Moodle, find the associated Workshop 3 activity, and
provide your URL. Make sure your Workshop3 repository is public so we
can clone your repository and evaluate your work.
