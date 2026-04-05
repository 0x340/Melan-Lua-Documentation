# `off`

`off` is a global table containing selected engine offsets exposed to Lua.

These values are useful when combining `mem.*` with known structures.

## Available Offsets

### Primitive

- `off.Primitive_Position`
- `off.Primitive_Rotation`
- `off.Primitive_LinearVelocity`
- `off.Primitive_AngularVelocity`

### Humanoid

- `off.Humanoid_Health`
- `off.Humanoid_MaxHealth`
- `off.Humanoid_HipHeight`
- `off.Humanoid_AutoRotate`

### BasePart / Instance

- `off.BasePart_Primitive`
- `off.Instance_ChildrenStart`

## Example

Read health through offsets:

```lua
local character = rbx.local_character()
local humanoid = rbx.find_class(character, "Humanoid")

if humanoid ~= 0 then
    local health = mem.rf(humanoid + off.Humanoid_Health)
    local maxHealth = mem.rf(humanoid + off.Humanoid_MaxHealth)
    print("health:", health, "/", maxHealth)
end
```

Write primitive position directly:

```lua
local prim = rbx.primitive(somePart)
if prim ~= 0 then
    mem.wv3(prim + off.Primitive_Position, 0, 25, 0)
end
```

## Notes

- Offsets are numbers, not functions.
- These values come from the native code and should be treated as version-sensitive.

