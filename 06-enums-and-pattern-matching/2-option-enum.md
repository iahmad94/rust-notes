## the `Option` enum

rust has no null type. the `Option` enum is used instead to express when code could potentially return an empty value.

this is pretty much the `Option` or `Maybe` type in functional languages. this pattern allows the compiler to guarantee every returnable value is handled in the code. this eliminates bugs from unhandled inputs.

```rust
enum Option<T> {
    None,
    Some(T),
}
```

`<T>` is syntax for generic type. to make things conceptually simpler, the `Option` enum can be defined this way for an `i32`:

```rust
enum Option_i32 {
    None,
    Some(i32),
}
```

in the above example, any instance of the `Option_i32` type can have either `None` value or `Some` value. IF the instance of `Option_i32` has `Some` value, it also has an i32 value associated with it.

think of `Option` like a wrapper around a type that says that a value exists or doesn't.

to get the value out of a `Some` wrapper, use one of the `unwrap` methods. the book recommends reading the  [`Option` enum docs](https://doc.rust-lang.org/std/option/enum.Option.html) and so do i, BUT tl;dr:

- `unwrap(self)` exists, but don't use it bc it could **panic**
- `unwrap_or(self, default: T)`
  - returns the `Some` val or provided default
  - eagerly evaluated (as apposed to lazily), so don't use it
- `unwrap_or_else<F>(self, f: F)`
  - returns the `Some` val or lazily evaluates a return from a closure
  - aka handle the error on the fly

```rust
let k = 10;
assert_eq!(Some(4).unwrap_or_else(|| 2 * k), 4); // true
assert_eq!(None.unwrap_or_else(|| 2 * k), 20);   // true
```
