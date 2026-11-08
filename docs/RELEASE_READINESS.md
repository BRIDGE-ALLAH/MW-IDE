# MOONWITNESS IDE Release Readiness

This checklist is revision-specific. A checked item is supported by evidence linked below; a passing CI workflow is not a substitute for runtime, installer, security, or release acceptance.

## 1. Repository identity and governance

- [x] Public product identity, brand artwork, default themes, and application-facing labels are present.
- [x] Upstream Lapce relationship and compatibility-retained identifiers are documented.
- [x] Build instructions target the canonical MOONWITNESS IDE repository.
- [x] Repository description identifies MOONWITNESS IDE.
- [x] Repository homepage points to the canonical repository URL.
- [x] Repository topics include `code-editor`, `developer-tools`, `ide`, `moonwitness`, and `rust`.
- [x] Default branch is `main`.
- [ ] Obsolete `master` branch removed.
- [ ] Branch protection / ruleset configured for `main`.

Repository metadata was inspected on 2026-11-08. `main` is the default branch. The repository still contains `master` and `maintenance/release-safety`; all three branches are currently reported as unprotected. The available GitHub integration does not expose branch deletion or repository-settings mutation.

## 2. Source and CI verification

### Previously verified revision

- **Commit:** `a05266b779a0a929ac547a4ef1da73e1e9c0aab5`
- **Workflow:** [CI #24](https://github.com/BRIDGE-ALLAH/MW-IDE/actions/runs/42446003584)
- **Result:** completed / success
- **Jobs:** 7 of 7 succeeded

Evidence from CI #24:

- [x] Formatting and spellchecking (Ubuntu).
- [x] Clippy (Ubuntu).
- [x] Clippy (macOS).
- [x] Clippy (Windows).
- [x] Build and workspace library unit tests (Ubuntu).
- [x] Build and workspace library unit tests (macOS).
- [x] Build and workspace library unit tests (Windows).
- [x] Workspace documentation tests on all three build matrix platforms.
- [x] Windows portable-feature build.

The workflow uploaded three short-lived CI artifacts: `moonwitness-ide-ubuntu-latest`, `moonwitness-ide-macos-latest`, and `moonwitness-ide-windows-latest`. They are associated with CI #24 and the commit above; their recorded expiration is 2026-11-15. These artifacts are CI outputs, not signed installers.

### Current HEAD after CI workflow maintenance

- **Commit:** `26c8e746859d2154ed1afcb16474464ef9eb8ce3`
- The CI push trigger was narrowed to `main`; the obsolete `master` push trigger was removed.
- A fresh CI result for this new HEAD must be inspected before marking this revision CI-verified.

The earlier run #23 for commit `c3fb9e5219e31a83bb83272b5a73d4c29249b8ae` was cancelled. It is not counted as a passing run.

## 3. Local reproduction and runtime

- [ ] A maintainer independently reproduces the documented build on a clean local environment for the release revision.
- [ ] Clean-install launch smoke test completed on Linux.
- [ ] Clean-install launch smoke test completed on macOS.
- [ ] Clean-install launch smoke test completed on Windows.
- [ ] Workspace open, edit/save, LSP, terminal, source control, debug, and settings persistence exercised on supported platforms.
- [ ] Upgrade and uninstall behavior tested.

The CI build proves compilation and the tests executed by that workflow. It does not prove successful application startup, GPU compatibility, or complete editor workflows on clean target machines. No local build is claimed for commit `26c8e746859d2154ed1afcb16474464ef9eb8ce3`.

## 4. Packaging and distribution

- [ ] Tagged release-candidate workflow successfully exercised on all platforms.
- [ ] Draft archives and SHA-256 checksums downloaded and independently verified.
- [ ] Linux distribution packages / installation behavior validated.
- [ ] macOS application bundle, signing, and notarization validated.
- [ ] Windows installer and signing validated.
- [ ] App icons, file associations, desktop integration, menus, and About dialog inspected.
- [ ] User-data directories and Lapce-derived settings compatibility validated.

The release-candidate workflow is configured to build Linux, macOS, and Windows executable ZIP archives and create or update a **draft** GitHub Release. It requires a tag matching the workspace version (currently `v0.4.6`). The workflow has not yet been exercised with a release tag. It does not produce signed installers or notarized application bundles.

## 5. Security, licensing, and supply chain

- [ ] Dependency and license inventory reviewed, including transitive dependencies and bundled assets.
- [ ] Upstream notices and third-party license obligations verified for distributed packages.
- [ ] Secret scanning and dependency vulnerability checks completed.
- [ ] Threat model reviewed for plugins, remote development, terminals, and future AI integrations.
- [ ] SBOM generated and archived.
- [ ] Reproducible build or provenance approach documented and verified.

## 6. Product acceptance

- [x] README distinguishes inherited editor capabilities from roadmap directions.
- [x] Blueprint and design-system documents label planned capabilities as proposals until implemented.
- [ ] Repository intelligence features have implementation and accuracy evidence.
- [ ] Local Verification Records feature is implemented and tested end-to-end; its current specification remains **proposed**, not shipped.
- [ ] Critical editor user journeys have platform-specific runtime smoke-test evidence.
- [ ] Known limitations and upstream divergences are documented for the candidate revision.

MOONWITNESS XV services (including ARSY and LUMEN) are not treated as active integrations without separate implementation and contract evidence.

## 7. Release authorization

- [ ] All mandatory checks above completed or explicitly waived with owner and rationale.
- [ ] Version bump and changelog entry prepared for an accepted release candidate.
- [ ] Git tag created for the exact reviewed commit.
- [ ] Draft release assets and checksums verified.
- [ ] Maintainer acceptance recorded.
- [ ] Stable GitHub Release published.
- [ ] Production distribution / deployment (if applicable) verified.

**Current status: NOT RELEASE-READY.** The source at commit `a05266b` passed the seven-job CI workflow and produced three platform artifacts, making it suitable for clone-and-test evaluation. The current HEAD is `26c8e746859d2154ed1afcb16474464ef9eb8ce3` and requires its own fresh CI result. Runtime acceptance, installers/signing, security and supply-chain review, release-tag validation, branch protection, and removal of `master` remain incomplete.
