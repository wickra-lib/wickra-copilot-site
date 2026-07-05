# WASM

A `wasm-bindgen` build for the browser and other WebAssembly runtimes. The same
`Copilot` handle and JSON command protocol as the native bindings — the sequential
path that produces byte-identical output to the parallel build.

```bash
npm install wickra-copilot-wasm
```

```javascript
import init, { Copilot } from 'wickra-copilot-wasm'

await init()

const spec = JSON.stringify({
  symbols: ['BTCUSDT'],
  lookback: 20,
  facts: ['price_move', 'liquidation_cluster', 'funding_flip'],
})

const copilot = new Copilot(spec)
const context = JSON.parse(copilot.command(JSON.stringify({ cmd: 'build_context', feeds })))
for (const fact of context.facts) console.log(fact.human)
```

The WASM binding is the deterministic fact core only; wiring an LLM on top is left to
the host page.

## More

- [npm (wickra-copilot-wasm)](https://www.npmjs.com/package/wickra-copilot-wasm)
- [Source & bindings](https://github.com/wickra-lib/wickra-copilot/tree/main/bindings/wasm)
