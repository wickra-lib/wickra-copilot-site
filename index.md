---
layout: home
title: Wickra Copilot — a local market copilot grounded in real microstructure
titleTemplate: false

hero:
  name: "Wickra Copilot"
  text: "A local market copilot."
  tagline: "Grounded in real order-book, liquidation and funding microstructure — not vibes. Derive hard facts with the Wickra core, then ask any LLM (or none). LLM-agnostic, offline-first, read-only."
  image:
    src: /wickra-mark.svg
    alt: Wickra Copilot
  actions:
    - theme: brand
      text: View on GitHub
      link: https://github.com/wickra-lib/wickra-copilot
    - theme: alt
      text: Facts & spec
      link: https://github.com/wickra-lib/wickra-copilot/tree/main/docs
    - theme: alt
      text: API
      link: /api/rust

features:
  - icon: 🧭
    title: Grounded in real microstructure
    details: "A MarketContext is a list of hard, numeric facts — price moves, order-book imbalance, liquidation clusters, funding flips, OI changes, volatility spikes — each carrying a ready-made human sentence. Ask \"why did BTC just dump?\" and the answer is anchored to the real book."
  - icon: 🔌
    title: LLM-agnostic
    details: The network call lives in a separate crate. Use Ollama fully offline, or OpenAI, Claude or Gemini with your own key — or no LLM at all and read the facts directly. No vendor lock-in.
  - icon: 🔒
    title: Deterministic core, no I/O
    details: The fact-derivation core has no network, no key and no I/O — only the optional LLM adapter reaches out. The MarketContext is a pure function of the feed, byte-identical across every binding.
  - icon: 👁️
    title: Read-only, local
    details: It reads market data and asks questions; it never places orders. It runs on your own machine with your own key read from the environment — not a hosted service, not a SaaS.
  - icon: 🌲
    title: The context is data, not code
    details: A ContextSpec is a set of symbols, a lookback and the facts to derive. Because it is data, the exact same MarketContext crosses the C ABI and WASM unchanged.
  - icon: 🌐
    title: 10 languages
    details: "The core is a JSON-over-C-ABI data API (Copilot::command) in Rust, Python, Node.js, WASM, C, C++, C#, Go, Java and R, plus a command-line reference consumer."
---

<script setup>
const installTabs = [
  { label: 'Python', lang: 'bash', code: 'pip install wickra-copilot' },
  { label: 'Node',   lang: 'bash', code: 'npm install wickra-copilot' },
  { label: 'Rust',   lang: 'bash', code: 'cargo add wickra-copilot' },
  { label: 'WASM',   lang: 'bash', code: 'npm install wickra-copilot-wasm' },
  { label: 'C',      lang: 'bash', code: '# prebuilt header + library from GitHub releases:\n# github.com/wickra-lib/wickra-copilot/releases' },
  { label: 'C#',     lang: 'bash', code: 'dotnet add package WickraCopilot' },
  { label: 'Go',     lang: 'bash', code: 'go get github.com/wickra-lib/wickra-copilot-go' },
  { label: 'Java',   lang: 'xml',  code: '<!-- Maven Central -->\n<dependency>\n  <groupId>org.wickra</groupId>\n  <artifactId>wickra-copilot</artifactId>\n  <version>0.1.0</version>\n</dependency>' },
  { label: 'R',      lang: 'r',    code: 'install.packages("wickracopilot", repos = "https://wickra-lib.r-universe.dev")' },
]

const pyCode = `import json
from wickra_copilot import Copilot

spec = json.dumps({
    "symbols": ["BTCUSDT"],
    "lookback": 20,
    "facts": ["price_move", "liquidation_cluster", "funding_flip"],
})

copilot = Copilot(spec)
context = json.loads(copilot.command(json.dumps({"cmd": "build_context", "feeds": feeds})))
for fact in context["facts"]:
    print(fact["human"])`

const nodeCode = `import { Copilot } from 'wickra-copilot'

const spec = JSON.stringify({
  symbols: ['BTCUSDT'],
  lookback: 20,
  facts: ['price_move', 'liquidation_cluster', 'funding_flip'],
})

const copilot = new Copilot(spec)
const context = JSON.parse(copilot.command(JSON.stringify({ cmd: 'build_context', feeds })))
for (const fact of context.facts) console.log(fact.human)`

const cliCode = `# Build the market context and print its derived facts (deterministic, offline):
wickra-copilot context --spec golden/specs/dump.json --feeds golden/feeds

# Build the context and ask a local LLM to explain it (Ollama, no API key):
wickra-copilot ask --spec golden/specs/dump.json --feeds golden/feeds \\
  --question "Why did BTC just dump?" --provider ollama`

const snippetTabs = [
  { label: 'Python', lang: 'python',     code: pyCode },
  { label: 'Node',   lang: 'javascript', code: nodeCode },
  { label: 'CLI',    lang: 'bash',       code: cliCode },
]
</script>

## The context is JSON, not code

A `ContextSpec` names the `symbols` to inspect, a `lookback` window and the `facts`
to derive. The builder walks each symbol's feed and returns a stable, self-explaining
`MarketContext`.

```json
{
  "symbols": ["BTCUSDT"],
  "lookback": 20,
  "timeframe": "1m",
  "facts": ["price_move", "orderbook_imbalance", "liquidation_cluster", "funding_flip", "oi_change", "volatility_spike"]
}
```

Each `Fact` carries a signed `value`, a ranking `magnitude`, a timestamp and a
ready-made `human` sentence (e.g. `"BTCUSDT dropped -6.44% over the last 20 bars."`),
so the context explains itself before any LLM sees it.

## Install

The same copilot from every language — native Rust, Python, Node.js and WASM, plus
a C ABI for C, C++, C#, Go, Java and R.

<InstallTabs :tabs="installTabs" />

## Grounding first, generation second

Build the deterministic `MarketContext` from the feed, then hand it to the LLM of
your choice — or none. The `command` API returns the same bytes in every binding.

<InstallTabs :tabs="snippetTabs" />

## Built on the Wickra core

Wickra Copilot is part of the [Wickra](https://wickra.org) ecosystem. Its facts are
derived from the same typed microstructure feeds that
[`wickra-core`](https://github.com/wickra-lib/wickra) and
[`wickra-exchange`](https://github.com/wickra-lib/wickra-exchange) produce, so the
copilot reasons over exactly the numbers a backtest or a live chart would see.

> Wickra Copilot is a software library, not a trading system, and gives no financial
> advice — use at your own risk.
