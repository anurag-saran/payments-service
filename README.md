# payments-service

[![Lightwell updates](https://img.shields.io/github/issues-search?query=repo%3Aanurag-saran%2Fpayments-service%20is%3Apr%20is%3Aopen%20label%3Alightwell&label=Lightwell%20updates&color=0E4429)](https://github.com/anurag-saran/payments-service/pulls?q=is%3Apr+is%3Aopen+label%3Alightwell)

Sample Maven payments service (demo app only).

Baseline dependency: `commons-io:2.11.0`.

Lightwell plugin code lives in [`lightwell-github-plugin-demo`](https://github.com/anurag-saran/lightwell-github-plugin-demo). This repo only has a thin workflow that calls that plugin.

**Badge:** open Lightwell remediation PR count — click to review, then **merge** or **close**.

## Layout

- `pom.xml` / `src/` — the app
- `.github/workflows/lightwell-remediate.yml` — thin caller to the plugin repo

## Try it

1. **Settings → Actions**: allow actions, **Read and write**, allow Actions to create PRs
2. **Actions → Lightwell Remediate → Run workflow**
3. Click the badge / open the `lightwell` PR → merge or close

## Reset after merge

Set `commons-io` back to `2.11.0` in `pom.xml` before re-running.
