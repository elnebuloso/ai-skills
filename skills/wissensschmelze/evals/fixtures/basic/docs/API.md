# HTTP-API (Referenz)

| Methode | Pfad | Beschreibung |
|---------|------|--------------|
| POST | `/subscriptions` | Webhook-Endpoint registrieren |
| DELETE | `/subscriptions/{id}` | Registrierung entfernen |
| GET | `/events?since=<ts>` | Events seit Zeitstempel abrufen |

Auth: Bearer-Token im `Authorization`-Header. Tokens werden im Dashboard erzeugt.
