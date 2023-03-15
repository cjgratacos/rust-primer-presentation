# Ownership and Borrowing

- Ownership and Borrowing are one of the core concepts that makes Rust unique.
- Thanks to this concepts, Rust handles all of the memory management (allocation and deallocation) for the user with a guarantee that no data races will occur.

## Ownership

- A set of rules that govern how a Rust program manages memory
- The rules are:
    - Each value in Rust has an owner.
    - There can only be one owner at a time.
    - When the owner goes out of scope, the value will be dropped.

Examples:
```rust,should_panic
let x = "Something".to_string();
let y = x; // Ownership of String "Something" is given to variable y.
println!("x: {}", x); // This will fail because x no longer is owner of "Something".

```

```rust,should_panic
 {                      // s is not valid here, it’s not yet declared
    let s = "hello";   // s is valid from this point forward

    // do stuff with s
}                      // this scope is now over, and s is no longer valid
println!("s: {}", s); // This will fail because s is no longer in scope.
```

```rust,should_panic,editable

fn something(x: String) {
    println!("x: {}", x);
}

fn main() {
    let y = "something".to_string();
    something(y); // y ownership is given to the function something.
    println!("y: {}", y); // This will fail because y no longer is owner of "something".
}

```

- As you can see Rust handled the allocation and deallocation of the variables thanks to the ownership system.

## References and Borrowing

- A set of rules that govern how a Rust shares data.
- The rules are:
    - A value can be shared with the following rules:
	    - At any given time, you can have either one mutable reference or any number of immutable references.
	    - References must always be valid.

### Immutable References
```rust,editable
fn main() {
    let s1 = "hello".to_string();

    let len = calculate_length(&s1);

    println!("The length of '{}' is {}.", s1, len);
}

fn calculate_length(s: &String) -> usize {
    s.len()
}
```

![Memory](./imgs/trpl04-05.svg)

### Mutable References
```rust,editable
fn main() {
    let mut s = String::from("hello");

    change(&mut s);
}

fn change(some_string: &mut String) {
    some_string.push_str(", world");
}

```
```rust,should_panic,editable
    let mut s = String::from("hello");

    let r1 = &mut s;
    let r2 = &mut s;

    println!("{}, {}", r1, r2);
```
```rust,should_panic,editable
    let mut s = String::from("hello");

    let r1 = &s; // no problem
    let r2 = &s; // no problem
    let r3 = &mut s; // BIG PROBLEM

    println!("{}, {}, and {}", r1, r2, r3);

```
