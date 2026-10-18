# Spec Assistant

A Claude project set up for interior architecture. Upload your products once, then ask in plain English for finish options, finish schedules, spec clauses, QA checks, revision change logs and supplier quote emails.

The job it's built for: *"spec interior options for 9 floors"* going from a couple of days to a couple of hours, most of which is you checking and refining rather than typing.

No installs, no coding, nothing to put on your work computer. It runs in [claude.ai](https://claude.ai).

## What it's good for

| Ask it to... | You get |
|---|---|
| **Give me options** | Distinct finish palettes per level or space (warm / neutral / bold, or budget tiers), each with a short rationale |
| **Make a schedule** | Level, room, floor / wall / ceiling / base finish codes and notes, ready for Excel |
| **Revit export** | The same schedule as a CSV whose columns match Revit's room finish parameters (see Tier 2) |
| **Read these supplier sheets** | New product register rows pulled from PDFs or links, with every missing value marked `not stated` so you know what to ask the supplier |
| **QA check** | Schedule vs register vs spec vs programme: unknown codes, unspecified items, non-wet-rated products in wet rooms, floors with no slip rating, lead times that blow the programme |
| **What changed?** | A change log between two schedule revisions plus a draft transmittal note |
| **Quote emails** | The schedule grouped by supplier, with one quote / lead time / samples email per supplier |
| **Write the spec** | Selections turned into clauses in your firm's own format |
| **Admin** | RFIs, consultant emails, meeting minutes and transmittals from rough notes |

It only uses products you give it. If nothing fits, it says `NO MATCH - source needed` instead of making something up.

## Try it in 2 minutes

The [`examples/`](examples) folder is a small fake project (3 levels, 12 products, two schedule revisions, a spec extract and a supplier sheet) with some deliberate mistakes planted in it. After setting up the project below, upload everything in `examples/` and ask:

> Run a QA check on rev B against the register, spec and programme.

It should catch a code that isn't in the register, a timber floor in a bathroom, a feature wall panel with a 16 week lead time on a 10 week ordering window, an item scheduled with no spec clause, and a spec item that isn't in the schedule.

Then try *"What changed between rev A and rev B?"* and *"Draft quote request emails to each supplier for everything in rev B."*

When you're done, delete the example files from the project and upload your own.

## Set up (about 10 minutes)

1. Go to [claude.ai](https://claude.ai) and sign in (a free account works; Pro gives more room for big catalogues).
2. Open **Projects** and create a new project called *Spec Assistant*.
3. Open [`PROJECT_INSTRUCTIONS.md`](PROJECT_INSTRUCTIONS.md), copy the text in the box, and paste it into the project's **instructions**.
4. Add your products to the project's files. Either:
   - fill in [`templates/product-register.csv`](templates/product-register.csv) with your go-to products (one row per product, with a finish code like `FL-01`), or
   - upload supplier PDFs and ask it to build the register for you (there's a prompt for that in [`PROMPTS.md`](PROMPTS.md)).
5. Optional: upload your firm's schedule or spec template so it copies your format.
6. Start a chat inside the project and try a prompt from [`PROMPTS.md`](PROMPTS.md).

Tip: download any file here with the **Download raw file** button on its page.

## Before you use it on real work

- **Check your firm's AI policy.** Some firms don't allow client project material in AI tools, some have an approved setup. If in doubt, use it with your product library and a de-identified brief.
- **Check every code and value it outputs** against your register and the supplier's sheet. It is told never to invent products or ratings, but you are the final check.
- **Compliance is yours.** It flags slip, fire, acoustic, wet-area and accessibility items with `CHECK:` but never confirms compliance. The QA check is a second pair of eyes, not a sign-off.

## Roadmap

### Tier 1: Spec Assistant (this repo, ready now)
Claude project instructions, nine modes, example prompts, templates and a sample project.

### Tier 2: Round trip with Revit via Dynamo (planned)
Two Dynamo graphs (Dynamo ships with Revit, so no add-in install):
- **Export rooms:** pulls level, number, name and area for every room to a CSV, so the assistant works from the real model (and can calculate quantities for quote emails).
- **Import finishes:** reads the Revit export CSV and fills each room's **Floor Finish, Wall Finish, Ceiling Finish and Base Finish** parameters, plus custom ones such as per-elevation wall finishes. It runs in **preview mode** first, writing a "here's what would change" file, and only writes to the model when you confirm.

The result: "palette B for levels 2 to 9" in Claude, two clicks in Revit, and the finish schedule and room tags update across every floor. Always run on a copy of the model first.

### Tier 3: Talk to Revit directly (later, Revit 2027 only)
Revit 2027 includes Autodesk Assistant (tech preview), and Autodesk has released an official Revit MCP server (tech preview, June 2026) that lets Claude read and edit an open model. Promising but early: it needs Windows, IT approval and some setup, and early reviews say it is unreliable on multi-step tasks. Worth revisiting once it is out of preview.

## Files

| File | What it is |
|---|---|
| `PROJECT_INSTRUCTIONS.md` | The text you paste into the Claude project |
| `PROMPTS.md` | Example prompts for each mode |
| `templates/product-register.csv` | Your product library (replace the example rows) |
| `templates/finish-schedule.csv` | The schedule / Revit export column format |
| `examples/` | A small fake project with planted mistakes, for trying it out |
