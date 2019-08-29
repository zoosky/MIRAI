# Installation Guide

In order to use MIRAI, you need to install Rust, install Z3, and install MIRAI into cargo.

## Installing Rust

You should install rustup and then use it to get hold of the latest Rust compiler.
See [here](https://doc.rust-lang.org/book/ch01-01-installation.html) for instructions.

Mirai depends on unstable private APIs of the rust compiler to do things like parsing, type checking and
lowering to MIR. These can only be accessed by using the nightly build of the compiler. So use rustup to set
the (last known good) nightly build as the default for the mirai project.

```rustup override set nightly```

## Installing Z3

For Linux, you can try to link with the libz3.a library in binaries. If that does not work, you'll have to build a
customized Z3 [yourself](https://github.com/facebookexperimental/MIRAI/blob/master/documentation/Z3AndLinux.md).

The simplest way to install Z3 on a system with brew is just
```
brew install z3
```

If that works, you're done. If not, you can find pre-built binaries for Z3 
[here](https://github.com/Z3Prover/z3/releases). There are also binary libraries
for macOS and Windows included in the binaries directory of MIRAI.

For macOS, the binary will have to be placed somewhere where it can be 
found and dynamically loaded by the Rust runtime. This can be done by copying the binary into `/usr/local/lib`.

```
cp binaries/libz3.dylib /usr/local/lib
```

For Windows, the binary does not have to be moved.

## Installing MIRAI into cargo

If you just want to use MIRAI you can simply do:
```
cargo install --git https://github.com/facebookexperimental/MIRAI --force --version 1.0.1 mirai
```

If you are running on Linux you'll have to arrange for static linking of Z3:
```
export RUSTFLAGS='-Clink-arg=-L./binaries -Clink-arg=-lstdc++'
```

If you want to help develop MIRAI see the [developer guide](https://github.com/facebookexperimental/MIRAI/blob/master/documentation/DeveloperGuide.md)
