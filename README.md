# WebAssembly

## Install WABT: The WebAssembly Binary Toolkit

Source: [wabt](https://github.com/WebAssembly/wabt)

```
brew install wabt
```

## Using the Binary Toolkit

```wat
(;./src/add1.wat;)
(module
    (func $add (param $lhs i32) (param $rhs i32) (result i32)
        local.get $lhs
        local.get $rhs
        i32.add
    )
    (export "add" (func $add))
)
```

```wat
(;./src/add2.wat [S-expressions];)

(module
    (func $add (param $lhs i32) (param $rhs i32) (result i32)
        (i32.add
            (local.get $lhs)
            (local.get $rhs)
        )
    )
    (export "add" (func $add))
)
```

### Compile WebAssembly Text format file to WebAssembly binary file

```
wat2wasm ./src/add1.wat -o ./build/add.wasm
wat2wasm ./src/add2.wat -o ./build/add_sexpr.wasm
```

### Inpect WebAssembly binary file

```
wasm-objdump build/add.wasm -x
wasm-objdump build/add-sexpr.wasm -x
```

### Conver WebAssembly binary file back to WebAssembly Text format file

```
wasm2wat ./build/add_sexpr.wasm -o ./build/roundtrip.wat
```

```wat
(module
  (type (;0;) (func (param i32 i32) (result i32)))
  (func (;0;) (type 0) (param i32 i32) (result i32)
    local.get 0
    local.get 1
    i32.add)
  (export "add" (func 0)))
```
