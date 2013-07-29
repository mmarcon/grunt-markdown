# grunt-markdown

[![Build Status](https://travis-ci.org/treasonx/grunt-markdown.png?branch=master)](https://travis-ci.org/treasonx/grunt-markdown)

This grunt task takes a set of markdown files and converts them to HTML. It supports [GFM](http://github.github.com/github-flavored-markdown/) with code highlighting. The code highlighting is done using [highlight.js](http://softwaremaniacs.org/soft/highlight/en/).

## Getting Started
Install this grunt plugin next to your project's [grunt.js gruntfile](http://gruntjs.com/getting-started) with:

```bash
npm install grunt-markdown --save-dev
```

Then add this line to your gruntfile:

```javascript
grunt.loadNpmTasks('grunt-markdown');
```

## Documentation
Creating a markdown task is simple. For the basic functionality add the following config in your gruntfile:

```javascript
grunt.initConfig({
  markdown: {
    all: {
      files: [
        {
          expand: true,
          src: 'docs/src/*.md',
          dest: 'docs/html/',
          ext: '.html'
        }
      ]
    }
  }
});

```

Here is an example config using all of the options:

```javascript
grunt.initConfig({
  markdown: {
    all: {
      files: [
        {
          expand: true,
          src: 'docs/src/*.md',
          dest: 'docs/html/',
          ext: '.html'
        }
      ],
      options: {
        template: 'myTemplate.jst',
        markdownOptions: {
          gfm: true,
          highlight: manual,
          codeLines: {
            before: '<span>',
            after: '</span>'
          }
        }
      }
    }
  }
});

```
These are the properties that the `markdown` task accepts:

* `files`: This plugin supports use of the [files API](http://gruntjs.com/configuring-tasks#files) introduced in Grunt 0.4.0. Files may be specified using any one of the [Compact Format](http://gruntjs.com/configuring-tasks#compact-format), [Files Objects Format](http://gruntjs.com/configuring-tasks#files-object-format), or [Files Array Format](http://gruntjs.com/configuring-tasks#files-array-format) (as in the above example).
* `options`: options to be passed to the markdown parser 
    * `template`: If you wish to specify your own html template, use the `template` option. Include the following line: `<%=content%>` where you want the compiled markdown inserted in your template
    * `markdownOptions`: Options passed directly to the markdown parser.

Most markdown options are passed as-is to the [marked](https://github.com/chjj/marked) markdown parser. The only option that is processed prior to compiling the markdown is the `highlight` option. If you specify `auto` or `manual` the task will handle highlighting code blocks for you use highlight.js. If you pass a custom function as the highlight option it will be used to highlight the code.

* `auto`: Will try to detect the language
* `manual`: will pass the language name from markdown to the highlight function
* `codeLines`: specify text that should wrap code lines

## Meta info associaced to markdown pages

When this tool generates HTML pages from `*.md` files it would be nice to provide some meta information that can be used to generate custom
`title` and `meta description` tags. This fork of `grunt-markdown` supports exactly that.

`*.md` files can be annotated as follows (both annotation are optional):

    <!--
    @-name:nice page title
    @-description: google will love this!
    -->
    
The resulting HTML will contain:

    <title>nice page title</title>
    <meta name="description" content="google will love this!">
    
When a custom template is provided, the meta information is accessible via `<%=meta.title%>` and `<%=meta.description%>`.

## License
Original Copyright (c) 2012 James Morrin
Licensed under the MIT license.
