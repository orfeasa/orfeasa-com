# orfeasa-com

Source for [orfeasa.com](https://orfeasa.com/), a personal website built with [Hugo](https://gohugo.io/) and based on the [hugo-coder](https://github.com/luizdepra/hugo-coder/) theme.

## Stack

- Framework: Hugo (extended build recommended)
- Theme: `themes/hugo-coder` (git submodule)
- Hosting: GitHub Pages via GitHub Actions

## Project Structure

- `config.toml`: Main site configuration.
- `content/`: Markdown pages and posts.
- `assets/`: Hugo Pipes assets such as custom CSS.
- `static/`: Static files copied directly to the generated site.
- `layouts/`: Local template overrides.
- `themes/hugo-coder/`: Theme source.
- `.github/workflows/hugo.yml`: GitHub Pages build and deploy workflow.

## Local Development

Initialize the theme submodule:

```sh
git submodule update --init --recursive
```

Run the dev server:

```sh
hugo server
```

Run a production-style build:

```sh
hugo --gc --minify
```

The generated site is written to `public/`.

## Content Notes

- Posts use TOML front matter with `+++`.
- Draft posts are excluded from normal production builds.
- Menu entries are configured in `config.toml` under `[[menu.main]]`.
- Custom CSS lives in `assets/css/style.css`.
- Footer visibility is controlled by `hidefooter` in `config.toml`, with behavior implemented in `layouts/partials/footer.html`.

## Deployment

GitHub Pages deployment is defined in `.github/workflows/hugo.yml`.

- Trigger: pushes to `main` and manual `workflow_dispatch`
- Build command: `hugo --gc --minify --baseURL "${{ steps.pages.outputs.base_url }}/"`
- Hugo version is pinned in the workflow via `HUGO_VERSION`

If local Hugo differs from the workflow version, verify rendering parity before publishing major style or template changes.

## License

This software is licensed under the MIT license. For more information, read the [LICENSE](LICENSE) file.
