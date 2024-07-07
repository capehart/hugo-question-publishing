+++
title = 'About'
date = 2024-07-06T10:00:35-04:00
draft = false
+++
# About

I think this page should be published:
* The `site` and the `theme` are minimally changed from the `skeleton`
* The page is at the top level of `content/`
* The page is standard markdown
* The theme has a template defined at `layouts/_default/single.html`.
* The `layouts/_default/single.html` page includes a `{{ .Content }}` section
* The [docs](https://gohugo.io/templates/lookup-order/#target-a-template) indicate that files in the root content directory have a `page` _content type_, and imply that they should be rendered with a `single.html` template.
* I would expect the **theme**'s `layouts/_default/single.html` to to take effect, but the page does not get published even with an explicit `layouts/page/single.html` in the **site**. 
* The page does not publish whether it has the default `single.html` from the skeleton or a simplified one [as referenced here](https://gohugo.io/templates/single/)

I assume this is something like an FAQ, but I [checked the FAQ](https://gohugo.io/troubleshooting/faq/#why-is-a-given-page-not-published) and I confirmed that:
* `draft` is set to `false`
* the `date` is in the **past**
* there is no `publishDate`
* there is no `expiryDate`

Just to be sure, I've launched `hugo server` with flags that should ensure a build anyway.

```
rm -rf public
hugo server --disableFastRender --logLevel debug --verbose --buildDrafts --buildFuture --buildExpired --watch
```

When `hugo server` starts, there are no `WARN` or `ERROR` messages displayed in the console.

The output from starting the server is:
```
❯ hugo server --disableFastRender --logLevel debug --verbose --buildDrafts --buildFuture --buildExpired --watch
Watching for changes in /Users/capehart/tmp/problem-example/{archetypes,assets,content,data,i18n,layouts,static,themes}
Watching for config changes in /Users/capehart/tmp/problem-example/hugo.toml
Start building sites …
hugo v0.128.2+extended darwin/amd64 BuildDate=2024-07-04T08:13:25Z VendorInfo=brew

INFO  static: syncing static files to / duration 2.698186ms
INFO  build:  step process substep collect files 8 files_total 8 pages_total 1 resources_total 7 duration 6.33605ms
INFO  build:  step process duration 8.361172ms
INFO  build:  step assemble duration 3.510017ms
INFO  build:  step render substep pages site en outputFormat html duration 40.292779ms
INFO  build:  step render substep pages site en outputFormat rss duration 1.312885ms
INFO  build:  step render pages 7 content 3 duration 42.019626ms
INFO  build:  step render deferred count 0 duration 5.025µs
INFO  build:  step postProcess duration 9.045µs
INFO  build:  duration 54.642743ms

                   | EN
-------------------+-----
  Pages            | 13
  Paginator pages  |  0
  Non-page files   |  1
  Static files     |  1
  Processed images |  0
  Aliases          |  0
  Cleaned          |  0

Built in 56 ms
Environment: "development"
Serving pages from disk
Web Server is available at http://localhost:1313/ (bind address 127.0.0.1)
Press Ctrl+C to stop
```

# Hugo site structure (without `public` or `theme`)
```
.
├── archetypes
│   └── default.md
├── assets
├── content
│   ├── about.md
│   └── index.md
├── data
├── hugo.toml
├── i18n
├── layouts
│   └── page
│       └── single.html
├── public  (see `public` section below)
├── static
└── themes
    └── santa
    (see `theme` section below)
```


# Hugo theme structure
```
.
├── LICENSE
├── README.md
├── archetypes
│   └── default.md
├── assets
│   ├── css
│   │   └── main.css
│   └── js
│       └── main.js
├── content
│   ├── _index.md
│   └── posts
│       ├── _index.md
│       ├── post-1.md
│       ├── post-2.md
│       └── post-3
│           ├── bryce-canyon.jpg
│           └── index.md
├── layouts
│   ├── _default
│   │   ├── baseof.html
│   │   ├── home.html
│   │   ├── list.html
│   │   └── single.html
│   └── partials
│       ├── footer.html
│       ├── head
│       │   ├── css.html
│       │   └── js.html
│       ├── head.html
│       ├── header.html
│       ├── menu.html
│       ├── show-template.html
│       └── terms.html
├── static
│   └── favicon.ico
└── theme.toml
```

# Hugo `public` structure

```
.
├── categories
│   ├── index.html
│   └── index.xml
├── css
│   └── main.css
├── favicon.ico
├── index.html
├── index.xml
├── js
│   └── main.js
├── posts
│   └── post-3
│       └── bryce-canyon.jpg
├── sitemap.xml
└── tags
    ├── index.html
    └── index.xml

7 directories, 11 files
```

# Hugo Env for help debugging:
```
❯ hugo env
hugo v0.128.2+extended darwin/amd64 BuildDate=2024-07-04T08:13:25Z VendorInfo=brew
GOOS="darwin"
GOARCH="amd64"
GOVERSION="go1.22.5"
github.com/sass/libsass="3.6.5"
github.com/webmproject/libwebp="v1.3.2"
github.com/sass/dart-sass/protocol="2.7.1"
github.com/sass/dart-sass/compiler="1.77.6"
github.com/sass/dart-sass/implementation="1.77.6"
```

# Repositories for reproducing the issue

## Site
* https://github.com/capehart/hugo-question-publishing

## Theme
* https://github.com/capehart/hugo-santa-theme
