# Call a Wasm Function from Host

This example demonstrates how to define a wasm library that holds a function to be exported, and then run the wasm function over WasmEdge Runtime.

This example consists of two projects:

- [`wasm-lib`](wasm-lib) is a wasm library, in which a function is defined.

- [`call-wasm-lib`](call-wasm-lib) is a host application that loads the wasm binary generated from `wasm-lib`, and runs the wasm function exported by the wasm library over WasmEdge Runtime.

Now let's build and run this example.

- Install `rustup` and `Rust nightly`

  Go to the [official Rust webpage](https://www.rust-lang.org/tools/install) and follow the instructions to install `rustup`. Then, run the following commands in your terminal:

  ```bash
  rustup default nightly
  rustup target add wasm32-wasi
  ```

- Download example

  ```bash
  git clone git@github.com:apepkuss/wasmedge-rust-examples.git
  cd wasmedge-rust-examples
  ```

- Install `libwasmedge`

  ```bash
  ./install_libwasmedge.sh -p /usr/local
  ```

  > For users in China mainland, try the following command to install `libwasmedge` if failed to run the command above
  >
  > ```bash
  > ./install_libwasmedge_zh.sh -p /usr/local
  > ```

  > To install a specific version of `libwasmedge`, use `-v` option. For example, the following command installs `libwasmedge 0.11.2` to `/usr/local/`
  >
  > ```bash
  > ./install_libwasmedge.sh -p /usr/local -v 0.11.2
  > ```

- Build `wasm-lib`

  ```bash
  cd call-func-from-host
  cargo build -p wasm-lib --target wasm32-wasi --release
  ```

  If the command runs successfully, `wasm-lib.wasm` can be found in the directory of `./target/wasm32-wasi/release/`.

- Build and run `call-wasm-lib`

  ```bash
  // in the directory of call-func-from-host
  cargo run -p call-wasm-lib -- ./target/wasm32-wasi/release/wasm_lib.wasm 5
  ```

  If the command runs successfully, then the following message is printed out on the screen:

  ```bash
  fib(5) = 8
  ```