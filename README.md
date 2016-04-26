# Supercell

_Supercell is an ITCSS-compatible library for building grid-like structures in our
UIs. It can be consumed on its own, or as part of Toolkit._

## Contents

0. [Installation](#installation)
0. [Configuration](#configuration)
0. [Usage](#usage)
  0. [Responsive](#responsive)
0. [Options](#options)
0. [Example](#example)

## Installation

Supercell is split into two core files:

* **`_tools.widths.scss`**, which contains a mixin which we need to call (i.e.
  Supercell does not execute this mixin itself) in order to generate a suite of
  (responsive) width classes in the format `.u-width-1/2`.
* **`_objects.layout.scss`**, which is the actual grid-like structure that will
  lay out our UI.

The classes from `_objects.layout.scss` are augmented by the classes generated
by `_tools.widths.scss`’ mixin in order to create layout structures that are
sized accordingly, e.g.:

```HTML
<div class="o-layout">
  <div class="o-layout__item  u-width-1/2">
    ...
  </div>
</div>
```

The reason that the layout and the widths are kept in different
files/suites-of-classes is simple: it allows us to use our width classes (e.g.
`.u-1/2@small`) on non-layout related bits of UI, for example, making an `img`
half of the width of its container in a blog post.

## Configuration

**N.B. If you are using Supercell as part of Toolkit, you will not need to
configure anything. Please ignore this section.**

There are only two parts of Supercell that might need configuring:

1. **The size of the gutters between items.**  
   To modify the size of the gutters in between layout items, simply predefine
   the `$global-spacing-unit` variable _just before_ you `@import`
   `objects.layout.scss`, like so:

   ```SCSS
   $global-spacing-unit: 20px;
   @import "objects.layout";
   ```
2. **The method used to manage rogue whitespace between `inline-block` elements.**  
   Because Supercell uses `inline-block` (which gives us a number of ways of
   manipulating our layouts by using text-level CSS properties), we do have the
   problem of needing to remove the whitespace that is left in between each
   item.

   There are [a number of ways of handling
   this](https://jsfiddle.net/9dy6rwfz/), but they usually all require special
   attention in the markup. These are the most reliable ways of removing the
   whitespace, but are the least user-friendly.

   By default, Supercell uses the `font-size: 0;` hack to remove the whitespace,
   without authors needing to do anything in their HTML to combat the problem.
   This hack is very author-friendly, but isn’t 100% always guaranteed to work.
   If you would like to disable the `font-size: 0;` hack and are prepared to
   implement a markup-based fix, predefine the `$use-markup-fix` just before you
   `@import` `objects.layout`, like so:
   ```SCSS
   $use-markup-fix: true;
   @import "objects.layout";
   ```

## Usage

To generate your width classes (e.g. `.u-width-1/2`) you need to call the
`widths()` mixin in your project, passing in the number of columns you would
like to create. To create a 12 column layout system, simply call the mixin like
so:

```SCSS
@include widths(12);
```

To generate a 12 and a 16 column layout system, call the mixin like so:

```SCSS
@include widths(12 16);
```

To generate a 3, a 4, and an 8 column layout system, call the mixin like so:

```SCSS
@include widths(3 4 8);
```

Supercell will now generate a full suite of classes that will satisfy every
possible width that falls into those boundaries.

### Responsive

In the interests of being as unopinionated as possible, Supercell will not
auto-generate any media queries or responsive classes. This is because the
implementor (i.e. _you_) should be able to decide  where your breakpoints land,
and what their values are. It also allows the implementor to use their media
query manager of choice (e.g. I like [Sass
MQ](https://github.com/sass-mq/sass-mq)) or nothing at all.

To generate responsive variants, simply call the mixin again with two distinct
additions:

1. The mixin must be called within a media query.
2. You must provide a [Responsive
   Suffix](http://csswizardry.com/2015/08/bemit-taking-the-bem-naming-convention-a-step-further/#responsive-suffixes)
   parameter which denotes the point at which that class takes effect.

To generate a 12 column layout system for use on screens over 1200px wide:

```SCSS
@media screen and (min-width: 1200px) {
  @include widths(12, \@large);
}
```

This will create a suite of classes—that only exist in scenarios over 1200px
wide—that look like this:

```CSS
@media screen and (min-width: 1200px) {

  .u-width-1/12@large {
    width: 8.333333333% !important;
  }

  .u-width-2/12@large {
    width: 16.666666667% !important;
  }

  ...

  .u-width-11/12@large {
    width: 91.666666667% !important;
  }
    

  .u-width-12\/12@large {
    width: 100% !important;
  }
    

}
```

## Options

There are a _lot_ of different options (and combinations of options) for
different styles of layout. Below is a rough summary, but please refer to the
comments in the Sass for a more complete description of what each option
provides.

* **`.o-layout--[narrow|wide|flush]`**: Narrow, wide, or no gutters between
  items.
* **`.o-layout--[middle|bottom]`**: Align all items to the vertical middles or
  bottoms of each other (top alignment is the default).
* **`.o-layout--[center|right]`**: Begin filling up layout items from the
  horizontal center or the right hand side of the layout context (filling from
  the left is the default).
* **`.o-layout--reverse`**: Completely reverse the displayed order of the layout
  items.
* **`.o-layout--spaced`**: Add vertical gutters to layout items (they do not
  carry vertical spacing by default).

## Example

```HTML
<ul class="o-layout  o-layout--reverse">

  <li class="o-layout__item
             u-width-1/1  u-width-1/4@medium  u-width-1/2@large">
    100% by default, then 25% width on medium screens, before finally being 50%
    width on large screens and beyond. Displays last on-screen despite being
    defined first in the markup.
  </li>

  <li class="o-layout__item
             u-width-1/2  u-width-1/4@medium">
    50% width by default, then 25% width on medium screens and beyond. Displays
    third on-screen despite being defined second in the markup.
  </li>

  <li class="o-layout__item
             u-width-1/2  u-width-1/4@medium">
    50% width by default, then 25% width on medium screens and beyond. Displays
    second on-screen despite being defined third in the markup.
  </li>

  <li class="o-layout__item
             u-width-1/1  u-width-1/4@medium  u-width-1/1@large">
    100% by default, then 25% width on medium screens, before finally being 100%
    width again on large screens and beyond. Displays first on-screen despite
    being defined last in the markup.
  </li>

</ul>
```
