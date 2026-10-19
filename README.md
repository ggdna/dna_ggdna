# dna_ggdna

English | [Deutsch](README.de.md)

[![CI](https://github.com/ggdna/dna_ggdna/actions/workflows/quick_check.yaml/badge.svg)](https://github.com/ggdna/dna_ggdna/actions/workflows/quick_check.yaml)

Gives a ggdna repo every topic layer, the authoring guide for DNA layers and
the ggdna identity in one dependency.

## Motivation

Every topic — README, guides, translation, index, blog, install guides,
VS Code, clean code, scripts and the gg workflow — is a layer of its own
without parents. The topic layers also ask every layer that lists them for
the identity of the organization: the copyright holder, the company, the
GitHub org with its URL, the ticket prefix and the name of the quick check
pipeline. Without an umbrella, every ggdna repo would list each topic layer
and set these variables itself.

This layer does both once for the organization. It also carries dna_helix:
the ggdna repos are DNA layers themselves and follow its rules for
authoring and publishing one.

## Usage

Declare it as a dev-dependency and initialize once:

```bash
pnpm add -D @ggdna/dna-ggdna   # TypeScript projects
dart pub add dev:dna_ggdna     # Dart projects
gg dna init
```

`gg dna init` places a test that instantiates and verifies the DNA on every
test run. The layer ships no files of its own; the test copies those of its
parents: the guides and templates to `doc/`, the skills to
`.claude/skills/`, the scripts to `scripts/`, the VS Code settings to
`.vscode/`, the quick check workflow to `.github/workflows/`, and
`CLAUDE.md` and the Prettier configuration to the root of the repo.

Type `/gg` in Claude Code to see the steps of the ticket workflow and which
one comes next. The README of each parent layer describes its own skills
and scripts.

## Scope

The layer carries no topic of its own: a guide, a skill or a script is
changed in its topic layer, not here. `dna/_dna.json` does not list
dna_plan and dna_design_layers, so ggdna repos do not get them through this
layer.

The topic layers do not build on this umbrella: it lists them, and the
engine rejects a graph in which a layer reappears.

## Layers

`dna/_dna.json` lists these parents, applied in this order; the umbrella
itself is applied last:

- [dna_helix](https://github.com/ggdna/dna_helix) — the DNA guide and the
  `/dna` skill: how a DNA layer is built, configured and published
- [dna_readme](https://github.com/ggdna/dna_readme) — the README guides
  and templates, the `/readme` skill and the README check script
- [dna_guides](https://github.com/ggdna/dna_guides) — the rules for
  writing guides and documentation, and the `/guide` skill
- [dna_translate](https://github.com/ggdna/dna_translate) — the rules that
  keep English and German documentation in sync, the German blog template
  and the `/translate` skill
- [dna_index](https://github.com/ggdna/dna_index) — the guide and the
  template of the `index.jsonc` that describes a repo, and the `/index`
  skill
- [dna_blog](https://github.com/ggdna/dna_blog) — the blog guide, the blog
  post template and the `/blog` skill
- [dna_install](https://github.com/ggdna/dna_install) — the install guides
  that set up a development machine, and the `/install` skill
- [dna_vscode](https://github.com/ggdna/dna_vscode) — the shared VS Code
  settings and extensions, the Prettier configuration and the `/vscode`
  skill
- [dna_clean_code](https://github.com/ggdna/dna_clean_code) — the code and
  test guides, language neutral and for Dart and TypeScript, and the
  `/code`, `/test`, `/review-light` and `/review-heavy` skills
- [dna_scripts](https://github.com/ggdna/dna_scripts) — the node scripts
  for the git and GitHub workflow, their shared functions and the
  `/scripts` skill
- [dna_gg](https://github.com/ggsuite/dna_gg) — the gg ticket workflow:
  the develop guides, `CLAUDE.md` and the `/gg` skills; it builds on
  dna_install, dna_index and dna_github, which adds the quick check
  workflow and the GitHub setup script

## Variables

`dna/_vars.json` sets the identity of ggdna:

- `dnaCopyrightHolder` — the holder named in the license header of every
  file, `ggdna`
- `dnaCompany` — the company, `ggdna`
- `dnaGitOrg` — the GitHub organization, `ggdna`
- `dnaGitOrgUrl` — the URL of that organization,
  `https://github.com/ggdna`
- `dnaJiraPrefix` — the prefix of a ticket id, `GGD`
- `dnaGitQuickCheckPipelineName` — the name of the quick check pipeline
  the branch rules require, `Quick Check`

A repo listing this layer sets none of them: `dna/_dna.json` marks all six
`mustOverride: false`, which lifts the duty the topic layers pass on.

## Development

The `dna/` folder is hand-authored source and is never generated. The repo
instantiates its own DNA — run `dart test` after changes; commit first, a
file the DNA would overwrite must not carry uncommitted work.

Edit only `dna/_dna.json` and `dna/_vars.json`, never the copies in
`doc/`, `.claude/`, `scripts/` and `.vscode/`: the test overwrites them
with the files of the parent layers.

## License

MIT — see [LICENSE](LICENSE).
