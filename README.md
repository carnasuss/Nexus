# Nexus
This is a module-based framework created by me, and used for game organization and management.
It does support one shared API which can be used for managing, sharing, controlling different memory locations.
Note: This is a experimental project.
## Latest Version
Get latest Nexus version [here](https://www.roblox.com/library/9843212996/Nexus)
## Basic Usage
General pattern used in framework is single server/client script. Both scripts load server/client components which represents scripts but in a module wrap.
```lua
local Nexus = require(game.ReplicatedStorage.Nexus)
local Components = path.to.components -- Depends on which side this script belongs

Nexus.Start(Components)
```
### Component Example
Component is a structure, which made for serving some purpose (basically a script):
```lua
local Nexus = require(game.ReplicatedStorage.Nexus) -- Require framework.

local Services = require(Nexus.GetPackage("ServiceUtil"))
local TableUtil = require(Nexus.GetPackage("TableUtil"))
local Maid = require(Nexus.GetPackage("Maid"))
local Promise = require(Nexus.GetPackage("Promise"))

local new = Nexus.new -- Importing constructor function.

-- Component construction:

local Component = new "Component" { Name = "Component" } -- Construct new Component

function Component:OnNexusInit() -- When Nexus being initialized: Use this for creating events, constants, enums, e.t.c
    -- self.Name = component_info.Name
    -- self._maid = Maid.new()
end

function Component:OnNexusStart() -- When Nexus being started: Use this for game logic, math operations, e.t.c
	
end

function Component:OnDestroy() -- When Nexus being stopped (exclusive for client-side): Add tasks to self._maid for terminating memory leaks
    self._maid:DoCleaning()
    self = nil
end

return Component
```
You may create specific objects that can help you with your development with same "new" function:
```lua
self.Enum = new "Enum" {
  ["SOME"] = {
    ["THING"] = ""
  }
}
```
```lua
self.SomeEvent = new "RemoteListener" {
  Name = "SomeEvent".
  Type = "Event"
}
self.SomeEvent.OnServerEvent:Connect(function()
    -- Some code here.
end)
```
As it was said above, Nexus shares same API for every script.
You can access other component (only on the same script side) using: 
```lua
Nexus.GetComponent("Name")
```
Getting remote event/function that was created with "new" is possible with:
```lua
Nexus.GetRemote("Name")
```
Last feature added in Nexus is package management:
```lua
Nexus.GetPackage("Maid")
```
# Conclusion
Nexus is a fully customizable, semi-declarative open-source framework made for educational purposes.
Feel free to leave feedback to this framework :)
