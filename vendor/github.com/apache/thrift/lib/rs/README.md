# Rust Thrift library

## Overview

This crate implements the components required to build a working Thrift server
and client. It is divided into the following modules:

 1. errors
 2. protocol
 3. transport
 4. server
 5. autogen

The modules are layered as shown. The `generated` layer is code generated by the
Thrift compiler's Rust plugin. It uses the components defined in this crate to
serialize and deserialize types and implement RPC. Users interact with these
types and services by writing their own code on top.

 ```text
 +-----------+
 |  app dev  |
 +-----------+
 | generated | <-> errors/results
 +-----------+
 |  protocol |
 +-----------+
 | transport |
 +-----------+
 ```

## Using this crate

Add `thrift = "x.y.z"` to your `Cargo.toml`, where `x.y.z` is the version of the
Thrift compiler you're using.

## API Documentation

Full [Rustdoc](https://docs.rs/thrift/)

## Contributing

Bug reports and PRs are always welcome! Please see the
[Thrift website](https://thrift.apache.org/) for more details.

Thrift Rust support requires code in several directories:

* `compiler/cpp/src/thrift/generate/t_rs_generator.cc`: binding code generator
* `lib/rs`: runtime library
* `lib/rs/test`: supplemental tests
* `tutorial/rs`: tutorial client and server
* `test/rs`: cross-language test client and server

All library code, test code and auto-generated code compiles and passes clippy
without warnings. All new code must do the same! When making changes ensure that:

* `rustc` does does output any warnings
* `clippy` with default settings does not output any warnings (includes auto-generated code)
* `cargo test` is successful
* `make precross` and `make check` are successful
* `tutorial/bin/tutorial_client` and `tutorial/bin/tutorial_server` communicate