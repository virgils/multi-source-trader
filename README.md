# multi-source-trader

Claude Code, wired up as an MCP client to three servers, for manual financial research
and trading sessions:

- **Robinhood Agentic Trading** — execution (trade preview/execute, portfolio, technicals)
- **Octagon** — fundamentals, SEC filings, earnings transcripts, research
- **Alpha Vantage** — price data, technical indicators

This is the manual/testing phase: no custom app, scheduler, or automated guardrail code.
Claude Code itself, following the rules in [`CLAUDE.md`](./CLAUDE.md), is the only safety
net. A scheduled, guardrailed app may get built later, once the decision quality from
manual sessions holds up.

Right now the goal is narrower than "trade for real": this is about testing the
Robinhood MCP connection itself, using real data from Octagon and Alpha Vantage, and
seeing how Claude reasons over that data — not yet about relying on it for live trading
decisions.

## Setup

1. Copy `.env.example` to `.env` and fill in real values (see [`TODO.md`](./TODO.md) for
   exactly what's still needed). `.env` is git-ignored — never commit real keys.
2. `.mcp.json` reads credentials from those env vars via `${VAR}` substitution, so make
   sure they're exported into the shell environment Claude Code starts from.
3. Restart Claude Code (or run `/mcp`) so it picks up the servers, and confirm all three
   show as connected.

## How a trading session works

Open Claude Code in this project and ask it to research a ticker or review your
portfolio. It will pull data from Octagon and Alpha Vantage, summarize findings, and
only propose a trade (with a stated confidence level) if the rules in `CLAUDE.md` are
satisfied. It will never call `execute_trade` without first showing you a `preview_trade`
result and getting explicit confirmation in the chat.

## Status

Scaffolding only — see [`TODO.md`](./TODO.md) for the credentials and position-size
limit still needed before any server actually connects or a real dry run can be run.
