# Error Handling

- Errors are part of life, Rust uses the `Result<T,E>` to handle recoverable errors and the macro `panic!()` for unrecoverable errors.
```rust 
enum Result<T, E> {
    Ok(T),
    Err(E),
}
```
```rust,editable
use std::fs::File;

fn main() { 
    let greeting_file_result = File::open("hello.txt");
    println!("{:?}", greeting_file_result);

    // let greeting_file = match greeting_file_result {
    //     Ok(file) => file,
    //     Err(error) => panic!("Problem opening the file: {:?}", error),
    // };

    // let result = greeting_file_result.expect("hello.txt should be included in this project");
    //let file = greeting_file_result?;

    //... process file result;
}
```
