# Proxy

This folder contains an example of a Grain component targeting the `wasi:http/proxy` world, providing the ability to act as a web request handler.

Although Grain doesn't yet natively output components, this is made possible via `wasm-tools`. If you don't have `wasm-tools` installed, you can find it [here](https://github.com/bytecodealliance/wasm-tools).

## Compiling

All commands are run from the root of this GitHub project.

First, compile your program normally.

```sh
grain compile proxy/exports.gr --release --use-start-section -o proxy.wasm
```

Next, embed the WIT interface in the module.

```sh
wasm-tools component embed ./wasi-http --world proxy -o proxy.embedded.wasm proxy.wasm
```

Finally, create the component.

```sh
wasm-tools component new -o proxy.component.wasm --adapt ./adapters/wasi_snapshot_preview1.proxy.wasm proxy.embedded.wasm
```

## Running

### Via Wasmtime

```sh
wasmtime serve -W tail-call -S common -S http proxy.component.wasm

# In another terminal...
curl localhost:8080
```

### Via jco

```sh
jco serve proxy.component.wasm

# In another terminal...
curl localhost:8000
```

## Modifying

Make changes to `proxy/proxy.gr` and follow the steps above to recompile. You can find documentation for all of the generated bindings in `proxy/imports.md`.
