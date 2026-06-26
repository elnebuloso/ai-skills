# Wechsel: Polling raus, Webhooks rein

Das Polling von Januar war ein Fehlgriff. In Lasttests mit 800 Clients (die
Annahme "< 100 Clients" stimmte nie) ging die DB in die Knie.

**Neue Entscheidung:** Push per Webhooks. Der Server stößt die Clients aktiv an,
sobald ein Event eintrifft. Polling ist damit komplett vom Tisch.

Folge: Wir brauchen eine Retry-Strategie für fehlgeschlagene Webhook-Zustellungen.
