# Memory

### The Stack

- The stack is very fast, and is where memory is allocated in Rust by default. 
- But the allocation is local to a function call, and is limited in size.

Example:

```rust
fn foo() {
    println!("This is foo!");
}

fn main() {
    let x = 42; // This will be allocated in the stack.
    foo(); // This function stack will be allocated in the stack.
}

```


### The Heap

- The heap, on the other hand, is slower, and is explicitly allocated by your program.
- But it’s effectively unlimited in size, and is globally accessible. 
- Note this meaning of heap, which allocates arbitrary-sized blocks of memory in arbitrary order.
- Values can be boxed (allocated on the heap) by creating a Box<T>. 
- A box is a smart pointer to a heap allocated value of type T. 
- When a box goes out of scope, its destructor is called, the inner object is destroyed, and the memory on the heap is freed.

Boxed values can be dereferenced using the * operator; this removes one layer of indirection.

Example:
```rust
fn main() {
    let x = Box::new(5); // This will be allocated in the heap.
    let func: Box<dyn Fn(usize)> = Box::new(|x| {
        println!("x: {}", x);
    }); // This anonymous function will be stored in the heap.

    func(5); // The function will be run from the heap by a reference on the stack.
}

```

<script defer class="speakerdeck-embed" data-id="760299e421d649f985d5b04952dcc4f2" data-ratio="1.77777777777778" src="//speakerdeck.com/assets/embed.js"></script>

