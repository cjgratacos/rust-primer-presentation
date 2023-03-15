# Concepts


## Variables and Mutability

- By default in Rust all variables are immutable unless explicitly configured.
- Immutable variables cannot be changed onced created.
```rust,should_panic,editable
fn main() {
    let x = 5;
    println!("The value of x is: {x}");
    x = 6;
    println!("The value of x is: {x}");
}
```
```rust,editable
fn main() {
    let mut x = 5;
    println!("The value of x is: {x}");
    x = 6;
    println!("The value of x is: {x}");
}
```

## Constants
- No mut.
- Always immutable.
- Use `const` keyword.
- Type must be annotated.
```rust
const THREE_HOURS_IN_SECONDS: u32 = 60 * 60 * 3;

```

## Shadowing
```rust,editable
fn main() {
    let x = 5;

    let x = x + 1;

    {
        let x = x * 2;
        println!("The value of x in the inner scope is: {x}");
    }

    println!("The value of x is: {x}");
}
```

## Data Types
- Integer Types:
    - 8 bit: i8,u8
    - 16 bit: i16,u16
    - 32 bit: i32,u32
    - 64 bit: i64,u64
    - 128 bit: i128,u128
    - arch: isize, usize
- Integer Literal:
    - Decimal: 98_222
    - Hex: 0xff
    - Octal: 0o77
    - Binary: 0b1111_0000
    - Byte (u8 only): b'A'
- Floating Point Types:
    - 32 bit: f32
    - 64 bit: f64
    - 128 bit: f128
    - arch: fsize
- Boolean Types:
    - true, false
- Character Types:
    - Default: UTF-8 encoded
- Compound Types:
    - Tuple Type: `let tup: (i32, f64, u8) = (500, 6.4, 1);`
    - Array Type: `let a = [1, 2, 3, 4, 5];`
- Numeric Operations:
```rust
fn main() {
    // addition
    let sum = 5 + 10;

    // subtraction
    let difference = 95.5 - 4.3;

    // multiplication
    let product = 4 * 30;

    // division
    let quotient = 56.7 / 32.2;
    let truncated = -5 / 3; // Results in -1

    // remainder
    let remainder = 43 % 5;
}
```

## Functions
```rust,editable
fn main() {
    println!("Hello, world!");

    another_function();
}

fn another_function() {
    println!("Another function.");
}
```

### Parameters
```rust,editable
fn main() {
    print_labeled_measurement(5, 'h');
}

fn print_labeled_measurement(value: i32, unit_label: char) {
    println!("The measurement is: {value}{unit_label}");
}
```
### Functions with Return Value
```rust,editable
fn five() -> i32 {
    5
}

fn main() {
    let x = five();

    println!("The value of x is: {x}");
}
```

## Comments
```rust,editable
// This is a comment
/** This is a comment **/
/// This is a special comment that gets used for documentation
```
## Control Flow

### If expression
- Rust has `if expressions`
- Rust `if` evaluations expect a `bool`, and integers will not be casted to bool.
```rust,editable
// If example
fn main() {
    let number = 3;

    if number < 5 {
        println!("condition was true");
    } else {
        println!("condition was false");
    }
}
```
```rust,should_panic,editable
// If bool requirement
fn main() {
    let number = 3;

    if number {
        println!("number was three");
    }
}
```
```rust,editable
// If-else example
fn main() {
    let number = 6;

    if number % 4 == 0 {
        println!("number is divisible by 4");
    } else if number % 3 == 0 {
        println!("number is divisible by 3");
    } else if number % 2 == 0 {
        println!("number is divisible by 2");
    } else {
        println!("number is not divisible by 4, 3, or 2");
    }
}
```
```rust,editable
// If expression example
fn main() {
    let condition = true;
    let number = if condition { 5 } else { 6 };

    println!("The value of number is: {number}");
}
```
```rust,should_panic,editable
// If expression all blocs should return the same value
fn main() {
    let condition = true;

    let number = if condition { 5 } else { "six" };

    println!("The value of number is: {number}");
}
```
### Loops
- Rust has loops.
- Loops can be expressions.
- It has `loop` for infinite loop.
```rust
fn main() {
    loop {
        println!("again!");
    }
}
```
```rust
fn main() {
    let mut counter = 0;

    let result = loop {
        counter += 1;

        if counter == 10 {
            break counter * 2;
        }
    };

    println!("The result is {result}");
}
```
- It has `while` for predicate loop.
```rust
fn main() {
    let top = 10;
    let mut counter = 0;
    while counter < top {
	println!("Counter: {counter}");
	counter += 1;
    }
}

```
- It has `for` for iterator loop.
```rust
fn main() {
    let list = [0,1,2,3,4,5,6,7,8,9];
    for element in list {
	println!("Element: {element}");
    }
}

```
- It has `break`, `label`, `continue` on blocks.
```rust
fn main() {
    let mut count = 0;
    'counting_up: loop {
        println!("count = {count}");
        let mut remaining = 10;

        loop {
            println!("remaining = {remaining}");
            if remaining == 9 {
                break;
            }
            if count == 2 {
                break 'counting_up;
            }
            remaining -= 1;
        }

        count += 1;
    }
    println!("End count = {count}");
}

```

### Match Expression
- Rust has `match expressions`
```rust
fn main() {
    let x = true;

    let result = match x {
	true => "It is True",
	false => "It is False",
    };

    println!("Result: {result}");
}
```

## Notes
- Rust contains both expressions and statements as a language. Example:
```rust
fn main() {
    let y = {
        let x = 3;
        x + 1
    }; // Expression

    println!("The value of y is: {y}");
}
```

```rust
fn main() {
    let y = 4; // Statement
    println!("The value of y is: {y}");
}
```
- Rust like any other language has reserve keywors, to learn more about the go here: [Keywords](https://doc.rust-lang.org/book/appendix-01-keywords.html).
