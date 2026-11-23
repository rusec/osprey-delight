# Customizing

Osprey Delight makes heavy use of various Hugo features, e.g. [modules](https://gohugo.io/hugo-modules/). It directly benefits from Hugo's virtual file system and [directory structure](https://gohugo.io/getting-started/directory-structure/), [partials](https://gohugo.io/templates/partials/), as well as using the awesome [Hugo Pipes](https://gohugo.io/hugo-pipes/) whenever it makes sense.

This also means that you normally do not need to maintain a separate fork due to the wide availability of customization options.

## Custom CSS <a href="custom-css"></a>

Place a file named `custom.css` in your `assets/css/` folder (create the directories if needed). It replaces the theme's `custom.css` and is imported last, so its rules win over the theme's.

> The theme's built-in `custom.css` contains useful customization examples, so don't be afraid to copy, override and experiment with it.

Colours, fonts and sizes are CSS variables, so you can change them without touching the theme's rules:

```css
:root {
  --accent-color: #cc0033;
  --primary-bg-color: #ffffff;
}
```

The full list is in `assets/css/themes/<scheme>/colors.css`, `assets/css/themes/color-map-*.css`, `assets/css/themes/<scheme>/fontface.css` and `assets/css/fontsizing.css`.

If your `custom.css` uses `@import`, put it at the very top of the file. CSS ignores an `@import` that comes after a rule.

### Your own fonts

1. Put the font files in your site's `static/fonts/` folder, e.g. `static/fonts/inter/inter-regular.woff2`.
2. Declare the font and point the font variables at it in your `custom.css`:

```css
@font-face {
  font-family: "Inter";
  font-weight: 400;
  font-display: swap;
  src: url("./fonts/inter/inter-regular.woff2") format("woff2");
}

:root {
  --font-body: "Inter", Arial, sans-serif;   /* body text, nav */
  --font-header: "Inter", Georgia, serif;    /* h1–h3, blockquotes */
}
```

The other font variables are `--font-code`, `--font-tagline` (the landing title) and `--nav-font`.

- Use `.woff2` or `.woff` files. Other formats (`.ttf`, `.otf`) fail the build unless you add them to `externals` in `layouts/partials/head.html`.
- `./fonts/…` is relative to the site's stylesheet (`/style.css`), so it points to `static/fonts/…`.
- For Google Fonts instead, put `@import url("https://fonts.googleapis.com/css2?family=…&display=swap");` on the first line of `custom.css`.

### Theming

Get creative and build your own theme for Osprey Delight!
A theme ([example dark theme](./assets/css/themes/dedark)) consists of three optional files in `assets/css/themes/<name>/`:

File                | Purpose                                                            | Recommendation
--------------------|------------------------------------------------------------------- |------------------------
`colors.css`        | Colors (CSS variables)                                             | Use a color scheme generator site (e.g. "coolors") to get some ideas, align with your logo's colors.
`fontface.css`      | Font settings (`@font-face` and font variables)                    | Use [Google fonts](https://fonts.google.com/) for a font that fits. Tools such as [webfont helper](https://gwfh.mranftl.com/fonts) help you with independently self-hosting the font.
`custom.css`        | Any other custom adaptions                                         | Just like the [custom CSS described before](#custom-css), but theme-local instead of global.

Set the theme in your config.yaml, e.g.:

```yaml
Params:
  # ...
  theme: "dedark"
```

### Syntax Highlighting (for Blog)

Limiting external dependencies is important for performance. Therefore, only Hugo's internal [Chroma Syntax Highlighting](https://gohugo.io/content-management/syntax-highlighting/) is supported out of the box. Here's how to use it:

1. Generate a Chromastyle of your choice (in this case `solarized-dark`): `hugo gen chromastyles --style=solarized-dark > solarized.css`
2. Move the file to your `assets/css/` folder and add `@import "solarized.css";` at the top of your `custom.css` (the example site does the same)
3. Add `pygmentsUseClasses: true` to your config.yaml

> Refer to [the official Hugo documentation](https://gohugo.io/content-management/syntax-highlighting/) for more info. 

## Templates

In this section, you can learn how to adjust templates or theme structure to your needs.

### Add your own sections

Adjust the config.yaml file by adding another entry to `menu`, for instance one for music:

```yaml
Menu:
  Main:
  # ...
  - name: "Music"
    identifier: "music"
    url: "/#music"
    weight: 2
```

This will create a section with name "Music" in the nav bar and renders the content of `content/music.md` given by the identifier.

If you need further styling of this section you can place a `music.html` partial in `layouts/partials/sections` (e.g. by using the `default.html` in the same folder as starting point).

The weight determines the position on the page as well as in the nav bar.

### Advanced: Extend the head

In case you want to load custom HTML for additional scripts etc. inside the page's `head`: 
Place a file named `head-extended.html` in your `layouts/partials/` folder (create the directories if needed). 

This file can e.g. contain additional `<script>` or `<link>` tags.

## Module settings

Osprey Delight makes heavy use of [Hugo Mods](https://github.com/hugo-mods) to enrich its functionality. 
In this section, you can learn how to customize the modules.

### [icons](https://github.com/hugo-mods/icons)

To add an icon to the footer (say SoundCloud, [as in this discussion](https://github.com/kdevo/osprey-delight/discussions/19)):

1. Create the file `data/icons.yml` in your project root (see also the [theme-internal `icons.yaml`](./data/icons.yaml))
2. Add the line `soundcloud: fab soundcloud` to it
3. Check out all options for [the pattern](https://github.com/hugo-mods/icons#data-pattern) used by this theme

### [lazyimg](https://github.com/hugo-mods/lazyimg)

Customization options for experts are described in the [README](https://github.com/hugo-mods/lazyimg/blob/main/README.md).