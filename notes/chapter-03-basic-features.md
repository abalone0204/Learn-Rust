# Chapter 3

## Variables and mutability

### Shadowing

```rust
let spaces = "   ";
let spaces = spaces.len(); // <- this is a brand new variable
```

- pros:
  - don't need to come up with different name
- cons:
  - a little bit confusing

faq: `let` vs `let mut`
  - we can assign different type, since the later ones will be a whole new variable

## Data types

- compound types
  - tuple: different type
    - `x.0`, `x.1`
    - destructuring
  - array: same type, fixed size
    - on stack, not heap
    - `x[0]`, `x[1]`

  - vector: flexible size

## Functions

- expression & return values

```rs
let y = {
    let x = 3;
    x + 1 // this is an expression
};

fn five() -> i32 {
    5
}

fn six() -> i32 {
    return 6;
}
```

```rs
fn main() {
    let x = plus_one(5);

    println!("The value of x is: {}", x);
}

fn plus_one(x: i32) -> i32 {
    x + 1; // <- this is a statement
}
```

will get this error

```
error[E0308]: mismatched types
 --> src/main.rs:7:28
  |
7 |   fn plus_one(x: i32) -> i32 {
  |  ____________________________^
8 | |     x + 1;
  | |          - help: consider removing this semicolon
9 | | }
  | |_^ expected i32, found ()
  |
  = note: expected type `i32`
             found type `()`
```

## Control flow

- must be boolean
- if, else if, else
- too many `else if` is a crap, you should consider use `match` (which will be mentioned in chapter 6)

- use with `let`

```rs
fn main() {
    let condition = true;
    let number = if condition {
        5
    } else {
        6
    };

    println!("The value of number is: {}", number);
}
```

- iteration: `iter`

```rs
fn main() {
    let a = [10, 20, 30, 40, 50];

    for element in a.iter() {
        println!("the value is: {}", element);
    }
}
```

- `Range`

```rs
fn main() {
    for number in (1..4).rev() {
        println!("{}!", number);
    }
    println!("LIFTOFF!!!");
}
```

output:
```
3!
2!
1!
LIFTOFF!!!
```


