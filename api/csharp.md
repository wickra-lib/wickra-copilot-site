# C#

Idiomatic .NET over the C ABI. Construct a `Copilot` from a JSON spec, then drive it
with `Command(json) -> json`.

```bash
dotnet add package WickraCopilot
```

```csharp
using WickraCopilot;

var spec = """
{"symbols":["BTCUSDT"],"lookback":20,
 "facts":["price_move","liquidation_cluster","funding_flip"]}
""";

using var copilot = new Copilot(spec);
var response = copilot.Command("""{"cmd":"build_context","feeds":{ }}""");
Console.WriteLine(response);
```

Targets .NET 8. The binding is the deterministic fact core only.

## More

- [NuGet](https://www.nuget.org/packages/WickraCopilot)
- [Source & examples](https://github.com/wickra-lib/wickra-copilot/tree/main/examples/csharp)
