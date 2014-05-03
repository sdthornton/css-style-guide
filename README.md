# CSS Style Guide :book:
*A generally agreed upon approach to css and scss (originally composed for BespokeOffers.com)*

> "Good code is its own best documentation." – Steve McConnell

## Table of Contents

- **[Precusory Information](#precursory-information)**
  1. [Browsers & Selectors](#browsers--selectors)
  1. [OOCSS](#oocss)


- **[Selector Types](#selector-types)**
  1. [Id's](#ids)
  1. [Classes](#classes)
  1. [Tags](#tags)
  1. [Universal](#universal)
  1. [Pseudo Elements](#pseudo-elements)
  1. [Special Selectors](#special-selectors)


- **[Formatting](#formatting)**
  1. [Whitespace](#whitespace)
  1. [Namespacing](#namespacing)
  1. [Selectors](#selectors)
  1. [Commenting](#commenting)
  1. [Sizes & Numbers](#sizes--numbers)
  1. [Class Naming](#class-naming)
  1. [Colors](#colors)


- **[Ordering & Organizing](#ordering--organizing)**
  1. [Ordering](#ordering)
  1. [Organization](#organization)


- **[Sass with Rails](#sass-with-rails)**


## Precursory Information

#### Browsers & Selectors

  + Browsers read css selectors from right to left. For example, `footer nav a` is parsed by the browser first by searching the DOM for any `a` tags, then finding which of those exist within a `nav` tag, and then finding which of those exist within a `footer` tag. In this example, while a page may only have four (4) anchor tags within the footer nav, the browser still parses through all anchor tags on the page just to style four (4) links. **Decendant selectors are therefore very expensive and should be avoided as much as possilbe**.

#### OOCSS

  + Object Oriented CSS (OOCSS) is a way of writing class names that encourages code reuse, reduces the number of descendant selectors, and ultimately creates faster and more efficient stylesheets that are easier to maintain. With OOCSS content is king and modules are the knights of the round table.

  + While there is still debate over the best way to use OOCSS this style guide takes an approach we've found to be most easily implemented and maintained on a large app. Our implementation of this strategy uses two underscores to declare children selectors, two hyphens to declare class name alternatives, and most distinctly uses actual class names as modules (as opposed to SASS @extend placeholders). Ultimately, we've found that using class names for our modules reduces our stylesheet size even though it means our elements usually have more classes. For a large app, a smaller stylesheet is more important to us than reducing the number of class names on elements.


## Selector Types

*The information in this section is a bit redundant but has been placed here in order to give a deeper understanding of css selectors*

#### Id's
  + Matches an element based on its `id` attribute

  + Prefer class names over id's when writing css selectors

  + Use underscores to match rails, simple_form, and other ruby generated content

    ```scss
    #foo_bar {}
    ```

#### Classes
  + Matches an element based on the names within its `class` attribute

  + Use hyphens to match OOCSS namespacing

  + Use double underscores to imply a child selector

  + Use double hyphens to imply a variant selector

    ```scss
    .foo-bar {}
    .foo-bar__child-element {}
    .foo-bar--alternative {}
    ```

#### Tags
  + Matches an element based on its tag name, e.g. `div`

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

  + `[class^="foo"]` *applies to all elements that have a class name that beings with the string `foo`*

  + `[class*="bar"]` *applies to all elements that have a class name that contains the string `bar`*

  + `[class$="baz"]` *applies to all elements that have a class name that ends with the string `baz`*


## Formatting

#### Whitespace
  + Add a single space between selectors and parentheses

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

  + Add a semi-colon after each declaration and a return after multiple declarations

    ```scss
    // Bad
    .foo-bar { background: #000; color: #fff }

    // Good
    .foo-bar {
      background: #000;
      color: #fff;
    }
    ```

  + Add a space after the colon (`:`) between a declaration's name and value

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

  + Add a line-break between indented child selectors (scss)

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

  + Add a line-break between separate selectors

    ```scss
    // Bad
    .foo {}
    .bar {}

    // Good
    .foo {}

    .bar {}
    ```

  + Add a return after the last declaration and the closing curly bracket (`}`)

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

#### Namespacing
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

#### Selectors
  + Avoid using id's

    ```scss
    // <div id="foo" class="foo-bar">
    // bad
    #foo {}

    // Good
    .foo-bar
    ```

  + Scope children elements with class names, rather than descendant selectors

    ```scss
    // Bad
    // <footer>
    //   <nav>
    //     <a href="#">Link</a>
    //   </nav>
    // </footer>
    footer nav a {}

    // Good
    // <footer class="site-footer">
    //   <nav>
    //     <a href="#" class="site-footer__link">Link</a>
    //   </nav>
    // </footer>
    .site-footer__link {}
    ```

  + Use a maximum of four descendant selectors (but prefer less) and avoid universal selectors. If you need more, then add an appropriate class instead.

    ```scss
    // Bad
    // <header>
    //   <nav>
    //     <ul>
    //       <li>
    //         <a href="#">Link</a>
    //       </li>
    //     </ul>
    //   </nav>
    // </header>
    header {
      nav {
        ul {
          li {
            a {}
          }
        }
      }
    }

    // Good
    // <header>
    //   <nav class="main-nav">
    //     <ul>
    //       <li>
    //         <a href="#" class="main-nav__link">Link</a>
    //       </li>
    //     </ul>
    //   </nav>
    // </header>
    .main-nav__link {}
    ```

  + Don't prepend element tags to class names (unless absolutely needed)

    ```scss
    // Bad
    a.main-nav__link {}

    // Good
    .main-nav__link {}
    ```

  + Rely on inheritance

    ```scss
    // Bad
    .foo-bar p { color: #fff; }

    // Good  
    .foo-bar { color: #fff; }
    ```

#### Commenting
  + Use `//` for comment blocks unless you intend for the compiled css to contain the comment

    ```scss
    // Bad

    /* Just a regular ol' comment */
    /* An important comment that I want in the compiled css */

    // Good

    // Just a regular ol' comment
    /* An important comment that I want in the compiled css */
    ```

#### Sizes & Numbers
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

  + Prefer relative, unit-less line-height

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

  + For zero (0) amounts, don't append a unit

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

#### Class Naming
  + Use human-readable class names but no longer than needed

    ```scss
    // Bad
    .cnt {}
    .navigation {}
    .this-is-a-nav-link-element {}

    // Good
    .content {}
    .nav {}
    .nav__link {}
    ```

#### Colors
  + Use lowercase hex codes for colors

    ```scss
    // Bad
    .foo-bar {
      background: rgba(0,0,0,0.75);
      color: rgb(255,255,255);
    }

    // Good
    .foo-bar {
      background: transparentize(#000, 0.25);
      color: #ffffff;
    }
    ```

  + Use sass variables for colors

    ```scss
    // _variables.scss
    $smoke: #f7f7f7;

    // _global.scss
    .foo-bar {
      background: $smoke;
    }
    ```

## Ordering & Organizing

#### Ordering
  + Alphabetize delcarations

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

  + Delcare @extends first, followed by @includes, and then the rest of your declarations

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

  + Declare variations of a class after original selector
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

#### Organization
  + Use modules and appropriate class names rather than repeating declarations

    ```scss
    // Bad

    /* <div class="buy-now">Buy Now</div> */
    .buy-now {
      background: #000;
      color: #fff;
      display: block;
      padding: 10px;
    }

    /* <div class="checkout">Checkout</div> */
    .checkout {
      background: #000;
      color: #fff;
      display: block;
      padding: 10px;
    }

    // Good

    /* <div class="buy-now button">Buy Now</div>
       <div class="checkout button">Checkout</div> */
    .button {
      background: #000;
      color: #fff;
      display: block;
      padding: 10px;
    }
    ```

## Sass with Rails
  + Prefer @import's in application.css.scss over *= require. This prevents duplication of @extend's and removes the need to declare imports in each file.

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
