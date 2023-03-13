# Hello World

Like any other Programing language, the first step of learning is how to do a Hello world.

```sh
$ cargo new hello_world
$ cd hello_world

```

The project structure:

```sh
.
├── Cargo.toml
└── src
    └── main.rs

```

```sh
$ cargo run
   Compiling hello_world v0.1.0
    Finished dev [unoptimized + debuginfo] target(s) in 0.17s
     Running `target/debug/hello_world`
Hello, world!

```

```rust
// ./src/main.rs
fn main() {
    println!("Hello, world!");
}

```
