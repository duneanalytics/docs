# Dune Docs

Welcome to the Dune docs!

Dune is a crypto analytics tool by and for the community.

These docs are open source and built with [Material for MkDocs](https://squidfunk.github.io/mkdocs-material).

Any contributions are welcome, from spelling mistakes to entire guides on the EVM. Just submit a PR.

## Install

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