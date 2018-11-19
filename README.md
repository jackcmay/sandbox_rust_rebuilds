
To reproduce:

```sh
$ cargo build
$ cargo build -p member
$ cargo build
$ cargo build -p memeber
```

For each command above the member is rebuilt, its should not be.  The root is also rebuild for each `cargo build` command.

To get rid of the rebuild problem you can:


* Comment out the `request` dependency in the root Cargo.toml

```rust
reqwest = "0.9.0"
```

* Or remove the `env_logger` dependency in the member's Cargo.toml the member is not rebuild.

```rust
env_logger = "0.5.12"
```

* Or remove the crate type from member's Cargo.toml

```rust
[lib]
crate-type = ["cdylib"]
```
