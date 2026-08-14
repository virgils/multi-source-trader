# Setup TODO — before this can do anything real

The MCP config and rules file are scaffolded with placeholder values. Nothing will
actually connect until these are filled in.

## Credentials (edit `.env`, never commit real values — it's git-ignored)

- [ ] `ROBINHOOD_MCP_URL` / `ROBINHOOD_API_KEY` — from your Robinhood account's
      Agentic Trading setup (Settings → Agentic Trading). Also confirm the auth
      header format Robinhood actually expects — `.mcp.json` currently assumes
      `Authorization: Bearer ${ROBINHOOD_API_KEY}`, which may need adjusting once
      real connection details are in hand.
- [ ] `OCTAGON_API_KEY` — from octagonai.co, API Keys section.

Massive needs no `.env` entry — it's the remote `https://mcp.massive.com/` server,
authenticated via OAuth. The first time Claude Code connects, it'll open a browser
prompt to log in with your Massive account and authorize access; nothing to install.

## CLAUDE.md

- [ ] Replace `TODO_POSITION_SIZE_PERCENT` in rule 6 with the real max % of account
      value for a single proposed trade.

## Verification (once credentials are real)

- [ ] Restart Claude Code / run `/mcp` so it picks up the new `.mcp.json` values.
- [ ] Complete the OAuth login prompts for Massive (and Robinhood, if it's OAuth-based
      too) when Claude Code opens them on first connect.
- [ ] Confirm all three servers show as connected (`/mcp`).
- [ ] List tools from each server; note Robinhood's exact `preview_trade` /
      `execute_trade` tool names and required parameters.
- [ ] Run the Step 3 dry run on a real ticker: Octagon + Massive + Robinhood
      position data, summarize, state confidence — no `preview_trade` or
      `execute_trade` calls in that test.
