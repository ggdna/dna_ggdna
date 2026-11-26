<!--
@license
Copyright (c) ggdna

Use of this source code is governed by terms that can be
found in the LICENSE file in the root of this package.
-->

# Bring Language Folders to Every ggdna Repo

## Motivation

- This umbrella layer gives a repo the whole set of topic layers at once.
  The topic layers now keep documentation per language: `doc/<lang>/`
  without a quarter, `pm/<lang>/<yyyy>-Q<n>/` for everything planned.
- A repo that adds this layer gets the new layout and guides in English,
  German and Farsi with a single update.

## Strategy

- Regenerate the DNA of this repo, so its instances show what a consumer
  receives; the hand-written part of the layer stays unchanged

## What a consumer gets: guides and templates

- Generated guides move from `doc/guides/` to `doc/en/guides/`, the
  templates to `doc/en/templates/`
- Every guide also ships in `doc/de/guides/` and `doc/fa/guides/`;
  translated headings keep fixed English anchors
- The German blog template moves to `doc/de/templates/blog-template.md`
- `.prettierignore` and `.pubignore` cover `doc/*/guides/` and
  `doc/*/templates/` for every language

## What a consumer gets: skills and scripts

- Every skill reads its guide from `doc/en/guides/`
- `/blog` files posts in `pm/<lang>/<yyyy>-Q<n>/blog`
- `/translate` and the new `doc/en/guides/translate-guide.md` sync all
  languages set by the variable `dnaLanguages` (default `en`, e.g.
  `en,de,fa`); generated guides are never translated
- `scripts/check-readme.js` checks `README.<lang>.md` and its language
  switcher for every language of the repo
- `/guide` ships a new guide in English, German and Farsi
- `/gg-review-architecture` reads
  `pm/<lang>/<yyyy>-Q<n>/architecture/`
- `/dna` reports a `dna/_dna.json` without `"isLayer": true`
- The gg skills look for requirements and blog posts below
  `pm/<lang>/<yyyy>-Q<n>/`

## Open Points

- Consumers move their hand-written docs into the language folders
  themselves; generated files follow on the next DNA build
