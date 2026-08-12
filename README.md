# payments-service

[![Lightwell updates](https://img.shields.io/github/issues-search?query=repo%3Aanurag-saran%2Fpayments-service%20is%3Apr%20is%3Aopen%20label%3Alightwell&label=Lightwell%20updates&color=0E4429)](https://github.com/anurag-saran/payments-service/pulls?q=is%3Apr+is%3Aopen+label%3Alightwell)

Sample Maven payments service used to try the **Lightwell GitHub plugin**.

Baseline dependency: `commons-io:2.11.0` (matches a Lightwell remediated version in the catalog).

**Badge above:** live count of open Lightwell remediation PRs. Click it to review, then **merge** to accept or **close** to reject.

## How it works (Dependabot-style)

1. The plugin **runs automatically** (on schedule, when `pom.xml` / catalog changes, or manual run).
2. If matching Lightwell libraries are found, it **opens a PR** (label `lightwell`) with the pom bumps.
3. You see the count on the badge → click → **merge** or **close**.

## One-time setup

1. Repo **Settings → Actions → General**
2. **Allow all actions and reusable workflows**
3. **Workflow permissions** → **Read and write permissions**
4. Check **Allow GitHub Actions to create and approve pull requests**
5. Save

## Try it

1. **Actions** → **Lightwell Remediate** → **Run workflow** (or wait for schedule / pom change)
2. Click the **Lightwell updates** badge (or open **Pull requests** filtered by `label:lightwell`)
3. Review the diff, then **Merge** or **Close**

Expected pom change:

```diff
-            <version>2.11.0</version>
+            <version>2.11.0.rhlw-00001</version>
```

## Layout

- `pom.xml` / `src/` — the payments service app
- `lightwell-github/` — catalog + scan/apply scripts
- `.github/workflows/lightwell-remediate.yml` — auto scan + open/update PR

## Local dry-run

```bash
python3 lightwell-github/scan_poms.py --root .
cat lightwell-github/out/report.md
```

## Reset after a successful merge

Set `commons-io` back to `2.11.0` in `pom.xml` before re-running the demo.
