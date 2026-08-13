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

Produces a **fat / shaded** `target/payments-service.jar` (dependencies packaged inside),
CycloneDX `target/bom.json`, and JaCoCo under `target/site/jacoco/`.

## Fast-lane demo (jackson / commons-io / httpclient)

On `main`, those three stay on community versions matching the Lightwell catalog.
A remediation PR that only bumps them typically grades **A/B** → shrink-allowed
lanes (*Just smoke-test it* / *Test the parts you use*).

`coverage-map.json` maps tests to app classes so the router can select:

| Remediation | Primary call site | Selected tests (typical) |
|-------------|-------------------|--------------------------|
| jackson-databind | `PaymentService` | `PaymentServiceTest` + `BootSmokeIT` |
| commons-io | `ReportArchive` | `ReportArchiveTest` + `BootSmokeIT` |
| httpclient | `GatewayClient` | `GatewayClientTest` + `BootSmokeIT` |

`./scripts/demo-live-cycle.sh start` bumps jackson only (cleanest fast-lane hero).

## Lightwell plugin

```text
Plugin repo → Actions → Lightwell Remediate → target anurag-saran/payments-service
```

Badge JSON lives on branch `lightwell/badge` (not `main`).

After a remediation PR merges (or any `pom.xml` change on `main`),
**Lightwell badge sync** re-scans and republishes the count so the README
badge drops to `0 available` without a manual plugin run.

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
- `coverage-map.json` — per-test coverage for fast-lane test selection
- `settings.xml.template` — Lightwell Maven credentials
- `.upgrade-delta/` — vendored upgrade-delta live pipeline (optional; for PaC)
- `.tekton/pull-request-live.yaml` — PaC trigger for live grading
- `lightwell-badge.json` — shields endpoint (published on `lightwell/badge`)
