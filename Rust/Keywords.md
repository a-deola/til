The following list contains keywords that are reserved for current or future use by the Rust language. They cannot be used as identifiers (except as raw identifiers).

### Keywords Currently in Use

- `as` - casting, disambiguation, or renaming in use statements  
- `async` - return a `Future` 
- `await` - suspend until a `Future` completes  
- `break` - exit a loop  
- `const` - constant definitions or raw pointers  
- `continue` - next loop iteration  
- `crate` - refers to the crate root  
- `dyn` - dynamic dispatch  
- `else` - fallback in conditionals  
- `enum` - defines an enum  
- `extern` - external function or variable  
- `false` - Boolean literal  
- `fn` - define a function  
- `for` - iterate, trait impl, or lifetime  
- `if` - conditional branching  
- `impl` - implement traits or inherent impls  
- `in` - used in `for` loops  
- `let` - bind variable  
- `loop` - infinite loop  
- `match` - pattern matching  
- `mod` - module definition  
- `move` - closure ownership  
- `mut` - mutable bindings  
- `pub` - public visibility  
- `ref` - reference binding  
- `return` - return from function  
- `Self` - type alias for current type  
- `self` - current instance or module  
- `static` - global value or static lifetime  
- `struct` - define a struct  
- `super` - parent module  
- `trait` - define a trait  
- `true` - Boolean literal  
- `type` - type alias or associated type  
- `union` - define a union  
- `unsafe` - mark unsafe code  
- `use` - import paths  
- `where` - type constraints  
- `while` - conditional loop  

### Keywords Reserved for Future Use

- `abstract`  
- `become`  
- `box`  
- `do`  
- `final`  
- `gen`  
- `macro`  
- `override`  
- `priv`  
- `try`  
- `typeof`  
- `unsized`  
- `virtual`  
- `yield`

### Raw Identifiers

You can use keywords as identifiers by prefixing them with `r#`.

#### Example

```rust
// Invalid
fn match(needle: &str, haystack: &str) -> bool {
    haystack.contains(needle)
}

// Valid
fn r#match(needle: &str, haystack: &str) -> bool {
    haystack.contains(needle)
}

fn main() {
    assert!(r#match("foo", "foobar"));
}