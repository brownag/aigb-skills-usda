# TODO

## Goal
Make `../aigb-skills` match the authoritative `aigb-skills-usda` packaged skill content and sync behavior so `make sync` in `aigb-skills-usda` is deterministic and produces no churn, while preserving tracked provenance for copied/customized skills.

## Tasks

### 1. Establish alignment baseline
- [x] Compare current `aigb-skills-usda` and `../aigb-skills` skill inventories, catalogs, and sync scripts.
- [x] Identify skills that are USDA-authoritative copies, source-only skills that must remain in `../aigb-skills`, and externally pinned skills requiring tagged refs.
- [x] Record any customizations that are being copied from USDA into `../aigb-skills` rather than transformed during sync.

### 2. Copy authoritative USDA skill content into `../aigb-skills`
- [x] For every skill present in `aigb-skills-usda`, copy the full skill directory into the matching `../aigb-skills/skills/<name>` directory.
- [x] Preserve `../aigb-skills` skills that are not present in USDA unless catalog/sync evidence shows they are obsolete.
- [x] Ensure copied skills retain proper frontmatter attribution and source/provenance metadata.

### 3. Align catalog provenance and pinned refs
- [x] Update `../aigb-skills/catalog/skills.lock.json` so USDA-authoritative copied skills use `source_repo: aigb-skills` and matching local `source_path` entries where appropriate.
- [x] Keep external tagged skills pinned to their required `source_ref` values and upstream URLs.
- [x] Avoid hardcoded per-skill special cases unless they are explicitly documented and unavoidable.

### 4. Align sync implementation for deterministic materialization
- [x] Port the USDA sync improvements into `../aigb-skills/scripts/sync-skills.js`, including metadata normalization, tag fetching, auto-clone/`--no-clone`, alias handling, and deterministic sanitization.
- [x] Ensure metadata injection does not create churn against the copied USDA-authoritative skill files.
- [x] Keep maintainer-only sync behavior separate from packaged install behavior.

### 5. Validate no-churn sync path
- [x] Run package parsing and relevant validation in both repositories.
- [x] Run `make sync` in `../aigb-skills` and verify it is stable.
- [x] Run `make sync` in `aigb-skills-usda` and verify the USDA working tree has no unintended skill churn.
- [x] Run `npm run validate:skills` and `npm run test:validate` where available.

## Notes
- For this work, `aigb-skills-usda` is the authority.
- Preferred customization strategy: copy modified/customized skill content into `../aigb-skills` and keep attribution/provenance metadata, not opaque sync-time patching.
- Special cases may exist, but they must be tracked and minimized.
- Final success is a deterministic sync that does not dirty `aigb-skills-usda`.
