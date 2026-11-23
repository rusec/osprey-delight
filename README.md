<a href="https://git.io/osprey-delight" target="_blank">
    <img alt="Osprey Delight Logo" src="https://raw.githubusercontent.com/rusec/osprey-delight/master/images/osprey-delight-logo.png" width="250">
</a>

---

[![GitHub Release](https://img.shields.io/github/v/release/rusec/osprey-delight?style=flat-square&color=%230097a7&logo=github)](https://github.com/rusec/osprey-delight/releases/latest)
[![Discussions](https://img.shields.io/badge/GitHub-Discussions-%230097a7?logo=github&style=flat-square)](https://github.com/kdevo/osprey-delight/discussions)
[![Hugo Minimum Version](https://img.shields.io/badge/hugo-%3E=v0.158-%230097a7?logo=hugo&style=flat-square)](https://github.com/gohugoio/hugo/releases)
[![Built with hugo-mods](https://img.shields.io/static/v1?label=%E2%9D%A4&message=hugo-mods&color=0097a7&style=flat-square)](https://github.com/hugo-mods)

## RUSEC fork

This is the [RUSEC](https://github.com/rusec) fork of [kdevo/osprey-delight](https://github.com/kdevo/osprey-delight), forked at [`c2a1781`](https://github.com/kdevo/osprey-delight/commit/c2a1781f205f959ab63ddf37237869ca1354e6d3) (February 2025) and including [PR #64](https://github.com/kdevo/osprey-delight/pull/64) by questoph.

Changes from upstream:
- Builds on Hugo 0.170, which removed libsass and the extended edition.
- Styles are migrated from Sass to plain CSS in `assets/css/` built by Hugo's `css.Build`.
- `hugo-mods/release-notify` is removed because it calls the removed `getJSON` function.
- Fixed various deprecations from newer Hugo versions.
- The module path is `github.com/rusec/osprey-delight/v5`.

Due to Hugo's way of breaking their API regularly [[1]](https://github.com/kdevo/osprey-delight/issues/58) [[2]](https://commaok.xyz/post/on_hugo/) [3](https://news.ycombinator.com/item?id=47618120#47624794), the original theme is no longer developed. Consider [sponsoring the theme developer](https://github.com/sponsors/kdevo).

## Quickstart

> If you're new to Hugo, [visit the docs](https://gohugo.io/getting-started/quick-start/) for an overview of the static site generator.

### Install the development tools

1. Install [Git](https://git-scm.com/downloads).
2. Install [Go](https://go.dev/dl/) 1.27 or newer.

### Develop this theme

3. Clone the repo. You don't need to install Hugo: the `./hugo` wrapper builds the version pinned in `tools/go.mod` on first run.
   ```sh
   git clone https://github.com/rusec/osprey-delight.git
   cd osprey-delight
   ```
4. Run the example site and open http://localhost:1313:
   ```sh
   ./hugo server --source exampleSite
   ```
   To try another colour scheme, prefix the command with `HUGO_PARAMS_THEME=dedark` (or `origin`).
5. Before committing, check for `ERROR` or `deprecated` lines:
   ```sh
   ./hugo --source exampleSite --logLevel info
   ```

### Use the theme in your site

3. Install [Hugo](https://gohugo.io/installation/) standard version 0.158 or newer.
4. Create the site and make it a module (replace `<username>/<projectname>` with your GitHub repo):
   ```sh
   hugo new site my-site
   cd my-site
   hugo mod init github.com/<username>/<projectname>
   ```
5. Optional: pin the Hugo version for everyone working on the site. This adds a `tools/go.mod` and a `./hugo` wrapper that builds that exact version on first run:
   ```sh
   mkdir tools && cd tools
   go mod init github.com/<username>/<projectname>/tools
   go get -tool github.com/gohugoio/hugo@vX.Y.Z
   cd ..
   curl -O https://raw.githubusercontent.com/rusec/osprey-delight/master/hugo
   chmod +x hugo
   ```
   From here on, use `./hugo` instead of `hugo`.
6. Replace the generated `hugo.toml` with the [example config](https://github.com/rusec/osprey-delight/blob/master/exampleSite/config.yaml):
   ```sh
   rm hugo.toml
   curl -O https://raw.githubusercontent.com/rusec/osprey-delight/master/exampleSite/config.yaml
   ```
7. In `config.yaml`, delete the two `replacements:` lines under `module:`. They only work inside this repo.
8. Download the theme and start the site, then open http://localhost:1313:
   ```sh
   hugo mod get
   hugo server
   ```

To update the theme later, run `hugo mod get -u github.com/rusec/osprey-delight/v5` and commit `go.mod` and `go.sum`.

## Overview

Osprey Delight is the free-minded artist's choice for a clutter-free and blazingly fast single-page portfolio.

> It originates from [the great Osprey theme](https://github.com/tomanistor/osprey) by [Toma Nistor](https://github.com/tomanistor) and adds new optimizations and features to your **delight**.

### Features

- Modular and made out of extensible section building blocks:
  - About: Introduce yourself
  - Gallery: Show your work using a grid-based gallery with interactive modal boxes
  - Blog: Lightweight blog features
  - Contact: Contact form with Basin support and built-in spambot protection
- Use your high-quality images [assets](https://gohugo.io/categories/asset-management):
  - Lazy image loading plus completely automatic resizing using [lazyimg](https://github.com/hugo-mods/lazyimg) module
  - Blur-up technique using automatic low-quality image placeholders (LQIP)
  - Modern WebP support with fallback for older browsers
- SEO:
  - [Score 100 at PageSpeed Insights](https://developers.google.com/speed/pagespeed/insights/?url=https%3A%2F%2Fkdevo.github.io%2F). Every bit is fine-tuned with performance in mind!
  - Auto-generated structures ensure that everyone finds you
- Delightful UX:
  - Choose between different themes
  - Awesome social icons in footer via [icons module](https://github.com/hugo-mods/icons)
  - Smooth scrolling plus scroll-spy
  - Automatically fetches GitHub repo data
  - Sane fallbacks for No-Script/No-JS users
- Heavily [customizable](#customize-it) - no need to maintain a fork!

In general, many [open issues](https://github.com/tomanistor/osprey/issues) of the original theme have been resolved and its code has been rewritten.

## Configuration and Usage <a href="config"></a>

It's best if you simply check out the fully commented [config file](https://github.com/rusec/osprey-delight/blob/master/exampleSite/config.yaml).
This theme follows a learning-by-doing approach.

### Images

This theme is asset-driven! It "knows" how to handle your precious assets, and there usually is no need for manual resizing.
For that to work, provide all of the following images in the [`assets` directory](https://gohugo.io/hugo-pipes/introduction/#asset-directory) (do not use the `static` directory).

The following table shows recommendations regarding the required assets:

| Image Type  | Config Key                   | Minimum Width | Note                                                                                |
| ----------- | ---------------------------- | ------------- | ----------------------------------------------------------------------------------- |
| Logo        | `logoBig` (config.yaml)      | 200px         | Transparent, minimum margin top/bottom                                              |
| Navbar-Logo | `logoSmall` (config.yaml)    | 96px          | Transparent, small margin top/bottom, prefer square format                          |
| Gallery     | `image` (content/gallery/\*) | 400px         | Transparent, medium margin top/bottom/left/right, prefer square or landscape format |
| Background  | `background` (config.yaml)   | 1920px        | Optional, use a high-quality JPG                                                    |

### Content files

#### About section

To create an about section that renders on the home page, run:

```console
hugo new about.md
```

#### Gallery item

To create a new gallery item, run:

```console
hugo new gallery/my-item.md
```

You will get a fully documented file, which describes each config option separately.

### Contact form

Basin is a free AJAX contact form service that is used by this theme.

To set it up:

1. [Sign up for a free account](https://usebasin.com/users/sign_up) and create a form.
2. Copy and paste your form's URL endpoint to the `ajaxBasin` config.yaml parameter.
3. Select the `Submit this form via AJAX` option on your Basin dashboard.

![Basin AJAX setup](https://raw.githubusercontent.com/rusec/osprey-delight/master/images/basin-ajax-setup.png)

#### Enable spambot protection

Under "Setup" → "Set a Custom Honeypot Field", input `_anti_spam_honeypot`.
Basin will [ignore all messages that contain this specific field](https://usebasin.com/docs/features/spam-filtering). This should work since there is a hidden field that users normally do not use, but spambots will blindly input their data.

![Basin Anti Spambot](https://raw.githubusercontent.com/rusec/osprey-delight/master/images/basin-custom-honeypot.png)

[Please do not make a tick in the "reCAPTCHA" checkbox](https://github.com/kdevo/osprey-delight/discussions/22), this service is not supported and also typically not necessary.

## Learn more

### Customize it <a href="customize-it"></a>

Want to have full control over appearance? Check out [how to customize the theme more granularly](https://github.com/rusec/osprey-delight/blob/master/CUSTOMIZING.md).

### Need help?

The theme has a GitHub-powered [community forum](https://github.com/kdevo/osprey-delight/discussions) and [Q&A](https://github.com/kdevo/osprey-delight/discussions/categories/q-a).

### Contributing

Read [how to contribute](https://github.com/rusec/osprey-delight/blob/master/CONTRIBUTING.md)!