# `rbx`

Helpers for working with Roblox instance addresses and primitive addresses.

This API does not return wrapped objects. It returns plain integer addresses and plain Lua tables.

## Globals

### `rbx.workspace() -> integer`

Returns the current `Workspace` instance address.

```lua
local ws = rbx.workspace()
```

### `rbx.local_player() -> integer`

Returns the local player instance address.

### `rbx.local_character() -> integer`

Returns the local character model address.

### `rbx.camera() -> integer`

Returns the current camera address.

## Instance Lookup

### `rbx.find_child(parent, name) -> integer`

Finds the first child by exact name. Returns `0` on failure.

```lua
local bodyEffects = rbx.find_child(character, "BodyEffects")
```

### `rbx.find_class(parent, className) -> integer`

Finds the first child by class name. Returns `0` on failure.

```lua
local tool = rbx.find_class(character, "Tool")
```

### `rbx.get_children(parent) -> table`

Returns an array-style table of child instance addresses.

```lua
local children = rbx.get_children(rbx.workspace())

for i, child in ipairs(children) do
    print(i, child)
end
```

## Metadata

### `rbx.name(address) -> string`

Returns the instance name. Returns `""` on failure.

### `rbx.classname(address) -> string`

Returns the instance class name. Returns `""` on failure.

```lua
print(rbx.name(someInstance), rbx.classname(someInstance))
```

## Primitive Helpers

### `rbx.primitive(instance) -> integer`

Returns the primitive address associated with a `BasePart`-like instance. Returns `0` on failure.

```lua
local prim = rbx.primitive(part)
if prim ~= 0 then
    print("primitive:", prim)
end
```

### `rbx.position(primitive) -> x, y, z`

Reads a primitive position.

### `rbx.set_position(primitive, x, y, z)`

Writes a primitive position.

```lua
local x, y, z = rbx.position(prim)
rbx.set_position(prim, x, y + 10, z)
```

### `rbx.size(primitive) -> x, y, z`

Reads a primitive size.

### `rbx.set_size(primitive, x, y, z)`

Writes a primitive size.

```lua
local sx, sy, sz = rbx.size(prim)
rbx.set_size(prim, sx * 2, sy, sz)
```

### `rbx.velocity(primitive) -> x, y, z`

Reads assembly linear velocity.

### `rbx.set_velocity(primitive, x, y, z)`

Writes assembly linear velocity.

```lua
rbx.set_velocity(prim, 0, 100, 0)
```

## Common Pattern

Find a named part in `Workspace` and resize it:

```lua
local ws = rbx.workspace()
local children = rbx.get_children(ws)

for i, child in ipairs(children) do
    if rbx.name(child) == "Part" then
        local prim = rbx.primitive(child)
        if prim ~= 0 then
            rbx.set_size(prim, 20, 20, 20)
        end
    end
end
```

## Important Notes

- Always treat `0` as an invalid address.
- `rbx.get_children(...)` returns child instances, not primitives.
- Position, size, and velocity helpers work on primitive addresses.
- There is no `Vector3.new(...)`; use plain number triples.

