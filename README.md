# GitHub actions for TuringLang

This repository contains a collection of GitHub actions to be used across different TuringLang repositories.

## DocsNav

This action inserts a MultiDocumenter-style top navigation bar to `Documenter.jl` generated sites.

`TuringNavbar.html` in `DocsNav/scripts` directory contains code for building navigation bar for Turing language satellite packages' documentation but you can use your own navigation bar for your project!

### Example usage

```yaml
- name: Add Navbar
  uses: TuringLang/actions/DocsNav
  with:
    doc-path: 'Path to the Documenter.jl output', default: 'docs/build'
    navbar-url: 'URL of the navbar HTML to be inserted.', default: './scripts/TuringNavbar.html'
    exclude-paths: 'Comma-separated list of paths to exclude from navbar insertion.'
```

### Parameters

| Parameter | Description | Default |
| --- | --- | --- |
| `doc-path` | Path to the built HTML documentation | `docs/build` (following Documenter.jl conventions) |
| `navbar-url` | Path to, or URL of, the navbar HTML to be inserted | `DocsNav/scripts/TuringNavbar.html` in this repository |
| `exclude-paths` | Comma-separated list of paths to exclude from navbar insertion | `""` |

----------

## DocsDocumenter

This action performs a complete build and deploy of Documenter.jl documentation, inserting the above navbar in the process.

**Note**: This action takes care of calling `deploydocs()`, so your `docs/make.jl` file does not need to contain a call to `deploydocs()`.
This does not affect local documentation building because `deploydocs()` doesn't do anything locally.However, on CI, it will cause the documentation to be deployed twice: once without the navbar and once with.

### Example usage

```yaml
name: Documentation

on:
  push:
    branches:
      - main
    tags: '*'
  pull_request:
    branches:
      - main

concurrency:
  # Skip intermediate builds: always.
r # Cancel intermediate builds: only if it is a pull request build.
  group: ${{ github.workflow }}-${{ github.ref }}
  cancel-in-progress: ${{ startsWith(github.ref, 'refs/pull/') }}

permissions:
  contents: write
  pull-requests: read

jobs:
  docs:
    runs-on: ubuntu-latest

    steps:
      - name: Build and deploy Documenter.jl docs
        uses: TuringLang/DocsNav/DocsDocumenter@v2
```

### Parameters

| Parameter | Description | Default |
| --- | --- | --- |
| `doc-path` | Path to the documentation root | `docs` (following Documenter.jl conventions) |
| `doc-make-path` | Path to the `make.jl` file | `docs/make.jl` (following Documenter.jl conventions) |
| `julia-version` | Julia version to use | `'1'` |
| `exclude-paths` | Comma-separated list of paths to exclude from navbar insertion | `""` |
