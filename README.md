# Claude Code for Airline Route Analysts

A starter kit for using **Claude Code** + a **Google Flights MCP** to analyze routes, watch competitors, model network experiments, and turn fare/availability data into decisions — fast.

Drops you into a working setup with example prompts, a sample dataset, and a pre-wired MCP server so Claude can hit Google Flights in real time.

---

## What you'll be able to do in 30 minutes

- Ask Claude *"what does the DEN→ATL fare curve look like 0–60 days out across ULCCs and legacies?"* and get a real comparison pulled live
- Drop in a CSV of routes and have Claude generate a profitability scorecard
- Build a "Saturday night special" finder for any origin
- Get an instant competitor watch on any market in any region
- Stress-test hypotheticals like *"if a ULCC added a 4x weekly DEN→PVD seasonal, what does the fare environment look like today?"*

---

## Start here

1. **First time on a Mac terminal?** Open [`SETUP-MAC.md`](./SETUP-MAC.md) — it walks you through every command in order. Don't skip steps.
2. **Already have Claude Code installed?** Skip to the **Run** section in `SETUP-MAC.md`.
3. **Want to know what to ask Claude?** Open [`PROMPTS.md`](./PROMPTS.md).
4. **Want a guided first session?** Start with [`examples/01-first-search.md`](./examples/01-first-search.md).

---

## What's in this repo

```
.
├── SETUP-MAC.md                ← do this first
├── .mcp.json                   ← pre-wires the Google Flights MCP for this folder
├── PROMPTS.md                  ← 15+ copy/paste prompts for flight analysis
├── examples/
│   ├── 01-first-search.md      ← your first 5 minutes with Claude + flight data
│   ├── 02-route-report.md      ← build a real route scorecard
│   └── 03-ulcc-playbook.md     ← ULCC-specific ideas (P2P, ancillaries, fleet)
└── data/
    └── sample-routes.csv       ← 20 mock routes to practice on
```

---

## What the MCP gives Claude

The `fli` Google Flights MCP exposes ~10 tools that Claude can call mid-conversation:

- Search one-way and round-trip fares between any two airports
- Pull date-range queries (cheapest weekday/weekend in a window)
- Filter by carrier, stop count, cabin
- Browse airports/airlines

No API key required for basic searches. (Optional SerpAPI key gives 250 free deeper searches/month.)

---

## Why Claude Code (not just chat)

- It can **read files** (CSVs, route plans, schedules)
- It can **run scripts** (Python, SQL, anything you'd hand off to a junior analyst)
- It can **call MCPs** like Google Flights mid-thought
- It can **write you new tools** as you find gaps — *"make me a script that scores 50 routes overnight"* is a real ask

The chat app is great for one-shot questions. Claude Code is for **doing work**.

---

## Credits + caveats

- MCP server: [punitarani/fli](https://github.com/punitarani/fli) (Apache-2.0)
- Live flight data is best-effort — verify anything that goes into a real decision
- This is a starter; fork it, break it, make it yours
