# Functional Language Features

- Rust language design has taken inspiration from many functional programming languages and techniques.
- This includes `closures`, treating classes as first class citizen, etc.
- Rust been a zero cost abtraction language gives us the advantage that the high level description or code, doesn't affect performance, more on this later.

## Closures
```rust 

fn sub_one(x:i32) -> i32 {
    x - 1
}
fn main() {
    // closure that prints a text
    let print_text = || println!("Hello, World!");
    
    print_text(); 

    // Closure with parameter
    let add_one = |x| x + 1;
    let answer = add_one(41);
    println!("The answer to live is {answer}");

    // Assigning function to variable
    let operation = sub_one;

    let answer = operation(43);
    println!("The answer to live is {answer}");
}
```

```rust 
// Ways to define a function
fn  add_one_v1   (x: u32) -> u32 { x + 1 }
let add_one_v2 = |x: u32| -> u32 { x + 1 };
let add_one_v3 = |x|             { x + 1 };
let add_one_v4 = |x|               x + 1  ;
```

```rust,should_panic
// Example of code failing because attempting to call a closure whose types are inferred with two different types
// Need to define type
let example_closure = |x| x;

let s = example_closure(String::from("hello"));
let n = example_closure(5);
```
```rust 
// Example of capturing reference
fn main() {
let list = vec![1, 2, 3];
println!("Before defining closure: {:?}", list);

let only_borrows = || println!("From closure: {:?}", list);

println!("Before calling closure: {:?}", list);
only_borrows();
println!("After calling closure: {:?}", list);
}
```
```rust 
// Example of capturing mutable reference
fn main() {
let mut list = vec![1, 2, 3];
println!("Before defining closure: {:?}", list);

let mut borrows_mutably = || list.push(7);

borrows_mutably();
println!("After calling closure: {:?}", list);
}
```
```rust 
// Example of moving ownership
use std::thread;

fn main() {
    let list = vec![1, 2, 3];
    println!("Before defining closure: {:?}", list);

    thread::spawn(move || println!("From thread: {:?}", list))
        .join()
        .unwrap();
}
```
```rust 
// Example of Rust Optional unwrap or else complex moving capture values
impl<T> Option<T> {
    pub fn unwrap_or_else<F>(self, f: F) -> T
    where
        F: FnOnce() -> T
    {
        match self {
            Some(x) => x,
            None => f(),
        }
    }
}
```
```rust 
// Example of Rust list sorting
#[derive(Debug)]
struct Rectangle {
    width: u32,
    height: u32,
}

fn main() {
    let mut list = [
        Rectangle { width: 10, height: 1 },
        Rectangle { width: 3, height: 5 },
        Rectangle { width: 7, height: 12 },
    ];

    let mut num_sort_operations = 0;
    list.sort_by_key(|r| {
        num_sort_operations += 1;
        r.width
    });
    println!("{:#?}, sorted in {num_sort_operations} operations", list);
}
```

## Iterator
```rust 
// Example of iterator
let v1 = vec![1, 2, 3];

let v1_iter = v1.iter();

for val in v1_iter {
    println!("Got: {}", val);
}

```
```rust
// Example iterator next
pub trait Iterator {
    type Item;

    fn next(&mut self) -> Option<Self::Item>;

    // methods with default implementations elided
}

fn main() {
    let v1 = vec![1, 2, 3];

    let mut v1_iter = v1.iter();

    assert_eq!(v1_iter.next(), Some(&1));
    assert_eq!(v1_iter.next(), Some(&2));
    assert_eq!(v1_iter.next(), Some(&3));
    assert_eq!(v1_iter.next(), None);
}
```
```rust 
// Example of chaining methods that consume iterators
fn main() {
    let v1 = vec![1, 2, 3];

    let total: i32 = v1.iter().sum();

    assert_eq!(total, 6);
}
```
```rust 
// Example of methods that produce other iterators
fn main() {
    let v1: Vec<i32> = vec![1, 2, 3];

    let v2: Vec<_> = v1.iter().map(|x| x + 1).collect();

    assert_eq!(v2, vec![2, 3, 4]);
}
```
```rust
fn iterator() -> Vec<i32>{
    let v1: Vec<i32> = vec![1, 2, 3];

    v1.iter().map(|x| x + 1).collect()
}

fn transform() -> Vec<i32>{
    let v1: Vec<i32> = vec![1, 2, 3];

    {
        let mut result: Vec<_> = Vec::new();
        let map = |x:i32| x + 1;
        for v in v1 {
            result.push(map(v));
        }

        result
    }
}

fn main() {
    let i = iterator();
    let t = transform();
    println!("Iterator: {:?}", i);
    println!("Transform: {:?}", t);
}

```
- [Iterator](https://doc.rust-lang.org/stable/std/iter/trait.Iterator.html)
