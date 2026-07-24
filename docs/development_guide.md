# Development Guide

## Setup

```bash
git clone --recurse-submodules https://github.com/anomalyco/rustObscuraProto.git
cd rustObscuraProto
cargo build
```

## Building

- `cargo build` — build debug
- `cargo build --release` — build release
- `cargo clean` — clean build artifacts

## Testing

```bash
cargo test                  # run all tests
cargo test -- --nocapture   # show test output
cargo test <test_name>      # run specific test
```

## Code Quality

```bash
cargo fmt                  # format code
cargo fmt --check          # check formatting
cargo clippy               # lint
cargo clippy -- -D warnings  # lint (deny warnings)
```

## Pre-commit

The repository uses [pre-commit](https://pre-commit.com) to automatically run `cargo fmt` and `cargo clippy` before each commit. If either tool fails, the commit is rejected — fix the issues, `git add` the changes, and retry.

### Setup

```bash
pip install pre-commit       # or: brew install pre-commit
pre-commit install           # install git hooks from repo root
```

Three checks:
- **`fmt`** — enforces `cargo fmt` style
- **`clippy`** — lints with `-D warnings`

### Using

To run all hooks manually without committing:

```bash
pre-commit run --all-files
```

## Project Layout

```
rustObscuraProto/
├── src/
│   ├── lib.rs              # Crate root (re-exports)
│   ├── bridge.rs           # CXX bridge + Rust wrappers
│   ├── wrapper.h           # C++ wrapper declarations
│   ├── wrapper.cpp         # C++ wrapper implementation
│   └── tests.rs            # Integration tests
├── examples/
│   ├── echo.rs             # Minimal echo example
│   ├── request_response.rs # Request-response pattern
│   └── streaming.rs        # Bidirectional streaming
├── build.rs                # CMake + CXX build script
├── Cargo.toml              # Package manifest
└── CMakeLists.txt          # CMake for ObscuraProto C++ lib
```

## How It Works

1. `build.rs` invokes CMake to fetch and build `ObscuraProto` C++ library
2. `cxx-build` compiles the CXX bridge (generates Rust ↔ C++ bindings)
3. The `#[cxx::bridge]` module in `bridge.rs` declares types and functions shared between Rust and C++
4. `wrapper.cpp` implements C++ free functions that bridge the API gap
5. Rust wrapper types in `bridge.rs` provide idiomatic Rust APIs over the generated bindings
