# SBOM Vulnerability Test Fixture

⚠️ **DO NOT INSTALL.** This repository is a *static* fixture listing known-compromised
package versions, used only as input for SBOM generation and vulnerability-scanner testing.

- No code from these packages is present or executed here.
- There is intentionally **no lockfile** and **no `node_modules`**.
- `npm/yarn/pnpm install` is blocked by a `preinstall` guard and must never be run.

## Files

- `package.json` — minimal manifest (one representative version per package) for SBOM tooling
  that parses manifests statically (GitHub dependency graph, Syft, cdxgen, `npm sbom`).
- `compromised-packages.json` — plain data file listing **all** compromised versions. Inert;
  ignored by dependency-graph tooling. Use this when your scanner harness needs the full list.

## Generating an SBOM (no install required)

Manifest-based SBOM generators read `package.json` without fetching or executing anything, e.g.:

```
syft dir:. -o spdx-json
# or
cdxgen -o bom.json
```

GitHub's dependency graph parses `package.json` server-side automatically; export via
**Insights → Dependency graph → Export SBOM**.
