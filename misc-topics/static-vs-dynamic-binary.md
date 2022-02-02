statically-linked vs dynamically-linked binaries
---

`rust` compiles to a dynamically-linked binary, unlike languages like `go` that compile to a single, self-contained, static binary.

## what is a static binary?
libraries used are copied into the binary
### pros +
- standalone doesn't require libraries (like `glibc`) to exist on a platfrom to run
- won't break due to underlying library version incompatibility
### cons -
- but underlying libraries won't get updated without recompiling the binary
- every static bin will have its own copy of the common library running in memory
- larger file size

## dynamic?
libraries used are dynamically referenced at runtime
### pros -
- underlying libraries can be updated as long as they remain compatible
- dynamically-linked programs can share libraries instead of having their own copy in memory
- smaller file size
- different languages can use the same libraries
### cons -
- requires underlying libraries to exist (ie won't run without `glibc`)
- breaks if a required library is missing or otherwise incompatible

## conclusion
- use static when you can't make assumptions about the target system.
- use dynamic when you want efficient memory usage (both ram and disk space).

