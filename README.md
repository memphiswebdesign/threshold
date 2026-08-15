# Threshold Hospitality Group

Jekyll + Liquid site, styled with Tailwind CSS v4, deployed on Netlify.

## Stack

| Piece | Choice |
| --- | --- |
| Static site generator | Jekyll 4.4 (Liquid templating) |
| CSS | Tailwind CSS v4 (CSS-first config, no `tailwind.config.js`) |
| Typeface | Manrope (Google Fonts) |
| Host | Netlify, building from `main` |

## Local setup

Requires Ruby 3.2.2 (see `.ruby-version`) and Node 20 (see `.nvmrc`).

```bash
bundle install
npm install
```

## Development

```bash
npm run dev
```

Runs the Tailwind watcher and `jekyll serve --livereload` together on
http://localhost:4000. Edit any `.html`, `.md`, or `_src/main.css` and the page
reloads.

## Production build

```bash
npm run build
```

Compiles Tailwind to `assets/css/main.css`, then builds Jekyll into `_site/`.
This is the exact command Netlify runs.

## How the two build steps fit together

Tailwind is a Node tool and Jekyll is a Ruby tool, so the build has two stages.
Netlify sees the `Gemfile` and runs `bundle install` on its own, sees
`package.json` and runs `npm install`, then runs `npm run build`, which compiles
CSS *before* Jekyll copies `assets/` into `_site/`. Order matters — Jekyll only
copies what exists when it runs.

`assets/css/main.css` is generated and therefore gitignored. The source of truth
is `_src/main.css`.

## Design tokens

Tailwind v4 is configured in CSS. All brand colors and the type stack live in
the `@theme` block in `_src/main.css`. Adding `--color-foo-500: #hex` there
automatically creates `bg-foo-500`, `text-foo-500`, `border-foo-500`, and so on.

The current palette is a **placeholder** pending the brand asset guide.

## Structure

```
_src/main.css      Tailwind input + @theme design tokens
_layouts/          Page shells
_includes/         head / header / footer partials
assets/            Images and generated CSS
index.html         Home page
_config.yml        Jekyll + site metadata
netlify.toml       Build command, headers
```
