# Mac Setup — Step by Step

> Never opened Terminal before? You're about 15 minutes away from having Claude pull live flight data. Just go in order.

---

## 1. Open Terminal

Press **⌘ + Space** → type **Terminal** → press **Enter**.

A black/white window appears. That's your terminal. You type, press Enter, things happen.

---

## 2. Install Homebrew (Mac's package manager)

Copy this whole line, paste into Terminal, press Enter:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

It will:
- Ask for your Mac password (the one you use to log in). Type it — **you won't see characters appear, that's normal**. Press Enter.
- Run for 3–5 minutes. Let it finish.
- At the end it prints "Next steps" with two commands. **Copy and run those commands** — they put `brew` on your PATH so the rest of this works. (Usually it's two `echo` lines and one `eval` line.)

Verify it worked:

```bash
brew --version
```

You should see something like `Homebrew 4.x.x`. Good.

---

## 3. Install the things Claude needs

One command:

```bash
brew install python@3.12 pipx node
pipx ensurepath
```

This installs:
- **Python 3.12** — for the flight MCP
- **pipx** — Python app installer
- **Node.js** — used by some Claude tools

Close Terminal completely (**⌘ + Q**), reopen it. (This makes the new PATH take effect.)

---

## 4. Install the Google Flights MCP

```bash
pipx install 'flights[mcp]'
```

Verify:

```bash
fli-mcp --help
```

If you see a "Flight Search MCP Server" banner, it works. Press **Ctrl + C** to stop it.

---

## 5. Install Claude Code

```bash
curl -fsSL https://claude.ai/install.sh | bash
```

When it finishes, close Terminal and reopen it again.

---

## 6. Login to Claude Code

```bash
claude
```

It will print a URL. **Cmd-click** the URL (or copy it into your browser). Login with your paid Claude account. Approve. Come back to Terminal — it'll say you're logged in.

Type `/exit` to leave for now.

---

## 7. Get this repo

```bash
cd ~
git clone https://github.com/bjr909/claude-code-flight-analyst.git
cd claude-code-flight-analyst
```

---

## 8. Run

```bash
claude
```

When Claude Code starts inside this folder, it will see `.mcp.json` and ask if you trust the Google Flights MCP config. **Say yes.** From now on, Claude in this folder can call live flight tools.

**First thing to try:** open [`examples/01-first-search.md`](./examples/01-first-search.md) and paste the first prompt into Claude.

---

## If something breaks

- Claude says the MCP isn't connected → run `fli-mcp --help` in Terminal. If that errors, redo step 4.
- "command not found: brew" → you skipped the "Next steps" at the end of step 2. Re-run them.
- "command not found: claude" → close and reopen Terminal after step 5.
- Anything else → text Brett with a screenshot of the error. He'll figure it out.

---

## What you just did

You installed:
- A package manager (Homebrew)
- A Python runtime + tools (Python, pipx)
- A JavaScript runtime (Node.js)
- A live Google Flights data tool (fli-mcp)
- Claude Code (the AI agent that can use all of the above)

You can use this same setup to install practically any developer tool from now on. You're not "just" a flight analyst anymore — you have a full programming environment.
