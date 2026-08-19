# 🧾 Diagnostics needed for Confluence → ADO Wiki Migrator support cases

When reporting an issue, please include the following information. This helps us quickly identify the root cause and reproduce the problem.

## Quick checklist

- [ ] Log file: `log_file-YYYY-MM-DD_hh.mm.ss.log`
- [ ] Log file: `turndown.log`
- [ ] Source Confluence HTML (.html) file
- [ ] Generated Markdown (.md) file
- [ ] Confluence page title (from web UI)
- [ ] Migration command (fully redacted)

---

## 1. Log files

Please attach:

* `log_file-YYYY-MM-DD_hh.mm.ss.log`
* `turndown.log`

📍 Location:
Same folder as `confluence-ado-migrator.exe`

Example:

```
log_file-2026-04-27_12.42.48.log
turndown.log
```

---

## 2. Source Confluence HTML file

Please provide the **original exported Confluence HTML file** for the affected page.

📍 Location:
Inside your `--src-path` export folder.

📄 Naming patterns:

* `<Page-Name-with-dashes>_<PageID>.html`
* or `<PageID>.html`

Example:

```
Product-Requirements_950599.html
950599.html
```

---

### How to find the Page ID

If you are unsure which file corresponds to the page:

1. Open the page in Confluence in your browser
2. Look at the URL

Example:

```
https://solidifydemo.atlassian.net/wiki/spaces/PMT/pages/950599/Template+-+Product+requirements
```

➡️ Page ID = `950599`

---

## 3. Generated Markdown (.md) file

Please include the **output Markdown file** produced by the tool.

📍 Location:
Inside your `--out-path` directory.

You may need to navigate through the generated page hierarchy, for example:

```
C:\confluence-migrator-demo\out\
  Product-Management-Team\
    pmt\
      pmt-single-attachment.md
```

---

## 4. Confluence page title (manual copy)

Please copy the **exact page title from Confluence (web UI)**.

⚠️ Important:

* Do NOT use screenshots
* Do NOT copy from HTML or local files
* Open the page in Confluence and copy the title text directly

Example:

```
Template - Product requirements
```

---

## 5. Full migration command (redacted)

Please include the exact command used to run `confluence-ado-migrator.exe`.

This is required to reproduce configuration-related issues.

### ⚠️ Security requirement (important)

Before sending, **remove or redact all secrets**:

Replace:

* Passwords → `<REDACTED>`
* API keys → `<REDACTED>`
* PAT tokens → `<REDACTED>`
* Any OAuth tokens → `<REDACTED>`

Do NOT remove parameters themselves — only the values.

---

### 💻 Example (redacted correctly)

```powershell
C:\dev\devops-migration-confluence\confluence-ado-migrator.exe `
--url "https://xxx.atlassian.net" `
--confluence-space-key "SOLIDIFY" `
--auth-method "basic" `
--username "john.doe@solidify.se" `
--password "<REDACTED>" `
--api-version "cloud" `
--src-path "C:\path\to\local\export\folder" `
--out-path "C:\path\to\target\folder" `
--license-file-path "C:\Temp\license.json" `
--confluence-space-name "Solidify Wiki" `
--ado-url "https://dev.azure.com/solidifydemo" `
--ado-project "ContosoAir" `
--ado-work-items-project "ContosoAir" `
--ado-pat "<REDACTED>" `
--ado-jira-id-field "Custom.JiraID" `
--jira-url "https://solidifydemo.atlassian.net" `
--ado-wiki-name "ContosoAir.wiki" `
--include-page-labels "y" `
--pure-markdown "n" `
--regenerate-mapping-files "n"
```

---

## Why we need this

These files let us:

* recreate the problem in an end-to-end scenario for testing
* verify Confluence source structure
