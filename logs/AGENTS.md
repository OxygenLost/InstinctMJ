# Agent Guide - Logs

## Scope

- This guide applies to `logs/**`.

## Rules

- Treat run directories under `logs/instinct_rl/**` as generated artifacts; do not rename, rewrite, or delete them unless the user explicitly asks.
- Keep human-facing configuration notes in `logs/README.md` instead of scattering the information across ad-hoc comments.
- Do not document local checkpoint filenames or local weight paths here unless the user explicitly asks; pretrained weights are expected to be distributed externally (for example via Google Drive).
- When the maintained configuration for a task changes, update `logs/README.md` with the new config snapshot paths and config highlights.
- When documenting released policies, prefer a runnable `instinct-play` command template over local run-directory notes.
- If another README needs to point people to a maintained setup, prefer linking back to `logs/README.md` so there is a single source of truth.
