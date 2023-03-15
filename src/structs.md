# Structs

- A struct, or structure, is a custom data type that lets you package together and name multiple related values that make up a meaningful group.

```rust
// Example of struct with name fields
struct User {
    active: bool,
    username: String,
    email: String,
    sign_in_count: u64,
}

fn build_user(email: String, username: String) -> User {
    User {
        active: true,
        username: username,
        // Example of field init
        email,
        sign_in_count: 1,
    }
}

fn main() {
    let user1 = User {
        active: true,
        username: String::from("someusername123"),
        email: String::from("someone@example.com"),
        sign_in_count: 1,
    };

    let mut user2 = User {
        active: true,
        username: String::from("someusername456"),
        email: String::from("someone@example.com"),
        sign_in_count: 1,
    };

    user2.email = String::from("anotheremail@example.com");

    let user3 = build_user(String::from("someemail@example.com"). String::from("ThisIsMe"));

    // Creating Instances from Other Instances with Struct Update Syntax
    let user4 = User {
        username: String::from("someusername789"),
        ..user3
    }
}
```

```rust
// Example of structs with anon fields
struct Color(i32, i32, i32);
struct Point(i32, i32, i32);

fn main() {
    let black = Color(0, 0, 0);
    let origin = Point(0, 0, 0);
}

```

```rust
// Example of Unit Like structs
struct AlwaysEqual;

fn main() {
    let subject = AlwaysEqual;
}
```
```rust
// Example of defining methods
struct Rectangle {
    width: u32,
    height: u32,
}

impl Rectangle {
    pub fn new(width: u32, height: u32)-> Self {
        Rectangle {
            width,
            height
        }
    }

    pub fn area(&self) -> u32 {
        self.width * self.height
    }
}

impl Rectangle {
    pub fn is_square(&self) -> bool {
        self.width == self.height
    }
}

fn main() {
    let rec = Rectangle::new(2,3);
    let area = rec.area();
    let is_square = rec.is_square();
    println!("Rectangle area: {area}");
    println!("Rectangle is square: {is_square}");
}
```
