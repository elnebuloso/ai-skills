# ai-skills

Ein kuratiertes Skill-Pack für [Claude Code](https://docs.claude.com/en/docs/claude-code). Gute Workflows als wiederverwendbare Skills — damit sich bewährte Abläufe nicht in jeder Session neu erklären müssen.

## Skills

| Skill | Beschreibung | Trigger |
|-------|--------------|---------|
| [`bananas`](skills/bananas/SKILL.md) | Session-Cleanup-Check: prüft Git-State, Tests, Debug-Reste, Memory und offene Gesprächsfäden, bevor du eine Session schließt. | „alles sauber?", „kann ich die Session abschließen?", „Bananenschalen?", „are we done?" |

## Installation (Claude Code)

Skills liegen in Claude Code unter `~/.claude/skills/`. Du hast zwei Möglichkeiten:

### Variante A — einzelnen Skill kopieren

```bash
git clone https://github.com/elnebuloso/ai-skills.git
cp -r ai-skills/skills/bananas ~/.claude/skills/bananas
```

### Variante B — per Symlink (bleibt mit dem Repo aktuell)

```bash
git clone https://github.com/elnebuloso/ai-skills.git ~/ai-skills
ln -s ~/ai-skills/skills/bananas ~/.claude/skills/bananas
```

Nach der Installation steht der Skill in Claude Code zur Verfügung. Du kannst ihn über seinen Trigger ansprechen oder direkt mit `/bananas` aufrufen.

## Repository-Struktur

```
skills/
└── <skill-name>/
    ├── SKILL.md          # Frontmatter (name, description) + Anleitung
    └── evals/
        └── evals.json    # Beispiel-Prompts zum Testen des Skills
```

Jeder Skill steht in einem eigenen Ordner. Die `SKILL.md` enthält im Frontmatter `name` und `description` — die `description` entscheidet, wann Claude den Skill aktiviert.

## Lizenz

[MIT](LICENSE)
