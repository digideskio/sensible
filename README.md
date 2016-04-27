<img id="logo" align="right" height="60" src="http://imgh.us/noun_3400_cc.svg">

# sensible

`Sensible` maintains your media-queries where they belong – in your SASS/SCSS. It also makes them available with the same name space in your JS without polluting your HTML. Check out the [demo](http://codepen.io/meodai/pen/kzwAy?editors=011). [Demo2](http://codepen.io/meodai/pen/GZRjom?editors=0110)


## Setup

Install with npm / Download or checkout from Github

```shell
npm install sensible --save-dev
```

Import **_mediaqueries.scss** into your main scss/sass file.

```sass
@import 'mediaqueries';
```

Optionally include **mediaQuery.js** into your html file.

```html
<script src="mediaQuery.js"></script>
```

Alternatively you can require mediaQuery.js with AMD.

```javascript
require(['lib/browser/mediaQuery'], function ( mediaQuery ) {})
```

Note: If you support IE9 and below, make sure you include [matchMedia.js](https://github.com/paulirish/matchMedia.js). If you use bower, this should already be in your ```bower_components``` folder as it is a sensible dependency.


## Usage SCSS

### Set up your breakpoints
The variable `$breakpoints` must be defined before you import mediaqueries.

```sass
$breakpoints: (
    "mobile"              : "only screen and (max-width:740px)",
    "tablet"              : "only screen and (max-width:1050px)",
    "desktop"             : "only screen and (min-width:1051px)",
    "print"               : "print"
);
```

### Use the `breakpoint([device])` mixin

```sass
body {
    padding: 40px;
}

@include breakpoint(tablet) {
    body {
        padding: 20px;
    }
}

.main {
    margin: 40px;
    @include breakpoint(mobile) {
        margin: 20px;
    }
}
```


## Usage JS
All the defined breakpoints are available

```javascript
// mediaQuery.onEnter / onLeave (queryString,callback,callOnRegister)

mediaQuery.onEnter('mobile tablet', function(query){
  console.log(query);
},true);

mediaQuery.onLeave('mobile', function(query){
  console.log(query);
},true);

if ( mediaQuery.is('mobile') ){
  console.log("I'm a mobile")
}

if ( mediaQuery.isNot('mobile') ){
  console.log("I'm a not a mobile")
}
```

- - -

## Grid !Optional
`_grid.scss` can be included optionally. `@import 'grid';` and called like this: `@include sensibleGrid()`

It provides a lightweight, flexible and responsive grid based on sensible. The classes generated by it will look like this:

```css
.l-one-whole, .l-one-half, .l-one-quarter, .l-one-whole--mobile, .l-one-half--mobile, .l-one-quarter--mobile
```

Wrap these elements in an element with the class `.l-grid`. Check out the [demo](http://codepen.io/meodai/pen/kzwAy?editors=011) .

The best thing is that they work like you'd expect them to:

```css
.l-one-whole { width: 100% }
.l-one-half { width: 50% }
//etc..
```

You can use it with the classes listed here to fully configure it:

```sass
@include sensibleGrid (
    $modern: false, // flex-box or inline-block (consider using autoprefixer if you use flex-box)
    $gutter: 20px,	// gutter between the col's
    $gutterType: padding, //the gutter can be set as a padding or a margin (margin will use calc() doe)
    $base-font-size: 16px, // base-font-size only used for inline-block layout
    $slug: "l-", // slug used for generated classes
    $pushClasses: false, // do you need .l-push-one-quarter etc. classes ?
    $gridWidths: ( // grid withs and names
        "one-whole"         : 100%,
        "one-half"          : 50%,
        "one-quarter"       : 25%,
        "three-quarters"    : 75%,
        "one-third"         : 33.333%,
        "two-thirds"        : 66.666%,
        "one-fifth"         : 20%,
        "four-fifths"       : 80%,
        "one-sixth"         : 16.666%,
        "five-sixths"       : 83.333%
    ),
    $gridBreakpoints: "mobile-portrait" "mobile" "not-mobile" "tablet-portrait" "tablet" "not-tablet"  "print" // only include the breakpoints you use here to avoid a bloated css
)
```

- - -

## Responsive visibility !Optional
This mixin generates visibility classes in order to hide or show elements on specific breakpoints.
Similar to [Twitter Bootstrap](http://getbootstrap.com/2.3.2/scaffolding.html#responsive).
`_responsive-visbility.scss` can be included optionally. `@import 'responsive-visibility';` and called like this: `@include sensibleGrid()`

```sass
@include responsive-visibility(
  $visibility-breakpoints,
  $overwrite: false,
  $displaTypes: "inline" "inline-block"
)
```

- `$visibility-breakpoints` is a list of you breakpoints you want to include, make sure to they have the same names as in `$breakpoints`

- `$overwrite` by default the mixin generates classes that just show or hide any elements, it will be up to you to show or hide them initially. If `$overwrite` is set to true, the mixin will take care of the hiding for you.

Example with `$overwrite:true` :

```sass
@include responsive-visibility("only-mobile" "only-tablet", true);
```

Will generate:

```css
@media only screen and (max-width: 740px) {
  .is-visible-only-mobile {
    display: block !important;
    visibility: visible;
  }
  .is-hidden-only-mobile, .is-visible-only-tablet {
    display: none !important;
    visibility: hidden;
  }
}
@media only screen and (min-width: 741px) and (max-width: 1051px) {
  .is-visible-only-tablet {
    display: block !important;
    visibility: visible;
  }
  .is-hidden-only-tablet, .is-visible-only-mobile {
    display: none !important;
    visibility: hidden;
  }
}
```

Example with `$overwrite:false`:

```scss
@include responsive-visibility("mobile" "tablet" "desktop", false);
```

Will generate:

```css
@media only screen and (min-width: 1051px) {
  .is-visible-only-desktop {
    display: block !important;
    visibility: visible;
  }
  .is-hidden-only-desktop, .is-visible-only-mobile, .is-visible-only-tablet {
    display: none !important;
    visibility: hidden;
  }
}
//etc...
```
### Logo:
lego by jon trillana from the Noun Project
