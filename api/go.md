# Go

A cgo wrapper over the C ABI. Construct a `Copilot` from a JSON spec, then drive it
with `Command(json) -> json`.

```bash
go get github.com/wickra-lib/wickra-copilot-go
```

```go
package main

import (
	"fmt"

	wickra "github.com/wickra-lib/wickra-copilot-go"
)

func main() {
	spec := `{"symbols":["BTCUSDT"],"lookback":20,
	  "facts":["price_move","liquidation_cluster","funding_flip"]}`

	copilot, err := wickra.New(spec)
	if err != nil {
		panic(err)
	}
	defer copilot.Close()

	context, err := copilot.Command(`{"cmd":"build_context","feeds":{}}`)
	if err != nil {
		panic(err)
	}
	fmt.Println("wickra-copilot", wickra.Version())
	fmt.Println(context)
}
```

## More

- [Go module (pkg.go.dev)](https://pkg.go.dev/github.com/wickra-lib/wickra-copilot-go)
- [Source & examples](https://github.com/wickra-lib/wickra-copilot/tree/main/examples/go)
