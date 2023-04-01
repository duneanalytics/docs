# Dune Docs

Welcome to the Dune Docs!

Dune is a crypto analytics tool by and for the community.

These docs are open source and built with [Material for MkDocs](https://squidfunk.github.io/mkdocs-material).

Any contributions are welcome, from spelling mistakes to entire guides on the EVM. Just submit a PR.

## Want to use the chatgpt integration and ask our docs questions (in a CLI)?

You'll need to follow the [autodoc setup guide](https://github.com/context-labs/autodoc):

Autodoc requires Node v18.0.0 or greater. v19.0.0 or greater is recommended. Make sure you're running the proper version:

```bash
$ node -v
```

Example output:
```bash
v19.8.1
```

Install the Autodoc CLI tool as a global NPM module:

```bash
$ npm install -g @context-labs/autodoc
```

Then, you'll need to SET or EXPORT your OpenAI API key.

Now just clone this repo, and then all you need to do is run `doc q` in the repo and you'll be able to ask questions! Hopefully we'll have a frontend for this soon :)

## Install Dune Docs Locally

If you'd like to run the docs locally, follow these instructions.

Setup your local python 3 environment, e.g. with [Miniconda](https://docs.conda.io/en/latest/miniconda.html).

Install the python libraries:

```bash
pip install -r requirements.txt
```

Run the docs locally:

```bash
mkdocs serve
```

## Notes

Remember to use relative paths to markdown files for internal links (e.g. `[link](../../relative/path/to/index.md)`), otherwise the mkdocs compiler will not detect broken internal links - [read more](/index.md).

## Translations

Dune docs are kindly translated by members of our community.

Currently they are available in English and Chinese.

Each translation is run as a separate `mkdocs-material` project. For example, with the Chinese docs navigate to `zh` and run `mkdocs serve`. The build process automatically merges together translations into a single docs site with language switcher.

To propose a new language, open an issue or reach out to us on Discord!

## Upgrades

To upgrade `mkdocs-material`, you need to pin a new version of `mkdocs-material` and update the hard-coded value for stylesheets in `overrides/main.html`.

- Update `requirements.txt` with new version of `mkdocs-material`
- Upgrade your local environment
- Find the auto-generated stylesheet file name, see [example](https://github.com/squidfunk/mkdocs-material/tree/8.5.11/material/assets/stylesheets)
- Update in `overrides/main.html`
- Do the same for the `mkdocs-material-insiders`
- Update the `mkdocs-material` version on Vercel
