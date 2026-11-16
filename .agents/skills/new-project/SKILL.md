---
name: new-project
description: Spawn an isolated Aurelius Software Factory project branch (project/<project-slug>) or Git worktree (~/projects/<project-slug>) with NASA FRET specs, DSPy/Z3 oracle registers, Decision Records, OMEGA approval records, and active kill-gate hooks.
---
# Aurelius New Project Spawner (`new-project`)

Use `aurelius-new-project` (`~/.local/bin/aurelius-new-project`) whenever starting a new mission module or isolated capability inside the Aurelius Mother Factory.

## Usage

### 1. Standard Branch Mode (inside `DevSec_secure-coding`)
```bash
aurelius-new-project <project-slug>
```
Creates and checks out `project/<project-slug>` cleanly off `main`.

### 2. Isolated Worktree Mode (concurrent multi-agent development)
```bash
aurelius-new-project <project-slug> --worktree
```
Creates an isolated Git worktree at `~/projects/<project-slug>` bound to branch `project/<project-slug>` off `main`.

## Scaffolded Layout

Given `<project-slug>` (normalized to snake_case `<project_slug>` for Python/Lustre identifiers):

- `src/<project_slug>/` — SEI CERT & NIST SSDF compliant Python package (`state_machine.py`)
- `tests/test_<project_slug>.py` — Formal transition obligation unit tests (`>=90%` coverage gate)
- `specs/<project_slug>.fretish` — 6-field NASA `FRETish` specifications for `fret-cli` and Z3/JKind
- `decision-records/` — Seeded Software Factory Decision Records (`DR-000-schema.yaml`, `DR-001`, `DR-004`, `DR-006`, `DR-009`)
- `registers/component-register.yaml` & `registers/oracle-catalog.yaml` — Component I/O and formal solver oracle traceability
- `.reports/` — Output directory for Bandit, Semgrep, TruffleHog, Checkov, and Trivy reports
- `omega/APPROVAL-RECORD.json` — OMEGA Authority 100 checkpoint (`CP-0`..`CP-4`) & 6-dimension Taste ratification record
- `aurelius-compliance.json` — Frozen Pydantic v2 OSCAL / CMMC Level 2 compliance manifest
- `tools/validate_registers.py` & `scripts/qa_verify.js` — Symlinked to `~/.local/share/aurelius-factory/` so `.agents/hooks.json` `PostToolUse` kill gates automatically enforce Bandit (`-lll`), register integrity, and OMEGA compliance on every file edit.

## Post-Spawn Verification Workflow

1. Formalize requirements in `specs/<project_slug>.fretish` with `fret-cli formalize '<sentence>' -l pt -lang lustre` and `.agents/dspy_factory/fret_devsecops_program.py`.
2. Run unit tests & coverage: `pytest --cov=src/<project_slug> --cov-branch --cov-fail-under=90`.
3. Run kill-gate validators: `python tools/validate_registers.py && node scripts/qa_verify.js`.
