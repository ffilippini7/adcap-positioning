# Adcap Positioning Table — GitHub Pages Website

A static website that displays the Adcap positioning/recommendation table,
powered by data from an Excel file.

---

## How It Works

```
Tabla_Positioning.xlsx  →  build.py  →  data.json  →  index.html (renders it)
```

- **`Tabla_Positioning.xlsx`** — Your source of truth (the Excel you already maintain).
- **`build.py`** — A Python script that reads the Excel and generates `data.json`.
- **`data.json`** — A lightweight JSON file the website reads.
- **`index.html`** — The website itself (no server needed, pure HTML/CSS/JS).

---

## Step-by-Step Setup

### 1. Install Prerequisites

You need **Python 3** and **Git** installed on your computer.

Install the Python library used to read Excel files:

```bash
pip install openpyxl
```

### 2. Create the GitHub Repository

1. Go to [github.com/new](https://github.com/new)
2. Name it something like `adcap-positioning`
3. Set it to **Public** (required for free GitHub Pages)
4. Click **Create repository**

### 3. Clone and Add Files

```bash
# Clone the empty repo
git clone https://github.com/YOUR_USERNAME/adcap-positioning.git
cd adcap-positioning
```

Copy ALL the files I provided into this folder:
- `index.html`
- `build.py`
- `Tabla_Positioning.xlsx`
- `.github/workflows/deploy.yml`
- `.gitignore`

### 4. Generate data.json (First Time)

```bash
python build.py
```

You should see:
```
✅ Generated data.json from Tabla_Positioning.xlsx
```

### 5. Push to GitHub

```bash
git add .
git commit -m "Initial positioning table"
git push origin main
```

### 6. Enable GitHub Pages

1. Go to your repo on GitHub → **Settings** → **Pages**
2. Under **Source**, select **GitHub Actions**
3. The workflow will run automatically on the next push

### 7. Access Your Website

After a minute or two, your site will be live at:

```
https://YOUR_USERNAME.github.io/adcap-positioning/
```

---

## How to Update (Your Weekly Workflow)

Every time you update the Excel:

```bash
# 1. Replace the Excel file in the repo folder with your updated version

# 2. Regenerate the JSON
python build.py

# 3. Push the changes
git add .
git commit -m "Update positioning 2026-04-20"
git push
```

The GitHub Action will automatically rebuild and redeploy the site.

**Even simpler**: if you just push the updated `.xlsx` file, the GitHub Action
will also run `build.py` for you automatically. But it's good practice to run
it locally first to verify the output.

---

## Customization

### Changing the Excel Structure

The `build.py` script reads from the **last sheet** in the workbook (which is
the Spanish version). If you change the row numbers or add new categories,
you'll need to update the `read_category()` calls at the bottom of `build.py`.

### Changing Visual Style

All styling is in `index.html` inside the `<style>` tag. The color scheme uses
CSS variables at the top — you can adjust them there.

---

## Troubleshooting

| Problem | Fix |
|---------|-----|
| `data.json` not found error on the website | Make sure you ran `python build.py` and committed `data.json` |
| Colors are wrong | Check the dot colors in the Excel — the script maps `#00B050` → green, `#FFC000` → yellow, `#C00000` → red |
| GitHub Pages 404 | Go to Settings → Pages and make sure Source is set to "GitHub Actions" |
| Python error `No module named openpyxl` | Run `pip install openpyxl` |
