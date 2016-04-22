# JigSass Objects Media
[![NPM version][npm-image]][npm-url]  
[![Dependency Status][daviddm-image]][daviddm-url]   

 > A flexbox enabled version of @Stubbornella's media object

The [media object](http://bit.ly/Ku2rqE), introduced by Nichole Sullivan, is a
layout abstraction for placing fixed width content and fluid content side by side.

JigSass Media is a flexbox enabled implementation of the orginal, with optional fallback
(See [Configuration](https://txhawks.github.io/jigsass-objects-media/#configutation)).

## Installation

Using npm:

```sh
npm i -S jigsass-objects-media
```

## Usage
First, you need to import JigSass Objects Media:
First, import JigSass Objects Media to your main stylesheet:

```scss
@import 'path/to/jigsass-objects-media/scss/index';
```
And optionally [reconfigure](https://txhawks.github.io/jigsass-objects-media/#configuration) the defaults to your liking.

Like all other JigSass modules, JigSass Button does not automatically generate any CSS when imported.
In order to use its classes, you would have to first explicitly indicate your intention to use
them by enabling their generation in the associated 
[configurations map](https://txhawks.github.io/jigsass-objects-media/#css-output), 
leaving us only with CSS we need:

All JigSass Media classes are responsive-enabled, using
[JigSass MQ](https://txhawks.github.io/jigsass-tools-mq/) and the breakpoints defined in the
[$jigsass-breakpoints](https://txhawks.github.io/jigsass-tools-mq/#variable-jigsass-breakpoints)
variable.

Based on enabled selectors in the 
[configuration map](https://txhawks.github.io/jigsass-objects-media/#css-output), 
responsive modifiers are generated according to the following logic:

```scss
.o-media[--modifier][-[-from-{breakpoint-name}][-until-{breakpoint-name}][-misc-{breakpoint-name}]]
```

So, assuming the `medium`, `large` and `landscape` breakpoints are defined in `$jigsass-breakpoints`
as `600px`, `1024px` and `(orientation: landscape)` respectively,

```scss
$jigsass-media-obj-conf: (
  no-breakpoint: (
    bottom: true,
  ),
  until-medium: (
    bottom: true,
  ),
  from-large-when-landscape: (
    bottom: true,
  ),
)
```

will generate the following classes:
  - `.o-media--bottom`, which is not limited to any media-query.
  - `.o-media--bottom--until-medium`, which will be in effect at
    `(max-width: 37.49em)` and will override styles in the default class
    until that point.
  - `.o-media-bottom--from-large-when-landscape`, which will go into effect at
    `(min-width: 64em) and (orientation: landscape)` and will override styles
    in the default class under these  conditions.


-----

At its simplest form, the media object is simply a fixed element next to a fluid element,
filling up available space:

```example:html
<div class='u-cf o-media'>
  <figure class='o-media__fig'>
    <div class='[ fpo fpo--b fpo--fig ]'></div>
  </figure>
  <div class='o-media__content fpo'>
    <p style='text-align: center'<strong>.o-media__content</strong></p>
  </div>
</div>
```

Like all JigSass object,  JigSass Media is responsive-enabled, and an instance
may be set to stack vertically by using responsive modifier classes on the container
(resize window to see object stacking and unstacking):

```example:html
<div class='u-cf [ o-media--from-small-until-medium o-media--from-large ]'>
  <figure class='o-media__fig'>
    <div class='[ fpo fpo--b fpo--fig ]'></div>
  </figure>
  <div class='o-media__content fpo'>
    <p style='text-align: center'>
      <strong>Media object only from small until medium and  from large on.</strong>
    </p>
  </div>
</div>
```

One of the media object's key features, is that it can be endlessly nested:

```example:html
<! -- First level -->
<div class='u-cf o-media'>
  <figure class='o-media__fig'>
    <div class='[ fpo fpo--b fpo--fig ]'></div>
  </figure>
  <div class='o-media__content fpo'>
    <span>Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.</span>

    <! -- Second level -->
    <div class='u-cf o-media--from-medium'>
      <figure class='o-media__fig'><div class='[ fpo fpo--b fpo--fig ]'></div></figure>
      <div class='o-media__content fpo fpo--c'>
        <span>Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim venia.</span>

        <! -- Third level -->
        <div class='u-cf o-media--from-medium'>
          <figure class='o-media__fig'><div class='[ fpo fpo--b fpo--fig ]'></div></figure>
          <div class='o-media__content fpo'>
            <span>Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit.</span>

            <! -- fourth level -->
            <div class='u-cf o-media--from-large'>
              <figure class='o-media__fig'><div class='[ fpo fpo--b fpo--fig ]'></div></figure>
              <div class='o-media__content fpo fpo--c'>
                Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
              </div>
            </div>
            <div class='u-cf o-media--from-large o-media--rev--from-large'>
              <figure class='o-media__fig'><div class='[ fpo fpo--b fpo--fig ]'></div></figure>
              <div class='o-media__content fpo fpo--d'>
                <strong>Media objects can also be reversed</strong> Media Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
              </div>
            </div>
          </div>
        </div>
      </div>
  </div>
</div>
```

JigSass Media also offers vertical alignment modifiers 
([middle](https://txhawks.github.io/jigsass-objects-media/#middle-aligned), [bottem](https://txhawks.github.io/jigsass-objects-media/#bottom-aligned)) and a [reverse](https://txhawks.github.io/jigsass-objects-media/#reversed) modifier.



## Documention

The full documentation was generated using mdcss, and is available at 
[https://txhawks.github.io/jigsass-objects-media/](https://txhawks.github.io/jigsass-objects-media/)


## Contributing

It is a best practice for JigSass modules to *not* automatically generate css on `@import`, but 
rather have to user explicitly enable the generation of specific styles from the module.

Contributions in the form of pull-requests, issues, bug reports, etc. are welcome.
Please feel free to fork, hack or modify JigSass Objects Lists in any way you see fit.


#### Writing documentation

Good documentation is crucial for usability, scalability and maintainability. When 
contributing, please do make sure that both its Sass functionality (functions, mixins, 
variables and placeholder selectors), as well as the CSS it generates (selectors, 
concepts, usage exmples, etc.) are well documented.

Jigsass Media uses Jonathan Neal's [mdcss](//github.com/jonathantneal/mdcss).

When styles and documentation comments are not automatically generated by your module on `@import`,
please use the `sgSrc/sg.scss` file to enable their generation.

In addition, any file in `sgSrc/assets` will be available for use in the style guide.


## File structure
```bash
┬ ./
│
├─┬ scss/ 
│ └─ index.scss # The module's importable file.
│
├─┬ sgSrc/      # Style guide sources
│ │
│ ├── sg.scc    # It is a best practice for JigSass 
│ │             # modules to not automatically generate 
│ │             # css and documentation on `@import.` 
│ │             # Please use this file to enable css
│ │             # and documentation comments) generation.
│ │
│ └── assets/   # Files in `sgSrc/assets` will be 
│               # available for use in the style guide
│
└─┬ docs/      # Documention
  │
  └── styleguide/ # Generated documentation 
                  # of the module's CSS
 
```

**License:** MIT



[npm-image]: https://badge.fury.io/js/jigsass-objects-media.svg
[npm-url]: https://npmjs.org/package/jigsass-objects-media

[daviddm-image]: https://david-dm.org/TxHawks/jigsass-objects-media.svg?theme=shields.io
[daviddm-url]: https://david-dm.org/TxHawks/jigsass-objects-media
