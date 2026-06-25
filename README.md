# ai-skills

Ein kuratiertes Skill-Pack für [Claude Code](https://docs.claude.com/en/docs/claude-code). Bewährte Workflows als wiederverwendbare Skills — damit sich gute Abläufe nicht in jeder Session neu erklären müssen.

## Skills

Die Skills begleiten den Session-Lebenszyklus: morgens einsteigen, abends übergeben — und bei Bedarf die Doku verdichten.

| Skill | Beschreibung | Trigger (Beispiele) |
|-------|--------------|---------------------|
| [`moin`](skills/moin/SKILL.md) | **Session-Einstieg.** Übernimmt die hinterlassene Übergabe (Standard `docs/HANDOFF.md`), gleicht sie gegen den echten Stand ab (git, Commits, Dateien), fasst zusammen und schlägt den ersten Schritt vor. | „Moin", „guten Morgen", „wo haben wir gestern aufgehört?", „lies dich in den Handoff ein" |
| [`feierabend`](skills/feierabend/SKILL.md) | **Session-Abschluss.** Schreibt die Übergabe (Standard `docs/HANDOFF.md`), spürt Stolperfallen für morgen auf und gibt einen Start-Prompt mit — damit die nächste Session reibungslos anknüpft. | „Feierabend", „das reicht für heute", „ich gehe gleich weg", „schreib eine Übergabe" |
| [`wissensschmelze`](skills/wissensschmelze/SKILL.md) | **Doku verdichten.** Schmilzt die gesamte Doku (Standard `docs/`) zu einer Wissensdatei `KNOWLEDGE-YYYY-MM-DD-HHMM.md` ein, trennt dabei gültigen Stand von überholtem Bias und entsorgt Altlasten erst nach Review. | „Wissensschmelze", „verdichte die Doku", „docs einschmelzen", „Bias aus der Doku werfen" |

`moin` und `feierabend` sind ein Paar: Was am Abend übergeben wird, übernimmt der Morgen. `wissensschmelze` räumt dazwischen auf, wenn die Doku zu viel Altlast trägt.

## Installation

Das Repo ist ein Claude-Code-Plugin-Marketplace — Marketplace hinzufügen, Pack installieren:

```bash
/plugin marketplace add elnebuloso/ai-skills
/plugin install elnebuloso@ai-skills
```

Danach sind alle Skills verfügbar. Du kannst sie über ihren Trigger ansprechen (z.B. „Moin") oder direkt unter dem Namespace `elnebuloso:` aufrufen, etwa `/elnebuloso:moin`. Der Namespace verhindert Konflikte mit gleichnamigen Skills aus anderen Plugins.

So installiert gilt das Pack nutzerweit — in allen Projekten.

### Nur in einem Projekt (Projekt-Scope)

Soll das Pack ausschließlich in einem bestimmten Repo gelten, statt nutzerweit, aktiviere es über eine eingecheckte `.claude/settings.json` in **diesem** Projekt:

```json
{
  "extraKnownMarketplaces": {
    "ai-skills": {
      "source": { "source": "github", "repo": "elnebuloso/ai-skills" }
    }
  },
  "enabledPlugins": ["elnebuloso@ai-skills"]
}
```

Beim ersten Öffnen des Projekts fragt Claude Code einmalig, ob du dem Workspace vertraust. Nach dem Vertrauen wird die Marketplace-Quelle automatisch hinzugefügt und das Pack beim Session-Start geladen — ohne separate Bestätigung pro Plugin und nur in diesem Projekt. Das Vertrauen wird pro Verzeichnis gespeichert; für den ersten Start ist Netzwerkzugriff nötig (das Pack wird von GitHub geholt).

Wer nur einen einzelnen Skill projekt-lokal will, legt ihn direkt unter `.claude/skills/<name>/SKILL.md` im Repo ab (ohne Marketplace, gilt nur dort).

### Updates

Jeder Push veröffentlicht eine neue Version (das Plugin ist nicht auf eine feste Version gepinnt — jeder Commit zählt). Für den neuesten Stand:

```bash
/plugin marketplace update ai-skills
/plugin update elnebuloso@ai-skills
```

### Manuell (ohne Plugin)

Alternativ einen einzelnen Skill direkt nach `~/.claude/skills/` kopieren:

```bash
git clone https://github.com/elnebuloso/ai-skills.git
cp -r ai-skills/skills/moin ~/.claude/skills/moin
```

## Repository-Struktur

```
.claude-plugin/
├── marketplace.json     # Marketplace-Definition
└── plugin.json          # Plugin-Manifest (das Skill-Pack)
skills/
└── <skill-name>/
    └── SKILL.md         # Frontmatter (name, description) + Anleitung
```

Jeder Skill steht in einem eigenen Ordner. Die `SKILL.md` enthält im Frontmatter `name` und `description` — die `description` entscheidet, wann Claude den Skill aktiviert.

## Lizenz

[MIT](LICENSE)
