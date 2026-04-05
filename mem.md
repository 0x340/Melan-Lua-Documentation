# `mem`

Low-level memory read and write helpers.

All `mem` functions operate on raw addresses. Invalid reads or writes can throw runtime errors.

## Read Functions

### `mem.rf(address) -> number`

Reads a `float`.

```lua
local value = mem.rf(0x12345678)
```

### `mem.ri(address) -> integer`

Reads a signed 32-bit integer.

```lua
local value = mem.ri(0x12345678)
```

### `mem.rq(address) -> integer`

Reads a 64-bit integer or pointer-like value.

```lua
local ptr = mem.rq(0x12345678)
```

### `mem.rb(address) -> boolean`

Reads a boolean.

```lua
local enabled = mem.rb(0x12345678)
```

### `mem.rv3(address) -> x, y, z`

Reads a `vector3`-shaped value as three numbers.

```lua
local x, y, z = mem.rv3(0x12345678)
print(x, y, z)
```

## Write Functions

### `mem.wf(address, value)`

Writes a `float`.

```lua
mem.wf(0x12345678, 125.0)
```

### `mem.wi(address, value)`

Writes a signed 32-bit integer.

```lua
mem.wi(0x12345678, 100)
```

### `mem.wq(address, value)`

Writes a 64-bit integer.

```lua
mem.wq(0x12345678, 0)
```

### `mem.wb(address, value)`

Writes a boolean.

```lua
mem.wb(0x12345678, true)
```

### `mem.wv3(address, x, y, z)`

Writes three float components as a vector3-like structure.

```lua
mem.wv3(0x12345678, 10, 20, 30)
```

## Notes

- These functions are the lowest-level scripting tools in the VM.
- Prefer `rbx.*` helpers when a helper already exists for the task.
- Use the `off` table when you need a known offset.

Example:

```lua
local prim = rbx.primitive(some_part)
mem.wv3(prim + off.Primitive_Position, 0, 50, 0)
```

