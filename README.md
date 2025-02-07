LITCRYPT [![Build Status](https://travis-ci.org/anvie/litcrypt.rs.svg?branch=master)](https://travis-ci.org/anvie/litcrypt.rs) ![Crates.io](https://img.shields.io/crates/v/litcrypt)
===========

It is abbreviation from "Literal Encryption", a Rust proc macro designed to encrypt
text literal using simple "XOR" algorithm, this will hide your plain string from static analyzer
and protect your valuable app from cracking activity.

LITCRYPT works by encrypting string literal at compile-time, the encrypted
string remain encrypted in both disk and memory at runtime, only decrypted when used.

USAGE
-----

Dependencies:

```rust
[dependencies]
litcrypt = "0.3"
```

Example:

```rust
#[macro_use]
extern crate litcrypt;

use_litcrypt!();

fn main(){
    println!("his name is: {}", lc!("Voldemort"));
}
```

`use_litcrypt!` macro call should be called first for initialization before you can
use `lc!` macro function. The first parameter is your secret key used for encrypt your
literal string. This key is also encrypted and will not visible under static analyzer.

Please take note that you need to set your encryption key using environment variable 
`LITCRYPT_ENCRYPT_KEY` before compile:
e.g:

    $ export LITCRYPT_ENCRYPT_KEY="myverysuperdupermegaultrasecretkey"

Litcrypt will encrypt each string written inside `lc!` statically.

Check the output binary using `strings` command to verify:

    $ strings target/debug/my_valuable_app | grep Voldemort

If the output is blank then your valuable string in your app is safe from static analyzer tool
like Hexeditor etc.

For working example code see `./examples` directory, and test using:

    $ cargo run --example simple

[] Robin.
