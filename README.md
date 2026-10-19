# stemforge plugins

Claude-Code-Plugins von Stephan Schmidt, gebaut mit kit aus gepinnten Quellen. Nichts hier von Hand
ändern: Jede Datei unter `plugins/` und `.claude-plugin/` entsteht beim Bau neu.

| Plugin | Inhalt |
|---|---|
| `dev` | Ideen-Eingang `ssc-pour` und alle 37 Skills von Matt Pocock ([mattpocock/skills](https://github.com/mattpocock/skills)) |

## Installation

```bash
claude plugin marketplace add stemForge/plugins
claude plugin install dev@stemforge --scope project
```

Andere Agenten (Codex, Hermes …): `npx skills add stemForge/plugins`.

## Lizenz

Eigene Skills: MIT (`LICENSE`). Übernommene Skills behalten die Lizenz ihres Originals; Herkunft,
gepinnter Commit und Lizenz stehen im Frontmatter (`metadata.derived_from`) und in `LICENSE.upstream`.
