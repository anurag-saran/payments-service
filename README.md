# payments-service

[![Lightwell library updates](https://img.shields.io/endpoint?url=https%3A%2F%2Fraw.githubusercontent.com%2Fanurag-saran%2Fpayments-service%2Fmain%2Flightwell-badge.json)](https://github.com/anurag-saran/payments-service/pulls?q=is%3Apr+is%3Aopen+label%3Alightwell)

Sample Maven payments service — **demo app only** (no plugin code, no GitHub Actions workflows).

Baseline dependencies (Lightwell public demo feeds):

| Tier | Coordinate | Version |
|------|------------|---------|
| validated | `commons-io:commons-io` | `2.11.0` |
| validated | `com.fasterxml.jackson.core:jackson-databind` | `2.13.4` |
| validated | `ch.qos.logback:logback-classic` | `1.2.11` |
| remediated | `org.springframework:spring-core` | `5.3.18` |
| remediated | `com.fasterxml.woodstox:woodstox-core` | `6.0.3` |

Lightwell remediations are opened against this repo by the plugin:

https://github.com/anurag-saran/lightwell-github-plugin-demo

**Badge:** number of Lightwell library updates available for this app (from the public demo catalog). Click to open the remediation PR.

## Layout

- `pom.xml` / `src/` — the app
- `lightwell-badge.json` — shields.io endpoint payload (updated by the plugin scan)

## Try the plugin

1. Go to the plugin repo → **Actions → Lightwell Remediate → Run workflow**
2. Target: `anurag-saran/payments-service`
3. Come back here → open the Lightwell PR → merge or close

## Reset after merge

Restore the baseline versions in `pom.xml` (table above) before re-running. The badge will show available updates again on the next plugin scan.
