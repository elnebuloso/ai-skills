# ai-skills

Ein kuratiertes Skill-Pack für [Claude Code](https://docs.claude.com/en/docs/claude-code). Gute Workflows als wiederverwendbare Skills — damit sich bewährte Abläufe nicht in jeder Session neu erklären müssen.

## Skills

| Skill | Beschreibung | Trigger |
|-------|--------------|---------|
| [`bananas`](skills/bananas/SKILL.md) | Session-Cleanup-Check: prüft Git-State, Tests, Debug-Reste, Memory und offene Gesprächsfäden, bevor du eine Session schließt. | „alles sauber?", „kann ich die Session abschließen?", „Bananenschalen?", „are we done?" |

## Installation (Claude Code)

Das Repo ist ein Claude-Code-Plugin-Marketplace. Marketplace hinzufügen und Pack installieren — zwei Befehle:

```bash
/plugin marketplace add elnebuloso/ai-skills
/plugin install elnebuloso@ai-skills
```

Danach sind alle Skills aus dem Pack verfügbar. Sie sind unter dem Namespace `elnebuloso:` adressierbar — du kannst sie über ihren Trigger ansprechen (z.B. „alles sauber?") oder direkt mit `/elnebuloso:bananas` aufrufen. Der Namespace verhindert Konflikte, falls ein anderes Plugin einen gleichnamigen Skill mitbringt.

### Manuelle Installation (ohne Plugin)

Alternativ einen einzelnen Skill nach `~/.claude/skills/` kopieren:

```bash
git clone https://github.com/elnebuloso/ai-skills.git
cp -r ai-skills/skills/bananas ~/.claude/skills/bananas
```

## Updates

Neue Skills und Änderungen werden mit jedem Push veröffentlicht (das Plugin ist nicht auf eine feste Version gepinnt — jeder Commit zählt als neue Version). Um den neuesten Stand zu holen:

```bash
/plugin marketplace update ai-skills
/plugin update elnebuloso@ai-skills
```

## Repository-Struktur

```
.claude-plugin/
├── marketplace.json     # Marketplace-Definition
└── plugin.json          # Plugin-Manifest (das Skill-Pack)
skills/
└── <skill-name>/
    ├── SKILL.md          # Frontmatter (name, description) + Anleitung
    └── evals/
        └── evals.json    # Beispiel-Prompts zum Testen des Skills
```

Jeder Skill steht in einem eigenen Ordner. Die `SKILL.md` enthält im Frontmatter `name` und `description` — die `description` entscheidet, wann Claude den Skill aktiviert.

## Lizenz

[MIT](LICENSE)
