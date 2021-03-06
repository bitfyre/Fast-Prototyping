Fast Prototyping with HAML, Sass, Compass, and Middleman
========================================================

First a Little Background
=========================

What is HAML?
=============

- HTML Abstraction Markup Language
- A Markup/Templating language that generates clean semantic XHTML
- Originally created by [Hampton Catlin](http://hamptoncatlin.com/ "Hampton Catlin")
- Currently maintained by [Nathan Weizenbaum](http://nex-3.com/ "Nathan Weizenbaum") & [Chris Eppstein](http://chriseppstein.github.com/ "Chris Eppstein")
- Can be found at [http://haml-lang.com/](http://haml-lang.com/ "#haml")

What is Sass?
=============

- Syntactically Awesome Stylesheets
- A stylesheet authoring language that adds things like Variables, Nesting, Mixins, and now Functions to CSS
- Also, originally created by [Hampton Catlin](http://hamptoncatlin.com/ "Hampton Catlin")
- Currently maintained by [Nathan Weizenbaum](http://nex-3.com/ "Nathan Weizenbaum") & [Chris Eppstein](http://chriseppstein.github.com/ "Chris Eppstein")
- Can be found at [http://sass-lang.com/](http://sass-lang.com/ "Sass - Syntactically Awesome Stylesheets")

What is Compass?
================

- CSS Authoring Framework built on top of Sass
- CSS Grid Frameworks, CSS3 helpers, common functions, module for common CSS tasks (e.g. buttons, resets, typography basics)
- Created and Maintained by [Chris Eppstein](http://chriseppstein.github.com/ "Chris Eppstein")
- Can be found at [http://compass-style.org](http://compass-style.org "Sass - Syntactically Awesome Stylesheets")

What is Middleman?
================

- Static Site Generator
- Brings HAML, Sass, and Compass together into nice neat easy to use package
- Built on Sinatra and Padrino to give us all sorts of useful helpers to speed up development
- Created and Maintained [Thomas Reynolds](http://awardwinningfjords.com/ "Award Winning Fjords « Thomas Reynolds")
- Can be found at [https://github.com/tdreyno/middleman/](https://github.com/tdreyno/middleman/ "Middleman on Github")

HAML
====

- Whitespace aware
- By default Outputs clean nicely indented HTML

Quick Example
=============

### HAML

    #section
      %article
        %h1 Hello World
        %p Lorem ipsum dolor sit amet, consectetur adipisicing elit.
      /
        end article
      %aside
        %p.related
          %a{:href => "/related-articles/", :title => "Articles Related to Hello World!"} Related Articles

### HTML

    <div id='section'>
      <article>
        <h1>Hello World</h1>
        <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit.</p>
      </article>
      <!--
        end article
      -->
      <aside>
        <p class='related'>
          <a href='/related-articles/' title='Articles Related to Hello World!'>Related Articles</a>
        </p>
      </aside>
    </div>

Useful Features of HAML
=======================

- Follows CSS conventions 
- Specify different Doctypes `!!!`, `!!! Strict`, `!!! 5`, etc.
- Recognizes conditional comments with `/[if IE]`
- HAML comments `-# Comment Here`
- Run Ruby within templates
- Ruby Interpolation `#{@title}`
- Includes various filters plain text, javascript, css, textile, and more `:plain`, `:javascript`, `:css`, `:textile`

Sass
====

- Provides a way to author CSS with:
  * Variables
  * Selector and Property Nesting
  * Mixins
  * Selector Inheritance
  * Functions, as of sass 3.1
- Compiled to CSS
- Comes with two different syntaxes 
  * Sass, the original more HAML like
  * Scss ("Sassy css"), New as of 3.0, a superset of CSS3
- Used to be bundled with HAML gem, separated as of 3.1

Variables
=========

### Sass

    $font-size: 12
    $text-color: #222

    html
      font-size: $font-size / 16em
      color: $text-color

### Scss

    $font-size: 12;
    $text-color: #222;

    html {
      font-size: $font-size / 16.0em;
      color: $text-color;
    }

### CSS

    html {
      font-size: 0.75em;
      color: #222;
    }

Nesting
=======

### Sass

    nav
      ul
        list-style: none;
      li
        float: left;
        a
          display:block
          padding:
            top: 5px
            right: 10px
            bottom: 4px
            left: 10px
          color: blue
          &:hover, &:focus 
            color: red

### Scss

    nav {
      ul {
        list-style: none;
      }
      li {
        float: left;
    
        a {
          display:block;
          padding: {
            top: 5px;
            right: 10px;
            bottom: 4px:
            left: 10px;
          }
          color: blue;
          &:hover, &:focus {
            color: red;
          }
        }
      }
    }

### CSS

    nav ul {
        list-style: none;
    }
      nav ul li {
        float: left;
      }
        nav ul li a {
          display:block;
          padding-top: 5px;
          padding-right: 10px;
          padding-bottom: 4px:
          padding-left: 10px;
          color: blue;
        }
          nav ul li a:hover, nav ul li a:focus {
            color: red;
          }

Mixins
======

### Sass

    =hover-link
      text-decoration: none
      &:hover
        text-decoration: underline

    a
      @include hover-link

### Scss

    @mixin hover-link {
      text-decoration: none;
      &:hover {
        text-decoration: underline; 
      } 
    }

    a {
      @include hover-link;
    }

### CSS

    a {
      text-decoration: none; 
    }
      a:hover {
        text-decoration: underline; 
      }

Selector Inheritance
====================

### Sass

    .error
      border: 1px #f00
      background: #fdd

    .error.intrusion
      font-size: 1.3em
      font-weight: bold

    .badError
      @extend .error
      border-width: 3px

### Scss

    .error {
      border: 1px #f00;
      background: #fdd;
    }

    .error.intrusion {
      font-size: 1.3em;
      font-weight: bold;
    }

    .badError {
      @extend .error;
      border-width: 3px;
    }

### CSS

    .error, .badError {
      border: 1px #f00;
      background: #fdd;
    }

    .error.intrusion,
    .badError.intrusion {
      font-size: 1.3em;
      font-weight: bold;
    }

    .badError {
      border-width: 3px;
    }

Functions
=========

### Sass

    @function pxs2ems($px: 0, $context: $font-size)
      $ems: $px / $context * 1em
      @return $ems
    
    h1
      font-size: pxs2ems(24, 12)

### Scss

    @function pxs2ems($px: 0, $context: $font-size) {
      $ems: ($px / $context) * 1em;
      @return $ems;
    }
    
    h1 {
      font-size: pxs2ems(24, 12);
    }

### CSS

    h1 {
      font-size: 2em;
    }

Additional Sass & Scss Notes
============================

- Sass orginally inspired by terseness of HAML
- Scss inspired by the LESS framework, trying to make Sass more accessible to designers
- Also contains Control Directives `@if`, `@for`, `@each`, `@while`
- Can `@import` css, scss, sass files into each other
- Will when using @import compiles out to a single file
- Supports a variety of output styles `:nested`, `:expanded`, `:compact`, `:compressed`
- Useful Command line tool to swap between css, sass, scss, and less

    sass-convert --from scss --to sass _utilities.scss _utilities.sass

Compass
=======

- CSS Authoring Framework built on top of Sass
- Integrates with most Ruby web framworks
- Simplifies CSS3 authoring (no more typing, -webkit, -moz, -ms, -o, etc.)
- Has a variety of CSS grid frameworks ported as extensions
  * Blueprint (Default)
  * 960gs
  * YUI
  * HTML 5 Boilerplate
- Even has a custom frameworks built specifically on Compass
  * Susy (one of my favorites)
- Also has a number of other Utility Extensions
  * Compass Colors
  * Fancy Buttons

Grid Frameworks
===============

- CSS Grid Frameworks done the right way
- No presentational classes in html
- Mixins & functions via sass

Middleman
=========

- A static site generator with HAML, SASS, Coffee Script, JS/CSS compression, image compression and cache busting
- Built on Thin, Sinatra, and Padrino
- Provides a simple easy way to build UI's in your favorite Ruby tools with out using a full webapp framework
- So you don't have 

Middleman Tools
===============

- CLI
  * `mm-init`
  * `mm-server`
  * `mm-build`
- Lorem Helpers
  * Words
  * Sentence
  * Paragraphs
  * Date
  * Name
  * Email
- Placeholder image via Placehold.it
- Can even run the sever app on Heroku or other Rack servers
- Helpers for stylesheet links, javascript links, partials

New Slick Stuff I haven't played with
=====================================

- New Project Templates
- YAML Data API
- Feature/Extension API


On to the Code
==============

Quetions?
=========

Thank You!
==========

Links
=====

### HAML

- [http://haml-lang.com/](http://haml-lang.com/)
- [http://haml-lang.com/tutorial.html](http://haml-lang.com/tutorial.html)
- [http://haml-lang.com/docs/yardoc/file.HAML_REFERENCE.html](http://haml-lang.com/docs/yardoc/file.HAML_REFERENCE.html)

### Sass

- [http://sass-lang.com/](http://sass-lang.com/)
- [http://sass-lang.com/tutorial.html](http://sass-lang.com/tutorial.html)
- [http://sass-lang.com/docs/yardoc/file.SASS_REFERENCE.html](http://sass-lang.com/docs/yardoc/file.SASS_REFERENCE.html)

### Compass 

- [http://compass-style.org/](http://compass-style.org/)
- [http://vimeo.com/11671458](http://vimeo.com/11671458)

### Middleman

- [http://awardwinningfjords.com/2009/10/22/middleman.html](http://awardwinningfjords.com/2009/10/22/middleman.html)
- [https://github.com/tdreyno/middleman/wiki/](https://github.com/tdreyno/middleman/wiki/)
- [http://awardwinningfjords.com/2011/04/15/middleman-v11.html](http://awardwinningfjords.com/2011/04/15/middleman-v11.html)
- [http://middlemanapp.com/](http://middlemanapp.com/)