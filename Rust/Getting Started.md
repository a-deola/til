The main.rs (entry for a rust project ) file can be compiled and run using: 
```
rustc main.rs
./main
```
# Cargo
Cargo is Rust's build system and package manager, it can be used to initiate a rust project.

```
cargo new hello_cargo
```

This command creates a new project with a <span class="filename">src/</span> folder, a  <span class="filename">main.rs</span>  file, and a <span class="filename">Cargo.toml</span> file which contain the configuration for the project.

<span class="bold-pink-text">
TOML - Tom’s Obvious, Minimal Language
</span>

Cargo can compile and run the corresponding executable using:
```
cargo build
./target/debug/$project_name
```
or do both in one command using: 
```
cargo run
```

Cargo also provides a command called `cargo check`, this command quickly checks your code to make sure it compiles but doesn’t produce an executable. To get optimized builds, you can use `cargo build --release` to compile it with optimizations. This command will create an executable in _**target/release**_ instead of _**target/debug_