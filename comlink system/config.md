# Configuration

That's the default config file.

```lua lua/comlink/sh_config.lua
if Comlink.Config then return end
Comlink.Config = {}

Comlink.Config.Theme = {
    primary = Color(221, 160, 31),
    primaryTrans = Color(221, 160, 31, 100),
    white = Color(255, 255, 255),
    whiteTrans = Color(255, 255, 255, 93),
    darkTrans = Color(44, 44, 44, 93),
    blackTrans = Color(0, 0, 0, 230),
    red = Color(255, 58, 58),
    Indicators = {
        [0] = Color(148, 255, 95),
        [1] = Color(255, 196, 0),
        [2] = Color(255, 47, 47),
    }
}

-- Keybinds for muting and the menu
-- Shift + Key: Mutes / Unmutes / Fullmutes yourself/sound
-- Alt + Key: Quickswitch active/passive channels
-- Key: Opens menu
Comlink.Config.MenuKey = KEY_H
-- Languages: en / de
Comlink.Config.Language = "en"
-- HUD height offset
-- Default: 0
-- Min: 0; Max: 1
Comlink.Config.HeightOffset = 0
-- HUD width offset
-- Default: 0
-- Min: -0.75; Max: 0
Comlink.Config.WidthOffset = 0
-- Voice Fix
-- If you can't hear each other, or you can only hear each other with the comlink and not when you are standing next to each other
Comlink.Config.ApplyVoiceFix = false

-- Entity Settings
Comlink.Config.Entity = {
    model = "models/kingpommes/starwars/misc/palp_panel3.mdl",
    hp = 1000,
}

-- Comlink channels are registered here. 
-- This function can also be executed anywhere else in the shared code, but should only be executed after the addon has been loaded!
-- Example with job restriction

hook.Add("Comlink.Loaded", "Comlink.CreateChannels", function()
    Comlink:CreateChannel({
        name = "5th",
        color = Color(44, 105, 191),
        accessCheck = function(ply)
            return ply:IsInJob({"5th Commander Gojira", "5th Private", "5th Lieutenant"}) -- Job restricted channel using the job names
        end,
    })
    
    Comlink:CreateChannel({
        name = "Air Traffic",
        color = Color(67, 111, 255),
        accessCheck = function(ply) return true end -- This is a public channel end,
    })
    
    Comlink:CreateChannel({
        name = "Medic Emergency",
        color = Color(255, 67, 177),
        accessCheck = function(ply) return true end -- This is a public channel end,
    })
    
    Comlink:CreateChannel({
        name = "Announcement",
        color = Color(255, 195, 67),
        announcementChannel = true, -- This is an announcement channel. If you speak in this channel, you will be heard by the whole server!
        accessCheck = function(ply)
            return ply:IsInJob({"Team on duty"})
        end,
    })
    
    -- This creates just 15 blank channels for everyone
    for i = 1, 15 do
        Comlink:CreateChannel({
            name = "Frequence " .. i,
            color = Color(255, 255, 255),
            accessCheck = function(ply) return true end,
        })
    end    
end)
```