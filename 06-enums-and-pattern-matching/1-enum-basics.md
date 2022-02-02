## enum basics

used to "_enumerate_ all possible variants" of a type. for example, an ip address can be be:

- version 4 (127.0.0.1)
OR
- version 6 (2001:0db8:85a3:0000:0000:8a2e:0370:7334)

but cannot be both at the same time. there we can express type `IpAddrKind` as:

```rust
enum IpAddrKind {
    V4,
    V6,
}
```

once defined, an enum can be used as a type:

```rust
// --snip--
let four = IpAddrKind::V4;
let six = IpAddrKind::V6;

fn route(ip_kind: IpAddrKind) {}

route(IpAddrKind::V4);
route(IpAddrKind::V6);
```

enums variants can hold data directly. **note** that variant names automatically become constructor functions.

```rust
enum IpAddr {
    V4(String),
    V6(String),
}

// IpAddr::V4() and IpAddr::V6() automagically valid based on enum definition
let home = IpAddr::V4(String::from("127.0.0.1"));
let loopback = IpAddr::V6(String::from("::1"));
```

enum variants can hold any kind of data, including structs. this is from the rust standard library:

```rust

struct Ipv4Addr {
    // --snip--
}

struct Ipv6Addr {
    // --snip--
}

enum IpAddr {
    V4(Ipv4Addr),
    V6(Ipv6Addr),
}
```

enums can simplify multiple related structs into a single enum

```rust
struct QuitMessage; // unit struct
struct MoveMessage {
    x: i32,
    y: i32,
}
struct WriteMessage(String); // tuple struct
struct ChangeColorMessage(i32, i32, i32); // tuple struct

//
// refactors to
//

enum Message {
    Quit,
    Move { x: i32, y: i32 },
    Write(String),
    ChangeColor(i32, i32, i32),
}
```

just like with structs, we can use `impl` to define methods on an enum

```rust
enum Message {
    // --snip--
}
impl Message {
    fn call(&self) {
        // method body would be defined here
    }
}

let m = Message::Write(String::from("hello"));
m.call();
```
