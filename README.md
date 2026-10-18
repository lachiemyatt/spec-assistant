# Spec Assistant

A Claude project set up for interior architecture. Upload your products once, then ask for finish options, finish schedules, spec clauses and project admin in plain English.

The job it's built for: *"spec interior options for 9 floors"* going from a couple of days to a couple of hours, most of which is you checking and refining rather than typing.

No installs, no coding, nothing to put on your work computer. It runs in [claude.ai](https://claude.ai).

## What it's good for

- **Finish options.** Several distinct palettes per level or space (warm / neutral / bold, or budget tiers), each with a short rationale.
- **Finish schedules.** Level, room, floor / wall / ceiling / base finish codes, notes. Ready for Excel.
- **Revit-ready export.** The same schedule as a CSV whose columns match Revit's room finish parameters, so it can be pushed into the model later (see Tier 2).
- **Spec clauses.** Selections turned into clauses in your firm's own format.
- **Admin.** RFIs, consultant emails, meeting minutes and transmittals from rough notes.

It only uses products you give it. If nothing fits, it says `NO MATCH - source needed` instead of making something up.

## Set up (about 10 minutes)

1. Go to [claude.ai](https://claude.ai) and sign in (a free account works; Pro gives more room for big catalogues).
2. Open **Projects** and create a new project called *Spec Assistant*.
3. Open [`PROJECT_INSTRUCTIONS.md`](PROJECT_INSTRUCTIONS.md), copy the text in the box, and paste it into the project's **instructions**.
4. Add your products to the project's files. Either:
   - fill in [`templates/product-register.csv`](templates/product-register.csv) with your go-to products (one row per product, with a finish code like `FL-01`), or
   - upload supplier PDFs and ask it to build the register for you (there's a prompt for that in [`PROMPTS.md`](PROMPTS.md)).
5. Optional: upload your firm's schedule or spec template so it copies your format.
6. Start a chat inside the project and try a prompt from [`PROMPTS.md`](PROMPTS.md).

Tip: download the CSV templates with the **Download raw file** button on each file's page.

## Before you use it on real work

- **Check your firm's AI policy.** Some firms don't allow client project material in AI tools, some have an approved setup. If in doubt, use it with your product library and a de-identified brief.
- **Check every code it outputs** against your register. It is told never to invent products, but you are the final check.
- **Compliance is yours.** It flags slip, fire, acoustic, wet-area and accessibility items with `CHECK:` but never confirms compliance.

## Roadmap

### Tier 1: Spec Assistant (this repo, ready now)
Claude project + instructions + templates + example prompts.

### Tier 2: Excel to Revit with Dynamo (planned)
A Dynamo graph (Dynamo ships with Revit, so no add-in install) that reads the Revit export CSV, matches rows to Room Numbers, and fills each room's built-in **Floor Finish, Wall Finish, Ceiling Finish and Base Finish** parameters. Your room finish schedule fills itself. Small companion scripts in the same style: bulk sheet creation from a list, batch view renaming, room renumbering, schedule export to Excel. Always run on a copy of the model first.

### Tier 3: Talk to Revit directly (later, Revit 2027 only)
Revit 2027 includes Autodesk Assistant (tech preview), and Autodesk has released an official Revit MCP server (tech preview, June 2026) that lets Claude read and edit an open model. Promising but early: it needs Windows, IT approval and some setup, and early reviews say it is unreliable on multi-step tasks. Worth revisiting once it is out of preview.

## Files

| File | What it is |
|---|---|
| `PROJECT_INSTRUCTIONS.md` | The text you paste into the Claude project |
| `PROMPTS.md` | Example prompts for each mode |
| `templates/product-register.csv` | Your product library (replace the example rows) |
| `templates/finish-schedule.csv` | The schedule / Revit export column format |
