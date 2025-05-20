# 🦀 Rust Naming Conventions Cheat Sheet

## 📌 Variables & Functions
- **snake_case**

```rust
let user_name = "adeola";
fn get_user_info() -> String {}
```

---

## 📌 Structs & Enums
- **PascalCase (a.k.a. CamelCase)**

```rust
struct UserProfile {
    user_id: u32,
    is_active: bool,
}

enum UserRole {
    Admin,
    Guest,
}
```

---

## 📌 Constants & Statics
- **SCREAMING_SNAKE_CASE**

```rust
const MAX_USERS: usize = 100;
static APP_VERSION: &str = "1.0.0";
```

---

## 📌 Modules & Filenames
- **snake_case**

```rust
// Filename: user_profile.rs
mod user_profile;
```

---

## 📌 Traits
- **PascalCase**, typically capabilities or roles

```rust
trait Printable {
    fn print(&self);
}
```

---

## 📌 Lifetimes
- **Single lowercase letters**, usually `'a`, `'b`, etc.

```rust
fn reference<'a>(s: &'a str) -> &'a str {
    s
}
```
