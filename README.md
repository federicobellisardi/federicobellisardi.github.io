# federicobellisardi.github.io

Source of my personal academic website — <https://federicobellisardi.github.io>.

Built with [Jekyll][jekyllrb] and the [Chirpy][chirpy] theme (vendored into this
repository), deployed to GitHub Pages by the
[Build and Deploy](.github/workflows/pages-deploy.yml) workflow on every push to
`master`.

## Where things live

| Path                     | What it holds                                                       |
| ------------------------ | ------------------------------------------------------------------- |
| `_tabs/`                 | The site pages. Each file becomes a sidebar entry (see note below).  |
| `_tabs/about.md`         | The home page (`permalink: /`) — bio, research interests, teasers.   |
| `_posts/`                | Blog posts, named `YYYY-MM-DD-title.md`.                             |
| `_data/publications.yml` | Publication list — the single source for the home and Publications.  |
| `_data/profiles.yml`     | External profile links shown on the home and Contacts pages.         |
| `_data/contact.yml`      | The small icon row at the top of the sidebar.                        |
| `assets/files/`          | Downloadable files, including the CV.                                |
| `assets/img/`            | Images, avatar, and favicons.                                        |
| `assets/css/jekyll-theme-chirpy.scss` | Custom styles layered on top of the theme.              |

The sidebar navigation is generated from the `tabs` **collection** (the files in
`_tabs/`), which shadows any top-level `tabs:` key in `_config.yml`. To add a
page, add a file to `_tabs/` with `title`, `icon` and `order` in its front
matter.

## Routine updates

- **New publication** — add an entry to `_data/publications.yml`. It shows up on
  both the home page and `/publications/` automatically, with a resolvable DOI
  link and a "Cite" BibTeX snippet generated from the same data.
- **New post** — add `_posts/YYYY-MM-DD-slug.md` with `title`, `description`,
  `author: fbellisardi`, `date`, `categories` and `tags`. The three most recent
  posts are teased on the home page.
- **New CV** — drop the PDF in `assets/files/` and point `cv_path` in
  `_config.yml` at it.
- **New profile link** — add it to `_data/profiles.yml` (`home: true` also puts
  it in the home page hero).

## Analytics and comments

Both are wired up but inactive until you supply an account:

- **Analytics** — `_config.yml`'s `analytics.goatcounter.id`. Sign up free at
  <https://www.goatcounter.com/signup>, paste the code you pick, done. No
  cookie banner needed (GoatCounter doesn't track individuals).
- **Comments** — `_config.yml`'s `comments:` block, provider `giscus`
  (comments become GitHub Discussions on this repo, no third party involved).
  Enable "Discussions" in the repo settings, install the
  [giscus app](https://github.com/apps/giscus), then get the four `giscus.*`
  values from <https://giscus.app>. Leaving `provider:` empty (the default)
  keeps comments off.

Every other provider in those two blocks (Google Analytics, Disqus, Matomo,
...) works the same way — fill in its id/keys and set it as the provider.

## Self-hosted assets

`assets.self_host.enabled: true` in `_config.yml` serves fonts, Font Awesome,
Bootstrap, etc. from this domain (via the `assets/lib` submodule) instead of
Google Fonts / jsDelivr. The deploy workflow checks out that submodule
(`submodules: true`); if you clone locally, run
`git submodule update --init` first or `bundle exec jekyll build` will 404 on
those assets.

## Running locally

Requires Ruby 3.3+ and Bundler.

```console
$ bundle install
$ bundle exec jekyll serve
```

The site is then served at <http://127.0.0.1:4000>.

To rebuild the theme's JS/CSS bundles (only needed when editing `_javascript/`
or `_sass/`), install the Node dependencies and run the build:

```console
$ npm install
$ npm run build
```

## Checks

The deploy workflow runs [html-proofer][htmlproofer] against the built site and
fails the build on broken internal links. To reproduce it locally:

```console
$ JEKYLL_ENV=production bundle exec jekyll build
$ bundle exec htmlproofer _site --disable-external --allow-hash-href
```

## License

The site content is © Federico Bellisardi. The underlying Chirpy theme is
published under the [MIT License](LICENSE) by Cotes Chung.

[jekyllrb]: https://jekyllrb.com/
[chirpy]: https://github.com/cotes2020/jekyll-theme-chirpy
[htmlproofer]: https://github.com/gjtorikian/html-proofer
