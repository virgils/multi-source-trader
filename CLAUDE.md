# multi-source-trader

Manual/testing phase: Claude Code as an MCP client wired to three servers (Robinhood
execution, Octagon fundamentals/filings, Alpha Vantage price/technicals) for manual
financial research and trading sessions. No custom app, scheduler, or automated
guardrail code exists yet — the rules below are the only safety net.

## Trading session rules

1. NEVER call execute_trade without first calling preview_trade and showing the user
   the preview result, then getting their explicit "yes, execute" in the chat.
2. Before proposing any trade, pull data from BOTH Octagon (fundamentals/filings/news)
   AND Alpha Vantage (price/technicals) — never propose a trade using only one source.
3. If either data source fails or returns incomplete data, say so explicitly and lower
   confidence accordingly. Do not silently fill gaps from general knowledge.
4. Always state reasoning in plain terms before proposing an action: what the data
   showed, what it didn't show, and why that supports (or doesn't support) a trade.
5. Always state a confidence level (low/medium/high) for any proposed trade and why.
6. Never propose a trade sized larger than TODO_POSITION_SIZE_PERCENT% of the agentic
   account's total value. <!-- TODO: user to set this number, see TODO.md -->
7. This is a research and manual-execution session, not an autonomous agent. Nothing
   executes without explicit user confirmation in this conversation, every time.
