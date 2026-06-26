# Lokales Setup (Referenz)

1. `docker compose up -d` startet Postgres und den CDC-Connector.
2. `make seed` lädt Beispieldaten.
3. `make run` startet den Import-Worker.

Env-Variablen siehe `.env.example`.
