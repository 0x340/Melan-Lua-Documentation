# Melan Lua VM

Documentation for the embedded Lua VM for Melan.

## Contents

- [Environment](./environment.md)
- [Memory](./mem.md)
- [Roblox](./rbx.md)
- [User Interface](./ui.md)
- [Offsets](./off.md)
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
