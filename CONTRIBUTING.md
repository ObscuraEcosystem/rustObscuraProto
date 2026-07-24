# Contributing to rustObscuraProto

Thank you for your interest in contributing!

## System Dependencies

- **CMake** 3.14+
- **C++17** compiler (gcc, clang, or MSVC)
- **libsodium** (installed automatically by CMake FetchContent)
- **Rust** 1.75+ (edition 2021)

## Development Setup

```bash
git clone https://github.com/anomalyco/rustObscuraProto.git
cd rustObscuraProto
cargo build
```

## Pre-commit Hooks

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

## Pull Request Process

1. Fork the repository and create a feature branch from `develop`.
2. Run `cargo test` to ensure all tests pass.
3. Run `cargo clippy` and `cargo fmt --check` to ensure code quality.
4. Open a PR with a title and description of your changes.

## Project Structure

```
rustObscuraProto/
├── src/
│   ├── lib.rs              # Rust entry point
│   ├── bridge.rs           # CXX bridge declarations + Rust wrappers
│   ├── wrapper.h           # C++ wrapper header
│   ├── wrapper.cpp         # C++ wrapper implementation
│   └── tests.rs            # Integration tests
├── build.rs                # Build script (CMake + CXX)
├── Cargo.toml              # Package manifest
└── CMakeLists.txt          # CMake config for ObscuraProto
```

The C++ library is fetched and built by CMake during `cargo build`. The `cxx` bridge generates C++ bindings for the Rust declarations in `bridge.rs`.
