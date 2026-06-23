# Otzar — The Orthodox Web Directory

A browsable directory of resources across the Orthodox & Orthodox-adjacent world —
study texts, halacha, shiurim, kashrus, heritage, and outreach — spanning many
traditions and nine interface languages (English, Hebrew, Yiddish, Russian, French,
Spanish, Portuguese, Ladino & Ge'ez).

**Live site:** _enable GitHub Pages, then put your link here_
(e.g. `https://YOURNAME.github.io/orthodox-web-directory/`)

---

## What's here

| File | What it is |
|------|------------|
| `index.html` | The directory app. Loads its data from `data/full-data.json` at runtime. |
| `data/full-data.json` | The dataset — every resource, tradition, text, and authority. **Edit this to update the directory.** |
| `data/schema.json` | The JSON Schema (Draft 2020-12) the data conforms to — the data model / contract. |
| `build_full.py` | The builder script that generates `data/full-data.json`. The source of truth for the data. |

Current dataset: **113 resources · 24 traditions · 20 texts · 35 authorities.**

---

## Viewing it

The directory is a single static page. Because `index.html` loads its data with
`fetch()`, it must be served over `http(s)://` — **not** opened by double-clicking
the local file (browsers block local file reads).

- **Hosted (recommended):** see *Publishing with GitHub Pages* below.
- **Locally, for testing:** run a tiny web server in this folder and open the address it prints:
  ```bash
  python3 -m http.server 8000
  # then visit http://localhost:8000
  ```

---

## Updating the directory

Two ways, depending on how much you're changing:

1. **Quick edit (one entry):** edit `data/full-data.json` directly, commit, push.
   The live site reflects it immediately.
2. **Larger changes (recommended):** edit `build_full.py`, then regenerate:
   ```bash
   python3 build_full.py        # rewrites data/full-data.json
   ```
   Commit both files.

> **Keep `build_full.py` as the source of truth.** If you hand-edit
> `data/full-data.json` and later re-run the builder, the builder will overwrite
> your hand edits. Make lasting changes in `build_full.py`.

### Validating before you publish

A standalone schema validator (e.g. [Ajv](https://ajv.js.org/) or Python's
`jsonschema`) can check `data/full-data.json` against `data/schema.json`.
The builder also enforces referential integrity (every tradition/text/authority
reference must resolve) when it runs.

---

## Publishing with GitHub Pages

1. Push this repository to GitHub.
2. In the repo: **Settings → Pages**.
3. Under *Build and deployment → Source*, choose **Deploy from a branch**,
   pick your branch (e.g. `main`) and the `/ (root)` folder, and save.
4. After a minute, your site is live at
   `https://YOURNAME.github.io/REPONAME/`.

**Share that Pages URL** — it shows the working directory. The repository URL
(`github.com/...`) only shows the raw code, not the running app.

---

## Accepting corrections from others

Because the data lives in a plain JSON file under version control, anyone can
propose a fix via a **pull request** (editing `data/full-data.json`), or flag
something via an **issue**. You review and merge. Each change is tracked and
reversible.

---

## Notes & caveats

- **Verification:** each resource carries a `verification.status`
  (`verified-live`, `unconfirmed`, `not-checked`, `dead`) and, where checked, a date.
  These reflect link checks at a point in time, not a permanent guarantee.
- **Sensitive categories:** emerging/returning communities (Bnei Anusim, Bnei Menashe)
  are represented as *communities and the organizations serving them*, not as
  rulings on halachic status, which are debated.
- **Coverage is uneven by design:** some groups (e.g. internet-cautious Hasidic
  dynasties) have little web presence, so their thin coverage reflects reality.
- Data quality benefits from review by people close to these communities.

---

## License

See `LICENSE`. The code is offered under the MIT License. The dataset is
descriptive/factual; please verify entries before relying on them.
