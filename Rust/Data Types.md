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
#### Strings
There are two types of strings in Rust 
	- `&str` a view of a sequence of UTF8 encoded dynamic bytes, stored in  binary, stack or heap. Size is unknown and it points at the first byte of the string.
	- `String` : growable, mutable, owned UTF-8 encoded string, always allocated on the heap includes capacity i.e memory allocated for this string.
	
>[!info]
>A String literal is a string slice stored in the application binary (i.e there at compile time).

```rust
let mut title = String::from("Solana ");
title.push_str("Bootcamp"); // push_str() appends a literal to a String 
println!("{}", title);
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
Others compound types in Rust are __*struct*__ and *__enum__* 
##### Tuples
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

##### Arrays
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

##### Struct 
This is like an object in JS
```rust
struct User{
	name: String,
	age: u32,
	email: String,
}
impl User{
	fn birthday(&mut self){
		self.age += 1;
		println!("Happy {}th birthday, {}!", self.age, self.name);
		}
} 
fn main(){
	let mut alice = User{name: "Alice".into(), age: 30};
	alice.birthday();
}
```

##### Enums
```rust
enum Fruit{
	Apple,
	Orange,
	Grape,
}
//they can be refrenced with 

Fruit::Orange
```

##### Option
We may need to handle situations where a statement or function doesn't return us the value we are expecting, for this we can use Option.
- `None`, to indicate failure or lack of value, and
- `Some(value)`, a tuple struct that wraps a `value` with type `T`.

```rust
enum Result<T, E> {
	Ok(T),
	Err(E),
}
```

##### Collections
##### Vectors
Vectors are one of the most used types of collections. They can be created using `Vec::new()`  creates a new empty vector.

```rust
let v = Vec<i32> = Vec::new()
let names = vec!["Bob", "Frank", "Ferris"]
```

#### Adding to the vector

We use `push` to add to the vector, for example

```
v.push(19);
```

#### Retrieving items from the vector

2 ways to get say the 5th item

- using `get` e.g. `v.get(4);`
- using an index e.g. `v[4];`

## Slices

Slices are similar to arrays, but their length is not known at compile time. Instead, a slice is a two-word object, the first word is a pointer to the data, and the second word is the length of the slice. The word size is the same as usize, determined by the processor architecture eg 64 bits on an x86-64. Slices can be used to borrow a section of an array, and have the type signature `&[T]`."