# Example 2 — Build a Real Route Report

Goal: turn a list of routes into a one-page scorecard you could show a network planning meeting.

---

## The setup

There's a sample dataset at `data/sample-routes.csv` with 20 city pairs. Treat them as routes a hypothetical airline is *considering*.

---

## The prompt

Open Claude in this folder and paste:

```
Read data/sample-routes.csv. For each route, use the fli MCP to pull:

  - cheapest one-way fare in the next 21 days
  - cheapest carrier on that fare
  - whether any legacy carrier is among carriers serving the route
    in the next 21 days

Then build me a markdown scorecard called REPORT.md with:

  - Routes ranked by cheapest published competitor fare (highest first
    = most pricing room)
  - A "Legacy Status" column: serving / not serving
  - A "Whitespace Score" 0–10 that combines: high competitor fare,
    legacy not serving, and stage length under 1500 miles
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
(closer to a typical ULCC sweet spot) and weight competitor fare 2x
heavier than route absence. Update REPORT.md.
```

Claude will iterate without redoing the data pulls (it remembers what
it already got). This is the loop where flight analysis stops being a
spreadsheet exercise and starts being a conversation.

---

## Take this further

Ask Claude to build you a synthetic route list — *"give me 30 city
pairs across the lower 48 with a mix of stage lengths, then run the
same scorecard."* You don't need a real route list to get value;
you can prototype on anything.

Next: [`03-ulcc-playbook.md`](./03-ulcc-playbook.md).
