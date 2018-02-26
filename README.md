# Metalsmith webpack boilerplate

This project is built on [metalsmith.io]

## Necessary infrastructure

* **Database:** No database needed
* **PHP:** No php needed
* **Yarn modules:** Have a look into [package.json]

## Project setup

```bash
git clone ssh://git@git.uebb.de:12022/m.bachl/rderelaunch.git
yarn
```

## Common commands

| Command | Action |
| --- | --- |
| `yarn` | Installs dependencies |
| `yarn dev` | Run dev server including BrowserSync |
| `yarn server` | Run simple production server |
| `yarn build` | Build project |
| `yarn build:webpack` | Only build assets |
| `yarn build:prod` | Build production version |
| `yarn lint` | Checks for syntax errors in css and js |

## Directory structure

```bash
├─┬─ assets/ # Source files, will be processed by webpack
│ ├─┬─ favicons/ # Put your favicon.png in here
│ │ └─── favicon.png
│ ├─┬─ js/ # Your custom javascripts
│ │ ├─── app.js # Main scripts file 
│ │ └─── immediate.js
│ └─┬─ scss/ # Your custom scss definitions
│   └─── app.scss
├─┬─ content/ # Site's pages here. Files need to be called index.njk
│ ├─┬─ de/ # German pagetree
│ │ ├─┬─ subpage-01/
│ │ │ ├─┬─ subpage-01-01/
│ │ │ │ └─── index.njk
│ │ │ └─── index.njk
│ │ ├─┬─ subpage-02/
│ │ │ ├─┬─ subpage-02-01/
│ │ │ │ └─── index.njk
│ │ │ └─── index.njk
│ │ └─── index.njk
│ └─┬─ en/ # English pagetree
│   ├─┬─ subpage-01/
│   │ ├─┬─ subpage-01-01/
│   │ │ └─── index.njk
│   │ └─── index.njk
│   ├─┬─ subpage-02/
│   │ ├─┬─ subpage-02-01/
│   │ │ └─── index.njk
│   │ └─── index.njk
│   └─── index.njk
├─┬─ src/ # Source files which metalsmith uses to build our site
│ ├─── assets/ # will be automatically filled by webpack on build, don't touch those contents
│ ├─┬─ config/ # Metalsmith configuration
│ │ ├─── favicons.js
│ │ ├─── filters.js
│ │ ├─── navigations.js
│ │ ├─── paths.js
│ │ └─── sitemeta.js
│ └─┬─ layouts/ # Template files
│   ├─┬─ macros/ # Template partials (macros)
│   │ ├─── head.njk
│   │ ├─── layout.njk
│   │ └─── navigations.njk
│   └─── default.njk # Default template
└─── web/ # Just deploy the contents of this directory (containd metalsmith-generated content)
```

## Redirects

To add redirects for pages, just edit the `alias:` section in the desired index.njk and add the needed paths.

## Navigations

New pages must be assigned to the desired navigations manually. To assign them, add the corresponding navigation name to the `navGroup`-Array like this:

```bash
navGroup: [ primary, footer ]
```

### Navigations currently available:

* Main navigation (Key: `header`)
* Header meta navigation (Key: `headerMeta`)
* Footer navigation (Key: `footer`)
* Footer meta navigation (Key: `footerMeta`)

## Favicon

This boilerplate includes an automatic favicon generator (Plugin: [metalsmith-favicons]). To get it working, you just need to place the desired image as `favicon.png` into `/assets/favicons`.

**Hint:** The current version of the plugin seems to have some issues. When trying to activate the options `android`, `firefox` or `windows` in `/src/config/favicons.js`, the builder will crash with an error!

## Publishing pages

This boilerplate also includes the functionality to create pages without publishing them instantly. You can set the publishing status by setting the option `publish` in the pages metadata. These options are available for publishing pages:

* `publish: draft`  
Saves the page as a draft without publishing it.
* `publish: private`  
Needs to be tested what this does.
* `publish: unlisted`  
Removes the `collection` metadata, useful for publishing internally wihtout adding it to your posts lists or RSS feeds.
* `publish: 2021-12-21`  
Sets the date on which the page will be published. Needs rebuild of site (e.g. daily build cronjob).

## Useful docs

### Used Metalsmith plugins

* [metalsmith-assets]
* [metalsmith-multi-language]
* [metalsmith-fingerprint-ignore]
* [metalsmith-favicons]
* [metalsmith-collections]
* [metalsmith-publish]
* [metalsmith-permalinks]
* [metalsmith-navigation]
* [metalsmith-markdown]
* [metalsmith-in-place]

### Templating (Nunjucks)

* [Nunjucks Templating]

## Based on

* [axe312ger/metalsmith-webpack-suite]

[metalsmith.io]: https://www.metalsmith.io
[package.json]: package.json
[metalsmith-assets]: https://github.com/treygriffith/metalsmith-assets
[metalsmith-multi-language]: https://github.com/doup/metalsmith-multi-language
[metalsmith-fingerprint-ignore]: https://github.com/npm-graveyard/metalsmith-fingerprint-ignore
[metalsmith-favicons]: https://github.com/arccoza/metalsmith-favicons
[metalsmith-collections]: https://github.com/segmentio/metalsmith-collections
[metalsmith-publish]: https://github.com/mikestopcontinues/metalsmith-publish
[metalsmith-permalinks]: https://github.com/segmentio/metalsmith-permalinks
[metalsmith-navigation]: https://github.com/unstoppablecarl/metalsmith-navigation
[metalsmith-markdown]: https://github.com/segmentio/metalsmith-markdown
[metalsmith-in-place]: https://github.com/ismay/metalsmith-in-place
[Nunjucks Templating]: https://mozilla.github.io/nunjucks/templating.html
[Metalsmith Slack channel]: https://metalsmith-slack.herokuapp.com/
[axe312ger/metalsmith-webpack-suite]: https://github.com/axe312ger/metalsmith-webpack-suite