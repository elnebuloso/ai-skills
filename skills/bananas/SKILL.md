---
name: bananas
description: Use when the user wants to close a session, wrap up for the day, or asks if everything is clean. Trigger on phrases like "alles sauber?", "kann ich die session abschliessen?", "bin ich fertig?", "Bananenschalen?", "are we done?", "ready to close?", "wrap up", "anything left?". Run a full check of technical state and conversation loose ends before signing off.
---

# Session Cleanup — Bananenschalen-Check

Your job: find everything that could trip up a future session and report it clearly. Think of yourself as someone doing a last walk-through of a worksite before locking up.

**Announce at start:** "Ich prüfe auf herumliegende Bananenschalen 🍌 ..."

---

## What to check

### 1. Git state

```bash
git status
git stash list
git diff --stat HEAD
```

Look for:
- Uncommitted changes (staged or unstaged)
- Untracked files that look like they belong to the project
- Stashes that were forgotten
- Branches that were never pushed or merged

### 2. Tests

Run the project's test suite if one exists. A failing test left behind is a classic Bananenschale — everything looks fine until someone runs the suite in a fresh session.

If no test command is obvious, check for `package.json`, `Makefile`, `pytest.ini`, `go.mod`, etc. to find the right command.

### 3. Debug leftovers

Scan recently modified files for:
- `console.log`, `print(`, `debugger`, `TODO`, `FIXME`, `HACK`
- Hardcoded credentials or temporary values that look like placeholders

Only flag things in files that were touched in this session (use `git diff --name-only` or `git status` to identify them).

### 4. Memory

Check whether important insights from this session have been saved to memory. Think: was anything discovered that would be surprising or non-obvious to a future session that doesn't have this conversation?

Examples worth saving:
- An architectural decision that was made and why
- A constraint that isn't obvious from the code
- Something the user explicitly wanted you to remember

Don't over-save. Only things that would actually matter to a future session.

### 5. Conversation loose ends

Read back through the conversation. Look for:
- Tasks that were mentioned but never completed
- Questions that were asked but never answered
- "We should also..." statements that were left hanging
- Anything the user said they'd come back to

---

## How to report

Run all checks silently. Don't narrate the individual steps — the user doesn't need to see `git status` output or a list of files scanned. Just do the work internally and then present the result.

After checking everything, present a clear summary. Structure it like this:

**If everything is clean:**
```
✓ Alles sauber. Session kann geschlossen werden.

[1-2 sentence summary of what was accomplished]
```

Don't show the individual check results when everything is clean. Just the verdict and what got done today.

**If there are issues:**
```
Bananenschalen-Check: X Sachen gefunden

🍌 [KRITISCH] <title>
   Problem: <what it is>
   Risiko: <why it could cause problems in a future session>
   Beheben: <concrete fix suggestion>

🟡 [GERING] <title>
   Problem: <what it is>
   Risiko: <low severity explanation>
   Beheben: <concrete fix suggestion>

---
Empfehlung: Erst [die kritischen Punkte] beheben, dann session schliessen.
```

### Severity guide

**Kritisch** — would actively break things or cause confusion in a new session:
- Failing tests
- Uncommitted changes to important files
- A task that was explicitly promised but not done

**Gering** — could be annoying but won't break anything:
- A stray `console.log`
- A minor TODO in a non-critical place
- A memory item that would be nice to have but isn't essential

When in doubt, lean toward *gering*. The goal is to help, not to block.

---

## What NOT to report

- Committed, passing code — that's fine
- TODOs in files that weren't touched this session
- Missing documentation (unless the user specifically asked to write docs)
- Stylistic things that don't affect correctness
- Anything that would require significant new work to fix (flag it as "known loose end", don't mark it kritisch)

---

## After reporting

If issues were found, ask if they want help fixing them. Adapt the question to what was found:
- If there are KRITISCH items: "Soll ich die kritischen Punkte jetzt beheben?"
- If only GERING items: "Soll ich das direkt für dich erledigen?"
- If there's a mix: "Soll ich mit den kritischen Punkten anfangen?"

If everything is clean, wish the user a good break. Keep it short.

## Order of fixes in the recommendation

When writing the Empfehlung, think about logical order — not just severity order. Sometimes a GERING item needs to happen before a KRITISCH one. For example: if there are uncommitted changes (KRITISCH) and debug logs in those same files (GERING), the right order is: remove the logs first, then commit. Make the recommended order reflect actual execution order, not just severity ranking.
