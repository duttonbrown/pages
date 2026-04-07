# Dutton Brown — Pages (GitHub Pages)

Static HTML reports and dashboards hosted via GitHub Pages.

- URL: https://duttonbrown.github.io/pages/
- Repo: https://github.com/duttonbrown/pages.git
- Branch: `main`

## Structure
- `index.html` — Landing page with cards linking to reports
- `annual-report-2025.html` — 2025 Annual Report & 2026 Outlook
- `parts-usage/` — Parts usage and sales dashboards
- `brand-site/` — Brand site design concepts

## Cross-Machine Sync
- `dbpush` — commit & push all repos (skips settings_data.json)
- `dbpull` — pull latest on all repos (auto-stashes if dirty)
- `dbs` — show status across all repos
- Script: `~/repos/db-sync.sh` | Aliases in `~/.bashrc`
- Repos synced: db-development, db-marketing, db-brand, db-operations, db-design, pages
