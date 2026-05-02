# Example 3 — The Frontier Playbook

ULCC-flavored exercises. Frontier's economics are different from Delta or United, and the prompts here lean into that: ancillary revenue, P2P over hub-and-spoke, A321neo gauge changes, GoWild dynamics, and head-to-head with Spirit and Allegiant.

Each section is a real prompt you can paste into Claude. They build on each other but are independently runnable.

---

## A. The all-in fare reality check

Frontier's headline fares look amazing until you add bags + seats. Test it.

```
For DEN→LAS round-trip departing this Friday and returning Sunday,
pull the cheapest fare on:
  - Frontier
  - Spirit
  - Southwest
  - United basic economy

Then add a "realistic ULCC trip" surcharge: $55 carry-on, $50 seat
assignment, $60 checked bag (each way) for Frontier and Spirit.
Southwest gets 2 free bags. United basic gets 1 free carry-on
but no seat selection.

Build a markdown table comparing all-in cost. Tell me which carrier
wins on price for: (1) a no-bag traveler, (2) a typical leisure
traveler with one carry-on and one checked, (3) a family of 3
that wants to sit together.
```

The point: the analyst's instinct ("we're cheapest") and the customer's
math ("the all-in is $40 higher") are often different stories. Force the
spreadsheet to admit both.

---

## B. Frontier vs Spirit — head-to-head map

```
List 25 markets where both Frontier and Spirit publish service from
DEN. For each, pull the cheapest one-way fare in the next 30 days
on each carrier. Build a CSV `den-overlap.csv` with columns:
origin, dest, frontier_fare, spirit_fare, gap, gap_pct, advantage.

After building, give me a verbal summary:
  - In how many markets is Frontier cheaper?
  - What's the median gap?
  - Are there markets where the gap is > 30% in either direction?
    (those are the ones with pricing rationality questions)
```

This is the kind of report that, if it came out of Excel, would take
two hours. From Claude + fli, ~5 minutes.

---

## C. GoWild Pass break-even model

Frontier's GoWild Pass is the most ULCC thing they've ever done. Model whether it actually pays for a sample customer.

```
The GoWild Annual Pass is ~$599. Holders fly standby on any open
seat for $0.01 + taxes (about $15 round-trip after fees and taxes
on average).

Pretend a holder takes 2 round-trips per month, varied DEN-out
markets. Pull cheapest cash fares for 24 sample DEN round-trips
over the next 6 months (mix of weekday and weekend, mix of stage
length). Compute:

  - Average cash fare for a comparable booking
  - Total cash equivalent for 24 trips
  - GoWild break-even (how many trips before pass pays off)
  - The "regret factor": how often the fare was already so low
    ($59 or less) that GoWild barely saves anything

Build a verdict: who is GoWild actually a good deal for?
```

This is the kind of thing that should go on someone's whiteboard.

---

## D. The A321neo gauge experiment

Frontier swapping from A320neo (186 seats) to A321neo (240 seats) on a route is a meaningful capacity move. Use fares as a proxy for demand strength.

```
For these 10 candidate routes — DEN→<destinations from
data/sample-routes.csv> — pull average cheapest fare across the
next 30 days. Mark routes where the average is over $129 as
"demand looks strong" candidates for an A321 upgauge.

Then pull the same average for Spirit on the matching markets.
If Spirit's average is also strong, that supports the upgauge thesis.
If only Frontier's is strong, it might just be us being underpriced
elsewhere — flag those for a fare strategy review before any gauge
decision.
```

You're using public data as a directional signal, not a substitute
for revenue management. Make sure to say that to Claude when you
hand it off — it'll caveat properly.

---

## E. Build me a daily ULCC pulse

```
Write a Python script `ulcc_pulse.py` that I can run each morning.
It should:

  1. Hit fli for the cheapest one-way fare today (and 7d, 14d) on:
     - DEN→LAS, DEN→MCO, DEN→ATL, DEN→PHX, DEN→LAX, DEN→ORD
     - For each, on Frontier, Spirit, and the cheapest legacy carrier.
  2. Compare against a saved baseline (CSV of yesterday's pulls).
  3. Flag any fare that moved more than +/- $20 vs yesterday.
  4. Print a 10-line "morning brief" to the terminal.
  5. Save today's pulls as the new baseline.

Make the script idempotent. Save it in this folder.
```

Now you have a daily standup tool that runs in 30 seconds and
tells you what the market did overnight. Show it to your director
on Monday. Watch their face.

---

## F. The bring-your-own-question prompt

The unlock isn't any specific prompt — it's that you can scope a real
decision in plain English, hand Claude the data sources you trust,
and iterate. Try this one:

```
Here's the actual decision I'm working on this week:

  <write 2–3 sentences about a real route question you have>

What public-data signals would help? What could we pull via the fli
MCP right now? What's still missing that would need internal data?
Build a quick analysis with what's available and tell me the
confidence level.
```

That last bit — *"tell me the confidence level"* — is the prompt
discipline that turns Claude from a fast intern into a useful analyst.

---

## What you should walk away with

- A library of prompts that match how you actually think
- 1–2 scripts in this folder you can run any morning
- A clear sense of where Claude is genuinely useful vs where it
  needs your judgment to land the plane

Save your best prompts back to `PROMPTS.md` (or a new `MY-PLAYBOOK.md`)
and treat this folder like your personal workshop.
