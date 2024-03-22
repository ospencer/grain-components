# Command

This folder contains an example of a Grain component targeting the `wasi:cli/command` world, acting as a simple CLI tool.

Although Grain doesn't yet natively output components, this is made possible via `wasm-tools`. If you don't have `wasm-tools` installed, you can find it [here](https://github.com/bytecodealliance/wasm-tools).

## Compiling

All commands are run from the root of this GitHub project.

First, compile your program normally.

```sh
grain compile command/command.gr --release --use-start-section -o command.wasm
```

Then create the component.

```sh
wasm-tools component new -o command.component.wasm --adapt ./adapters/wasi_snapshot_preview1.command.wasm command.wasm
```

## Running

### Via Wasmtime

```sh
wasmtime -W tail-call command.component.wasm
```

### Via jco

```sh
jco run command.component.wasm
```
