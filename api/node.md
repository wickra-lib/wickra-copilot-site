# Node.js

Native napi-rs bindings over the Rust core. Construct a `Copilot` from a JSON spec,
then drive it with `command(json) -> json`.

```bash
npm install wickra-copilot
```

```javascript
import { Copilot } from 'wickra-copilot'

const spec = JSON.stringify({
  symbols: ['BTCUSDT'],
  lookback: 20,
  facts: ['price_move', 'liquidation_cluster', 'funding_flip'],
})

const copilot = new Copilot(spec)
const context = JSON.parse(copilot.command(JSON.stringify({ cmd: 'build_context', feeds })))
for (const fact of context.facts) console.log(fact.human)
```

## More

- [npm](https://www.npmjs.com/package/wickra-copilot)
- [Source & examples](https://github.com/wickra-lib/wickra-copilot/tree/main/examples/node)
