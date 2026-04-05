# Getting Started

## What This VM Is

The Melan Lua VM is an embedded scripting environment intended for lightweight automation, memory interaction, Roblox instance lookup, and menu-driven scripting tools.

It is built on standard Lua, then extended with a few custom global tables:

- `mem`
- `rbx`
- `ui`
- `off`

It also replaces `print(...)` so script output appears inside the Melan UI output panel.

## What This VM Is Not

This VM is not Luau and not a normal Roblox script context.

These Roblox-style patterns do not exist here:

- `workspace:GetChildren()`
- `part.Size = ...`
- `Vector3.new(...)`
- `Instance.new(...)`
- Luau-only syntax like `continue`

Instead, the VM works with raw addresses and plain Lua values.

## First Script

```lua
print("Melan Lua VM ready")

local ws = rbx.workspace()
print("workspace:", ws)

local kids = rbx.get_children(ws)
print("child count:", #kids)
```

## Important Mental Model

Most `rbx` functions accept or return integer addresses.

Example:

```lua
local workspace = rbx.workspace()
local players = rbx.find_class(workspace, "Players")
print("players address:", players)
```

If you want to move or resize a part, you usually:

1. Find an instance address.
2. Convert it to a primitive address with `rbx.primitive(instance)`.
3. Read or write values using `rbx.*` helpers or `mem.*`.

## State Persistence

The VM state persists between script runs until the VM is reset.

That means globals like `_G.enabled` survive across executions:

```lua
_G.enabled = not _G.enabled
print("enabled:", _G.enabled)
```

## Error Output

Two common error categories are reported:

- `[syntax] ...` for compile or parse errors
- `[error] ...` for runtime errors

## Good Habits

- Check returned addresses against `0`
- Avoid assuming Roblox property syntax exists
- Store toggle state in `_G`
- Use `ipairs(...)` for tables returned from `rbx.get_children(...)`

