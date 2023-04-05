# Tests

- Rust has testing ingrained inside the language, this means that Rust at its core has its own testing framework or methodology similar to Go.
- Rust by default uses its derive macro to define a test profile for compiling and running tests.
```rust
#[cfg(test)]
mod tests {
    #[test]
    fn it_works() {
        let result = 2 + 2;
        assert_eq!(result, 4);
    }
}
```
