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

### Data Types
Rust is a _**statically typed**_ language, however the compiler can usually infer types based on values and how they are used. There are two data types subsets: **Scalar** and **Compound** 

#### Scalar Types 
A scalar type represents a single value. Rust has four primary scalar types: integer, floating-point number, boolean and character.

##### Integer
An integer is a number without a fractional component. Built-in integer types in Rust are: 

| Length  | Signed | Unsigned |
| ------- | ------ | -------- |
| 8-bit   | i8     | u8       |
| 16-bit  | i16    | u16      |
| 32-bit  | i32    | u32      |
| 64-bit  | i64    | u64      |
| 128-bit | i128   | u128     |
| arch    | isize  | usize    |

_Signed_ and _unsigned_ refer to whether it’s possible for the number to be negative. Each signed variant can store numbers from -(2<sup> n-1 </sup>) to 2<sup> n-1 </sup> - 1 inclusive and each unsigned variant can store numbers from 0 to 2<sup>n</sup> -1, where _n_ is the number of bits that variant uses. 
	Additionally, the `isize` and `usize` types depend on the architecture of the computer your program is running on, which is denoted in the table as _**arch**_: 64 bits if you’re on a 64-bit architecture and 32 bits if you’re on a 32-bit architecture.
###### Integer Literals
| Number Literals | Example     |
| --------------- | ----------- |
| Decimal         | 98_000      |
| Hex             | 0xff        |
| Octal           | 0o77        |
| Binary          | 0b1111_0000 |
| Byte(u8 only)   | b 'A'       |
###### Integer Overflow 
>[!note]
 > **if a _u8_ variable type that holds value between _0 and 255_ is assigned a value outside that range, an _integer overflow_ would occur**

In _**debug**_ mode rust includes a checks for _**integer overflow**_ that causes a _**panic**_ at _**runtime**_ but in release mode the if an overflow occurs, rust performs _**two's complement wrapping**_; values greater than the maximum value the type can hold _**wrap around**_ to the minimum value the type can hold: for a u8,256 becomes 0 and so on.
To handle overflows, some methods provided by the standard library:
- Wrap in all modes with the `wrapping_*` methods, such as `wrapping_add`.
- Return the `None` value if there is overflow with the `checked_*` methods.
- Return the value and a boolean indicating whether there was overflow with the `overflowing_*` methods.
- Saturate at the value’s minimum or maximum values with the `saturating_*` methods.
##### Floating-Point Types
Rust has two primitive types for floating-point numbers which are numbers for representing decimal points, the `f32` and `f64`. The `f32` is capable of more precision, all floating-point types are signed.
```rust
fn main() {
    let x = 2.0; // f64

    let y: f32 = 3.0; // f32
}
```
##### Numeric Operations 
Rust supports the basic mathematical operations  for all the number types: addition, subtraction, multiplication, division, and modulo. Integer division truncates toward zero to the nearest integer.
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

##### Boolean Type
A boolean type in rust has two possible values: `true` and `false`, they are one byte in size, they are specified using `bool`. 
```rust 
fn main() {
    let t = true;

    let f: bool = false; // with explicit type annotation
```

##### Character Type
Rust's `Char` type is it's most primitive alphabetic type, It is four bytes in size and represents a **Unicode Scalar Value**, so it can represent Chinese or Japanese characters, emoji, accented letters, and zero-width spaces.
```rust
fn main() {
    let c = 'z';
    let z: char = 'ℤ'; // with explicit type annotation
    let heart_eyed_cat = '😻';
}
```

>[!note] 
>**the `char` is written with single quotes as opposed to strings which use double quotes. **

#### Compound Types
Compound types can group multiple values into one type, Rust has two primitive compound types: _**tuples**_  and  _**arrays**_ 

##### Tuple Type
A tuple is a general way of grouping together a number of values with a variety of types into one compound type, they have a fixed length: once declared they cannot grow or shrink. 
```rust
fn main() {
    let tup: (i32, f64, u8) = (500, 6.4, 1);
}
```
Values within a tuple can be destructured by matching the pattern or using a period(.) and the index of the value to be accessed.
```rust 
fn main() {
    let tup = (500, 6.4, 1);
	// destructured
    let (x, y, z) = tup;
    // dot notation
    let five_hundred = tup.0
    println!("The value of y is: {y}");
}
```
An empty tuple is called a _**unit**_ represented by `()`

##### Array Type
Another way to have a collection of multiple values is with an _**array**_. Unlike a tuple, every element of an array must have the same type. Unlike arrays in some other languages, arrays in Rust have a fixed length.
```rust
fn main() {
    let array = [1, 2, 3, 4, 5];
    //implicitly typed
    let a: [i32; 5] = [1, 2, 3, 4, 5];
    //array with the same value
    let a = [3; 5];

}
```
Element of an array can be accessed using indexing:
```rust
fn main() {
    let a = [1, 2, 3, 4, 5];

    let first = a[0];
    let second = a[1];
}
```
>[!note]
>**Rust's memory safety would panic and exit a program with a runtime error if an index past the end of the array is accessed**


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

#### Statements and Expressions
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

#### Functions With Return Values
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