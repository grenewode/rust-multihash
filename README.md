# rust-multihash

[![](https://img.shields.io/badge/made%20by-Protocol%20Labs-blue.svg?style=flat-square)](http://ipn.io)
[![](https://img.shields.io/badge/project-multiformats-blue.svg?style=flat-square)](https://github.com/multiformats/multiformats)
[![](https://img.shields.io/badge/freenode-%23ipfs-blue.svg?style=flat-square)](https://webchat.freenode.net/?channels=%23ipfs)
[![](https://img.shields.io/badge/readme%20style-standard-brightgreen.svg?style=flat-square)](https://github.com/RichardLitt/standard-readme)

[![Build Status](https://github.com/multiformats/rust-multihash/workflows/build/badge.svg)](https://github.com/multiformats/rust-multihash/actions)
[![Crates.io](https://img.shields.io/crates/v/multihash?style=flat-square)](https://crates.io/crates/multihash)
[![License](https://img.shields.io/crates/l/multihash?style=flat-square)](LICENSE)
[![Documentation](https://docs.rs/multihash/badge.svg?style=flat-square)](https://docs.rs/multihash)
[![Dependency Status](https://deps.rs/repo/github/multiformats/rust-multihash/status.svg)](https://deps.rs/repo/github/multiformats/rust-multihash)
[![Coverage Status]( https://img.shields.io/codecov/c/github/multiformats/rust-multihash?style=flat-square)](https://codecov.io/gh/multiformats/rust-multihash)

> [multihash](https://github.com/multiformats/multihash) implementation in Rust.

## Table of Contents

- [Install](#install)
- [Usage](#usage)
- [Supported Hash Types](#supported-hash-types)
- [Maintainers](#maintainers)
- [Contribute](#contribute)
- [License](#license)

## Install

First add this to your `Cargo.toml`

```toml
[dependencies]
multihash = "*"
```

Then run `cargo build`.

## Usage

```rust
use tiny_multihash::{Multihash, MultihashDigest, SHA2_256};

fn main() {
    let hash = Multihash::new(SHA2_256, b"my hash");
    println!("{:?}", hash);
}
```

### Using a custom code table

You can derive your own application specific code table:

```rust
use tiny_multihash::derive::Multihash;
use tiny_multihash::{Hasher, MultihashDigest};

const FOO: u64 = 0x01;
const BAR: u64 = 0x02;

#[derive(Clone, Debug, Eq, Multihash, PartialEq)]
pub enum Multihash {
    #[mh(code = FOO, hasher = tiny_multihash::Sha2_256)]
    Foo(tiny_multihash::Sha2Digest<tiny_multihash::U32>),
    #[mh(code = BAR, hasher = tiny_multihash::Sha2_512)]
    Bar(tiny_multihash::Sha2Digest<tiny_multihash::U64>),
}

fn main() {
    let hash = Multihash::new(FOO, b"my hash");
    println!("{:?}", hash);
}
```

## Supported Hash Types

* `SHA1`
* `SHA2-256`
* `SHA2-512`
* `SHA3`/`Keccak`
* `Blake2b-256`/`Blake2b-512`/`Blake2s-128`/`Blake2s-256`
* `Strobe`

## Maintainers

Captain: [@dignifiedquire](https://github.com/dignifiedquire).

## Contribute

Contributions welcome. Please check out [the issues](https://github.com/multiformats/rust-multihash/issues).

Check out our [contributing document](https://github.com/multiformats/multiformats/blob/master/contributing.md) for more information on how we work, and about contributing in general. Please be aware that all interactions related to multiformats are subject to the IPFS [Code of Conduct](https://github.com/ipfs/community/blob/master/code-of-conduct.md).

Small note: If editing the README, please conform to the [standard-readme](https://github.com/RichardLitt/standard-readme) specification.


## License

[MIT](LICENSE)
