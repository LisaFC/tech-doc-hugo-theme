
---
title: "Docsy User Guide"
linkTitle: "Docsy"
weight: 2
date: 2018-07-30
description: >
  This page page describes how to use this theme: How to install it, how to configure it, and the different components it contains.
---

## Getting Started

You need a [recent version](https://github.com/gohugoio/hugo/releases) of Hugo to run this project (if you install from the release page, make sure to get the `extended` Hugo version). Can be isntalled via Brew if you're running MacOs.

```bash
cd <your-hugo-project>/themes
git submodule add TODO(bep) 
git submodule update --init --recursive
```

If you want to do stylesheet changes, you will also need `PostCSS` to create the final assets. Navigate to the theme and run `npm install`.

You can also install these tools globally on your computer:

```bash
npm install -g postcss-cli
npm install -g autoprefixer
```

For Hugo documentation, see [gohugo.io](https://gohugo.io/)

## Site Configuration

See the examples with comments in `config.toml` in this project for how to add community links, configure Google Analytics etc.

## Change the Look

### Color variables etc.

SCSS variable project overrides can be added to `assets/scss/_variables_project.scss`. A simple example changing the primary and secondary color to two shades of purple:

```scss
$primary: #390040;
$secondary: #A23B72;
```

There are lots of variables you can set:

* See `assets/scss/_variables.scss` in the theme for color variables etc. that can be set to change the look and feel.
* Also see available variables in Bootstrap 4: https://getbootstrap.com/docs/4.0/getting-started/theming/ and https://github.com/twbs/bootstrap/blob/v4-dev/scss/_variables.scss

Some variables worth mentioning are:

```scss
$enable-gradients: true;
$enable-rounded: true;
$enable-shadows: true;
```

{{% alert title="Tip" %}}
PostCSS (autoprefixing of CSS browser-prefixes) is not enabled when running in server mode (it is a little slow), so Chrome is the recommended choice for development.
{{% /alert %}}

Also note that any SCSS import will try the project before the theme, so you can -- as one example -- create your own `_assets/scss/_content.scss` and get full control over how your Markdown content is styled.

### Font

The theme uses [Open Sans](https://fonts.google.com/specimen/Open+Sans) as its primary font. To disable Google Fonts and use a system font, set this SCSS variable:

```scss
$td-enable-google-fonts: false;
```

To configure another Google Font:

```scss
$google_font_name: "Open Sans";
$google_font_family: "Open+Sans:300,300i,400,400i,700,700i";
```

## Custom Shortcodes

### Shortcode Blocks

The theme comes with a set of custom  **Page Blocks** as [Hugo Shortcodes](https://gohugo.io/content-management/shortcodes/) that can be used to compose landing pages, about pages and similar.

These blocks share some common parameters:

height
: A pre-defined height of the block container. One of `min`, `med`, `max`, `full`, or `auto`. Setting it to `full` will fill the Viewport Height, which can be useful for landing pages.

color
: The block will be assigned a color from the theme palette if not provided, but you can set your own if needed. You can use all of Bootstrap's color names, theme color names or a grayscale shade. Some examples would be `primary`, `white`, `dark`, `warning`, `light`, `success`, `300`, `blue`, `orange`. This will become the **bakground color** of the block, but text colors will adapt to get proper contrast.

#### blocks/cover

The **blocks/cover** shortcode is meant to create a landing page type of block that fills the top of the page.

```go-html-template
{{</* blocks/cover title="Welcome!" image_anchor="center" height="full" color="primary" */>}}
<div class="mx-auto">
	<a class="btn btn-lg btn-primary mr-3 mb-4" href="{{</* absurl "docs/" */>}}">
		Learn More <i class="fas fa-arrow-alt-circle-right ml-2"></i>
	</a>
	<a class="btn btn-lg btn-secondary mr-3 mb-4" href="https://example.org">
		Download <i class="fab fa-github ml-2 "></i>
	</a>
	<p class="lead mt-5">This program is now available in <a href="#">AppStore!</a></p>
	<div class="mx-auto mt-5">
		{{</* blocks/link-down color="info" */>}}
	</div>
</div>
{{</* /blocks/cover */>}}
```

Note that the relevant shortcode parameters above will have sensible defaults, but is included here for completeness.

{{% alert title="Hugo Tip" %}}
> Using the bracket styled shortcode delimiter, `>}}`, tells Hugo that the inner content is HTML/plain text and needs no further processing. Changing it to `%}}` will treat it as Markdown. These can be mixed.
{{% /alert %}}

Parameters:

title
: The main display title for the block.

image_anchor
: The anchor used when cropping the background picture. Default is **center**. See the [Hugo Docs](https://gohugo.io/content-management/image-processing/#readout)

height
: See above.

color
: See above.


To set the background image, place an image with the word "background" in the name inside the [Page Bundle](https://gohugo.io/content-management/page-bundles/).


{{% alert title="Tip" %}}
If you also include the word **featured** in the image name, e.g. `my-featured-background.jpg`, it will also be used as the Twitter Card image when shared.
{{% /alert %}}


For available icons, see [Font Awesome](https://fontawesome.com/icons?d=gallery&m=free).

#### blocks/lead

The **blocks/lead** block shortcode is a simple lead/title block with centered text and a arrow down pointing to the next section.

```go-html-template
{{%/* blocks/lead color="dark" */%}}
TechOS is the OS of the future. 

Runs on **bare metal** in the **cloud**!
{{%/* /blocks/lead */%}}
```

Parameters:

height
: See above.

color
: See above.

#### blocks/section

The **section** shortcode is meant as a general-purpose content container. The example below shows it wrapping 3 feature sections.


```go-html-template
{{</* blocks/section color="dark" */>}}
{{%/* blocks/feature icon="fa-lightbulb" title="Fastest OS **on the planet**!" */%}}
The new **TechOS** operating system is an open source project. It is a new project, but with grand ambitions.
Please follow this space for updates!
{{%/* /blocks/feature */%}}
{{%/* blocks/feature icon="fab fa-github" title="Contributions welcome!" url="https://github.com/gohugoio/hugo" */%}}
We do a [Pull Request](https://github.com/gohugoio/hugo/pulls) contributions workflow on **GitHub**. New users are always welcome!
{{%/* /blocks/feature */%}}
{{%/* blocks/feature icon="fab fa-twitter" title="Follow us on Twitter!" url="https://twitter.com/GoHugoIO" */%}}
For announcement of latest features etc.
{{%/* /blocks/feature */%}}
{{</* /blocks/section */>}}
```

Parameters:

height
: See above.

color
: See above.


#### blocks/feature

```go-html-template

{{%/* blocks/feature icon="fab fa-github" title="Contributions welcome!" url="https://github.com/gohugoio/hugo" */%}}
We do a [Pull Request](https://github.com/gohugoio/hugo/pulls) contributions workflow on **GitHub**. New users are always welcome!
{{%/* /blocks/feature */%}}

```

Parameters

title
: The title to use.

url
: The URL to link to.

icon
: The icon class to use.

### Shortcode Helpers


## i18n

All UI strings (text for buttons etc.) are bundled inside `/i18n` in the theme. Translations (e.g. create a copy of `en.toml` to `jp.toml`) should be done in the theme, so it can be reused by others. Additional strings or overridden values, can be added to the project's `/i18n` folder.



{{% alert title="Hugo Tip" %}}
Run `hugo server --i18n-warnings` when doing translation work, as it will give you warnings on what strings are missing.
{{% /alert %}}

For `content`, each language can have its own language configuration and configured each its own content root, e.g. `content/en`. See the [Hugo Docs](https://gohugo.io/content-management/multilingual) on this for more information.

## Add your own logo

Add it to `assets/icons/logo.svg` in your project.

## Add your own favicons

The easiest is to create a set of favicons via http://cthedot.de/icongen and put them inside `static/favicons` in your Hugo project.

If you have special requirements, you can create your own `layouts/partials/favicons.html` with your links.

## Configure Search

1. Add you Google Custom Search Engine ID to the site params in `config.toml`. You can add different values per language if needed.
2. Add a content file in `content/en/search.md` (and one per other language if needed). It only needs a title and `layout: search.


## Customize Templates

### Add code to head or before body end

If you need to add some code (CSS import or similar) to the `head` section on every page, add a partial to your project:

```
layouts/partials/hooks/head-end.html
```

And add the code you need in that file.

Similar, if you want to add some code right before the `body` end:

```
layouts/partials/hooks/body-end.html
```
