# Layout

_Layout is an ITCSS-compatible library for building grid-like structures in our
UIs. It can be consumed on its own, or as part of Toolkit._

## Installation

Layout is split into two core files:

* **`_tools.widths.scss`**, which contains a mixin which we need to call (i.e.
  Layout does not execute this mixin itself) in order to generate a suite of
  (responsive) width classes in the format `.u-width-1/2`.
* **`_objects.layout.scss`**, which is the actual grid-like structure that will
  lay out our UI.

The classes from `_objects.layout.scss` are augmented by the classes generated
by `_tools.widths.scss`’ mixin in order to create grid structures that are sized
accordingly, e.g.:

```
<div class="o-layout">
  <div class="o-layout__item  u-width-1/2">
    ...
  </div>
</div>
```

## Implementation

To generate your responsive width classes (e.g. `.u-width-1/2`) you need to call
the `widths()` mixin in your project, passing in the number of columns you would
like to create. To create a 12 column grid system, simply call the mixin like
so:

```
@include widths(12);
```

To generate a 12 and a 16 column grid system, call the mixin like so:

```
@include widths(12 16);
```

To generate a 3, a 4, and an 8 column grid system, call the mixin like so:

```
@include widths(3 4 8);
```

### Responsive

In the interests of being as unopinionated as possible, Layout will not
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

To generate a 12 column grid system for use on screens over 1200px wide:

```
@media screen and (min-width: 1200px) {
  @include widths(12, \@large);
}
```

This will create a suite of classes—that only exist in scenarios over 1200px
wide—that look like this:

```
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
