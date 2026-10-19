<!--
@license
Copyright (c) ggdna

Use of this source code is governed by terms that can be
found in the LICENSE file in the root of this package.
-->

# Setup github guide under doc/guides

## Motivation

- This repo carried a top-level `guides/` folder with a single file,
  `setup-github-guide.md`. Every other guide lives in `doc/guides/`.
- The file ended a line with a trailing space, so `prettier --check .`
  failed on it, while the generated `doc/guides/` is excluded from that
  check.
- The goal: one place for all guides and a clean format check.

## Strategy

- Take the fixed setup github guide from the layers
- Let the DNA test instantiate it and remove the old file
- No hand-written change in this repo

## Implementation 1: The new place

- The DNA test instantiates `doc/guides/setup-github-guide.md`
- It removes `guides/setup-github-guide.md`, which is no longer produced,
  and the then empty `guides/` folder
- `prettier --check .` passes on the whole repo

## Implementation 2: Other regenerated files

- The development guide and the `/gg`, `/gg-publish` skills are
  regenerated from the current `dna_gg`, which also adds `/gg-review`

## Dependency updates

- `dna_github`: ships the setup github guide under `doc/guides/` and
  without trailing whitespace
- `dna_gg`: carries that guide on and brings the current development
  guide and gg skills

## Open Points

- None
