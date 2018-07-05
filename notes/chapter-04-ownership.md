# Ownership

- stack vs  heaps

- what is ownership
  - Each value in Rust has a variable that’s called its owner.
  - There can only be one owner at a time.
  - When the owner goes out of scope, the value will be dropped.

- string as example

```rs
let s1 = String::from("hello");
let s2 = s1;
// What happened?
```

- s1: pt, len, capacity

- `Copy` trait, scalar value

```rs
let x = 5;
let y = x;

println!("x = {}, y = {}", x, y);
```

- ⭐️⭐️ Ownership and function

```rs
fn main() {
    let s = String::from("hello");  // s comes into scope

    takes_ownership(s);             // s's value moves into the function...
                                    // ... and so is no longer valid here

    let x = 5;                      // x comes into scope

    makes_copy(x);                  // x would move into the function,
                                    // but i32 is Copy, so it’s okay to still
                                    // use x afterward

} // Here, x goes out of scope, then s. But because s's value was moved, nothing
  // special happens.

fn takes_ownership(some_string: String) { // some_string comes into scope
    println!("{}", some_string);
} // Here, some_string goes out of scope and `drop` is called. The backing
  // memory is freed.

fn makes_copy(some_integer: i32) { // some_integer comes into scope
    println!("{}", some_integer);
} // Here, some_integer goes out of scope. Nothing special happens.
```

- return ownership: 大変だ

```rs
fn main() {
    let s1 = gives_ownership();
    let s2 = String::from("hello");
    let s3 = takes_and_gives_back(s2);

fn gives_ownership() -> String {             
    let some_string = String::from("hello"); 
    some_string
}

fn takes_and_gives_back(a_string: String) -> String { 
    a_string
}
```

- to solve this, use `references`

## References & Borrowing

```rs
fn main() {
    let s1 = String::from("hello");

    let len = calculate_length(&s1);

    println!("The length of '{}' is {}.", s1, len);
}

fn calculate_length(s: &String) -> usize {
    s.len()
}
```

- `&`: reference parameter
- `*`: dereference operator

- mutable reference: 
```rs
fn main() {
    let mut s = String::from("hello");

    change(&mut s);
}

fn change(some_string: &mut String) {
    some_string.push_str(", world");
}
```

- limitation: you can only have one mutable reference to a particular piece of data in a particular scope

```rs
// won't work
let mut s = String::from("hello");
let r1 = &mut s;
let r2 = &mut s; 
```

- At any given time, you can have either (but not both of) one mutable reference or any number of immutable references.
- References must always be valid.

## Slices

> Slices let you reference a contiguous sequence of elements in a collection rather than the whole collection

- `for (i, &item) in bytes.iter().enumerate() {`:
  - `iter` is a method that returns each element in a collection
  - `enumerate` wraps the result of `iter` and returns each element as part of a tuple instead

```rs
fn main() {
    let mut s = String::from("hello world");

    let word = first_word(&s); // word will get the value 5

    s.clear(); // this empties the String, making it equal to ""

    // word still has the value 5 here, but there's no more string that
    // we could meaningfully use the value 5 with. word is now totally invalid!
}
```
