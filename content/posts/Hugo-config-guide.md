+++
title = "Hugo Config Guide"
date = "2026-05-01T22:57:12-04:00"
#dateFormat = "2006-01-02" # This value can be configured for per-post date formatting
author = ""
authorTwitter = "" #do not include @
cover = ""
tags = ["", ""]
keywords = ["", ""]
description = ""
showFullContent = false
readingTime = false
hideComments = false
showToc = true
+++


# Hugo Configuration Guide (`hugo.toml`)

A concise reference for the most useful configuration options in Hugo, especially for blog setups and themes like Terminal.

---

## 🧭 Basic Site Configuration

```toml
baseURL = "https://yourusername.github.io/your-repo/"
languageCode = "en-us"
title = "My Blog"
theme = "terminal"
paginate = 5
```

### Options

* `baseURL` → Full URL of your deployed site
* `languageCode` → Default language
* `title` → Site title
* `theme` → Theme name (folder inside `/themes`)
* `paginate` → Number of posts per page

---

## 🧠 Content Behavior

```toml
summaryLength = 30
enableRobotsTXT = true
```

* `summaryLength` → Number of words in summaries
* `enableRobotsTXT` → Auto-generate `robots.txt`

---

## 🗂 URLs & Structure

```toml
[permalinks]
  posts = "/posts/:year/:month/:title/"
```

* Customize how URLs are generated
* Common variables:

  * `:year`
  * `:month`
  * `:title`
  * `:slug`

---

## ✍️ Markdown & Code Highlighting

Check [Hugo doc](https://gohugo.io/configuration/markup/) for more details

```toml
[markup]
  [markup.highlight]
    codeFences = true
    guessSyntax = true
    lineNos = false
    style = "monokai"
    noClasses = false
```

### Highlight options

* `codeFences` → Enable ``` blocks
* `guessSyntax` → Auto-detect language
* `lineNos` → Show line numbers
* `style` → Color theme
* `noClasses` → Inline styles vs CSS classes

---

## 📐 Goldmark (Markdown engine)

```toml
[markup.goldmark.renderer]
  unsafe = true
```

* Allows raw HTML inside Markdown

---

## 🧩 Params (Theme-specific)

```toml
[params]
  contentTypeName = "posts"
  themeColor = "orange"
  showMenuItems = 2
  fullWidthTheme = false
  centerTheme = true
```

⚠️ These depend on the theme. For Terminal:

* `contentTypeName` → Which folder is treated as posts
* `themeColor` → Accent color
* `showMenuItems` → Items in navbar
* `fullWidthTheme` → Stretch layout
* `centerTheme` → Center content

---

## 🌍 Languages & Menus

```toml
[languages]
  [languages.en]
    title = "My Blog"

    [languages.en.menu]

      [[languages.en.menu.main]]
        identifier = "about"
        name = "About"
        url = "/about"

      [[languages.en.menu.main]]
        identifier = "posts"
        name = "Posts"
        url = "/posts"
```

---

## Imaging

Check [Hugo doc](https://gohugo.io/configuration/imaging/)

## 🖼 Static Files

Hugo automatically maps:

```
/static → /
```

Example:

```bash
static/images/test.png
```

Becomes:

```
/images/test.png
```

---

## ⚡ Performance & Build

```toml
[minify]
  disableXML = true

[build]
  writeStats = true
```

* `minify` → Compress output
* `writeStats` → Useful for analyzing assets

---

## 🔍 Taxonomies (Tags & Categories)

```toml
[taxonomies]
  tag = "tags"
  category = "categories"
```

Use in posts:

```yaml
tags: ["physics", "ml"]
```

---

## 📡 Outputs

```toml
[outputs]
  home = ["HTML", "RSS"]
```

* Enable RSS feeds or JSON output

---

## 🧪 Development vs Production

Local preview:

```bash
hugo serve
```

Production build:

```bash
hugo --minify
```

---

## 🧠 Best Practices

* Always set `draft = false` before publishing
* Use **page bundles** for posts with images
* Avoid hardcoding `/your-repo/` in Markdown → use relative paths
* Keep `baseURL` correct for GitHub Pages

---

## 🚀 Example Minimal Config

```toml
baseURL = "https://yourusername.github.io/your-repo/"
languageCode = "en-us"
title = "My Blog"
theme = "terminal"

[markup]
  [markup.highlight]
    codeFences = true
    guessSyntax = true
```

---

## ✨ Advanced (Optional)

```toml
[params]
  customCSS = ["css/custom.css"]
  customJS = ["js/custom.js"]
```

* Add custom styles or scripts

---

## 🧭 Final Note

Hugo’s power comes from:

* Markdown + configuration
* Templates (themes)
* Static asset pipeline

Most behavior is controlled either by:

1. `hugo.toml`
2. Theme `params`
3. Layout overrides

---

Happy writing ✨
