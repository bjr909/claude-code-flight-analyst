# Prompts — Copy, Paste, Modify

Drop any of these into Claude Code (running in this folder so the Google Flights MCP is hot). Replace anything in `<angle brackets>` with your own values.

---

## 1. Route fare curve

> Pull the cheapest one-way DEN→<DESTINATION> fare for every day in the next 60 days. Group by day-of-week. Tell me which DOW has the lowest median fare and the highest. Plot ASCII bars.

## 2. Head-to-head competitor check

> For DEN→ATL on <DATE>, get the cheapest fare from each major carrier serving the route. Then do the same for the same date 7, 14, and 30 days out. Tell me where the ULCCs are undercutting and where they're leaving money on the table.

## 3. Saturday night special finder

> From DEN, find every market where the cheapest round-trip departing this Friday and returning Sunday night is under $79. Sort by price. Limit to non-stop only.

## 4. Stage-length vs price sanity check

> Search the cheapest one-way DEN→<DEST> fares for the next 30 days for these markets: <list 5–10 markets>. Compute a $/mile metric. Flag any market where pricing is dramatically above or below the $/mile median.

## 5. Day-of-week schedule pressure test

> For DEN→PHX, get the cheapest non-stop on every weekday for the next 4 weeks. If demand is strong (high prices) on Tue/Wed but weak on Sat, suggest a frequency rebalance.

## 6. Connection time profile

> For ORD→DEN→LAX over the next 7 days, what's the cheapest itinerary? Show the layover time. Flag any layover under 35 min or over 3 hr.

## 7. Seasonal swing check

> Compare cheapest DEN→MCO round-trip on three dates: 4 weeks from today, 12 weeks from today (peak summer), and 24 weeks from today (Thanksgiving week). Quantify the seasonal premium.

## 8. New-route whitespace scan

> Take the airports in `data/sample-routes.csv`. For each pair where the `legacy_serves` column says "no", search the cheapest competitor fare in the next 30 days. Surface 5 markets where the lowest published fare is over $200 — those have pricing room.

## 9. Bag-fee parity model

> Pull the cheapest DEN→LAS round-trip on a typical ULCC and a non-ULCC for next Friday return Sunday. Add a typical ULCC carry-on fee ($55) and a checked bag ($60). Compare all-in cost. Where does the ULCC still win?

## 10. Network resilience drill

> If DEN closed for 24 hours next Tuesday, which routes have the cheapest available alternative routings via DFW, ORD, or LAS? Build a CSV of swap options.

## 11. Build me a tool

> Write a Python script `route_scorecard.py` that: takes a CSV of (origin, dest) pairs, calls the fli MCP via subprocess for each, and outputs a CSV with columns: origin, dest, cheapest_30d, cheapest_carrier, days_below_$99, $/mile.

## 12. Slack-style daily digest

> Every time I run this prompt, give me a 6-bullet "morning brief" for an airline route analyst: cheapest new fares posted, biggest competitor moves on top-50 routes, and any anomaly worth watching.

## 13. ULCC vs ULCC overlap

> List 20 markets where two major US ULCCs both publish service from DEN. For each, pull their cheapest fares for the next 30 days. Compute the average gap. Which carrier is systematically pricing higher?

## 14. Subscription pass sniff test

> Some ULCCs sell an "all-you-can-fly" annual pass for ~$599 with standby-only seats. Model the ROI: pull 24 cheap DEN-out round-trips at flexible dates, compute the average cash fare being displaced, and tell me how many trips per year someone would need before the pass pays off.

## 15. Bring me your own question

> _Here's the actual decision I'm trying to make: <describe>. Help me figure out what data we'd need, pull what you can via the MCP, and tell me what's still missing._

(That last one is the real unlock — Claude is genuinely good at scoping a question, not just answering one.)

---

## Tips

- Specify dates in ISO (`2026-09-15`) — avoids ambiguity
- The MCP is rate-limited; don't ask Claude to scan 5,000 routes in one go. Batch them.
- If Claude makes something up, ask: *"did you actually call fli for that or did you guess?"* — it will tell you the truth.
- Save prompts that work into your own `my-prompts.md` file in this folder. Iterate.
