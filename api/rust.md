# Rust

The native crate. Fold a `ContextSpec` over a feed with `build_context`, or drive a
`Copilot` handle with the JSON command protocol every other binding uses.

```bash
cargo add wickra-copilot
```

```rust
use copilot_core::{build_context, ContextSpec, FeedSnapshot};
use std::collections::BTreeMap;

let spec = ContextSpec::from_json(SPEC).expect("valid spec");

let mut feeds: BTreeMap<String, FeedSnapshot> = BTreeMap::new();
// ... fill `feeds` with each symbol's candles / book / liquidation / funding data ...

let context = build_context(&feeds, &spec).expect("build_context");
for fact in &context.facts {
    println!("{}", fact.human);
}
```

## More

- [crates.io/crates/wickra-copilot](https://crates.io/crates/wickra-copilot) · [docs.rs](https://docs.rs/wickra-copilot)
- [Source & examples](https://github.com/wickra-lib/wickra-copilot/tree/main/examples/rust)
- [Facts & spec](https://github.com/wickra-lib/wickra-copilot/tree/main/docs)
