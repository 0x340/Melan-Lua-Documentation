# Melan Lua VM

Documentation for the embedded Lua VM exposed by Melan.

This VM is a lightweight external scripting runtime built on standard Lua 5.4 with custom bindings for memory access, Roblox instance traversal, and simple UI widgets. It is not a Luau executor and it does not expose normal Roblox object syntax such as `workspace:GetChildren()` or `Vector3.new(...)`.

## Contents

- [Getting Started](./getting-started.md)
- [Environment](./environment.md)
- [mem](./mem.md)
- [rbx](./rbx.md)
- [ui](./ui.md)
- [off](./off.md)
- [Examples](./examples.md)

## Quick Example

```lua
print("hello from melan")

local workspace = rbx.workspace()
local children = rbx.get_children(workspace)

for i, child in ipairs(children) do
    print(i, rbx.name(child), rbx.classname(child))
end
```

