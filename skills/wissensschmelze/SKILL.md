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

Jeder Lauf gießt einen neuen, datierten Barren: `docs/KNOWLEDGE-YYYY-MM-DD-HHMM.md`.
Der Zeitstempel im Namen hält fest, wann diese Schmelze entstanden ist. Frühere
Barren **bleiben liegen** – sie werden nie eingeschmolzen oder gelöscht. Die Kette
der datierten `KNOWLEDGE`-Dateien *ist* der chronologische Kontext: jede ein
eingefrorener Stand „so sah das Wissen damals aus". Die **jüngste** Datei ist der
gültige Stand, die älteren sind das Archiv, an dem man die Entwicklung abliest.
So bleibt der Skill beliebig oft nutzbar, ohne dass je Geschichte verloren geht.

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

Liegen bereits `KNOWLEDGE-*.md` aus früheren Schmelzen vor, sind sie deine
**wichtigste Vorzustands-Quelle**: der bereits verdichtete Stand, an dem du
ablesen kannst, was sich seitdem verändert hat. Du **liest** sie als Kontext –
aber du schmilzt sie **nicht** ein und löschst sie **nie**. Jede frühere
`KNOWLEDGE`-Datei ist ein eingefrorener Stand und bleibt als chronologisches
Archiv unverändert liegen. Deine neue Datei tritt einfach datiert daneben.

### 2. Schmelzgut von Referenz trennen

Nicht alles unter `docs/` gehört in eine Historie. Sortiere, bevor du schmilzt:

- **Schmelzgut** – das Narrativ und die Entscheidungen: wie das Projekt dahin
  kam, wo es steht; was probiert, verworfen, beschlossen wurde. Das wird
  verdichtet und danach entsorgt.
- **Operative Referenz** – Setup-Anleitungen, API-/Schnittstellen-Doku, ADRs,
  Diagramme, Runbooks. Solche Doku beschreibt keinen Weg, sondern einen
  **aktuellen Zustand zum Nachschlagen**. Sie gehört nicht in eine Historie und
  wird **nicht** mit eingeschmolzen oder gelöscht.
- **Frühere `KNOWLEDGE-*.md`** – die datierten Barren vergangener Schmelzen.
  Sie sind Vorzustand zum Lesen und zugleich das chronologische Archiv. Sie
  werden **weder eingeschmolzen noch gelöscht** und bleiben unverändert liegen.

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
einschmelzen und danach entsorgen würdest, welche du als operative Referenz
stehen lässt und welche früheren `KNOWLEDGE`-Dateien als Archiv unangetastet
liegen bleiben.

Dann warte. Erst nach dem Go geht es weiter – das ist der Punkt, an dem die
eiserne Regel greift.

### 5. Nach dem Go: das Schmelzgut entsorgen

Nach der Freigabe entsorge die eingeschmolzenen Narrativ-Quellen. Unangetastet
bleiben: die als operative Referenz stehengelassenen Dateien **und alle früheren
`KNOWLEDGE-*.md`** – die werden nie gelöscht, sie sind das chronologische Archiv.

Unter `docs/` liegen am Ende also: deine neue `KNOWLEDGE-<Zeitstempel>.md` als
jüngster, gültiger Stand, die älteren `KNOWLEDGE`-Barren daneben als Verlauf, und
die operative Referenz. Verschwunden ist nur der rohe Wust. Alles außerhalb von
`docs/` bleibt ohnehin unberührt. Besenrein heißt hier: kein roher Wust mehr, kein
mitgeschleppter Bias – aber die Geschichte bleibt lückenlos ablesbar.
