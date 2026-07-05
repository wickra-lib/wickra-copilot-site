# About Wickra Copilot

Wickra Copilot is a local market copilot grounded in real microstructure. It folds
live order-book, liquidation and funding data into a `MarketContext` — a list of
hard, numeric facts — and hands that grounding to the LLM of your choice, so an
answer to *"why did BTC just dump?"* is anchored to the real book, not vibes.

## What makes it different

- **Grounded, not generated.** A `MarketContext` is a pure function of the feed:
  price moves, order-book imbalance, liquidation clusters, funding flips, OI changes
  and volatility spikes, each with a ready-made human sentence.
- **The core is deterministic and offline.** Fact derivation has no network, no key
  and no I/O, and is byte-identical across all ten bindings and both build profiles.
  The network call lives in a separate crate.
- **LLM-agnostic, your own key.** Ollama runs fully offline; OpenAI, Claude or Gemini
  use your own key over their endpoints — or skip the LLM and read the facts directly.
  Not a hosted service, not a SaaS.
- **Read-only.** It reads market data and asks questions; it never places orders.

## Why it exists

LLMs hallucinate market state. Wickra Copilot fixes the grounding: it computes the
facts first, deterministically, then lets a model narrate them. It defines the
context surface once, in Rust, and exposes it as a JSON-over-C-ABI data API to Rust,
Python, Node.js, WASM and — over a C ABI — C, C++, C#, Go, Java and R.

## Open source

Released under the **MIT OR Apache-2.0** license — permissive, OSI-approved, free for
any use including commercial. Source, issues and releases on
[GitHub](https://github.com/wickra-lib/wickra-copilot).

## Disclaimer

Wickra Copilot is a software library, **not** a trading system, and is provided
**as-is with no warranty**. It surfaces facts and narrates them; it does not give
financial advice. Use it at your own risk.
