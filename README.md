# Pandoc Website Template

[![pages-deploy](https://github.com/alxmrs/pandoc-website-template/actions/workflows/pages.yml/badge.svg)](https://github.com/alxmrs/pandoc-website-template/actions/workflows/pages.yml)
[![shellcheck](https://github.com/alxmrs/pandoc-website-template/actions/workflows/shellcheck.yml/badge.svg)](https://github.com/alxmrs/pandoc-website-template/actions/workflows/shellcheck.yml)

A template to build static websites with [Pandoc](https://pandoc.org/). 

Demo site: [pandoc.merose.com](https://pandoc.merose.com/).

## Use

### `build`

`bin/build` walks the source directory, invokes Pandoc on each file, and copies assets to a destination folder. It also
gathers all files not named "index.md" into an RSS feed.
 
This tool is configurable by environment variables.

| Variable  | Description                                         | Default                                                                              |
|-----------|-----------------------------------------------------|--------------------------------------------------------------------------------------|
| `SRC`     | Root directory of input sources.                    | `src/`                                                                               |
| `DST`     | Root directory for generated output.                | `public/`                                                                            |
| `ASSETS`  | Directory for static assets, like CSS and images    | `assets/`                                                                            |
| `SRC_EXT` | Input sources file extension.                       | `md`                                                                                 |
| `DST_EXT` | Output generation file extension.                   | `html`                                                                               |
| `HEADER`  | path/to/header.html (`--include-before-body`).      | `template/header.html`                                                               |
| `FOOTER`  | path/to/footer.html (`--include-after-body`).       | `template/footer.html`                                                               |
| `CSS`     | path/to/style.css embedded in header of a web page. | `/assets/css/main.css`                                                               |
| `PANOPTS` | Arguments to pass to Pandoc for each input file.    | `--css $CSS --metadata-file=$ROOT/defaults.yml -B $HEADER -A $FOOTER" -V lang=en-US` |

To make it easier to edit metadata for every page, consider making changes to the `defaults.yml` at the project root.

> Note: Configuring RSS still needs to happen in the `bin/build` file today.

The defaults of this script are oriented for creating static websites. However, the configuration could be molded to 
support a wide variety of tasks; for instance, generating a CV or a slide deck. See [these examples](https://pandoc.org/demos.html) 
for more inspiration.


### `watch`

`bin/watch` will watch the source directory. On any changes, it will invoke the build script.

> Note: if you change files outside of `$SRC` (i.e. in `template/` or `assets/`), you'll need to terminate and 
> re-run this script.

### Deployment

This template will publish the static site to [Github Pages](https://pages.github.com) via [Github Actions](http://github.com/actions).


## Thanks to 

- The [contributors of Pandoc](https://github.com/jgm/pandoc/graphs/contributors)
- Will Styler's [inspiration](http://wstyler.ucsd.edu/posts/lmimg/spcv.txt)
- [Pure sh Bible](https://github.com/dylanaraps/pure-sh-bible)
- [Drew McConville](http://bettermotherfuckingwebsite.com/)
