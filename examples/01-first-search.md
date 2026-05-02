# Example 1 — Your First 5 Minutes

Goal: confirm the Google Flights MCP is working and feel what a Claude flight session is like.

---

## Step 1 — Start Claude in this folder

In Terminal, with this folder as your working directory:

```bash
claude
```

The first time, it'll ask you to approve `.mcp.json`. Say yes.

---

## Step 2 — Paste this prompt

```
Use the fli MCP to find the cheapest one-way DEN→LAS fare on Frontier
in the next 14 days. Tell me the date, fare, and how it compares to
the cheapest non-Frontier option on the same date.
```

---

## Step 3 — Watch what happens

Claude will:
1. Decide to call the `fli` MCP
2. Show you the tool call (you can see exactly what it asked the MCP)
3. Get real data back
4. Summarize it in plain English

If it returns numbers — you're live. The whole stack works.

---

## Step 4 — Try a follow-up

Without leaving the chat, type:

```
Now do the same for DEN→PHX, DEN→MCO, and DEN→LAX. Build me a small
markdown table.
```

Claude will run three more searches, no extra setup needed.

---

## Step 5 — Try a "build me something" prompt

```
Write a Python script `cheapest.py` that takes an origin, a destination,
and a number of days, calls the fli MCP, and prints the cheapest fare
in the window. Save it to this folder.
```

Claude will create the file. You can run it anytime in Terminal:

```bash
python3 cheapest.py DEN ATL 14
```

You just gave yourself a permanent flight-search CLI tool. That took 90 seconds.

---

## What just clicked

- You can call **live data**, mid-thought, in natural language
- You can ask Claude to **build tools you keep**, not just answer one-off questions
- Everything you do is in plain text files — version it, share it, fork it

Now go to [`02-route-report.md`](./02-route-report.md).
