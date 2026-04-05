# Environment

## Base Runtime

The VM uses standard Lua 5.4 semantics, not Luau semantics.

## Loaded Standard Libraries

Only a small set of standard libraries is loaded:

- `_G`
- `math`
- `string`
- `table`

You should not assume these libraries are available unless you add them yourself in the VM:

- `io`
- `os`
- `debug`
- `package`
- `coroutine`
- `utf8`

## Overridden Globals

### `print(...)`

`print` is overridden to write text to the Melan Lua output buffer.

Signature:

```lua
print(...)
```

Behavior:

- Converts all arguments to strings
- Joins them with tabs
- Pushes the line into the UI output log

Example:

```lua
print("x", 10, true)
```

## Persistence

The Lua state is persistent until reset. Global variables and `_G` values survive between runs.

Example:

```lua
_G.counter = (_G.counter or 0) + 1
print("runs:", _G.counter)
```

## Data Model

Custom APIs are exposed through global tables:

- `mem` for raw memory reads and writes
- `rbx` for Roblox instance and primitive helpers
- `ui` for script-defined menu widgets
- `off` for selected engine offsets

