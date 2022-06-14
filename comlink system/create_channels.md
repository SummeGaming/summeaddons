# Create channels

The easiest way of creating more channels is to create them in the config.sh file. 
[!ref](config.md)

To do this, simply execute the function in the config file inside the hook and adjust it with the necessary parameters and additions.
```lua lua/comlink/sh_config.lua
-- A simple public channel
Comlink:CreateChannel({
    name = "Public Channel",
    color = Color(67, 111, 255),
    accessCheck = function(ply) return true end -- This is a public channel end,
})
```

