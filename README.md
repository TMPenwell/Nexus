# Nexus

**An AI tutor for Excel analytics that won't give students the answer.**

🔗 **[Try it live →](https://tmpenwell.github.io/Nexus/)**

Nexus teaches nine analytics skills to MIS and business students — sorting, filtering, the Analysis ToolPak, PivotTables, INDEX/MATCH/MATCH, correlation, z-test, t-test, and regression — by walking each learner through a real IT service-desk problem *by hand* until they hit the wall, and then naming the information system that wall points to.

Built by [Tasha Penwell](https://github.com/TMPenwell) (Bytes and Bits) for QBA 1720 at Ohio University.

---

## What makes it different

**It refuses to do the math.** Nexus gives the *formula*; Excel computes the number. It will never tell a student "the average is 4.2." Students learn the tool instead of collecting answers — and an AI that never performs arithmetic can't fabricate it.

**It enforces a learning cycle.** Every lesson moves through Kolb's four stages — Concrete Experience → Reflective Observation → Abstract Conceptualization → Active Experimentation — one stage per reply. The model emits a machine-readable stage tag, and the interface reads that tag to advance a visible loop dial. The tutor cannot hand over the formula before the student has met the problem and reflected on it.

**It won't let bad statistics slide.** Read causation into a correlation and it stops you.

**Excel is the on-ramp, not the destination.** Each lesson closes by connecting the skill to the system it foreshadows: sorting is a manual `ORDER BY`, filtering a manual `WHERE`, a PivotTable a manual `GROUP BY`, and regression is where you meet Excel's honest ceiling.

---

## Files

| File | What it is |
|---|---|
| `nexus.html` | The entire tutor — one self-contained file. Runs as a web page *and* as an Excel task-pane add-in. |
| `index.html` | Redirects the repo's GitHub Pages root to `nexus.html`. |
| `manifest.xml` | Sideload this into Excel to run Nexus as an add-in. |
| `nexus-icon-*.png` | Icons referenced by the manifest. |
| `Nexus_Autograde_NotFullyTested_Penwell_COMPLETE.xlsx` | A six-sheet, Scoreboard-ready version of the exercises. **Instructor copy — answer key included.** Not yet run end-to-end through Scoreboard. |

---

## Running it

### As a web page
Open **https://tmpenwell.github.io/Nexus/**. No login, no install. Click **Download workbook**, open it in Excel, then pick a skill from the sidebar.

### As an Excel add-in
The add-in puts the tutor in a task pane beside your spreadsheet and can insert the practice data straight into your open workbook.

1. Open Excel (web or desktop) → **Add-ins** → **Advanced** → **Upload My Add-in**
2. Choose `manifest.xml` from this repo
3. **Open Nexus** appears on the Home ribbon

You sideload once; it stays on your ribbon. Clearing browser data or switching browsers means uploading it again.

---

## How it works

```
nexus.html  →  Cloudflare Worker (holds the API key)  →  Gemini
   ↑
GitHub Pages
```

The front end contains **no API key**. It calls a Cloudflare Worker that holds the key server-side, checks a shared-secret header, and only accepts requests from this site's origin. The Worker code isn't in this repo.

Anyone wanting to run their own copy needs their own Gemini API key and their own Worker; point `ENDPOINT` in `nexus.html` at it.

---

## Status

Prototype. Content is generated live, so wording varies between sessions. An occasional "high demand, try again" is the model provider, not the app.

**In development:** a "My sheet" mode that teaches on a student's own worksheet. It's visible in the sidebar but disabled — it works on clean tabular data and not on formatted trackers or templates, and that gap needs solving before it ships.

---

## Background

Nexus grew out of PhD work in instructional technology. The common worry about AI in the classroom is that it hands students answers — but that's a design choice, not a property of the technology. Nexus is an argument that an AI tutor can be built to withhold the answer and make the student do the thinking.
