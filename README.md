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
by `_tools.widths.scss`’ mixin in order to create grid structures that sized
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

To generate a **12** and a 16 column grid system, call the mixin like so:

```
@include widths(12 16);
```

To generate a 3, a 4, and an 8 column grid system, call the mixin like so:

```
@include widths(3 4 8);
```

### Responsive

By default, Layout does not bundle any responsive functionality. This is because
it should be left to the implementor to decide how media queries are best handled.
