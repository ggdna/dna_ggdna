# dna_ggdna

The DNA of every ggdna repo — everything needed to author a DNA layer.

It is the umbrella: it carries no topic of its own and pulls in the whole
set, so one layer gives a repo all of them. The authoring topic lives in
[dna_helix](https://github.com/ggdna/dna_helix), which the topic layers
consume directly — they cannot take this umbrella, because it lists them
back and the engine rejects a graph in which the consuming repo reappears.

## Layers

| Layer | What it brings |
| --- | --- |
| [dna_helix](https://github.com/ggdna/dna_helix) | how a DNA layer is authored: the DNA guide and the `/dna` skill |
| [dna_readme](https://github.com/ggdna/dna_readme) | README structure and templates |
| [dna_guides](https://github.com/ggdna/dna_guides) | developer and AI guides |
| [dna_translate](https://github.com/ggdna/dna_translate) | multi-language docs, de and en in sync |
| [dna_index](https://github.com/ggdna/dna_index) | index and navigation files |
| [dna_blog](https://github.com/ggdna/dna_blog) | blog format, templates, layout |
| [dna_install](https://github.com/ggdna/dna_install) | install guides: editor, node, Azure, tooling |
| [dna_vscode](https://github.com/ggdna/dna_vscode) | shared editor settings and extensions |
| [dna_clean_code](https://github.com/ggdna/dna_clean_code) | how code is written and tested, per language |
| [dna_gg](https://github.com/ggdna/dna_gg) | the gg workflow, and the scripts it calls |

## Variables

- `dnaCopyrightHolder` — the name in the license header of every file,
  set to `ggdna` here

## Usage

Declare it as a dev-dependency and initialize once:

```bash
pnpm add -D @ggdna/dna-ggdna   # TypeScript projects
dart pub add dev:dna_ggdna     # Dart projects
gg dna init
```

The placed test instantiates and verifies the DNA on every test run.

## Development

The `dna/` folder is hand-authored source and is never generated. The repo
instantiates its own DNA — run `dart test` after changes; commit first, a
file the DNA would overwrite must not carry uncommitted work.
