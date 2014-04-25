# FED CSS Style Guide
*A generally agreed upon approach to css/scss for the Bespoke app*


## Precursory Information

#### How browsers read selectors

  + Browsers read css selectors from right to left. `footer nav a` then is parsed by the browser first by searching the dom for `a` tags, then finding which of those exist within a `nav` tag, and then find which of those exist within a `footer` tag. In this example, while a page may only have four (4) anchor tags within the footer nav, the browser still parses through all anchor tags on the page just to style four (4) links. **Decendant selectors are therefore very expensive and should be avoided as much as possilbe**.


## Selectors

#### Id's
  + Use underscores to match rails and simple_form generated content

    ```scss
    #foo_bar {}
    ```

#### Classes
  + Use hyphens to match OOCSS namespacing
  + Use double underscores to imply a child selector
  + Use double hyphens to imply a variant selector

    ```scss
    .foo-bar {}
    .foo-bar__child-element {}
    .foo-bar--alternative {}
    ```

#### Tags
  + Avoid except for global scoping

    ```scss
    // Bad
    // Style all the links within the footer
    .footer a {}

    // Good
    // Style all links on all pages
    a {}
    ```

#### Universal
  + Avoid except for global scoping

    ```scss
    [hidden="true"] {}
    * {...}
    [data-ui-component] {}
    ```

#### Pseudo Elements
  + Use for extra styling
  + For accessibility reasons, avoid declaring site copy within a pseudo element  
  + Use single colons, `:`, in order to maintain support for legacy browsers (this may change)

    ```scss
    // Bad
    .heading:before { content: "You are on page:" }

    // Good
    .icon-search:before {
      content: "/f00";
      display: inline-block;
      margin-right: 0.5em;
    }

    .4-col-grid:nth-child(4n) {
      margin-right: 0;
    }
    ```

#### Special Selectors
  + `*` *applies to all elements*
  + `.foo ~ .bar` *applies to all .bar elements that are preceded by .foo*
  + `.foo + .bar` *applies to all .bar elements that are immediately preceded by .foo*
  + `.foo > .bar` *applies to all .bar elements that are direct descendants of .foo*


## Formatting

#### Whitespace
  + Add a single space between declarations and parentheses

    ```scss
    // Bad
    .foo-bar{}

    // Good
    .foo-bar {}
    ```

  + Add a return between multiple selectors

    ```scss
    // Bad
    .foo-bar, .foo-bar-baz {}

    // Good
    .foo-bar,
    .foo-bar-baz {}
    ```

  + Add a semi-colon and a return after multiple declarations

    ```scss
    // Bad
    .foo-bar { background: #000; color: #fff }

    // Good
    .foo-bar {
      background: #000;
      color: #fff;
    }
    ```

  + For selectors with a single declaration, append a semi-colon but keep to one line

    ```scss
    .pull-left { float: left; }
    ```

  + Add a space after the colon in declarations

    ```scss
    // Bad
    .foo-bar {
      background:#000;
      color: #fff;
    }

    // Good
    .foo-bar {
      background: #000;
      color: #fff;
    }
    ```

  + Add a return between child declarations

    ```scss
    // Bad
    .foo-bar {
      background: #000;
      color: #fff;
      .child-element {
        border: solid 1px #ccc;
      }  
    }

    // Good
    .foo-bar {
      background: #000;
      color: #fff;

      .child-element {
        border: solid 1px #ccc;
      }
    }
    ```

  + Add a return between declarations

    ```scss
    // Bad
    .foo {}
    .bar {}

    // Good
    .foo {}

    .bar {}
    ```

  + Add a return after last delcaration

    ```scss
    // Bad
    .foo-bar {
      background: #000;
      color: #fff; }

    // Good
    .foo-bar {
      background: #000;
      color: #fff;
    }
    ```

  + Use soft tabs with two (2) spaces

    ```scss
    // Bad
    .foo-bar {
        background: #000;
        color: #fff;
    }

    // Good
    .foo-bar {
      background: #000;
      color: #fff;
    }
    ```

  + Don't add a space after commas within parentheses, but add a space after commas that separate declarations

    ```scss
    // Bad
    .foo-bar {
      box-shadow: inset 0 2px 2px rgba(0, 0, 0, 0.15),0 0 4px rgba(0, 0, 0, 0.15);
      transform: translate3d(-200px, 0, 0);
    }

    // Good
    .foo-bar {
      box-shadow: inset 0 2px 2px rgba(0,0,0,0.15), 0 0 4px rgba(0,0,0,0.15);
      transform: translate3d(-200px,0,0);
    }
    ```

#### Ordering
  + Alphabetize

    ```scss
    // Bad
    .container {
      position: relative;
      max-width: 960px;
      padding: 24px;
      margin: 0 auto;
    }

    // Good
    .container {
      margin: 0 auto;
      max-width: 960px;
      padding: 24px;
      position: relative;
    }
    ```

  + Delcare @extends first, then @includes, and then the rest of the declarations

    ```scss
    // Bad
    .foo-bar {
      background: #000;
      @extend: %clearfix;
      color: #fff;
      @include: box-shadow(0,0,2px,#000);
    }

    // Good
    .foo-bar {
      @extend %clearfix;
      @include box-shadow(0,0,2px,#000);
      background: #000;
      color: #fff;
    }
    ```

  + Declare variations of a class after original declaration
    ```scss
    .content {
      @extend %clearfix;
      max-width: 960px;
      padding: 24px;
      position: relative;
      width: 100%;
    }

    .content--small {
      max-width: 768px;
    }
    ```

#### Namespacing (follows OOCSS for classes and rails format for ids)
  + Use underscores for id's

    ```scss
    #foo_bar {}
    ```

  + Use hyphens for class names

    ```scss
    .foo-bar {}
    ```

  + Use two hyphens for class alternatives

    ```scss
    .foo-bar {}

    .foo-bar--alternative {}
    ```

  + Use two underscores for child elements

    ```scss
    .foo-bar {}

    .foo-bar__child {}
    ```

  + Scope children elements with classes, rather than descendant selectors

    ```scss
    // Bad
    .site-footer a {}

    // Good
    .site-footer__link {}
    ```

#### Organization
  + Use modules and appropriate class names rather than repeat declarations

    ```scss
    // Bad
    // <div class="buy-now">Buy Now</div>
    .buy-now {
      background: #000;
      color: #fff;
      display: block;
      padding: 10px;
    }

    // <div class="checkout">Checkout</div>
    .checkout {
      background: #000;
      color: #fff;
      display: block;
      padding: 10px;
    }

    // Good
    // <div class="buy-now button">Buy Now</div>
    // <div class="checkout button">Checkout</div>
    .button {
      background: #000;
      color: #fff;
      display: block;
      padding: 10px;
    }
    ```

#### Sizes
  + Append 0 to amounts between 0 and 1

    ```scss
    // Bad
    .foo-bar {
      margin: .5em;
      padding: .5em;
    }

    // Good
    .foo-bar {
      margin: 0.5em;
      padding: 0.5em;
    }
    ```

  + Prefer em's over px for padding, margin, and font-size

    ```scss
    // Assuming a 16px or 100% base font-size in html or body tag
    // Bad
    .foo-bar {
      font-size: 16px;
      margin: 24px 0;
      padding: 24px;
    }

    // Good
    .foo-bar {
      font-size: 1em;
      margin: 1.5em 0;
      padding: 1.5em;
    }
    ```

  + Prefer relative line-heights over px or em

    ```scss
    // Bad
    .foo-bar {
      font-size: 1em;
      line-height: 1.5em;
    }

    // Good
    .foo-bar {
      font-size: 1em;
      line-height: 1.5;
    }
    ```

  + For zero (0) amounts, don't append px or em

    ```scss
    // Bad
    .foo-bar {
      margin: 1em 0em;
      padding: 0em 1em;
    }

    // Good
    .foo-bar {
      margin: 1em 0;
      padding: 0 1em;
    }
    ```

#### Sass/Rails
  + Use sass variables for colors

    ```scss
    // _variables.scss
    $smoke: #f7f7f7;

    // _global.scss
    .foo-bar {
      background: $smoke;
    }
    ```

  + Prefer @import's in application.css.scss over *= require. This prevents duplication of @extend's and removes the need to declare imports in each file. (This may not yet be possible until after refactor of application.css.scss).
  + Use image-url and font-url in .scss files over <%= asset_path %> in .scss.erb files

    ```scss
    // Bad
    @font-face {
      font-family: "CustomFont";
      src: url('<%= asset_path "custom_font.eot" %>');
    }

    .foo-bar {
      background: url('<%= asset_path "background.png" %>');
    }

    // Good
    @font-face {
      font-family: "CustomFont";
      src: font-url('custom_font.eot');
    }

    .foo-bar {
      background: image-url('background.png');
    }
    ```
