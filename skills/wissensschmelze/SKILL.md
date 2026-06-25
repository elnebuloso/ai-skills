---
name: wissensschmelze
description: >-
  Wissensschmelze: Verdichte die gesamte Projekt-Doku unter docs/ zu einer
  einzigen Wissensdatei und wirf dabei Altlasten und veralteten Bias über Bord.
  Alles Narrative und alle Entscheidungen werden eingeschmolzen, klar getrennt in
  aktuell/gültig vs. historisch/überholt, und in
  docs/KNOWLEDGE-YYYY-MM-DD-HHMM.md verdichtet – damit eine frische Session ohne
  mitgeschleppte Fehlannahmen starten kann. Nutze diesen Skill, wenn der Nutzer
  die Doku verdichten, einschmelzen, bereinigen oder von Altlasten und Bias
  befreien will. Typische Formen: "Wissensschmelze", /wissensschmelze, "verdichte
  die Doku", "docs/ verdichten / einschmelzen / zusammenführen", "Doku bereinigen
  ohne Altlasten", "Bias / veraltete Annahmen aus der Doku werfen", "mach mir aus
  dem ganzen docs-Wust eine Wissensdatei", "Knowledge-Datei erzeugen", "vor der
  nächsten Planungsrunde die Historie verdichten". Das Zielverzeichnis ist
  standardmäßig docs/, kann aber beim Aufruf genannt werden (z. B. "verdichte die
  Doku in wiki/"). Auch sinngemäßes Verdichten der Doku ohne das Wort "Schmelze"
  zählt. NICHT für das Schreiben einer einzelnen
  neuen Doku-Datei, nicht für die Session-Übergabe am Arbeitsende (das ist
  feierabend), nicht für Code-Kommentare/Docstrings und nicht für reines Lesen
  oder Zusammenfassen ohne die Absicht, zu verdichten und aufzuräumen.
---

# Wissensschmelze: die Doku einschmelzen, den Bias abscheiden

Über die Zeit wächst unter `docs/` ein Wust: Entscheidungen, verworfene Ansätze,
frühere Fehlannahmen, halbe Notizen – alles gleichberechtigt nebeneinander. Wer
darauf eine neue Planungsrunde startet, schleppt den alten Bias mit. Dieser Skill
schmilzt den ganzen Wust zu einem Barren ein: das gültige Wissen wird verdichtet,
die Schlacke – überholte Annahmen und verworfene Wege – wird nicht weggeworfen,
sondern **als überholt markiert abgeschieden**, damit sie sichtbar bleibt, ohne
weiter als Wahrheit mitzuschmelzen.

Das Ergebnis ist eine einzige Datei: `docs/KNOWLEDGE-YYYY-MM-DD-HHMM.md`. Der
Zeitstempel im Namen hält fest, wann diese Schmelze entstanden ist – so bleibt
der Skill beliebig oft nutzbar, und man sieht jeder Wissensdatei ihr Alter an.

Das **Zielverzeichnis ist standardmäßig `docs/`** (rekursiv). Hat der Nutzer beim
Aufruf ein anderes Verzeichnis genannt (z. B. `documentation/`, `wiki/` oder ein
Unterordner), nimm das stattdessen – die Wissensdatei landet dann ebenfalls dort.
Im Folgenden steht `docs/` durchgehend für dieses Zielverzeichnis.

**Primärquelle ist alles unter `docs/` (rekursiv).** Alles außerhalb des
Zielverzeichnisses – übrige Repo-Doku, Code, ein `mkdocs/`- oder Wiki-Verzeichnis
– darfst du als Informationsquelle **lesend** heranziehen, falls dir Kontext
fehlt. Aber:

> **Außerhalb des Zielverzeichnisses wird nichts angelegt, geändert oder
> gelöscht.** Dort liest du nur. Geschrieben und aufgeräumt wird ausschließlich
> im Zielverzeichnis.

Und für `docs/` selbst gilt dieselbe eiserne Regel wie überall in diesem
Skill-Pack:

> **Du verdichtest eigenständig, aber du entsorgst nichts eigenmächtig.**
> Jede Löschung, jedes Leeren einer Datei läuft erst als Vorschlag über den
> Nutzer – dann handelst du. Das gilt ausnahmslos.

Weil dieser Skill am Ende Dateien entsorgt, ist ein eigener Branch (z. B.
`docs-wissensschmelze`) eine gute Idee. Schlag ihn vor, wenn ihr noch auf einem
Arbeits- oder Hauptbranch seid – erzwingen musst du ihn nicht.

## Ablauf

### 1. Sichten und in Chronologie bringen

Sichte alle Dateien unter `docs/` rekursiv. Ziehe ergänzend lesend heran, was
außerhalb hilft (z. B. `mkdocs/docs/`, ein Wiki, ein `findings.md`), falls der
Kontext sonst lückenhaft bliebe.

Bring das Material in eine **chronologische** Reihenfolge – denn nur so erkennst
du, was eine spätere Entscheidung eine frühere überholt hat. Stütz dich auf:

- Zeitstempel in Dateinamen (z. B. `2026-06-25-2056-...`),
- `git log` für Entstehungs- und Änderungszeit,
- inhaltliche Bezüge („ersetzt X", „Revert von Y").

Liegt bereits eine `KNOWLEDGE-*.md` aus einer früheren Schmelze vor, ist sie
deine **wichtigste Vorzustands-Quelle**: der bereits verdichtete Stand. Sie wird
mit eingeschmolzen und am Ende durch die neue ersetzt – es bleibt immer nur die
jüngste.

### 2. Schmelzgut von Referenz trennen

Nicht alles unter `docs/` gehört in eine Historie. Sortiere, bevor du schmilzt:

- **Schmelzgut** – das Narrativ und die Entscheidungen: wie das Projekt dahin
  kam, wo es steht; was probiert, verworfen, beschlossen wurde. Das wird
  verdichtet und danach entsorgt.
- **Operative Referenz** – Setup-Anleitungen, API-/Schnittstellen-Doku, ADRs,
  Diagramme, Runbooks. Solche Doku beschreibt keinen Weg, sondern einen
  **aktuellen Zustand zum Nachschlagen**. Sie gehört nicht in eine Historie und
  wird **nicht** mit eingeschmolzen oder gelöscht.

Wenn du unsicher bist, ob eine Datei Schmelzgut oder operative Referenz ist,
**frag nach**, bevor du sie einschmilzt – im Zweifel bleibt sie stehen. Räum
operative Referenz höchstens auf ausdrücklichen Wunsch separat auf.

### 3. Einschmelzen: die Wissensdatei schreiben

Hol dir zuerst den Zeitstempel für den Dateinamen aus der echten Uhr, nicht aus
dem Kopf:

```bash
date +%Y-%m-%d-%H%M
```

Schreib das verdichtete Wissen nach `docs/KNOWLEDGE-<Zeitstempel>.md`. Beginne
mit einem kurzen Kopf, der die Schmelze datiert und verankert:

```markdown
# Wissensstand <YYYY-MM-DD HH:MM>
Eingeschmolzen aus docs/ (Stand git HEAD <kurzer-hash>).
```

Inhaltlich gilt: **verdichtet, aber in den Kernentscheidungen lückenlos.** Das
Ziel ist nicht die kürzeste, sondern die ehrlichste Datei – jemand soll danach
das Gesamtbild verstehen, ohne die alten Dateien je gesehen zu haben.

Das Herzstück ist die **Trennung von Metall und Schlacke**:

- **Aktuell / gültig** – der heutige Stand, die tragenden Entscheidungen, das,
  worauf man jetzt aufbaut.
- **Historisch / überholt** – verworfene Ansätze und frühere Fehlannahmen,
  klar als überholt markiert und mit einem Satz, *warum* sie fallen gelassen
  wurden. Nicht löschen, nicht beschönigen – aber so kenntlich, dass niemand sie
  versehentlich wieder für gültig hält.

Diese Trennung ist der ganze Sinn der Schmelze: Ohne sie schleppst du den Bias
nur in verdichteter Form weiter; mit ihr fällt die Schlacke sichtbar aus dem
Barren heraus.

### 4. Stopp und Review – vor jeder Löschung

Zeig dem Nutzer die fertige `docs/KNOWLEDGE-<Zeitstempel>.md` zur Prüfung,
**bevor du irgendetwas löschst**. Sag dazu, welche Dateien du als Schmelzgut
einschmelzen und danach entsorgen würdest und welche du als operative Referenz
stehen lässt.

Dann warte. Erst nach dem Go geht es weiter – das ist der Punkt, an dem die
eiserne Regel greift.

### 5. Nach dem Go: die Schlacke entsorgen

Nach der Freigabe entsorge die eingeschmolzenen Quellen, sodass unter `docs/`
genau **eine** `KNOWLEDGE-*.md` übrig bleibt – die neue – plus die als operative
Referenz bewusst stehengelassenen Dateien. Eine ältere `KNOWLEDGE-*.md` aus einer
früheren Schmelze gehört zum Schmelzgut und wird mitentsorgt.

Alles außerhalb von `docs/` bleibt unangetastet. Zum Schluss ist der Arbeitsplatz
besenrein: kein Wust mehr, kein doppelter Stand, kein mitgeschleppter Bias – nur
der frisch gegossene Wissensbarren.
