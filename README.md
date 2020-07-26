# Pandoc Website Template

![CI](https://github.com/alxrsngrtn/pandoc-website-template/workflows/CI/badge.svg)

TL;DR: A template to build static websites with [Pandoc](https://pandoc.org/), [Github Actions](http://github.com/actions) & [Github Pages](https://pages.github.com/). 

## Use

`bin/build` walks a source directory, invokes a Pandoc command for each target file, and copies assets to a destination folder.
 
This tool is configurable by environment variables.

| Variable  | Description                                         | Default                                               |
|-----------|-----------------------------------------------------|-------------------------------------------------------|
| `SRC`     | Root directory of input sources.                    | `src/`                                                |
| `DST`     | Root directory for generated output.                | `public/`                                             |
| `STATIC`  | Directory for static assets.                        | `$SRC/static`                                         |
| `SRC_EXT` | Input sources file extension.                       | `md`                                                  |
| `DST_EXT` | Output generation file extension.                   | `html`                                                |
| `HEADER`  | path/to/header.html (`--include-before-body`).      | `$SRC/header.html`                                    |
| `FOOTER`  | path/to/footer.html (`--include-after-body`).       | `$SRC/footer.html`                                    |
| `CSS`     | path/to/style.css embedded in header of a web page. | `css/main.css`                                        |
| `PANOPTS` | Arguments to pass to Pandoc for each input file.    | `--css $CSS --email-obfuscation=javascript --metadata-file=defaults.yml -f markdown_github+yaml_metadata_block -t html5 -B $HEADER -A $FOOTER` |

The defaults of this script are oriented for creating static websites. However, the configuration is general enough to 
support a wide variety of tasks; for instance, generating a CV or a slide deck.

We use Github Actions and Github Pages to automatically update the website on source changes. Should this template 
be used beyond websites, the build script can be tuned setting CI environment variables.

## Thanks to 

- The [contributors of Pandoc](https://github.com/jgm/pandoc/graphs/contributors)
- Will Styler's [inspiration](http://wstyler.ucsd.edu/posts/lmimg/spcv.txt)
- [Pure sh Bible](https://github.com/dylanaraps/pure-sh-bible)
- [12 Factor](https://12factor.net)
