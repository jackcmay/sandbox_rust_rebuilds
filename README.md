
To reproduce:

```sh
$ cargo build
$ cargo build -p member
$ cargo build
$ cargo build -p memeber
```

For each command above the member is rebuilt, its should not be.  The root is also rebuild for each `cargo build` command.

Example output:
```
$ cargo build
    Finished dev [unoptimized + debuginfo] target(s) in 0.13s                                                                                              
$ cargo build -p member
   Compiling member v0.1.0 (sandbox_rust_rebuilds/member)                                                                          
    Finished dev [unoptimized + debuginfo] target(s) in 0.29s                                                                                              
$ cargo build
   Compiling member v0.1.0 (sandbox_rust_rebuilds/member)                                                                          
    Finished dev [unoptimized + debuginfo] target(s) in 0.38s 
```

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
