# R

A `.Call` binding over the C ABI. Construct a copilot from a JSON spec, then drive it
with `wkcopilot_command(copilot, json) -> json`.

```r
install.packages("wickracopilot", repos = "https://wickra-lib.r-universe.dev")
```

```r
library(wickracopilot)

spec <- '{"symbols":["BTCUSDT"],"lookback":20,
  "facts":["price_move","liquidation_cluster","funding_flip"]}'

copilot <- wkcopilot_new(spec)
response <- wkcopilot_command(copilot, '{"cmd":"build_context","feeds":{}}')
cat("wickra-copilot", wkcopilot_version(), "\n")
cat(response, "\n")
```

## More

- [r-universe](https://wickra-lib.r-universe.dev)
- [Source & examples](https://github.com/wickra-lib/wickra-copilot/tree/main/examples/r)
