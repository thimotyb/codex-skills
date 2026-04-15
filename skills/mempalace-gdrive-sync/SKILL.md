---
name: mempalace-gdrive-sync
description: Indicizza memoria nel mempalace su Google Drive montato in /mnt/g usando la CLI mempalace, senza scrivere file manuali nel palace.
---

# Mempalace GDrive Sync

Usa questa skill quando l'utente chiede di salvare memoria in mempalace, fare `mine`, o sincronizzare note nel DB mempalace su Google Drive.

## Regole operative

- Non creare/modificare file dentro `/mnt/g/Il mio Drive/mempalace` (niente `.md`, `.yaml`, ecc.).
- Usa solo `mempalace ... mine ...` per integrare memoria nel DB.
- I contenuti da salvare vanno preparati nel repo locale (esempio: `notes/`).

## Workflow

1. Verifica mount e palace:

```bash
ls -la "/mnt/g/Il mio Drive/mempalace"
```

2. Esegui `mine` dalla root del progetto locale:

```bash
mempalace --palace "/mnt/g/Il mio Drive/mempalace" mine <source_dir> --mode projects --wing <wing_name> --agent codex --limit 20
```

Esempio pratico:

```bash
cd /path/to/project
mempalace --palace "/mnt/g/Il mio Drive/mempalace" mine notes --mode projects --wing my_project --agent codex --limit 20
```

3. Verifica con ricerca:

```bash
mempalace --palace "/mnt/g/Il mio Drive/mempalace" search "keyword"
```

## Note

- Se il comando fallisce per permessi, eseguire fuori sandbox o con permessi elevati per accesso a `/mnt/g`.
- Se compare `Files skipped (already filed)`, i contenuti sono già presenti nel DB (comportamento atteso).
