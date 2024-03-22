# Http

This folder contains an example of a Grain component targeting the `wasi:cli/command` world, but unions `wasi:http/imports`. This is a CLI program that can also make HTTP requests without having to use raw sockets.

Although Grain doesn't yet natively output components, this is made possible via `wasm-tools`. If you don't have `wasm-tools` installed, you can find it [here](https://github.com/bytecodealliance/wasm-tools).

## Compiling

All commands are run from the root of this GitHub project.

First, compile your program normally.

```sh
grain compile http/exports.gr --release --use-start-section -o http.wasm
```

Next, embed the WIT interface in the module.

```sh
wasm-tools component embed ./wasi-http --world imports -o http.embedded.wasm http.wasm
```

Finally, create the component.

```sh
wasm-tools component new -o http.component.wasm --adapt ./adapters/wasi_snapshot_preview1.command.wasm http.embedded.wasm
```

## Running

### Via Wasmtime

```sh
wasmtime -W tail-call -S common -S http http.component.wasm
```

### Via jco

```sh
jco run http.component.wasm
```

## Modifying

Make changes to `http/http.gr` and follow the steps above to recompile. You can find documentation for all of the generated bindings in `http/imports.md`.
