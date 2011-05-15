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
        <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.</p>
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