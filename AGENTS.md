# AGENTS.md

## Repository Context

This repository contains the source for `orfeasa.com`, a personal website built with [Hugo](https://gohugo.io/).

- Framework: Hugo (extended build recommended)
- Theme: `hugo-coder` (git submodule at `themes/hugo-coder`)
- Hosting/CI: GitHub Pages (GitHub Actions)

## Project Structure

- `config.toml`: Main Hugo configuration (site params, social links, menu, theme settings).
- `content/`: Markdown content pages and blog posts.
  - `content/about.md`: Main about page.
  - `content/projects.md`: Projects page.
  - `content/posts/`: Blog posts (published and drafts).
- `static/`: Static assets copied directly to output (images, favicon files, fonts, CSS, PDF).
- `archetypes/`: Default template for new content files.
- `themes/hugo-coder/`: Theme source (submodule).
- `.github/workflows/hugo.yml`: Build + deploy workflow for GitHub Pages.

## Local Development

Prerequisites:

- Hugo installed locally (`hugo version`)
- Theme submodule initialized

Setup:

```sh
git submodule update --init --recursive
```

Run dev server:

```sh
hugo server
```

Production-style build:

```sh
hugo --gc --minify
```

Build output is generated in `public/`.

## Content & Publishing Notes

- Posts use front matter in TOML format (`+++` blocks).
- `draft = true` posts are excluded from normal production builds.
- Current menu entries are configured in `config.toml` under `[[menu.main]]`.
- Custom site-level CSS overrides live in `assets/css/style.css`; most styling comes from `hugo-coder`.

## Deployment Notes

GitHub Pages deployment is defined in `.github/workflows/hugo.yml`:

- Trigger: pushes to `main` (and manual `workflow_dispatch`)
- Build command: `hugo --gc --minify --baseURL "${{ steps.pages.outputs.base_url }}/"`
- Hugo version pinned in workflow env (`HUGO_VERSION`)

If local Hugo differs from the workflow version, verify rendering parity before publishing major style or template changes.

## Practical Guidance For Future Agents

- Treat this as a Hugo content/config repository, not a Node/React app.
- Prefer editing content under `content/` and config under `config.toml`.
- Do not modify theme internals unless explicitly requested; prefer overrides in project files.
- Keep the submodule initialized before debugging styling/layout issues.
- When validating changes, run a local Hugo build and check generated routes in `public/`.
