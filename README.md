# LibNPCInfo

Download Sites: [Curse](https://www.curseforge.com/wow/addons/libnpcinfo) | [Wago](https://addons.wago.io/addons/libnpcinfo) | [WowInterface](https://www.wowinterface.com/downloads/info26290-LibNPCInfo.html) | [Github Release](https://github.com/fang2hou/LibNPCInfo/releases)

## ⚜️ Introduction

Cause Blizzard do not provide an API for retrieving information about NPCs, this library is created to help you retrieve information about any NPC with its ID.

The algorithm behind this library is simple:

1. Create a new tooltip for scanning.
2. Attempt to set the unit of the tooltip to the NPC with the ID you want to retrieve information about.
3. Scrape the NPC's information from this tooltip.

It seems Blizzard limits the rate of tooltip unit setting, or the network quality also affects. Sometimes you need to wait a bit before you can retrieve information about a NPC. Since this library already added a double check for tooltips, usually you can safely use it.

## 🤌 Usage

```lua
-- Import the library
local lib = LibStub("LibNPCInfo")

-- The data is stored in the following format:
-- data = {
--  id: number
--  name: string
--  desc: string
-- }
local function dataHandler(data)
    print(format("%s, %s, %s", data.id, data.name, data.desc))
end

-- Only npcID will be returned if failed
local function failureHandler(npcID)
    print("failed: %d", npcID)
end

-- single call
lib.GetNPCInfoByID(43929, dataHandler, failureHandler, _G.print)
-- (print by callback function)
-- <<< 43929, 布靈登4000型, 等級??機械

-- multiple calls with the given ID table
local list = {43929, 32510}
lib.GetNPCInfoWithIDTable(list, dataHandler, _G.print)
-- (print by callback function)
-- <<< 43929, 布靈登4000型, 等級??機械
-- <<< 32510, 戰歌戰地衛士, 等級??人形生物(精英)
```
