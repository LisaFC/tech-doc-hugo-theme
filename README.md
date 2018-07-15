# Tech Doc Hugo

Hugo theme and skeleton project.

## Getting Started

You need a [recent version](https://github.com/gohugoio/hugo/releases) of Hugo to run this project (if you install from the release page, make sure to get the `extended` Hugo version). Can be isntalled via Brew if you're running MacOs.

```bash
git clone --recurse-submodules --depth 1 https://github.com/bep/tech-doc-hugo.git
cd tech-doc-hugo
hugo server
```

If you want to do stylesheet changes, you will also need `PostCSS` to create the final assets. This installs the needed tools globally on your PC:

```
npm install -g postcss-cli
npm install -g autoprefixer
```

In Hugo 0.45, you can also install it locally in the project with:

```
npm install
````

## Customize your site

For Hugo documentation, see [gohugo.io](https://gohugo.io/)

### Site Configuration

See the examples with comments in `config.toml` in this project for how to add community links, configure Google Analytics etc.

### Tweak the Look and Feel

SCSS variable project overrides can be added to `assets/scss/_variables_project.scss`.

* See `assets/scss/_variables.scss` in the theme for color variables etc. that can be set to change the look and feel.
* Also see available variables in Bootstrap 4: https://getbootstrap.com/docs/4.0/getting-started/theming/

> TIP: PostCSS (autoprefixing of CSS browser-prefixes) is not enabled when running in server mode (it is a little slow), so Chrome is the recomended choice for development.

### Set up Search

1. Add you Google Custom Search Engine ID to the site params in `config.toml`. You can add different values per language if needed.
2. Add a content file in `content/en/search.md` (and one per other language if needed). It only needs a title.


### Shortcode Blocks


### i18n

All UI strings (text for buttons etc.) are bundled inside `/i18n` in the theme. Translations (e.g. create a copy of `en.toml` to `jp.toml`) should be done in theme, so it can be reused by others. Additional strings or overridden values, can be added to the project's `/i18n` folder.

> Hugo tip: Run ` hugo server --i18n-warnings` when doing translation work, as it will give you warnings on what strings are missing.

For `content`, each language can have its own language configuration and configured each its own content root, e.g. `content/en`. See the [Hugo Docs](https://gohugo.io/content-management/multilingual) on this for more information.


### Add your own favicons

The easiest is to create a set of favicons via http://cthedot.de/icongen and put them inside `static/favicons` in your Hugo project.

If you have special requirements, you can create your own `layouts/partials/favicons.html` with your links.

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



