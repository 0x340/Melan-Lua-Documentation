# Examples

## Toggle Anti-Fall Damage Part Size

This is the correct style for the Melan VM.

```lua
local val = 999999999
local targetName = "NoRagdollNoFallDamage"

_G.antiFall = not (_G.antiFall or false)

local ws = rbx.workspace()
local children = rbx.get_children(ws)

for i, child in ipairs(children) do
    if rbx.name(child) == targetName then
        local prim = rbx.primitive(child)
        if prim ~= 0 then
            if _G.antiFall then
                rbx.set_size(prim, val, val, val)
            else
                rbx.set_size(prim, 50, 50, 50)
            end
        end
    end
end

print("Anti-Fall Damage", _G.antiFall and "ON" or "OFF")
```

## Print All Workspace Children

```lua
local ws = rbx.workspace()

for i, child in ipairs(rbx.get_children(ws)) do
    print(i, rbx.name(child), rbx.classname(child), child)
end
```

## Move Local Character Up

```lua
local character = rbx.local_character()
local root = rbx.find_child(character, "HumanoidRootPart")

if root ~= 0 then
    local prim = rbx.primitive(root)
    if prim ~= 0 then
        local x, y, z = rbx.position(prim)
        rbx.set_position(prim, x, y + 5, z)
    end
end
```

## Velocity Boost

```lua
local character = rbx.local_character()
local root = rbx.find_child(character, "HumanoidRootPart")

if root ~= 0 then
    local prim = rbx.primitive(root)
    if prim ~= 0 then
        rbx.set_velocity(prim, 0, 150, 0)
    end
end
```

## Health Reader

```lua
local character = rbx.local_character()
local humanoid = rbx.find_class(character, "Humanoid")

if humanoid ~= 0 then
    local health = mem.rf(humanoid + off.Humanoid_Health)
    print("health:", health)
end
```

## Simple UI Script

```lua
ui.text("Utility")
ui.separator()

local enabled = ui.checkbox("util_enabled", "Enabled", true)
local size = ui.slider_float("util_size", "Target Size", 50, 1, 500)

if enabled then
    print("current size:", size)
end
```

