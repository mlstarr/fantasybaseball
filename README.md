# 2026 Fantasy Baseball Draft Board

Personal draft tool with FanGraphs projection import, VORP rankings, snake draft board, and Google Sheets roster sync.

---

## Setup (one time)

### 1. Clone / create the repo

```bash
git clone https://github.com/YOUR_USERNAME/fantasy-baseball-2026.git
cd fantasy-baseball-2026
```

Or just create a new private repo on GitHub and add these files.

### 2. Add your API key

Copy `config.example.js` to `config.js` and fill in your values:

```js
window.ANTHROPIC_API_KEY = 'sk-ant-...';   // from console.anthropic.com
window.GOOGLE_SHEET_ID   = '1TnyZPrijWYgdcz0J6TA-q99zVA6QlwAevXXBVm3Epro';
```

`config.js` is in `.gitignore` — it will never be committed to GitHub.

### 3. Deploy to GitHub Pages

```bash
git add index.html .gitignore README.md
git commit -m "initial deploy"
git push
```

Then in your GitHub repo:
- Go to **Settings → Pages**
- Source: **Deploy from a branch**
- Branch: `main` / `(root)`
- Save

Your app will be live at `https://YOUR_USERNAME.github.io/fantasy-baseball-2026/`

Open it locally by just double-clicking `index.html` — no server needed.

---

## Loading real projections (before draft day)

1. Go to [fangraphs.com/projections](https://www.fangraphs.com/projections)
2. Select **ATC**, stats = **Batting** → scroll to bottom → **Export Data** → save CSV
3. Repeat: **ATC** / **Pitching**
4. Repeat: **THE BAT X** / **Batting**
5. Repeat: **THE BAT X** / **Pitching**
6. Open the app → **Import Data** tab → drop each CSV into the correct box
7. Click **Apply imported data**

The app auto-maps FanGraphs column names. Player positions are pulled from the
FanGraphs data where available, falling back to the built-in sample list.

---

## Draft day workflow

1. Open `index.html` (or your GitHub Pages URL)
2. Rankings are sorted by VORP by default — filter by position, search by name
3. When a player is picked: find them in the table, use the **+ Draft** dropdown to assign to the correct manager
4. The app auto-advances the snake order and syncs the roster to Google Sheets
5. Use **Sync to Sheets** button for a full re-sync at any point
6. **Undo pick** button in the header reverses the last pick

---

## Google Sheets sync

Writes to the **Rosters** tab in your sheet. Cell mapping:

| Manager | Label col | Name col | Bat rows | Pit rows |
|---------|-----------|----------|----------|----------|
| Steven  | A         | B        | 2–13     | 15–25    |
| Matt    | E         | F        | 2–12     | 15–26    |
| Joe     | I         | J        | 2–13     | 15–26    |
| David   | M         | N        | 2–12     | 15–25    |
| Terry   | Q         | R        | 2–12     | 15–26    |
| Tim     | U         | V        | 2–13     | 15–25    |
| Ryan    | Y         | Z        | 2–12     | 15–26    |
| Josiah  | AC        | AD       | 2–13     | 15–26    |

Sync uses the Anthropic API + Google Drive MCP. Requires a valid API key in `config.js`.

---

## Updating year-to-year

- Update `KEPT` array in `index.html` with new keepers/prospects
- Update `MANAGERS` order for new draft order
- Re-export CSVs from FanGraphs each spring
- Update `window.GOOGLE_SHEET_ID` in `config.js` if you create a new sheet
