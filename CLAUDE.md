# CLI-Anything (Hardened Fork)

**Upstream:** https://github.com/HKUDS/CLI-Anything
**Pinned at:** commit `9d06841` (2026-04-08)
**Owner:** David Dinius / Make Meaning LLC

## Purpose

This is a security-hardened fork of CLI-Anything for use in AI automation consulting workflows. The core plugin was audited on 2026-04-08 and found clean. This fork adds mandatory security gating that upstream lacks.

## Key Change: HARNESS.md Security Gate

Upstream HARNESS.md does not reference SECURITY.md, so harness builders never see the security guidelines. This fork adds a mandatory security checklist before Phase 3 (Implementation) that requires:

- Reading SECURITY.md before writing any subprocess code
- Allowlist validation for all subprocess arguments
- No `shell=True`, `eval()`, `exec()`, or `os.system()`
- Input escaping for script/XML/SVG generation
- Path traversal prevention via `os.path.abspath()`

## Harness Adoption Policy

Pre-built harnesses are NOT automatically trusted. Before using any harness:

1. Audit `utils/*_backend.py` — trace every subprocess call
2. Verify no `shell=True` usage
3. Verify argument allowlisting for user-controlled params
4. Run in Docker with no host mounts and no network access
5. Only then integrate into workflows

## Upstream Sync Policy

- Do NOT track upstream main automatically
- Review upstream changes before merging
- Re-audit any harness that receives upstream updates
- Pin dependencies to specific versions
