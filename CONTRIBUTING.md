# Contributing to the Website

The website relies on Jekyll, learn how to install it [here](https://jekyllrb.com/docs/installation/). Once you have Jekyll installed, clone the repository and start the local server by running `bundle exec jekyll serve`. A local version of the website will open at `http://localhost:4000/`.


To add a page, add a markdown file in the `docs` folder and put this header at the top:

<pre>
---
layout: page
title: (Your Page Name)
permalink: (/path/to/your/page)
parent: (Parent Page)
grand_parent: (either Documentation or Guides)
nav_order: 1
---
</pre>

Once you save the file, the page will be on the local server and update every time the file is saved.

## Conventions

### Version-specific data

If a page needs to use the version selector, this should be added under the page title:

<pre>
&lt;head>
    {% include version-select.html %}
&lt;/head>
</pre>

To hide text by default, add this line:
<pre>
&lt;ver-h data-version="<=1.19.3">(text you only want showing for 1.19.3 and below)&lt;/ver-h>
</pre>

To show text by default, add this line:
<pre>
&lt;ver-s data-version=">=1.19.4">(text you only want showing for 1.19.4 and above)&lt;/ver-s>
</pre>

The current allowed `data-version` values are:
- 1.20
- 1.19.4
- 1.19.3
- 1.19
- 1.18.2
- 1.18
- \>=1.19.4
- \>=1.19
- \>=1.18.2
- <=1.18.2
- <=1.19.3

### Field types

Several field types have special tags so at a glance it is easier to see what type a field is. If a page needs this, this should be added under the page title:

<pre>
&lt;head>
    {% include field-type-colors.html %}
&lt;/head>
</pre>

 Here's an example with a boolean field and an integer field:

* <span style="color: #FEC856;font-weight:bold">[B]</span> `some_boolean`: Example boolean, does nothing.
* <span style="color: #5573FF;font-weight:bold">[I]</span> `some_integer`: Example integer, does nothing.

To do this, add this text between the bullet point and the field name:
<pre>
&lt;span bool>[B]&lt;/span>
</pre>

Replace `bool` with the field type, and `B` with the first letter of the field type.

The current field types (and their colors) are:

- `list` (red)
- `bool` (orange)
- `float` (yellow)
- `double` (green)
- `int` (blue)
- `str` (purple)