# Building MOONWITNESS IDE from source

MOONWITNESS IDE is a Rust desktop application based on the Lapce codebase. The public product name is MOONWITNESS IDE; some internal Cargo package, executable, and feature identifiers still use `lapce` for compatibility.

## Requirements

- Git
- Rust and Cargo via [rustup](https://rustup.rs/)
- Rust toolchain compatible with the workspace's `rust-version` in the root `Cargo.toml`
- Native build dependencies for your operating system

Use a current stable Rust toolchain that satisfies the repository's declared minimum version. The CI workflow updates the installed stable toolchain before building.

## Get the source

```sh
git clone https://github.com/BRIDGE-ALLAH/MW-IDE.git
cd MW-IDE
```

## Linux

On Ubuntu, install the same native dependencies used by CI:

```sh
sudo make ubuntu-deps
```

On Fedora, the upstream build environment has used the following package set; package names can vary by Fedora release:

```sh
sudo dnf install clang libxkbcommon-x11-devel libxcb-devel vulkan-loader-devel wayland-devel openssl-devel pkgconf
```

Then build:

```sh
cargo fetch --locked
cargo build --locked
```

## macOS

1. Install Xcode Command Line Tools: `xcode-select --install`.
2. Install Rust with rustup.
3. Clone the repository and run the build commands below.

```sh
cargo fetch --locked
cargo build --locked
```

## Windows

1. Install the Visual Studio Build Tools with the C++ build tools workload and Windows SDK.
2. Install Rust with rustup using the MSVC toolchain.
3. Clone the repository and run the build commands below in a supported developer shell.

```powershell
cargo fetch --locked
cargo build --locked
```

## Run the application

The inherited executable name remains `lapce` until a separately tested compatibility migration is completed.

```sh
cargo dev
```

`cargo dev` is a project-local Cargo alias for `cargo run --bin lapce -- --wait`. It keeps the app attached to the terminal. On Windows with an older GPU that cannot use the default backend, set `WGPU_BACKEND=gl` in the user Cargo config (`%CARGO_HOME%\config.toml`) or for one session with `$env:WGPU_BACKEND = 'gl'`. Keep this compatibility override out of the shared project config unless it has been validated across supported platforms. To run without waiting for the app to close, use `cargo run --bin lapce`.

A normal development build is placed under `target/debug/`. Release builds can be produced with:

```sh
cargo build --release --locked
```

## CI-equivalent checks

The repository's GitHub Actions workflow currently runs formatting, Clippy, cross-platform builds, and workspace documentation tests. To run the corresponding checks locally:

```sh
cargo fmt --all --check
cargo clippy --profile ci
cargo test --profile ci --workspace --lib
cargo test --profile ci --doc --workspace
cargo build --profile ci --frozen
```

On Ubuntu, install native dependencies with `sudo make ubuntu-deps` before running the build and Clippy commands. CI also performs a portable-feature build on Windows.

A successful local build applies only to the machine and toolchain used. It does not establish that other platforms, installers, signing, packaging, or release acceptance have been verified.

## Troubleshooting and reporting

- Record the operating system, architecture, Rust version (`rustc --version`), exact command, and complete relevant error output.
- Confirm that the Rust toolchain satisfies the root manifest's declared `rust-version`.
- Avoid deleting or renaming internal `lapce` package and executable identifiers unless the change includes a compatibility plan and platform validation.
- Report reproducible problems through the repository's Issues tab after Issues has been enabled by the maintainer. Until then, contact the maintainer through the GitHub profile linked from this repository.

For inherited upstream implementation details, consult [Lapce](https://github.com/lapce/lapce). This repository's build instructions and project policies are the source of truth for MOONWITNESS IDE changes.
