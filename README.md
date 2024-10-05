# DocsNav: Global Navigation for your Documentation

This action inserts a MultiDocumenter-style top navigation bar to `Documenter.jl` generated sites.

`TuringNavbar.html` contains code for building navigation bar for Turing language satellite packages' documentation but you can use your own navigation bar for your project!

## How to use

```
- name: Add Navbar
  uses: shravanngoswamii/DocsNav@v1
  with:
    navbar-url: 'URL of the navbar HTML to be inserted.'
    exclude-paths: 'Comma-separated list of paths to exclude from navbar insertion.'
    token: ${{ secrets.GITHUB_TOKEN }}
```