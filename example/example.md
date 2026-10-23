# Example

`dna_ggdna` is a DNA layer: it bundles the topic layers every ggdna repo
takes, no code. Declare it as a dev dependency and instantiate it once:

```bash
dart pub add dev:dna_ggdna     # Dart projects
pnpm add -D @ggdna/dna-ggdna   # TypeScript projects
gg dna init
gg dna build
```

The placed test instantiates the layers on every test run and keeps the
repo in sync with them.
