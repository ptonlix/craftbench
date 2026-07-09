# BeeWeave Vault

This directory is the compiled knowledge layer of the monorepo.

Keep polished, reusable knowledge here: concepts, entities, procedures,
references, synthesis pages, project knowledge, and journal entries. Drafting and
article composition belong in `../workbench/`.

## Fixed Layout

- `concepts/` — abstract ideas, theories, mental models.
- `entities/` — concrete things: tools, projects, people, organizations.
- `skills/` — how-to knowledge and procedures, not Agent Skill source code.
- `references/` — source records, article batches, papers, factual references.
- `synthesis/` — cross-cutting analysis across multiple pages or sources.
- `journal/` — time-bound notes and periodic reflections.
- `projects/` — project-scoped knowledge.
- `_raw/` — quick-capture staging area before promotion into proper pages.
- `_archives/` — snapshots created by rebuild/restore flows.
- `_staging/` — review queue when staged writes are enabled.
- `.obsidian/` — Obsidian app configuration.

Run the wiki skills to initialize or maintain the operational files:

- `index.md`
- `log.md`
- `hot.md`
- `.manifest.json`

The default `BEEWEAVE_VAULT_PATH` in `.env.example` points here with `./vault`;
`setup.sh` expands that to an absolute path when it writes global config.
