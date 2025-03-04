# Storage System Functions

Starting from AP 0.8 and 0.7 for 1.21.1, the ME and RS Bridge both now share the same functionality along with the new crafting system.
The following functions can be used for both the ME and RS Bridge

!!! failure
    <center> <h3> You need to place the inventory/tank you want to use to export/import stuff next to the ME/RS Bridge and **NOT** next to the computer! <h3> </center>

!!! tip
    You can use the command `/advancedperipherals getHashItem` with an item in your hand to get the MD5 hash of the NBT tags of the item. An MD5 Hash can look like this `ae70053c97f877de546b0248b9ddf525`.

## Common Functions

!!! info
    The item arguments(`filter: table`) accepts our item/fluid/chemical filters, you can check the syntax of these filters [here](/../guides/filters).

### isConnected
```
isConnected() -> boolean
```

Returns true if the block is currently connected to a grid

---

### isOnline
```
isOnline() -> boolean
```

Returns true if the grid is currently online and available

---

### getItem
```
getItem(filter: table) -> table | nil, string
```

Returns the first item that matches the filter. Or nil with a debug message if none could be found

---

### getFluid
```
getFluid(filter: table) -> table | nil, string
```

Returns the first fluid that matches the filter. Or nil with a debug message if none could be found

---

### getChemical
```
getChemical(filter: table) -> table | nil, string
```

Returns the first mekanism chemical that matches the filter. Or nil with a debug message if none could be found

---

### listItems
```
listItems(filter: table) -> table | nil, string
```

Returns every item that matches the filter or an empty table if none could be found.
An empty filter can be provided to get every resource.
Returns nil if there was an issue parsing your table.

---

### listFluids
```
listFluids(filter: table) -> table | nil, string
```

Returns every fluid that matches the filter or an empty table if none could be found.
An empty filter can be provided to get every resource.
Returns nil if there was an issue parsing your table.

---

### listChemicals
```
listChemicals(filter: table) -> table | nil, string
```

Returns every mekanism chemical that matches the filter or an empty table if none could be found.
An empty filter can be provided to get every resource.
Returns nil if there was an issue parsing your table.

---

### listCraftableItems
```
listCraftableItems(filter: table) -> table | nil, string
```

Returns every craftable item that matches the filter even if there is currently no item stored or an empty table if none could be found.
An empty filter can be provided to get every resource.
Returns nil if there was an issue parsing your table.

---

### listCraftableFluids
```
listCraftableFluids(filter: table) -> table | nil, string
```

Returns every craftable fluid that matches the filter even if there is currently no fluid stored or an empty table if none could be found.
An empty filter can be provided to get every resource.
Returns nil if there was an issue parsing your table.

---

### listCraftableChemicals
```
listCraftableChemicals(filter: table) -> table | nil, string
```

Returns every craftable mekanism chemical that matches the filter even if there is currently no chemical stored or an empty table if none could be found.
An empty filter can be provided to get every resource.
Returns nil if there was an issue parsing your table.

---

### listCells
```
listCells() -> table | nil, string
```

Returns every storage cell in the drives of the grid. Supports standard RS/ME cells and some third party cells.
Please open a feature request if some custom addon cells do not work

---

### listDrives
```
listCells() -> table | nil, string
```

Returns every drive connected to the system with the cells in it.

---

## Importing/Exporting functions

You may are used to two different functions, `importItemFromPeripheral` and `importItem`
The functions now support both at the same time. It first tries to parse the given string `target` as a cardinal or relative direction.
If that fails, it tries to search for a peripheral on the CC network which exposes an item handler or capability.

### importItem
```
importItem(filter: table, target: string) -> table | nil, string
```

Imports an item from the specified target. The filter can be empty to import every item. 
One call imports 64 of resources by default, can be set using the count filter key.

---

### exportItem
```
exportItem(filter: table, target: string) -> table | nil, string
```

Exports an item to the specified target. The filter can be empty to export every item.
One call exports 64 of resources by default, can be set using the count filter key.

---

### importFluid
```
importFluid(filter: table, target: string) -> table | nil, string
```

Imports a fluid from the specified target. The filter can be empty to import every fluid.
One call imports 1000mB of resources by default, can be set using the count filter key.

---

### exportFluid
```
exportFluid(filter: table, target: string) -> table | nil, string
```

Exports a fluid to the specified target. The filter can be empty to export every fluid.
One call exports 1000mB of resources by default, can be set using the count filter key.

---

### importChemical
```
importChemical(filter: table, target: string) -> table | nil, string
```

Imports a mekanism chemical from the specified target. The filter can be empty to import every chemical.
One call imports 1000mB of resources by default, can be set using the count filter key.

---

### exportChemical
```
exportChemical(filter: table, target: string) -> table | nil, string
```

Exports a mekanism chemical to the specified target. The filter can be empty to export every chemical.
One call exports 1000Mb of resources by default, can be set using the count filter key.

---

## Energy Related Functions

### getStoredEnergy
```
getStoredEnergy() -> int
```

Returns the stored energy in the grid.

---

### getEnergyCapacity
```
getEnergyCapacity() -> int
```

Returns the maximum energy capacity of the grid

---

### getEnergyUsage
```
getEnergyUsage() -> int
```

Returns the energy usage of the grid

---

???+ note
    Currently only supported by the ME Bridge

### getAvgPowerInjection
```
getAvgPowerInjection() -> int
```

Returns the stored energy in the grid.

---

## Storage Related Functions

### getTotalExternItemStorage
```
getTotalExternItemStorage() -> int
```

Returns the total amount of available external item storage.
External storage is available storage by either RS2's external storage bus or AE2's storage bus
This function returns the available storage in items even with the byte system from AE2

---

### getTotalExternFluidStorage
```
getTotalExternFluidStorage() -> int
```

Returns the total amount of available external fluid storage.
External storage is available storage by either RS2's external storage bus or AE2's storage bus
This function returns the available storage in millibuckets even with the byte system from AE2

---

### getTotalExternChemicalStorage
```
getTotalExternChemicalStorage() -> int
```

Returns the total amount of available external mekanism chemical storage.
External storage is available storage by either RS2's external storage bus or AE2's storage bus
This function returns the available storage in millibuckets even with the byte system from AE2

---

### getTotalItemStorage
```
getTotalItemStorage() -> int
```

Returns the total amount of available internal item storage.
This function returns the available storage in items for RS and in bytes for AE2

---

### getTotalFluidStorage
```
getTotalFluidStorage() -> int
```

Returns the total amount of available internal fluid storage.
This function returns the available storage in millibuckets for RS and in bytes for AE2

---

### getTotalChemicalStorage
```
getTotalChemicalStorage() -> int
```

Returns the total amount of available internal mekanism chemical storage.
This function returns the available storage in millibuckets for RS and in bytes for AE2

---

### getUsedExternItemStorage
```
getUsedExternItemStorage() -> int
```

Returns the total amount of used external item storage.
External storage is available storage by either RS2's external storage bus or AE2's storage bus
This function returns the used storage in items even with the byte system from AE2

---

### getUsedExternFluidStorage
```
getUsedExternFluidStorage() -> int
```

Returns the total amount of used external fluid storage.
External storage is available storage by either RS2's external storage bus or AE2's storage bus
This function returns the used storage in millibuckets even with the byte system from AE2

---

### getUsedExternChemicalStorage
```
getUsedExternChemicalStorage() -> int
```

Returns the total amount of used external mekanism chemical storage.
External storage is available storage by either RS2's external storage bus or AE2's storage bus
This function returns the used storage in millibuckets even with the byte system from AE2

---

### getUsedItemStorage
```
getUsedItemStorage() -> int
```

Returns the total amount of used internal item storage.
This function returns the used storage in items for RS and in bytes for AE2

---

### getUsedItemStorage
```
getUsedItemStorage() -> int
```

Returns the total amount of used internal fluid storage.
This function returns the used storage in millibuckets for RS and in bytes for AE2

---

### getUsedItemStorage
```
getUsedItemStorage() -> int
```

Returns the total amount of used internal mekanism chemical storage.
This function returns the used storage in millibuckets for RS and in bytes for AE2

---

### getAvailableExternItemStorage
```
getAvailableExternItemStorage() -> int
```

Returns the total amount of available and not used external item storage.
External storage is available storage by either RS2's external storage bus or AE2's storage bus
This function returns the available and not used storage in items even with the byte system from AE2

---

### getAvailableExternFluidStorage
```
getAvailableExternFluidStorage() -> int
```

Returns the total amount of available and not used external fluid storage.
External storage is available storage by either RS2's external storage bus or AE2's storage bus
This function returns the available and not used storage in millibuckets even with the byte system from AE2

---

### getAvailableExternChemicalStorage
```
getAvailableExternChemicalStorage() -> int
```

Returns the total amount of available and not used external mekanism chemical storage.
External storage is available storage by either RS2's external storage bus or AE2's storage bus
This function returns the available and not used storage in millibuckets even with the byte system from AE2

---

### getAvailableItemStorage
```
getAvailableItemStorage() -> int
```

Returns the total amount of available and not used internal item storage.
This function returns the available and not used storage in items for RS and in bytes for AE2

---

### getAvailableFluidStorage
```
getAvailableFluidStorage() -> int
```

Returns the total amount of available and not used internal fluid storage.
This function returns the available and not used storage in millibuckets for RS and in bytes for AE2

---

### getAvailableChemicalStorage
```
getAvailableChemicalStorage() -> int
```

Returns the total amount of available and not used internal mekanism chemical storage.
This function returns the available and not used storage in millibuckets for RS and in bytes for AE2

---

## Crafting System and functions

Since 0.8 and beta 0.7 for 1.21.1 we created a new crafting system for both the ME and RS Bridge
The functionality is mostly the same but since the RS api is currently not as extensive as the AE2 api, the RS Craft Job may miss some functions.

The craft function now returns an object instead of a boolean. Using that object is optional.
That object contains information about the job, if it was canceled, what was requested, what items may miss if calculation was not successful and much more.

Crafting is in both RS and AE async. If you request a feature, it calculates the recipe in the background and if that was successful it starts the task.
To support that in a simple way on a users end, we created that custom object.

When you schedule a task, it firsts starts calculation in the background and sends an event that the item is either not craftable or the calculation was started.
If calculation is done, there are several things that can happen. If the calculation was not successful and there were missing items, it fires the crafting event with the message "MISSING_ITEMs".
The missing items can be retrieved using the object's function `getMissingItems`.
Depending on if you use RS or AE2, it also may return other debug messages if the calculation was nto successful like overflow or cycle detected.

If the calculation was successful, the event will fire with the message `CRAFTING_STARTED` and then starts the crafting.

There are now two ways to track the progress. the `crafting` event will fire when the crafting is done, it was canceled or if other things might happen that affects the task.
The event also gives you an id to get the crafting object you would also get from the initial `craftX` function. Simply use `getCraftingJob` to get the object.

The other way is to regularly check if the crafting is done or canceled by calling the objects `isDone` or `isCanceled` function.
Using the event is more simple there.

Every function and property is described in more details below.

### Crafting Event

The new crafting event will be fired when the state of a task will change.

The name of the event is prefixed depending if you use the RS or ME Bridge.
Use `rs_crafting` for the RS Bridge and `me_crafting` for the ME Bridge.
**Values:**

1. `error: boolean` If an error occurred and the calculation or crafting was not successful
2. `id: int` The id of the craft job. Can be used to get the craft object
3. `debug_message: string` A debug message describing the current task of the task

```lua linenums="1"
local event, error, id, message = os.pullEvent("rs_crafting")
print("A crafting update occurred for Job #" .. id)
if error then
    print("There was an error while calculating or crafting the resource with the message " .. message)
else 
    print("The new state of the task is " .. message)
end
```


### craftItem
```
craftItem(filter: table) -> table | nil, string
```

Schedules a craft job for items. Will fire the crafting event when changes occur.
Or nil if there was an issue with parsing the filter

---

### craftFluid
```
craftFluid(filter: table) -> table | nil, string
```

Schedules a craft job for fluids. Will fire the crafting event when changes occur.
Or nil if there was an issue with parsing the filter

---

### craftChemical
```
craftChemical(filter: table) -> table | nil, string
```

Schedules a craft job for mekanism chemicals. Will fire the crafting event when changes occur.
Or nil if there was an issue with parsing the filter

---

### getCraftingTasks
```
getCraftingTasks() -> table
```

Returns every crafting task that is currently running.

---

### getCraftingJob
```
getCraftingJob(id: int) -> table | nil, string
```

Returns the crafting job object with the id. Nil if no object could be found

---

### cancelCraftingTasks
```
cancelCraftingTasks(filter: table) -> int
```

Cancels every crafting task where the output matches the filter

---

### getPatterns
```
getPatterns(pattern_filter: table) -> table | nil, string
```

Returns every pattern available to the grid or nil if there was an issue with parsing one of the filters.
The filter of this function is a bit different

You **can** specify filters for the output and input of patterns. If you don't provide any filter or just no argument at all, it will return every pattern.

To specify an input or output filter, you need to use an `input`/`output` key in the filters table.

For example 
```lua
-- Filter for any patterns with sticks as an output
outputFilter = {
     output = { 
        name="minecraft:stick" 
     } 
}

-- Filter for any patterns with sticks as an input
inputFilter = {
     input = { 
        name="minecraft:stick" 
     } 
}

-- Filter for any patterns with sticks as an output and planks as an input
inputFilter = {
     input = {
        name = "minecraft:oak_planks"
     },
     output = { 
        name="minecraft:stick" 
     } 
}

-- Or use the function without argument to get every pattern
patterns = bridge.getPatterns()
```

---

### isItemCraftable
```
isItemCraftable(filter: table) -> boolean
```

Returns true if there is a pattern for the provided item or nil if there was an issue with parsing the filter.

---

### isItemCrafting
```
isItemCrafting(filter: table) -> boolean
```

Returns true if there is a crafting job running for the provided item or nil if there was an issue with parsing the filter.

---

### isFluidCraftable
```
isFluidCraftable(filter: table) -> boolean
```

Returns true if there is a pattern for the provided fluid or nil if there was an issue with parsing the filter.

---

### isFluidCrafting
```
isFluidCrafting(filter: table) -> boolean
```

Returns true if there is a crafting job running for the provided fluid or nil if there was an issue with parsing the filter.

---


### isChemicalCrafting
```
isChemicalCrafting(filter: table) -> boolean
```

Returns true if there is a pattern for the provided mekanism chemical or nil if there was an issue with parsing the filter.

---

### isChemicalCrafting
```
isChemicalCrafting(filter: table) -> boolean
```

Returns true if there is a crafting job running for the provided mekanism chemical or nil if there was an issue with parsing the filter.

---


