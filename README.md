# dna_ggdna

The DNA of every ggdna repo — everything needed to author a DNA layer.

It pulls in the whole set of topic layers and adds the one topic that is
ours: how a DNA layer itself is built, configured and published.

## Guides

- `dna/doc/guides/dna-guide.md` — the `dna/` layout and the `dot-`
  escape, what belongs in `_dna.json` and `_vars.json`, the three
  override mechanisms, and publishing one layer to both registries

## Skills

- `/dna` — checks this layer against the DNA guide: paths that would not
  instantiate, layers that are not dependencies, variables nothing
  declares, and manifests that drifted apart

## Layers

| Layer | What it brings |
| --- | --- |
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
