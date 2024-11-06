# DocsNav: Global Navigation for your Documentation

This action inserts a MultiDocumenter-style top navigation bar to `Documenter.jl` generated sites.

`TuringNavbar.html` in scripts directory contains code for building navigation bar for Turing language satellite packages' documentation but you can use your own navigation bar for your project!

## How to use

```yaml
- name: Add Navbar
  uses: TuringLang/DocsNav
  with:
    doc-path: 'Path to the Documenter.jl output', default: 'docs/build'
    navbar-url: 'URL of the navbar HTML to be inserted.', default: './scripts/TuringNavbar.html'
    exclude-paths: 'Comma-separated list of paths to exclude from navbar insertion.'
```
