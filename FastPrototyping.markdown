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

Scss & Sass
===========


sass-convert --from scss --to sass _utilities.scss _utilities.sass