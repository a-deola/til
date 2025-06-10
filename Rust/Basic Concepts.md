### Variables and Immutability
#### Variables
Variables in rust are immutable by default

```rust
let x = 5;  // immutable
let mut y = 6;  // mutable
```
#### Constants 
Constants are values bound to a name that are immutable by default, `mut` can't be used on them and the type of value must be annotated.
```rust
const TIME_IN_SECONDS: u32 = 60 * 60
```
#### Shadowing 
A variable can be shadowed when redeclared with the let keyword and assigned a new value, this new value overshadows the first.

```rust
fn main() {
    let x = 5; // x = 5

    let x = x + 1; // x = 6

    {
        let x = x * 2; // x = 12
        println!("The value of x in the inner scope is: {x}");
    }

    println!("The value of x is: {x}"); // x = 6
}
```

```
### Functions
In Rust function are defined with the `fn` keyword followed by the function name and a set of parentheses which hold parameters(if any) while the function body is within a set of curly brackets, the most important is the `main` function which is the entry point for most programs.
```rust
fn main() {
    println!("Hello, world!");

    another_function();
}

fn another_function() {
    println!("Another function.");
}
```
A function can be called by entering it's name followed by a set of parentheses

#### Parameters
These are special variables that are part of a function signature, the concrete value passed when the function is called is called an _**argument**_ although both parameter and argument are commonly used interchangeably.
>[!info]
>**In function signatures, you _must_ declare the type of each parameter.**

When defining multiple parameters, they are separated with commas:
```rust
fn main() {
    print_labeled_measurement(5, 'h');
}

fn print_labeled_measurement(value: i32, unit_label: char) {
    println!("The measurement is: {value}{unit_label}");
}
```

### Statements and Expressions
Function bodies are made up of statements and optionally end in an expression.
- **Statements** are instructions that perform some action and do not return a value, and as such cannot be assigned to another variable with a `let` statement.
- **Expressions** evaluate to a resultant value.
```rust
fn main() {
// expression
    let y = 6;
    
let x = (let y = 6); // would error
}
```

>[!info]
>**An expression does not include ending semicolons, else it becomes a statement and it will not return a value**

### Functions With Return Values
Functions can return values to the code that call them, the type of a return value must be declared after `->`. In Rust, a value can be returned early by using the `return` keyword however, most functions return the last expression implicitly.
```rust 
fn five() -> i32 {
    5
}

fn main() {
    let x = five();

    println!("The value of x is: {x}");
}
```

### Comments
In Rust, comments are used to document code or leave notes for developers. There are two main types of comments: **block** and **line** comments
#### Line Comments
Line comments start with `//` and continue to the end of the line.

```rust
// This is a line comment
let x = 5; // This is an inline comment
```

#### Block Comments

Block comments start with `/*` and end with `*/`. They can span multiple lines and be nested.
```rust 
/* This is a block comment
   that spans multiple lines */
let y = 10;

/* Nested block comment:
   /* inner comment */
   outer continues */

```

#### Documentation Comments
Rust supports special documentation comments that are used by `rustdoc` to generate HTML documentation.
##### Line Doc Comments(`///`)
Uses triple slashes to document the item that follows.
```rust
/// Adds two numbers together.
///
/// # Examples
///
/// ```rust
/// let result = add(2, 3);
/// assert_eq!(result, 5);
/// ```
fn add(a: i32, b: i32) -> i32 {
    a + b
}

```

##### Inner Doc Comments (`//!`)
Use `//!` to document the enclosing module or crate. Typically placed at the top of a file.
```rust 
//! This is documentation for the module or crate

```

|Comment Type|Syntax|Use Case|
|---|---|---|
|Line|`//`|Quick notes or short explanations|
|Block|`/* */`|Multi-line or nested comments|
|Doc (outer)|`///`|Documenting functions, structs, etc.|
|Doc (inner)|`//!`|Documenting the entire crate or module|

Use `cargo doc --open` to generate and view your documentation locally.

### Control Flow
#### `if` Expressions
An `if` expression allows you to branch your code depending on conditions. This condition _**must **_ resolve to a `bool`
```rust
fn main() {
    let number = 3;

    if number < 5 {
        println!("condition was true");
    } else {
        println!("condition was false");
    }
}
```

#### `else if` Expressions
Multiple conditions can be evaluated by combining `if` , `else if` and `else` expressions.
```rust
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
#### Using `if` in a `let` Statement
Because `if` is an expression, we can use it on the right side of a `let` statement to assign the outcome to a variable.
```rust
fn main() {
    let condition = true;
    let number = if condition { 5 } else { 6 };

    println!("The value of number is: {number}");
}
```


>[!note]
>**the value of both the of the `if` and `else` arms must be of the same type**

#### Loops
Rust has three kinds of loops: `loop`, `while`, and `for`

##### `loop`
The `loop` keyword tells Rust to execute a block of code over and over again until it is explicitly stopped.
```rust
fn main() {
    loop {
        println!("again!");
    }
}
```
The `break` keyword can be used to break out of a loop or the `continue` keyword to skip over any remaining code in a particular iteration of the loop and go to the next.
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
`return` can also be used from inside a loop, this would always exit the current function.

##### Loop Labels
When loops are nested `break` and `continue` apply to the innermost loop, but using a  _loop label_ you can specify the loop relevant to the keywords.
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

##### `while` Loop
A while loop runs while a condition is `true`.
```rust
fn main() {
    let mut number = 3;

    while number != 0 {
        println!("{number}!");

        number -= 1;
    }

    println!("LIFTOFF!!!");
}
```

##### `for` Loop
```rust
fn main() {
    let a = [10, 20, 30, 40, 50];

    for element in a {
        println!("the value is: {element}");
    }
}
```


### Matching
This is a powerful and flexible way to handle different conditions, using the `match` keyword. This is more flexible than an `if` expression in that the condition does not have to be boolean and pattern matching is possible.

##### Match Syntax
```rust
match VALUE {
	PATTERN => EXPRESSION,
	PATTERN => EXPRESSION,
	PATTERN => EXPRESSION,
}
```

#### Traits
They are a way to define the behaviour that a type has and can share with other types, **behaviour** is the methods we can call on the type. Trait definitions are a way to group method signatures together to define a set of behaviors necessary for that particular purpose.
##### Defining a trait
```rust
pub trait Summary {
fn summarize(&self) -> String;
}
```
##### Implementing a trait

```rust
pub struct Tweet {
    pub username: String,
    pub content: String,
    pub reply: bool,
    pub retweet: bool,
}

impl Summary for Tweet {
    fn summarize(&self) -> String {
        format!("{}: {}", self.username, self.content)
    }
}
```

##### Default Implementations

```r
pub trait Summary {
    fn summarize(&self) -> String {
        String::from("(Read more...)")
    }
}
```

##### Using traits (polymorphism)

```rust
pub fn notify(item: &impl Summary) {
    println!("Breaking news! 
```

### Generics
Generics are a way to parameterise across datatypes, such as we do below with `Option<T>` where `T` is the parameter that can be replaced by a datatype such as `i32`. The purpose of generics is to abstract away the datatype, and by doing that avoid duplication.

```rust
struct Point<T> { x: T, y: T, } 
fn main() { let my_point = Point { x: 5, y: 6 }; }
```

### Iterators

The iterator in Rust is optimised in that it has no effect until it is needed

```rust
let names = vec!["Bob", "Frank", "Ferris"];
let names_iter = names.iter();
```

This creates an iterator for us that we can then use to iterate through the collection using `.next()`

```rust
    fn iterator_demonstration() {
        let v1 = vec![4, 7, 9];
        let mut v1_iter = v1.iter();

        assert_eq!(v1_iter.next(), Some(&4));
        assert_eq!(v1_iter.next(), Some(&7));
        assert_eq!(v1_iter.next(), Some(&9));
        assert_eq!(v1_iter.next(), None);
    }
```

## Map and Collect methods

In Rust, `map` and `collect` are commonly used together for transforming vectors through functional programming patterns.

## `map` Method

`map` is called on iterators and transforms each element according to a provided closure:

```rust
let numbers = vec![1, 2, 3, 4];
let doubled: Vec<i32> = numbers
    .iter()           // Create iterator
    .map(|x| x * 2)   // Transform each element
    .collect();       // Collect back into Vec
// Result: [2, 4, 6, 8]
```

Key points about `map`:

- Returns an iterator (lazy evaluation - no work done until consumed)
- Takes a closure that defines the transformation
- Doesn't modify the original vector