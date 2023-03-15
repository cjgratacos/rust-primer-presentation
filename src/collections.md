# Collections

- Rust’s standard library includes a number of very useful data structures called collections. [Collection Standard Library](https://doc.rust-lang.org/std/collections/index.html)
- Rust most common collections are `vector`(similar to array or list on other languages), `string`, and `map`, but there are many more.
```rust
// Immutable
let v: Vec<i32> = Vec::new();
// Macro
let v = vec![1, 2, 3];
// Mutable
let mut v = Vec::new();

v.push(5);
v.push(6);
v.push(7);
v.push(8);
```
```rust
 // Example of reading vector
 let v = vec![1, 2, 3, 4, 5];

let third: &i32 = &v[2];
println!("The third element is {third}");

let third: Option<&i32> = v.get(2);
match third {
    Some(third) => println!("The third element is {third}"),
    None => println!("There is no third element."),
}
```
```rust,should_panic
// Example of bad logic
let v = vec![1, 2, 3, 4, 5];

let does_not_exist = &v[100];
let does_not_exist = v.get(100);

```
```rust
// Example of ownership with vectors
let mut v = vec![1, 2, 3, 4, 5];

let first = &v[0];

v.push(6);

println!("The first element is: {first}");
```
```rust
// Example of iterating over vector
let v = vec![100, 32, 57];

for i in &v {
    println!("{i}");
}

for i in v.iter() {
    println!("{i}");
}
```
```rust
// Using enums to store multiple types
enum SpreadsheetCell {
    Int(i32),
    Float(f64),
    Text(String),
}

let row = vec![
    SpreadsheetCell::Int(3),
    SpreadsheetCell::Text(String::from("blue")),
    SpreadsheetCell::Float(10.12),
];
```
```rust 
// How vector drops its elements
{
    let v = vec![1, 2, 3, 4];

    // do stuff with v
} // <- v goes out of scope and is freed here
// Drop happens from first to last element, aka from left to right
```

