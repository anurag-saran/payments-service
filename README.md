# payments-service

Sample Maven payments service used to try the **Lightwell GitHub plugin**.

Baseline dependency: `commons-io:2.11.0` (matches a Lightwell remediated version in the catalog).

## How it works (Dependabot-style)

1. The plugin **runs automatically** (on schedule, when `pom.xml` / catalog changes, or manual run).
2. If matching Lightwell libraries are found, it **opens a PR** with the pom bumps and explains what changed.
3. You **merge** to accept, or **close** to reject. No manual “open PR” button.

## One-time setup

1. Repo **Settings → Actions → General**
2. **Allow all actions and reusable workflows**
3. **Workflow permissions** → **Read and write permissions**
4. Check **Allow GitHub Actions to create and approve pull requests**
5. Save

## Try it

After the setup above, either wait for the automatic run or:

1. **Actions** → **Lightwell Remediate** → **Run workflow**
2. Open **Pull requests** — you should see a Lightwell remediation PR
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
