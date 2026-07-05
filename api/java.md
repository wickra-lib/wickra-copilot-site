# Java

An FFM (Panama) wrapper over the C ABI. Construct a `Copilot` from a JSON spec, then
drive it with `command(json) -> json`.

```xml
<!-- Maven Central -->
<dependency>
  <groupId>org.wickra</groupId>
  <artifactId>wickra-copilot</artifactId>
  <version>0.1.0</version>
</dependency>
```

```java
import org.wickra.copilot.Copilot;

public final class Context {
    public static void main(String[] args) {
        String spec = """
            {"symbols":["BTCUSDT"],"lookback":20,
             "facts":["price_move","liquidation_cluster","funding_flip"]}""";

        try (Copilot copilot = new Copilot(spec)) {
            String response = copilot.command("{\"cmd\":\"build_context\",\"feeds\":{}}");
            System.out.println("wickra-copilot " + Copilot.version());
            System.out.println(response);
        }
    }
}
```

The binding uses the Java Foreign Function & Memory API, so it needs JDK 22+ and
`--enable-native-access`.

## More

- [Maven Central](https://central.sonatype.com/artifact/org.wickra/wickra-copilot)
- [Source & examples](https://github.com/wickra-lib/wickra-copilot/tree/main/examples/java)
