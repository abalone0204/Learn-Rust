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