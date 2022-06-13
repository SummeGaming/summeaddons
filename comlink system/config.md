# Configuration

This is a basic page, with only a title and some text content.

```lua lua/squadsystem/sh_config.lua
SquadSystem.Config = {}

/* ----------------------------- Color settings ----------------------------- */

SquadSystem.Config.Theme = {
    primary = Color(0,228,171),
}

/* ----- Default keybind, users can change it via "summelibrary_hotkeys" ---- */
/* ------------------------- in their client console ------------------------ */

SquadSystem.Config.Key = KEY_G

/* ---------------------------- Language settings --------------------------- */
/* -------------------- Currently available: en | de | ru ------------------- */

SquadSystem.Config.Language = "en"

/* ---------------- Whether the sideboard should show avatars --------------- */

SquadSystem.Config.Sideboard = {
    showAvatars = true,
}

/* ------------- Whether to block damage caused by squad members ------------ */
/* ------------------------- Basically friendly fire ------------------------ */

SquadSystem.Config.BlockDamage = false

/* ------------------ Experience Rewards (Leveling System) ------------------ */
/* --------- (Vrondakis, Sublime, Bricks, Glorified & VoidFactions) --------- */

SquadSystem.Config.XPRewards = {
    enabled = false, -- whether to give a player xp every x minutes for being part of a squad
    frequency = 25, -- the interval in minutes
    amount = 100, -- the amount of xp to give
    notify = true, -- whether the player should be notified about it
}

/* ------------------------ Creator & Squadlist NPCs ------------------------ */

SquadSystem.Config.NPCModels = {
    creator = "models/mossman.mdl",
    publicList = "models/mossman.mdl",
}

/* -------------------- Customization of the squad ranks -------------------- */
/* ------------ The first two ALWAYS have the squadlead privilege ----------- */

SquadSystem.Config.Positions = {
    [1] = {
        name = "SQ-Leader",
        imgur = "XVgS82g",
    },
    [2] = {
        name = "SQ-CoLeader",
        imgur = "BaG6mmo",
    },
    [3] = {
        name = "Medic",
        imgur = "K9NmqdQ",
    },
    [4] = {
        name = "Marksman",
        imgur = "YoUuuxs",
    },
    [5] = {
        name = "Heavygunner",
        imgur = "yDobdHS",
    },
    [6] = {
        name = "Rifleman",
        imgur = "LbFCAVG",
    },
}

/* --------------- Customization of the communication options --------------- */

SquadSystem.Config.Communications = {
    ["Need healing"] = {
        chatMsg = "%PLAYER% needs medical treatment!",
        overheadMsg = "NEEDS HEALING",
        imgur = "Ew1RYeq",
        color = Color(255,145,145),
        time = 10,
    },
    ["Watching here"] = {
        chatMsg = "%PLAYER% is watching an area!",
        overheadMsg = "IS WATCHING HERE",
        imgur = "tPjRhA7",
        color = Color(0,238,255),
        time = 5,
    },
    ["Need support"] = {
        chatMsg = "%PLAYER% needs support!",
        overheadMsg = "NEEDS SUPPORT",
        imgur = "8h72EhA",
        color = Color(255,0,255),
        time = 5,
    },
    ["On position"] = {
        chatMsg = "%PLAYER% is on position!",
        overheadMsg = "IS ON POSITION",
        imgur = "4MDnmqR",
        color = Color(0,212,28),
        time = 5,
    },
    ["Awating commands"] = {
        chatMsg = "%PLAYER% is awaiting commands!",
        overheadMsg = "IS AWAITING COMMANDS",
        imgur = "nDzyJwx",
        color = Color(255,0,0),
        time = 5,
    },
    ["Sector is clear"] = {
        chatMsg = "%PLAYER% has cleared a sector!",
        overheadMsg = "SECTOR CLEARED",
        imgur = "MKQiStY",
        color = Color(0,255,115),
        time = 5,
    },
    ["Ping (Normal)"] = { -- If u change the name (Ping (Normal)) then change it also down there in the developer section!
        chatMsg = "%PLAYER% has marked a position!",
        overheadMsg = "POSITION MARKED",
        imgur = "7PwxRm0",
        color = Color(255,166,0),
        time = 5,
        callbackSv = function(ply)
            ply:SquadPing("normal")
        end,
    },
    ["Ping (Enemy)"] = { -- If u change the name (Ping (Enemy)) then change it also down there in the developer section!
        chatMsg = "%PLAYER% has localized an enemy!",
        overheadMsg = "ENEMY FOUND",
        imgur = "tciaGfe",
        color = Color(255,0,34),
        time = 5,
        callbackSv = function(ply)
            ply:SquadPing("enemy")
        end,
    },
}

/* ----------------- Customization of the squadlead commands ---------------- */

SquadSystem.Config.Commands = {
    ["Assemble!"] = {
        chatMsg = "%PLAYER% commands: Assemble!",
        color = Color(255,255,255),
        imgur = "LQMO027",
    },
    ["All-around defense!"] = {
        chatMsg = "%PLAYER% commands: All-around defense!",
        color = Color(255,255,255),
        imgur = "LQMO027",
    },
    ["Defend position!"] = {
        chatMsg = "%PLAYER% commands: Defend position!",
        color = Color(255,255,255),
        imgur = "LQMO027",
    },
    ["All units! Attack!"] = {
        chatMsg = "%PLAYER% commands: All units! Attack!",
        color = Color(255,255,255),
        imgur = "LQMO027",
    },
    ["Cease fire!"] = {
        chatMsg = "%PLAYER% commands: Cease fire!",
        color = Color(255,255,255),
        imgur = "LQMO027",
    },
    ["Retreat!"] = {
        chatMsg = "%PLAYER% commands: Retreat!",
        color = Color(255,255,255),
        imgur = "LQMO027",
    },
    ["Spread out!"] = {
        chatMsg = "%PLAYER% commands: Spread out!",
        color = Color(255,255,255),
        imgur = "LQMO027",
    },
    ["Seek cover!"] = {
        chatMsg = "%PLAYER% commands: Seek cover!",
        color = Color(255,255,255),
        imgur = "LQMO027",
    },
}

/* -------------------------------------------------------------------------- */
/*                              Developer section                             */
/*                Please only touch if u know what u are doing                */
/* -------------------------------------------------------------------------- */


hook.Add("SquadSystem.Loaded", "SquadSystem.PingKeybinds", function()
    if not CLIENT then return end
    SummeLibrary:RegisterBind({
        name = "SquadSystem - Ping",
        key = nil,
        func = function()
            if not LocalPlayer():GetSquad() then return end
            SquadSystem:RequestCommunication("Ping (Normal)") -- If you have changed the name above, change it also here!
        end,
    })

    SummeLibrary:RegisterBind({
        name = "SquadSystem - Ping (enemy)",
        key = nil,
        func = function()
            if not LocalPlayer():GetSquad() then return end
            SquadSystem:RequestCommunication("Ping (Enemy)") -- If you have changed the name above, change it also here!
        end,
    })
end)
```