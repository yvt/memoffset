# memoffset #

[![](http://meritbadge.herokuapp.com/memoffset)](https://crates.io/crates/memoffset)

C-Like `offset_of` functionality for Rust structs.

Introduces the following macros:
 * `offset_of!` for obtaining the offset of a member of a struct.
 * `span_of!` for obtaining the range that a field, or fields, span.

## Usage ##
Add the following dependency to your `Cargo.toml`:

```toml
[dependencies]
memoffset = "0.1"
```

Add the following lines at the top of your `main.rs` or `lib.rs` files.

```rust
#[macro_use]
extern crate memoffset;
```

## Examples ##
```rust
#[repr(C, packed)]
struct Foo {
	a: u32,
	b: u32,
	c: [u8; 5],
	d: u32,
}

assert_eq!(offset_of!(Foo, b), 4);
assert_eq!(offset_of!(Foo, c[3]), 11);

assert_eq!(span_of!(Foo, a),          0..4);
assert_eq!(span_of!(Foo, a ..  c),    0..8);
assert_eq!(span_of!(Foo, a ..  c[1]), 0..9);
assert_eq!(span_of!(Foo, a ..= c[1]), 0..10);
assert_eq!(span_of!(Foo, ..= d),      0..14);
assert_eq!(span_of!(Foo, b ..),       4..17);
```