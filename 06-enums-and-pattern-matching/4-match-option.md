## `match` and `Option<T>`

this version of `plus_one` can handle takes an optional i32 and returns `Some(i32` or `None`

```rust
fn plus_one(x: Option<i32>) -> Option<i32> {
    match x {
        None => None,
        Some(i) => Some(i + 1),
    }
}

let five = Some(5);
let six = plus_one(five);
let none = plus_one(None);
```

### `match` is **exhaustive** and BREAKS if all cases are not handled

this allows the compiler to double check that you don't have unhandled cases. for example, the following code breaks because the compiler can tell it doesn't handle the `None` case:

```rust
fn plus_one(x: Option<i32>) -> Option<i32> {
    match x {
        Some(i) => Some(i + 1),
        // None MUST BE HANDLED OR COMPILER ANGRY
    }
}
```

rust provides a few catch-all ways of exhausting the `match` operator

```rust
let dice_roll = 9;
match dice_roll {
    3 => add_fancy_hat(),
    7 => remove_fancy_hat(),
    other => move_player(other), // HIGHLIGHT
}

fn add_fancy_hat() {}
fn remove_fancy_hat() {}
fn move_player(num_spaces: u8) {}
```

`other` (or whatever you want to name it) names the catch-all pattern's value so it can be used.

```rust
let dice_roll = 9;
match dice_roll {
    3 => add_fancy_hat(),
    7 => remove_fancy_hat(),
    _ => reroll(), // HIGHLIGHT
}

fn add_fancy_hat() {}
fn remove_fancy_hat() {}
fn reroll() {}
```

`_` on the other hand discards the catch-all value.
