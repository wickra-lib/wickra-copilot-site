# Python

Native PyO3 bindings over the Rust core. Construct a `Copilot` from a JSON spec,
then drive it with `command(json) -> json`.

```bash
pip install wickra-copilot
```

```python
import json
from wickra_copilot import Copilot

spec = json.dumps({
    "symbols": ["BTCUSDT"],
    "lookback": 20,
    "facts": ["price_move", "liquidation_cluster", "funding_flip"],
})

copilot = Copilot(spec)
context = json.loads(copilot.command(json.dumps({"cmd": "build_context", "feeds": feeds})))
for fact in context["facts"]:
    print(fact["human"])
```

## More

- [PyPI](https://pypi.org/project/wickra-copilot/)
- [Source & examples](https://github.com/wickra-lib/wickra-copilot/tree/main/examples/python)
