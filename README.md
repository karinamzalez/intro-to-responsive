---
title: Responsive Web Design and Media Queries
length:
tags: front-end
---

### Goals

By the end of this lesson, you will:

* have an understanding of the history of responsive web design
* be familiar with the various types of media queries and page layouts and how to use them
* have the skills and understanding to implement media queries and add breakpoints effectively and as needed and feel confident that you understand how to control how your site looks on every screen size.

### Structure

We can't control how our users interact with our products, but we *can* make sure that our work looks good and functions correctly on all screen sizes. Your product lives online, it's important to make sure that no matter how a user accesses it they are able to use it successfully and without frustration.

A general understanding of responsive website design and how to use media queries and when to add breakpoints so your page layout resizes nicely is a great skill to have in your toolbelt.

#### Overview

In this session, we'll be diving into responsive page layouts and using media queries to control your page content at all screen sizes. This lesson assumes you are familiar with HTML and CSS fundamentals.

#### History of Responsive Layouts

Responsive web design is a strategy for building websites that work on all devices and screen sizes. In the not so distant past, the standard was to build sites for desktop or laptop screen resolutions. The introduction of smart phones turned this approach on its head, and designers were faced with a whole new set of challenges. In May 2010, Ethan Marcotte outlined an approach called [Responsive Web Design](http://alistapart.com/article/responsive-web-design/) that would become the gold standard in how to handle designing for such a large range of screen sizes and devices.

In a nutshell, this approach uses relative units to set the width and size of the page contents combined with specific breakpoints in the CSS that set styles based on the dimensions of the screen.

There are four primary page layout types:

###### Static Page Layout
A static layout is fixed width and sits in the center of the screen -- it is the traditional web layout. It works on one screen size and one screen size only. It will fail on screens any amount smaller or larger than the original design.

###### Liquid Page Layout
A liquid (also called 'fluid') page layout uses relative units instead of fixed units (think percentages instead of pixels).

Liquid layouts fill the whole page, regardless of the screen or browser width. It's an approach that doesn't take as much thought and planning as other techniques, making it quick and easy to implement. However, this ease of implementation comes with major disadvantages. These layouts fail at screen sizes significantly larger or smaller than the original design.

###### Adaptive Page Layout
An adaptive layout uses CSS media queries to detect the width of the browser and make layout adjustments accordingly. Unlike liquid layouts, adaptive layouts use fixed units like pixels to define widths. They behave like a series of static layouts defined by specific media queries.

Because adaptive layouts typically take less time to build than true responsive layouts, they are a great option for quickly updating an existing static layout to make it compatiable with mobile devices.

The primary drawback to this strategy is that screen widths that fall between the set breakpoints can feel awkward, with contents looking either too crowded or with far too much space.

###### Responsive Page Layout
At first glance, a response site looks a lot like an adaptive site. But start resizing your screen, and you'll see why it's the best solution. A true responsive page layout combines the best parts of a liquid layout and an adaptive layout to create the best experience for your users as they move between devices and screen sizes. By using both relative units and media queries, a responsive site allows us to transition through screen sizes seamlessly and effortlessly.

The site (Liquidapsive)[http://www.liquidapsive.com/] is a great resource showing simple examples of these layout types in action.


#### Using Media Queries

We know we want to build a site that works well on a variety of screen sizes, but we keep talking about "media queries" and "setting breakpoints". What does that mean?

**Media queries** are a Boolean chunk of logic that lives in your CSS, and when you write a series of media queries you are creating a very basic algorithm. They control at what screen size specific styles will be applied.

The W3C recognizes (several different media types)[https://www.w3.org/TR/CSS2/media.html#media-types], but for our purposes we'll primiarly use ``screen``. This indicates that the media query is intended for computer screens.

Other media types that can come in handy include ``print``, which adjusts styles for screened documents that are being printed, and ``handheld``, which is indended for handheld devices. There are also media types that focus on accessiblity by providing tactile braille feedback or working with speech synthesizers.

**Break points** are the pixel widths the media queries reference. When the media query is true (i.e. when the screen size matches what is specified by the break point), the styles specified in that media query will be applied.

If you want a much deeper dive into the how's and why's behind media queries, (Smashing Magazine)[https://www.smashingmagazine.com/2014/07/breakpoints-and-the-future-websites/] has an old, but good, article on the topic.

#### Guided Practice (We do)
#### Putting it into Practice

Let's try this out! We'll build a one-page site made up of layout elements that don't play all that nicely on all screen sizes. We'll have to consider how we want them to look on small, medium, and large screens and add the appropriate media queries and breakpoints so the layout adjusts appropriately.

To get started, we'll set up our HTML skeleton so we have a roadmap of where we're heading with the page before we start adding styles.

```html
<!doctype html>
<html>
<head>
    <title></title>
</head>
<body>

</body>
</html>
```

Now that we have our basic HTML page structure written, we can think about how we want to structure the cotents. We know we want to have nav main content, some secondary content in a sidebar on the right side of the screen, and a footer so we'll go ahead and add the appropriate tags for those chunks of content.

Working in index.html, let's start at the top and work our way down the page. For our primary navigation, we'll use the semantic ``header`` tag to wrap a ``nav`` tag that contains the unordered list that will become our navigation links.

```html
<body>
    <header>
        <nav>
            <ul>
                <li></li>
            </ul>
        </nav>
    </header>
</body>
```

Next, we'll add an ``article`` tag to hold the main content, an ``aside`` tag to hold our secondary sidebar content, and the ``footer`` tag. We have a basic roadmap of how we want to structure our content.

```html
<body>
    <header>
        <nav>
            <ul>
                <li></li>
            </ul>
        </nav>
    </header>
    <article></article>
    <aside></aside>
    <footer></footer>
</body>
```

Now we can easily see, thanks to the semantic tags we're using, what the intented heirarchy of the page is. Building our HTML page in deliberate, small steps helps us think through our layout which will help us keep our styles clean and organized.

Let's add a little bit of clarifying content to these sections. Add a title to your page, fill in the navigation, and include content in your ``article`` and ``aside``. Let's also wrap our articlce and aside in a ``section`` with a class of ``.container``. This will let us control where those elements go as a unit.

We'll keep this content simple for now so we can focus on getting the HTML elements to behave as we want.

```html
<!doctype html>
<html>
<head>
    <title>Responsive Site Example</title>
</head>
<body>
    <header>
        <nav>
            <ul>
                <li>A Link Here</li>
            </ul>
        </nav>
    </header>
    <section class="container">
        <article>
            <h1>Main Content</h1>
        </article>
        <aside>
            <h2>Secondary Content</h2>
        </aside>
    </section>
    <footer>
        <h3>Footer Content</h3>
    </footer>
</body>
</html>
```

For the sake of our sanity, let's pull in a reset file for our CSS. Browsers all have default styles they apply to HTML. Since these default styles are not consistant from browser to browser, it's a good idea to wipe out the default styles before you start writing your own. That's exactly what a reset file does: it resets the default styles! While you can write you own, we'll be using (this one)[http://meyerweb.com/eric/tools/css/reset/] from Eric Meyer. Simply copy and paste it into a new file called ``reset.css`` and add it in the ``<head>`` tag of ``index.html``.

Let's start writing our styles. Make a ``styles.css`` and add it to your ``index.html``. Pro-tip: Make sure you add it on the line **below** your ``reset.css``, or the reset file will override all the styles you write.

Let's start at the top and work our way down the page.

```css
body, html {
  font-family: sans-serif;
}

header {
  background: grey;
  height: 50px;
  margin-bottom: 25px;
  text-align: center;
}

nav {
  padding-top: 15px;
}

nav:hover {
  color: white;
}
```

Let's talk through what we've done here. First, we make sans-serif the default font family to be used through out the site. Sans-serif is generally easier to read on screens, but feel free to use a different font family.

For the header tag, we've done the following things:
- set the background color to gray
- set the height to 50px
- added a 25px margin to the bottom so the contents of our page don't crowd our nav bar
- centered all the content.

Since our ``header`` tag wraps our ``nav`` tag, we don't have to write as many styles here. We've added top padding to vertically center the link, and added a ``:hover`` suedo element that changes the text color to white so our users can tell when they move their cursor over it that it's clickable. And with that, our header navigation is good to go!

On to our body content!

```html
.container {
  height: 400px;
  margin: 0 auto;
}

.main-content {
  background-color: aquamarine;
  float: left;
  height: 400px;
  width: 75%;
}

.secondary-content {
  background-color: cadetblue;
  float: right;
  height: 400px;
  width: 25%;
}
```

This is fairly straightforward, but let's walk through it.

For our wrapping ``.container``, we set the height to match the heights set on ``.main-content`` and ``.secondary-content``. That's all we'll need to do with it at this point!

We've set different background colors on both the main content and secondary content to help us clearly see how they're behaving as we adjust our screen size.

We set ``float: left`` on the primary content and ``float: right`` on the secondary content to make them sit next to each other rather than stacked on top of eachother, and we gave them widths of 75% and 25%, respectively, so together they fill the whole screen band have clear heirarchy and importance.

Now all that's left is out footer! We'll give it the same treatment as the header, but instead of ``margin-bottom``, we use ``margin-top``.

```html
footer {
  background: grey;
  height: 50px;
  margin-top: 25px;
  text-align: center;
}
```
Boom! We have a simple site! Now, try making your browser window big and then make it small. It doesn't look awesome on small and large screens, does it? That's because we've made a liquid page layout, which is a great start but needs a little fine tuning to become responsive. That means it's time for media queries!