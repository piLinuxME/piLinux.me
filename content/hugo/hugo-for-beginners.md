---
categories: Programming
topic: Hugo
title: "Hugo for Beginners"
author:
  - M. Hasan
contributor:
#  - Contributor 1
synopsis: >
  A complete beginners’ guide on developing a blog site with Hugo static site generator
seoImageS: hugo-s.jpg
seoImageL: hugo-l.jpg
seoArticleSection: Programming
date: 2020-06-09T12:30:21+02:00
lastmod:
doi: 10.5281/zenodo.3887269
license: CC BY-SA 4.0
reference:
  - 1. Github.com, “The State of the Octoverse,” The State of the Octoverse, accessed May 31, 2020, https://octoverse.github.com/#top-languages.
  - 2. “Data Templates | Hugo,” February 1, 2017, https://gohugo.io/templates/data-templates/#data-driven-content.
  - 3. “Hugo vs Jekyll Benchmarked,” January 26, 2018, https://forestry.io/blog/hugo-vs-jekyll-benchmark/.
  - 4. “Complete List | Hugo Themes,” accessed June 4, 2020, https://themes.gohugo.io/.
  - 5. “StaticGen | Top Open Source Static Site Generators,” accessed June 4, 2020, https://www.staticgen.com/.
  - 6. “Releases - Gohugoio/Hugo,” GitHub, accessed June 4, 2020, https://github.com/gohugoio/hugo/releases.
  - 7. “Apache License, Version 2.0,” accessed June 4, 2020, https://www.apache.org/licenses/LICENSE-2.0.
  - 8. “Html/Template - The Go Programming Language,” accessed June 5, 2020, https://golang.org/pkg/html/template/.
  - 9. “Text/Template - The Go Programming Language,” accessed June 5, 2020, https://golang.org/pkg/text/template/.
  - 10. “Partial Templates | Hugo,” February 1, 2017, https://gohugo.io/templates/partials/.
  - 11. “Configure Hugo | Hugo,” January 2, 2017, https://gohugo.io/getting-started/configuration/.
  - 12. “Front Matter | Hugo,” January 9, 2017, https://gohugo.io/content-management/front-matter/.
  - 13. “Site Variables | Hugo,” February 1, 2017, https://gohugo.io/variables/site/.
  - 14. “Page Variables | Hugo,” February 1, 2017, https://gohugo.io/variables/page/.
  - 15. “Lists of Content in Hugo | Hugo,” February 1, 2017, https://gohugo.io/templates/lists/.
version: 1
nextVersion:
weight: 10
mathjax: false
draft: false
---

*A complete beginners’ guide on developing a blog site with Hugo static site generator*

*Final project: github.com/piLinuxME/collections/tree/master/hugo/hugo-for-beginners*

&nbsp;

### Abstract

Written in one of the fastest-growing languages[1] Golang, Hugo excels in building static sites from local markdown 
files and dynamic API-driven[2] content at a blistering speed[3]. There are numerous free themes[4] available online 
for rapid prototyping and development of a Hugo based blog site. This tutorial concentrates on developing a Hugo based 
site from scratch without importing any already developed theme.

&nbsp;

### Contents

- Abstract
- Introduction
- Environment Setup
    - Windows 10 (64-bit) OS
    - Ubuntu 18.04.4 LTS (64-bit) OS
- New Site Creation
- Theme Development
    - Template for Regular Pages
    - Template for Listing Pages
    - Template for Homepage
    - Template for 404 Error Page
- Summary
- References

&nbsp;

### Introduction

Unlike dynamic websites, static sites have fewer or no dependencies on databases, application servers and thus provides 
enhanced security, faster loading speed, and improved performance for end-users. Manually maintaining and updating each 
page of a static site is cumbersome. Hence, static site generators were born where the developer writes the 
functionality of the site, the content editor publishes or updates articles, and finally, the website generator renders 
the contents into HTML files and saves thousands of development and maintenance hours. Out of the 283 opensource static 
site generators enlisted on staticgen.com[5], here website development using Hugo generator is discussed thoroughly.

&nbsp;

### Environment Setup

For different architectures and operating systems (OS), the compiled versions of Hugo along with the source codes are 
available for free on Github[6] under version 2.0 of the Apache License[7]. Hugo version 0.72.0, Windows 10 (64-bit), 
and Ubuntu 18.04.4 LTS (64-bit) are considered for this tutorial.


##### Windows 10 (64-bit) OS

Hugo binary file for Windows OS can be extracted from 
*github.com/gohugoio/hugo/releases/download/v0.72.0/hugo_0.72.0_Windows-64bit.zip* and can be executed from the 
command-line interpreter. For demonstration, here **hugo.exe** file is saved in **D:\Hugo_workspace** directory. On a 
Windows machine, **hugo.exe** must be located in the same directory from where Hugo’s command-line interface (CLI) 
needs to be accessed unless the "PATH" environment variable is set.

```cmd
# change directory
D:\>cd Hugo_workspace

# check Hugo version
D:\Hugo_workspace>hugo version

# output:
# Hugo Static Site Generator v0.72.0-8A7EF3CF windows/amd64 BuildDate: 2020-05-31T12:08:42Z
```
Listing 1: Run Hugo on a Windows 10 64-bit machine

&nbsp;

##### Ubuntu 18.04.4 LTS (64-bit) OS

Hugo binaries have no dependency. After placing the binary file in **/usr/local/bin** directory, Hugo’s CLI can be 
accessed from any location.

```shell
# home directory
cd

# fetch binary file
wget https://github.com/gohugoio/hugo/releases/download/v0.72.0/hugo_0.72.0_Linux-64bit.tar.gz

# extract
tar -xvf hugo_0.72.0_Linux-64bit.tar.gz

# change directory
cd /usr/local/bin/

# copy hugo binary file
sudo cp ~/hugo .

# return back to the home directory
cd

# check Hugo version
hugo version

# output:
# Hugo Static Site Generator v0.72.0-8A7EF3CF linux/amd64 BuildDate: 2020-05-31T12:07:45Z
```
Listing 2: Run Hugo on a Linux 64-bit machine

&nbsp;

### New Site Creation

With a one-line command `hugo new site tutorial`, Hugo creates a new website scaffolded at **tutorial** project 
directory. The newly-created site’s directory structure is:

Table 1: Directory structure of a newly scaffolded Hugo site

---

|── archetypes

        |── default.md

|── content

|── data

|── layouts

|── static

|── themes

|── config.toml

---

&nbsp;

### Theme Development

This tutorial follows more of a pragmatic approach rather than diving into theories. With the development of a Hugo 
theme, directory structure and different features of Hugo will be explored.

At the root of the project, in this case at **tutorial/** path, executing `hugo new theme custom` creates a new theme 
named "custom" at **tutorial/themes/custom** location. The directory structure of **custom** is:

Table 2: Directory structure of a newly generated theme

---

|── archetypes

        |── default.md

|── layouts

        |── _default

                |── baseof.html

                |── list.html

                |── single.html

        |── partials

                |── footer.html

                |── head.html

                |── header.html

        |── 404.html

        |── index.html

|── static

        |── css

        |── js

|── LICENSE

|── theme.toml

---

&nbsp;

Hugo uses Golang’s data-driven html/template[8] package for generating HTML output safe against code injection and 
text/template[9] package to generate textual output. custom/layouts contains skeletons for four types of pages:

- Homepage
- Listing pages (index pages etc.)
- Regular pages (for About Us page, blog posts or articles, etc.)
- Custom 404 error page

*Listing 3* contains HTML codes of a single webpage built with the Bootstrap CSS and JS libraries. In the upcoming 
lessons, a Hugo theme is created from this webpage.

```html
<!DOCTYPE html>
<html lang="en">

    <head>
        <meta charset="utf-8" />
        <meta name="viewport" content="width=device-width,initial-scale=1" />
        <meta http-equiv="x-ua-compatible" content="IE=edge" />

        <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.5.0/css/bootstrap.min.css" integrity="sha384-9aIt2nRpC12Uk9gS9baDl411NQApFmC26EwAOH8WgZl5MYYxFfc+NcPb1dKGj7Sk" crossorigin="anonymous" />

        <style>
            .px-6 {
                padding-top: 4.5rem !important;
                padding-bottom: 4.5rem !important;
            }
            a {
                color: #000;
            }
            .navbar-nav-text {
                color: #000 !important;
            }
            h1, h2, h3, h4, h5, h6 {
                font-weight: 400;
            }
        </style>

        <title>Hugo for beginners</title>
    </head>

<body>

        <div class="navbar navbar-expand-lg fixed-top navbar-light bg-white">
            <div class="container">
                <a href="/" class="navbar-brand">Hugo for beginners</a>
                <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarResponsive" aria-controls="navbarResponsive" aria-expanded="false" aria-label="Toggle navigation">
                    <span class="navbar-toggler-icon"></span>
                </button>
                <div class="collapse navbar-collapse" id="navbarResponsive">
                    <ul class="navbar-nav">
                        <li class="nav-item dropdown">
                            <a class="nav-link navbar-nav-text" data-toggle="dropdown" href="#" id="blog">
                                Blog
                            </a>
                            <div class="dropdown-menu" aria-labelledby="web-development">
                                <a class="dropdown-item navbar-nav-text" href="/web-development/">
                                    Web Development
                                </a>
                            </div>
                        </li>
                    </ul>
                </div>
            </div>
        </div>

        <div class="container px-6">
            <div class="row">
                <div class="col-md-12">
                    Hello world!
                </div>
            </div>
            <br />
            <br />
            <br />
        </div>

        <footer>
            <div class="container">
                <div class="card">
                    <div class="card-body py-2">
                        <p class="card-text text-center">
                            <a href="./">Hugo for beginners</a> - Content available under a Creative Commons license
                            <a href="https://creativecommons.org/licenses/by-sa/4.0" target="_blank" rel="noreferrer">CC BY-SA 4.0</a>
                            unless otherwise specified.
                        </p>
                    </div>
                </div>
                <br />
            </div>
        </footer>

        <script src="https://code.jquery.com/jquery-3.5.1.slim.min.js" integrity="sha384-DfXdz2htPH0lsSSs5nCTpuj/zy4C+OGpamoFVy38MVBnE+IbbVYUew+OrCXaRkfj" crossorigin="anonymous"></script>

        <script src="https://cdn.jsdelivr.net/npm/popper.js@1.16.0/dist/umd/popper.min.js" integrity="sha384-Q6E9RHvbIyZFJoft+2mJbHaEWldlvI9IOYy5n3zV9zzTtmI3UksdQRVvoxMfooAo" crossorigin="anonymous"></script>

        <script src="https://stackpath.bootstrapcdn.com/bootstrap/4.5.0/js/bootstrap.min.js" integrity="sha384-OgVRvuATP1z7JjHLkuOU7Xw704+h835Lr+6QL9UvYjZE3Ipu6Tp75j7Bh/kR0JKI" crossorigin="anonymous"></script>

    </body>
</html>
```
Listing 3: HTML template of a single webpage

&nbsp;

##### Template for Regular Pages

In the PDF version of this article, *Listing 3* contains four different blocks denoted by four different colors – light 
gray, sky blue, light orange, and light gold in ascending order. On the web version, lines 4 – 28 refers to '`head`' 
block, lines 32 – 53 refers to the '`header`' block, lines 55 – 64 belongs to the '`main`' block and lines 66 – 85 
belongs to the '`footer`' section.

**themes/custom/layouts/_default/baseof.html** is the default template for all rendered regular pages. *Listing 4* shows 
an example of the **baseof.html** template.

```go-html-template
<!DOCTYPE html>
<html lang="en">

{{ block "head" . }}{{ end }}

<body>

{{ block "header" . }}{{ end }}

{{ block "main" . }}{{ end }}

{{ partial "footer.html" . }}

</body>
</html>
```
Listing 4: Example of a **baseof.html** template

&nbsp;

**themes/custom/layouts/_default/single.html** inherits from **baseof.html** template. Hence, in this example, only the 
three blocks – "`head`", "`header`" and "`main`" need to be defined in **single.html** template. *Listing 5* shows the 
first version of the **single.html** template that contains definitions of the three blocks each starting with 
`{{ define "block-name" }}` and ending with `{{ end }}`.

```go-html-template
{{ define "head" }}
    <head>
        <meta charset="utf-8" />
        <meta name="viewport" content="width=device-width,initial-scale=1" />
        <meta http-equiv="x-ua-compatible" content="IE=edge" />

        <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.5.0/css/bootstrap.min.css" integrity="sha384-9aIt2nRpC12Uk9gS9baDl411NQApFmC26EwAOH8WgZl5MYYxFfc+NcPb1dKGj7Sk" crossorigin="anonymous" />

        <style>
            .px-6 {
                padding-top: 4.5rem !important;
                padding-bottom: 4.5rem !important;
            }
            a {
                color: #000;
            }
            .navbar-nav-text {
                color: #000 !important;
            }
            h1, h2, h3, h4, h5, h6 {
                font-weight: 400;
            }
        </style>

        <title>Hugo for beginners</title>
    </head>
{{ end }}

{{ define "header" }}
        <div class="navbar navbar-expand-lg fixed-top navbar-light bg-white">
            <div class="container">
                <a href="/" class="navbar-brand">Hugo for beginners</a>
                <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarResponsive" aria-controls="navbarResponsive" aria-expanded="false" aria-label="Toggle navigation">
                    <span class="navbar-toggler-icon"></span>
                </button>
                <div class="collapse navbar-collapse" id="navbarResponsive">
                    <ul class="navbar-nav">
                        <li class="nav-item dropdown">
                            <a class="nav-link navbar-nav-text" data-toggle="dropdown" href="#" id="blog">
                                Blog
                            </a>
                            <div class="dropdown-menu" aria-labelledby="web-development">
                                <a class="dropdown-item navbar-nav-text" href="/web-development/">
                                    Web Development
                                </a>
                            </div>
                        </li>
                    </ul>
                </div>
            </div>
        </div>
{{ end }}

{{ define "main" }}
        <div class="container px-6">
            <div class="row">
                <div class="col-md-12">
		Hello world!
	</div>
            </div>
            <br /><br /><br />
        </div>
{{ end }}
```
Listing 5: Example of a **single.html** template

&nbsp;

Using partial templates[10] **single.html** template can be refactored easily to keep the templating DRY 
(don’t repeat yourself). *Listing 6* is the refactored version of the **single.html** template.

```go-html-template
{{ define "head" }}
{{ partial "head.html" . }}
{{ end }}

{{ define "header" }}
{{ partial "header.html" . }}
{{ end }}

{{ define "main" }}
{{ partial "main.html" . }}
{{ end }}
```
Listing 6: **single.html** template after code refactoring

&nbsp;

***IMPORTANT***: The trailing **dot** in `{{ partial "partial-name.html" . }}` is a must to include another template 
in the current template!

&nbsp;

Hugo looks for the partial templates in the following paths:
- **layouts/partials/<PARTIALNAME>.html**
- **themes/\<THEME\>/layouts/partials/<PARTIALNAME>.html**

&nbsp;

For this tutorial, the partial templates are saved at **themes/custom/layouts/partials/** location to make it easily 
portable. *Listings 7 – 9* contain codes of the three partial templates – **head.html**, **header.html**, and 
**main.html**.

```go-html-template
    <head>
        <meta charset="utf-8" />
        <meta name="viewport" content="width=device-width,initial-scale=1" />
        <meta http-equiv="x-ua-compatible" content="IE=edge" />

        <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.5.0/css/bootstrap.min.css" integrity="sha384-9aIt2nRpC12Uk9gS9baDl411NQApFmC26EwAOH8WgZl5MYYxFfc+NcPb1dKGj7Sk" crossorigin="anonymous" />

        <style>
            .px-6 {
                padding-top: 4.5rem !important;
                padding-bottom: 4.5rem !important;
            }
            a {
                color: #000;
            }
            .navbar-nav-text {
                color: #000 !important;
            }
            h1, h2, h3, h4, h5, h6 {
                font-weight: 400;
            }
        </style>

        <title>Hugo for beginners</title>
    </head>
```
Listing 7: **head.html** partial template

&nbsp;

```go-html-template
        <div class="navbar navbar-expand-lg fixed-top navbar-light bg-white">
            <div class="container">
                <a href="/" class="navbar-brand">Hugo for beginners</a>
                <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarResponsive" aria-controls="navbarResponsive" aria-expanded="false" aria-label="Toggle navigation">
                    <span class="navbar-toggler-icon"></span>
                </button>
                <div class="collapse navbar-collapse" id="navbarResponsive">
                    <ul class="navbar-nav">
                        <li class="nav-item dropdown">
                            <a class="nav-link navbar-nav-text" data-toggle="dropdown" href="#" id="blog">
                                Blog
                            </a>
                            <div class="dropdown-menu" aria-labelledby="web-development">
                                <a class="dropdown-item navbar-nav-text" href="/web-development/">
                                    Web Development
                                </a>
                            </div>
                        </li>
                    </ul>
                </div>
            </div>
        </div>
```
Listing 8: **header.html** partial template

&nbsp;

```go-html-template
        <div class="container px-6">
            <div class="row">
                <div class="col-md-12">
                    Hello world!
                </div>
            </div>
            <br /><br /><br />
        </div>
```
Listing 9: **main.html** partial template

&nbsp;

The **footer.html** partial template, called by **baseof.html** template, contains –

```go-html-template
        <footer>
            <div class="container">
                <div class="card">
                    <div class="card-body py-2">
                        <p class="card-text text-center">
                            <a href="./">Hugo for beginners</a> - Content available under a Creative Commons license
                            <a href="https://creativecommons.org/licenses/by-sa/4.0" target="_blank" rel="noreferrer">CC BY-SA 4.0</a>
                            unless otherwise specified.
                        </p>
                    </div>
                </div>
                <br />
            </div>
        </footer>

        <script src="https://code.jquery.com/jquery-3.5.1.slim.min.js" integrity="sha384-DfXdz2htPH0lsSSs5nCTpuj/zy4C+OGpamoFVy38MVBnE+IbbVYUew+OrCXaRkfj" crossorigin="anonymous"></script>

        <script src="https://cdn.jsdelivr.net/npm/popper.js@1.16.0/dist/umd/popper.min.js" integrity="sha384-Q6E9RHvbIyZFJoft+2mJbHaEWldlvI9IOYy5n3zV9zzTtmI3UksdQRVvoxMfooAo" crossorigin="anonymous"></script>

        <script src="https://stackpath.bootstrapcdn.com/bootstrap/4.5.0/js/bootstrap.min.js" integrity="sha384-OgVRvuATP1z7JjHLkuOU7Xw704+h835Lr+6QL9UvYjZE3Ipu6Tp75j7Bh/kR0JKI" crossorigin="anonymous"></script>
```
Listing 10: **footer.html** partial template

&nbsp;

By default, Hugo searches the layouts directory (in this case, **tutorial/layouts/**) for templates. Therefore, Hugo 
generator needs to be informed to load the theme named **custom** by adding `theme = "custom"` into the **config.toml** 
file located at the root of the project (**tutorial/** directory). Setting the base URL[11] of the site, activation of 
the relative URLs, and updating the title of the site is done by editing the **config.toml** file.

```toml
baseURL = "/"
title = "Hugo for beginners"
languageCode = "en-us"
theme = "custom"
relativeURLs = true
``` 
Listing 11: **config.toml** file for this tutorial

&nbsp;

Now executing `hugo new web-development/demo-article.md` at the root of the project creates a new markdown file 
**demo-article.md** in **tutorial/content/web-development/** directory. The content of **demo-article.md** is:

{{< highlight markdown >}}
---
title: "Demo Article"
date: 2020-06-07T15:59:27+02:00
draft: true
---
{{< / highlight >}}
Listing 12: Contents of **demo-article.md**

&nbsp;

The metadata mentioned in *listing 12* is generated automatically from the front matter[12] defined in **default.md** 
file located at **tutorial/archetypes/** path. Setting `draft: false` in **demo-article.md** and starting the server by 
executing `hugo server` renders the site in development mode and the newly created page becomes accessible at 
*localhost:1313/web-development/demo-article/*. But still, adding some content in **demo-article.md** is not being 
rendered in the browser. Updating the **main.html** partial template by replacing `Hello world!` inside 
`<div class="col-md-12"> … </div>` with `{{ .Content }}`, Hugo will start rendering contents from the 
**demo-article.md** file.

```go-html-template
        <div class="container px-6">
            <div class="row">
                <div class="col-md-12">
                    {{ .Content }}
                </div>
            </div>
            <br /><br /><br />
        </div>
```
Listing 13: Version 2 of **main.html** partial template

&nbsp;

Hugo can fetch much site-related information dynamically during the generation of static pages by using many 
built-in and user-defined site-variables[13] and page-variables[14]. Two of the most used variables are:
 
- `.Title`:  represents the title of a page, usually loads the value from the front matter of the markdown file of the 
respective page
- `.Site.Title`: represents the title of the site, value is set in the **config.toml** file located at the root of the 
project

***NOTE:*** The dot-prefix `{{ . }}` refers to the current context.

&nbsp;

The following two listings contain code snippets of the updated version of **head.html** and **header.html** partial 
templates where static contents are replaced by variables (only the modified lines are mentioned).

&nbsp;

```go-html-template
        <title>{{ .Title }}</title>
```
Listing 14: Replacing static page-title with the page-variable in **head.html** partial template

&nbsp;

```go-html-template
                <a href="/" class="navbar-brand">{{ .Site.Title }}</a>
```
Listing 15: Replacing static site-title with the site-variable in **header.html** partial template

&nbsp;
 
##### Template for Listing Pages

A list page[15], having access to all page-variables, makes it easy to render pieces of contents from other regular 
pages in different orders. Hugo looks up for the list page’s template **list.html** in 
**themes/\<THEME\>/layouts/_default/** directory, and for this tutorial in **themes/custom/layouts/_default/** 
directory. The following listing demonstrates an example of a list template.

```go-html-template
<!DOCTYPE html>
<html lang="en">

{{ block "head" . }}{{ end }}

<body>

{{ block "header" . }}{{ end }}
{{ block "main" . }}{{ end }}
{{ partial "footer.html" . }}

</body>
</html>

{{ define "head" }}
{{ partial "head.html" . }}
{{ end }}

{{ define "header" }}
{{ partial "header.html" . }}
{{ end }}

{{ define "main" }}
        <div class="container px-6">
            <div class="row">
                <div class="col-md-12">
                    <ul style="list-style: none;">
                    {{ range .RegularPages }}
                    {{ $pageUrl := replace .Permalink ( printf "%s" .Site.BaseURL) "" }}
                    {{ $pageUrlFull := (printf "/%s" $pageUrl) }}
                        <li><a href="{{ $pageUrlFull }}">{{ .Title }}</a></li>
	     {{ end }}
                    </ul>
                </div>
            </div>
            <br /><br /><br />
        </div>
{{ end }}
```
Listing 16: **list.html** template

&nbsp;

In this example, list pages show all available regular pages of the site. Since in **'Templates for Regular Pages'** 
section, a regular page titled **'Demo Article'** has been created in **web-development/** directory, automatically a 
listing page is generated at *localhost:1313/web-development/* which contains the link and title of the 
**'Demo Article'** page.

&nbsp;

##### Template for Homepage

Homepage is a special type of listing page. It can include all or some of the blocks from the **list.html** template 
defined by the `block` keyword. Hence, creating a basic template for homepage is quite easy as adding codes from 
*listing 17* in **themes/\<THEME\>/layouts/index.html** file.

```go-html-template
<!DOCTYPE html>
<html lang="en">

{{ block "head" . }}{{ end }}

<body>

{{ block "header" . }}{{ end }}

{{ block "mainHome" . }}{{ end }}

{{ partial "footer.html" . }}

</body>
</html>

{{ define "mainHome" }}
        <div class="container px-6">
            <div class="row">
                <div class="col-md-12">
                    Hello from homepage!
                </div>
            </div>
            <br /><br /><br />
        </div>
{{ end }}
```
Listing 17: **index.html** template

&nbsp;

In this example, '`head`' and '`header`' blocks are included from **list.html** template. A new block '`mainHome`' is 
introduced in **index.html** template to implement functions different than the listing pages.

***NOTE:*** If the same block name with different codes are implemented, block on **list.html** template gets 
overwritten by the block of **index.html** template.

&nbsp;

##### Template for 404 Error Page

Like single-page template, 404-page template also inherits from **baseof.html** template. *Listing 18* contains example 
codes of a 404-page template.

```go-html-template
{{ define "head" }}
{{ partial "head.html" . }}
{{ end }}

{{ define "header" }}
{{ partial "header.html" . }}
{{ end }}

{{ define "main" }}
        <div class="container px-6">
            <div class="row">
                <div class="col-md-12">
                    Lost in the space!
                </div>
            </div>
            <br /><br /><br />
        </div>

{{ end }}
```
Listing 18: **404.html** template

&nbsp;
 
### Summary

As the title suggests, this tutorial is mostly for them interested in starting their blog sites or migrating from 
database-driven platforms to static sites using Hugo static site generator. Any reader should be able to build a 
functioning blog following the steps mentioned in this tutorial. Addressing different aspects of the Go templating 
language is not the focus of this article.  If any reader aspires to build a sophisticated platform with Hugo, he or 
she should browse the official website and Github repository of Hugo until the author of this article publishes more 
tutorials for advanced developers.
