<!--
@license
Copyright (c) ggdna

Use of this source code is governed by terms that can be
found in the LICENSE file in the root of this package.
-->

# Take the scoped blog rules

## Motivation

- `dna_ggdna` bundles the topic layers of its organization into one
  layer. Its value is that every repo built on it follows the same,
  current rules.
- The blog layer changed what a post is: one post per repo, describing
  only that repo. `dna_ggdna` still carried the old rule of one post per
  ticket.
- The goal: this repo and everything instantiated from it write posts
  that stand on their own next to the code they describe.

## Strategy

- Raise the three layers that carry the new blog rules to their current
  versions
- Leave every other layer where it is
- Let the DNA test instantiate the new guides into this repo and verify
  them

## Implementation 1: Raise the layers

- `dna_blog`, `dna_translate` and `dna_gg` are raised in `pubspec.yaml`
  and `package.json` alike, so the Dart and the npm package stay equal
- No variable had to change: the organization variables were already set
  in `dna/_vars.json`

## Implementation 2: The instantiated guides

- The blog guide, the english and german templates and the `/blog` and
  `/translate` skills of this repo are regenerated
- The development guide now asks for a post in every repo of a ticket
  that has the blog guide
- This post is the first one of this repo written under the new rules

## Dependency updates

- `dna_blog` 0.3.0: one post per repo, only its own changes and what
  updated dependencies changed for it, no mention of the repos that use
  it; posts are filed under `doc/blog/<yyyy>`; the template got the
  optional section "Dependency updates"; the `dnaYear` variable is gone
- `dna_translate` 0.3.0: german posts are filed under
  `doc/de/blog/<yyyy>`; the german template got the section
  "Aktualisierte Abhängigkeiten"
- `dna_gg` 0.10.0: the publish step runs `/blog` in every repo of the
  ticket that has the blog guide

## Open Points

- Repos built on this layer get the new rules once they take this
  version
