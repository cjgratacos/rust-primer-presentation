# Smart Pointer

- Smart pointers are data structures that act like a pointer but also have additional metadata and capabilities.
- Rust has a variety of smart pointers defined in the standard library that provide functionality beyond that provided by references.
- Example of Rust smart pointers:
    - Box<T> for allocating values on the heap
    - Rc<T>, a reference counting type that enables multiple ownership
    - Ref<T> and RefMut<T>, accessed through RefCell<T>, a type that enforces the borrowing rules at runtime instead of compile time

## Box<T>
```rust 
// Example of rust
fn main() {
    let b = Box::new(5);
    println!("b = {}", b);
}
```

```rust,should_panic
enum List {
    Cons(i32, List),
    Nil,
}
```
![List](./imgs/trpl15-01.svg)
```rust 
enum List {
    Cons(i32, Box<List>),
    Nil,
}
```
![List](./imgs/trpl15-02.svg)

```rust
// Deref with *
fn main() {
    let x = 5;
    let y = Box::new(x);

    assert_eq!(5, x);
    assert_eq!(5, *y);
}
```

## Rc<T>
- The reference counter smart pointer
![List](./imgs/trpl15-03.svg)
```rust,should_panic
enum List {
    Cons(i32, Box<List>),
    Nil,
}

use crate::List::{Cons, Nil};

fn main() {
    let a = Cons(5, Box::new(Cons(10, Box::new(Nil))));
    let b = Cons(3, Box::new(a));
    let c = Cons(4, Box::new(a));
}
```
```rust 
enum List {
    Cons(i32, Rc<List>),
    Nil,
}

use crate::List::{Cons, Nil};
use std::rc::Rc;

fn main() {
    let a = Rc::new(Cons(5, Rc::new(Cons(10, Rc::new(Nil)))));
    let b = Cons(3, Rc::clone(&a));
    let c = Cons(4, Rc::clone(&a));
}
```

# Ref<T>, RefMut<T> and RefCell<T>
- Interior mutability is a design pattern in Rust that allows you to mutate data even when there are immutable references to that data; normally, this action is disallowed by the borrowing rules.
- To mutate data, the pattern uses `unsafe` code inside a data structure to bend Rust’s usual rules that govern mutation and borrowing.
- This smart pointer enforce the borrowing rules at runtime.
```rust 
#[derive(Debug)]
enum List {
    Cons(Rc<RefCell<i32>>, Rc<List>),
    Nil,
}

use crate::List::{Cons, Nil};
use std::cell::RefCell;
use std::rc::Rc;

fn main() {
    let value = Rc::new(RefCell::new(5));

    let a = Rc::new(Cons(Rc::clone(&value), Rc::new(Nil)));

    let b = Cons(Rc::new(RefCell::new(3)), Rc::clone(&a));
    let c = Cons(Rc::new(RefCell::new(4)), Rc::clone(&a));

    *value.borrow_mut() += 10;

    println!("a after = {:?}", a);
    println!("b after = {:?}", b);
    println!("c after = {:?}", c);
}
```

