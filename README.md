# payments-service

[![Lightwell library updates](https://img.shields.io/endpoint?url=https%3A%2F%2Fraw.githubusercontent.com%2Fanurag-saran%2Fpayments-service%2Flightwell%2Fbadge%2Flightwell-badge.json)](https://github.com/anurag-saran/payments-service/pulls?q=is%3Apr+is%3Aopen+label%3Alightwell)

**Shared demo app** for:

1. **[Lightwell GitHub plugin](https://github.com/anurag-saran/lightwell-github-plugin-demo)** — remediates matching community deps (badge + PR)
2. **[upgrade-delta](https://github.com/anurag-saran/upgrade-delta)** — live pom bump → grade → test routing (jackson hero)

Not a production payments product. Package: `com.example.payments`.

## Build

JDK 17+.

```bash
# CI / no Lightwell credentials (Maven Central community pins):
mvn -B -Pci-community verify

# Lightwell remediated pins (public demo repos and/or settings.xml):
cp settings.xml.template settings.xml   # edit if using authenticated feed
mvn -s settings.xml clean package
```

Produces `target/payments-service.jar`, CycloneDX `target/bom.json`, and JaCoCo under `target/site/jacoco/`.

## Dependency story

| Coordinate | On `main` | Role |
|------------|-----------|------|
| `jackson-databind` | community `2.13.4` | Lightwell + upgrade-delta live bump hero |
| Spring Boot / Spring / Security / commons-io / httpclient / json-smart | `*.rhlw-*` (default) or community (`-Pci-community`) | remediated baseline |
| `json-path` `2.6.0`, `snakeyaml` `1.30` | community | upgrade-delta scorecard lanes |

Reference after-state for the jackson demo (do not commit as baseline): `pom-demo-trigger.xml`.

## Lightwell plugin

```text
Plugin repo → Actions → Lightwell Remediate → target anurag-saran/payments-service
```

Badge JSON lives on branch `lightwell/badge` (not `main`).

## upgrade-delta (live)

Vendored pipeline bundle: copy from upgrade-delta via `./scripts/sync-vendor-bundle.sh` there, then sync into this repo (or run `scripts/pull-upgrade-delta-bundle.sh` here).

```bash
# Repeatable jackson demo (opens PR; do not merge):
./scripts/demo-live-cycle.sh start
# …watch upgrade-delta-live-pr-… on the cluster…
./scripts/demo-live-cycle.sh finish
```

Details: upgrade-delta `docs/DEMO-LIVE-POM.md` (paths now refer to this repo).

## Layout

- `pom.xml` / `src/` — Spring-ish payments service with real call sites
- `settings.xml.template` — Lightwell Maven credentials
- `.upgrade-delta/` — vendored upgrade-delta live pipeline (optional; for PaC)
- `.tekton/pull-request-live.yaml` — PaC trigger for live grading
- `lightwell-badge.json` — shields endpoint (published on `lightwell/badge`)
