# payments-service

[![Lightwell updates](https://img.shields.io/github/issues-search?query=repo%3Aanurag-saran%2Fpayments-service%20is%3Apr%20is%3Aopen%20label%3Alightwell&label=Lightwell%20updates&color=0E4429)](https://github.com/anurag-saran/payments-service/pulls?q=is%3Apr+is%3Aopen+label%3Alightwell)

Sample Maven payments service — **demo app only** (no plugin code, no GitHub Actions workflows).

Baseline dependency: `commons-io:2.11.0`.

Lightwell remediations are opened against this repo by the plugin:

https://github.com/anurag-saran/lightwell-github-plugin-demo

**Badge:** open Lightwell PR count — click to review, then **merge** or **close**.

## Layout

- `pom.xml` / `src/` — the app

## Try the plugin

1. Go to the plugin repo → **Actions → Lightwell Remediate → Run workflow**
2. Target: `anurag-saran/payments-service`
3. Come back here → open the Lightwell PR → merge or close

## Reset after merge

Set `commons-io` back to `2.11.0` in `pom.xml` before re-running.
