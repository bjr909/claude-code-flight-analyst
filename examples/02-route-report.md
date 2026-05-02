# Example 2 — Build a Real Route Report

Goal: turn a list of routes into a one-page scorecard you could show a network planning meeting.

---

## The setup

There's a sample dataset at `data/sample-routes.csv` with 20 city pairs. Pretend these are routes Frontier is *considering*.

---

## The prompt

Open Claude in this folder and paste:

```
Read data/sample-routes.csv. For each route, use the fli MCP to pull:

  - cheapest one-way fare in the next 21 days
  - cheapest carrier on that fare
  - whether Frontier is among carriers serving the route in the next 21 days

Then build me a markdown scorecard called REPORT.md with:

  - Routes ranked by cheapest published competitor fare (highest first
    = most pricing room)
  - A "Frontier Status" column: serving / not serving
  - A "Whitespace Score" 0–10 that combines: high competitor fare,
    Frontier not serving, and stage length under 1500 miles
  - A short executive summary at the top: top 3 opportunities and why

Be honest about which fields you couldn't fill in.
```

---

## What you should expect

Claude will:

1. Read the CSV
2. Loop through the routes (it'll batch sensibly)
3. Make ~20 calls to fli
4. Build `REPORT.md` in this folder
5. Give you a verbal summary

Total time: ~3–5 minutes depending on the MCP rate-limit.

---

## Make it yours

Once you have REPORT.md, push back:

```
Recompute the Whitespace Score with stage length under 1000 miles
(closer to Frontier's typical sweet spot) and weight competitor fare
2x heavier than route absence. Update REPORT.md.
```

Claude will iterate without redoing the data pulls (it remembers what
it already got). This is the loop where flight analysis stops being a
spreadsheet exercise and starts being a conversation.

---

## Take this further

Replace `sample-routes.csv` with a real Frontier prospect list. Same
prompt, same workflow. You now have a repeatable analysis you can run
weekly.

Next: [`03-frontier-playbook.md`](./03-frontier-playbook.md).
