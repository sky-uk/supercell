# Changelog

`sky-toolkit-core` follows [Semantic Versioning](http://semver.org) to help manage the impact of releasing new library versions.


## 1.9.0

### Dependencies

* [[normalize.css](https://github.com/necolas/normalize.css)] Switch hard-coded Normalize to dependency.
* [[supercell](https://github.com/sky-uk/supercell)] Switch layout system to Supercell.


## 1.8.0

### Features

* [defence] Protect links affected by the masthead's `skycom-focus` utility.


## 1.7.0

### Features

* [mixins] responsivize mixin to make any class available at specified breakpoints

### Enhancements

* [typography] used responsivize mixin to generate breakpoint specific text align classes
* [hide] used responsivize mixin to generate breakpoint specific hide classes


## 1.6.0

### Dependencies
* [[stylelint-config-sky-uk](https://github.com/sky-uk/css)] implemented for linting.
* Dependencies refactored to a flat structure.

### Fixes
* [Autoprefixer] Utilise `/*! autoprefixer: off */` comments to prevent Autoprefixer rewrites.


## 1.5.0

### Fixes

* [ie9] Improvements to `c-form-select` functionality.
* [[Stylelint]](http://stylelint.io) Fix linting command and amend errors.


## 1.4.0

### Dependencies

* [[sky-css-lint]](https://github.com/sky-uk/css) Use sky-css-lint for CSS / Sass linting.


## 1.3.0

### Dependencies

* [[Stylelint]](http://stylelint.io) Update to latest Stylelint; allowing for further modification of `.stylelintrc` at a later date.


## 1.2.0

### Dependencies

* [[Eyeglass]](https://github.com/sass-eyeglass/eyeglass) provide support for Eyeglass build tools. Fixes problems with importing nested `node_module` scss dependencies.


## 1.1.0

### Features

* [mixins-ui] `panel-indicator` extracted from tile into a mixin for use on any element. Use `@include panel-indicator();` for the default light panel or `@include panel-indicator("dark");` for the dark panel theme.


## 1.0.0

### Structure

* [project] devDependecies moved to Dependencies to enable sharing with `toolkit-ui`.
* [imports] settings and tools now utilise `all` to share imports across /all` and /tools`.

### Features

* [colors] `ui-` prefixed colors have moved to a `grey-` prefix for greater flexibility.
* [mixins] `focus-styles` for creating consistent keyboard focus effects.

### Enhancements

* [settings] Added global container max width as variable rather than hard-coding.

### Bug Fixes

* [page] Gradient orientation fixed for small devices.
* [font-face] Prevent Sky Text from outputting if a custom font is defined.

### Deprecations

* [legacy-typography] Config switch now fully deprecated.


## 0.5.2

### Features

* [divider] New mixins for creating divider gradient border and shadow.

### Enhancements

* [colors] Added `mid` gradient to `gradients` variable map.
* [forms] ie9 class to hide gradient text overflow for `c-form-select`.
* [functions] Added `convert-to-em` helper to convert em and px values to the equivalent em value ie `convert-to-em(40px) = 2em` with optional base font-size.
* [functions] Added `strip-unit` helper to remove units from a value. ie `strip-unit(400px) = 400`.
* [gradients] `background-gradient` can now utilise an inverted horizontal direction and percentage overrides.
* [settings] Update small breakpoint to 420px.


## 0.5.1

### Bug Fixes

* [page] Solid bg fallback for IE9 to replace broken gradient.


## 0.5.0

### Enhancements

* [gradients] Sky Cinema gradient implemented to `$gradients`, replacing Sky Movies.
* [typography] Typographic scale implemented in a responsive sass-map under `$text`.
* [sass-deprecate] Left-over code from sass-deprecate removed.

### Deprecations

* [legacy-typography] We removed the previous typographic variables in favour of a responsive approach. To deprecate gracefully, a toggle variable has been provided in settings/config. To continue using the previous classes set `$legacy-typography: true;` at the very top of your sass import, before toolkit-core.


## 0.4.0

### Enhancements

* [settings] Set settings maps to `!default` to enable easier overwriting of values if needed

### Deprecations

* [sass-deprecate] We removed the sass-deprecate library in favour of changelogs and improved release notes


## 0.3.15

### Enhancements

* [utilities] Added `.u-vertical-align` helper to allow vertical centering of elements
* [utilities] Added `tiny` variation to the spacing utility
* [tools] Added `radial` to the `background-gradient` mixin
* [settings] Added `ui-mid` to the `colors` map


### Bug Fixes

* [layout] Fixed margin left on `o-layout--narrow`
* [utilities] Fix missing zero-value spacing modifiers
* [utilities] Added IE9 specific form fixes

### Deprecations

* [defence] Moved defence to `toolkit-ui`
