# `ui`

Helpers for creating lightweight script-driven menu widgets.

Widgets persist by `id`, so calling the same widget again returns its current value instead of creating duplicates.

## Basics

Most widget functions take:

- a stable internal `id`
- a visible `label`
- optional defaults

## Functions

### `ui.separator()`

Adds a separator.

```lua
ui.separator()
```

### `ui.text(label)`

Adds a text label.

```lua
ui.text("Movement")
```

### `ui.checkbox(id, label, default) -> boolean`

Creates or reads a checkbox value.

```lua
local enabled = ui.checkbox("fly_enabled", "Enable Fly", false)
```

### `ui.slider_float(id, label, default, min, max) -> number`

Creates or reads a float slider.

```lua
local speed = ui.slider_float("fly_speed", "Fly Speed", 20.0, 0.0, 200.0)
```

### `ui.slider_int(id, label, default, min, max) -> integer`

Creates or reads an integer slider.

```lua
local power = ui.slider_int("power", "Power", 10, 1, 100)
```

### `ui.combo(id, label, items, defaultIndex) -> integer`

Creates or reads a combo box index.

```lua
local mode = ui.combo("aim_mode", "Aim Mode", {
    "Closest",
    "FOV",
    "Distance"
}, 0)
```

### `ui.multi_combo(id, label, items, defaults) -> table`

Creates or reads a multi-select control. Returns an array of booleans.

```lua
local parts = ui.multi_combo("hitboxes", "Hitboxes", {
    "Head",
    "Torso",
    "Arms",
    "Legs"
}, {
    true,
    true,
    false,
    false
})

if parts[1] then
    print("Head enabled")
end
```

### `ui.color(id, label, r, g, b, a) -> r, g, b, a`

Creates or reads a color picker.

```lua
local r, g, b, a = ui.color("esp_color", "ESP Color", 1, 0, 0, 1)
```

### `ui.clear()`

Clears all script-created widgets.

```lua
ui.clear()
```

## Example

```lua
ui.text("Example Panel")
ui.separator()

local enabled = ui.checkbox("example_enabled", "Enabled", true)
local amount = ui.slider_int("example_amount", "Amount", 50, 0, 100)

print("enabled:", enabled, "amount:", amount)
```

