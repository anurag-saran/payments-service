# payments-service

Sample Maven payments service used to try the **Lightwell GitHub plugin** flow.

Baseline dependency: `commons-io:2.11.0` (matches a Lightwell remediated version in the catalog).

## Try the plugin on GitHub

### One-time setup

1. Repo **Settings → Actions → General**
2. Allow Actions
3. **Workflow permissions** → **Read and write permissions** → Save

### Step 1 — Scan (preview only)

1. **Actions** → **Lightwell Scan** → **Run workflow**
2. Open the run **Summary**, or Issues → **Lightwell remediations available**
3. Review the proposed bump — **no PR yet**

Expected:

```diff
-            <version>2.11.0</version>
+            <version>2.11.0.rhlw-00001</version>
```

### Step 2 — Open PR (button)

1. **Actions** → **Lightwell Open PR** → **Run workflow**
2. Set `confirm` to `open-pr`
3. Run — creates a branch and pull request

## Layout

- `pom.xml` / `src/` — the payments service app
- `lightwell-github/` — catalog + scan/apply scripts
- `.github/workflows/` — Lightwell Scan and Lightwell Open PR

## Local dry-run

```bash
python3 lightwell-github/scan_poms.py --root .
cat lightwell-github/out/report.md
```

## Reset after a successful PR

Set `commons-io` back to `2.11.0` in `pom.xml` before re-running the demo.
