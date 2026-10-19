# dna_ggdna

[English](README.md) | Deutsch

[![CI](https://github.com/ggdna/dna_ggdna/actions/workflows/quick_check.yaml/badge.svg)](https://github.com/ggdna/dna_ggdna/actions/workflows/quick_check.yaml)

Gibt einem ggdna-Repo mit einer Abhängigkeit jede Themen-Schicht, den Guide
zum Erstellen von DNA-Schichten und die Identität von ggdna.

## Motivation

Jedes Thema — README, Guides, Übersetzung, Index, Blog,
Installations-Guides, VS Code, Clean Code, Skripte und der gg-Workflow —
ist eine eigene Schicht ohne Eltern. Die Themen-Schichten fragen außerdem
jede Schicht, die sie einbindet, nach der Identität der Organisation: dem
Rechteinhaber, der Firma, der GitHub-Organisation mit ihrer URL, dem
Ticket-Präfix und dem Namen der Quick-Check-Pipeline. Ohne
Umbrella-Schicht müsste jedes ggdna-Repo jede Themen-Schicht einzeln
einbinden und diese Variablen selbst setzen.

Diese Schicht erledigt beides einmal für die Organisation. Sie bringt
außerdem dna_helix mit: Die ggdna-Repos sind selbst DNA-Schichten und
folgen deren Regeln, um eine Schicht zu erstellen und zu veröffentlichen.

## Verwendung

Als Dev-Dependency eintragen und einmal initialisieren:

```bash
pnpm add -D @ggdna/dna-ggdna   # TypeScript projects
dart pub add dev:dna_ggdna     # Dart projects
gg dna init
```

`gg dna init` legt einen Test ab, der die DNA bei jedem Testlauf
instanziiert und prüft. Die Schicht liefert keine eigenen Dateien; der
Test kopiert die ihrer Eltern: die Guides und Templates nach `doc/`, die
Skills nach `.claude/skills/`, die Skripte nach `scripts/`, die
VS-Code-Einstellungen nach `.vscode/`, den Quick-Check-Workflow nach
`.github/workflows/` sowie `CLAUDE.md` und die Prettier-Konfiguration ins
Wurzelverzeichnis des Repos.

Tippe `/gg` in Claude Code, um die Schritte des Ticket-Workflows zu sehen
und welcher als Nächstes kommt. Die README jeder Eltern-Schicht beschreibt
deren eigene Skills und Skripte.

## Umfang

Die Schicht hat kein eigenes Thema: Ein Guide, ein Skill oder ein Skript
wird in seiner Themen-Schicht geändert, nicht hier. `dna/_dna.json` nennt
dna_plan und dna_design_layers nicht, ggdna-Repos bekommen sie also nicht
über diese Schicht.

Die Themen-Schichten bauen nicht auf dieser Umbrella-Schicht auf: Sie
bindet sie ein, und die Engine lehnt einen Graphen ab, in dem eine Schicht
erneut vorkommt.

## Schichten

`dna/_dna.json` nennt diese Eltern, angewendet in dieser Reihenfolge; die
Umbrella-Schicht selbst kommt zuletzt:

- [dna_helix](https://github.com/ggdna/dna_helix) — der DNA-Guide und der
  Skill `/dna`: wie eine DNA-Schicht gebaut, konfiguriert und
  veröffentlicht wird
- [dna_readme](https://github.com/ggdna/dna_readme) — die README-Guides
  und -Templates, der Skill `/readme` und das Skript, das die README prüft
- [dna_guides](https://github.com/ggdna/dna_guides) — die Regeln für
  Guides und Dokumentation und der Skill `/guide`
- [dna_translate](https://github.com/ggdna/dna_translate) — die Regeln,
  die englische und deutsche Dokumentation synchron halten, das deutsche
  Blog-Template und der Skill `/translate`
- [dna_index](https://github.com/ggdna/dna_index) — der Guide und das
  Template der `index.jsonc`, die ein Repo beschreibt, und der Skill
  `/index`
- [dna_blog](https://github.com/ggdna/dna_blog) — der Blog-Guide, das
  Template für Blogbeiträge und der Skill `/blog`
- [dna_install](https://github.com/ggdna/dna_install) — die
  Installations-Guides, die einen Entwicklungsrechner einrichten, und der
  Skill `/install`
- [dna_vscode](https://github.com/ggdna/dna_vscode) — die gemeinsamen
  VS-Code-Einstellungen und -Erweiterungen, die Prettier-Konfiguration
  und der Skill `/vscode`
- [dna_clean_code](https://github.com/ggdna/dna_clean_code) — die Code-
  und Test-Guides, sprachneutral sowie für Dart und TypeScript, und die
  Skills `/code`, `/test`, `/review-light` und `/review-heavy`
- [dna_scripts](https://github.com/ggdna/dna_scripts) — die Node-Skripte
  für den Git- und GitHub-Workflow, ihre gemeinsamen Funktionen und der
  Skill `/scripts`
- [dna_gg](https://github.com/ggsuite/dna_gg) — der gg-Ticket-Workflow:
  die Entwicklungs-Guides, `CLAUDE.md` und die `/gg`-Skills; sie baut auf
  dna_install, dna_index und dna_github auf, die den Quick-Check-Workflow
  und das GitHub-Setup-Skript beisteuert

## Variablen

`dna/_vars.json` setzt die Identität von ggdna:

- `dnaCopyrightHolder` — der Rechteinhaber im Lizenzkopf jeder Datei,
  `ggdna`
- `dnaCompany` — die Firma, `ggdna`
- `dnaGitOrg` — die GitHub-Organisation, `ggdna`
- `dnaGitOrgUrl` — die URL dieser Organisation,
  `https://github.com/ggdna`
- `dnaJiraPrefix` — das Präfix einer Ticket-ID, `GGD`
- `dnaGitQuickCheckPipelineName` — der Name der Quick-Check-Pipeline, die
  die Branch-Regeln verlangen, `Quick Check`

Ein Repo, das diese Schicht einbindet, setzt keine davon: `dna/_dna.json`
markiert alle sechs mit `mustOverride: false` und hebt damit die Pflicht
auf, die die Themen-Schichten weitergeben.

## Entwicklung

Der Ordner `dna/` ist handgeschriebene Quelle und wird nie generiert. Das
Repo instanziiert seine eigene DNA — nach Änderungen `dart test` laufen
lassen; vorher committen, denn eine Datei, die die DNA überschreiben
würde, darf keine uncommittete Arbeit enthalten.

Bearbeite nur `dna/_dna.json` und `dna/_vars.json`, nie die Kopien in
`doc/`, `.claude/`, `scripts/` und `.vscode/`: Der Test überschreibt sie
mit den Dateien der Eltern-Schichten.

## Lizenz

MIT — siehe [LICENSE](LICENSE).
