## Development

When starting the dev server, use background mode:

```
astro dev --background
```

Manage the background server with `astro dev stop`, `astro dev status`, and `astro dev logs`.

## Documentation

Full documentation: https://docs.astro.build

Consult these guides before working on related tasks:

- [Adding pages, dynamic routes, or middleware](https://docs.astro.build/en/guides/routing/)
- [Working with Astro components](https://docs.astro.build/en/basics/astro-components/)
- [Using React, Vue, Svelte, or other framework components](https://docs.astro.build/en/guides/framework-components/)
- [Adding or managing content](https://docs.astro.build/en/guides/content-collections/)
- [Adding styles or using Tailwind](https://docs.astro.build/en/guides/styling/)
- [Supporting multiple languages](https://docs.astro.build/en/guides/internationalization/)

## Deployment (GitHub Pages)

This site is deployed as a GitHub Pages **project site** at `https://daviidco.github.io/resume-cv/` — it does not live at the domain root. `astro.config.mjs` sets:

```js
site: 'https://daviidco.github.io',
base: '/resume-cv/',
```

Because of `base`, **never hardcode a root-relative internal path** (`href="/favicon.svg"`, `"/images/..."`, `href="/white"`, `url('/images/...')`, etc.). Astro does not rewrite plain strings coming from JSON data or literal attributes — only imported/optimized assets get that treatment. Instead, prefix every internal path with `import.meta.env.BASE_URL`, e.g.:

```astro
<link rel="icon" href={`${import.meta.env.BASE_URL}favicon.svg`} />
```

`profile.json` (`heroImage`, `resumePdf`) intentionally stores paths **without** a leading slash so they can be concatenated directly: `` `${import.meta.env.BASE_URL}${profile.heroImage}` ``. If you add new fields there that point at files in `public/`, follow the same convention.

Deployment itself is automated by `.github/workflows/deploy.yml`: every push to `main` builds with `withastro/action` (pinned to Node 22, since Astro 7 requires `>=22.12.0`) and publishes via `actions/deploy-pages`. In the GitHub repo settings, `Pages → Source` must be set to **GitHub Actions** for this to work.
