---
comments: true
---

# ME Bridge

!!! picture inline end
    ![!Image of the ME Bridge block](../img/previews/me_bridge.png){ align=right }

The ME Bridge is able to interact with Applied Energistics 2.
You can retrieve items, craft items, get all items as a list and more. The ME Bridge uses one channel.

!!! warning "Requirement"
    Requires the [Applied Energistics 2](https://www.curseforge.com/minecraft/mc-mods/applied-energistics-2) mod to be installed

<p class="picture-spacing" style="--ps:0.6rem;"></p>

---

<div class="center-table" markdown>

| Peripheral Name | Interfaces with | Has events | Introduced in |
| --------------- | --------------- | ---------- | ------------- |
| meBridge        | ME System       | Yes        | 0.3b          |

</div>

---

!!! failure
    <center> <h3> You need to place the inventory/tank you want to use to export/import stuff next to the ME Bridge and **NOT** next to the computer! <h3> </center>

=== "1.20.1-0.7 and older"

    !!! info
        If you are playing on 0.7 for the minecraft version 1.21.1 and older, please use the content tab for "1.21.1-0.7 and newer".
        The following documentation contains the legacy ME and RS bridge features which will be replaced with the next stable AP version.

        The newer ME and RS Bridge system will eventually be back ported to 1.20.1 and 1.19.2 with 0.8.

    <div class="result" markdown>

    ## Functions
    
    !!! info
    The item arguments(`item: table`) accepts our item filters, you can check the syntax of these filters [here](/../guides/filters).
    
    ### craftItem
    ```
    craftItem(item: table) -> boolean
    ```
    
    Tries to craft the provided `item`, returns true if it successfully starts crafting.
    
    #### Item Properties
    
    Check the [item filters guide](/../guides/filters) for more info!
    
    | item             | Description                                 |
    | ---------------- | ------------------------------------------- |
    | name: `string`   | The registry name of the item or a tag      |
    | count: `number?` | The amount of the item to craft             |
    | nbt: `string?`   | NBT to match the item on                    |
    
    **OR**
    
    | item                  | Description                                 |
    | --------------------- | ------------------------------------------- |
    | fingerprint: `string` | A unique fingerprint which identifies the<br>item to craft |
    | count: `number?`      | The amount of the item to craft             |
    
    ---
    
    ### craftFluid
    ```
    craftFluid(fluid: table, amount: number) -> boolean
    ```
    
    Tries to craft the provided `fluid` of the given `amount`, returns true if it successfully starts crafting.
    
    #### Fluid Properties
    
    Check the [fluid filters guide](/../guides/filters) for more info!
    
    | fluid             | Description                                 |
    | ---------------- | ------------------------------------------- |
    | name: `string`   | The registry name of the fluid or a tag      |
    | count: `number?` | The amount of the fluid to craft             |
    | nbt: `string?`   | NBT to match the fluid on                    |
    
    **OR**
    
    | fluid                  | Description                                 |
    | --------------------- | ------------------------------------------- |
    | fingerprint: `string` | A unique fingerprint which identifies the<br>fluid to craft |
    | count: `number?`      | The amount of the fluid to craft      
    
    ---
    
    ### getItem
    ```
    getItem(item: table) -> table
    ```
    
    Returns a table with information about the item type in the system.
    
    #### Properties
    
    | result                 | Description                                             |
    | ---------------------- | ------------------------------------------------------- |
    | name: `string`         | The registry name of the item                           |
    | fingerprint: `string?` | A unique fingerprint which identifies the item to craft |
    | amount: `number`       | The amount of the item in the system                    |
    | displayName: `string`  | The display name for the item                           |
    | isCraftable: `boolean` | Whether the item has a crafting pattern or not          |
    | nbt: `string?`         | NBT to match the item on                                |
    | tags: `table`          | A list of all of the item tags                          |
    
    ---
    
    ### importItem
    ```
    importItem(item: table, direction: string) -> number
    ```
    
    Imports an `item` from a container in the `direction` to the RS System.  
    Returns the number of the `item` imported into the system.
    
    !!! tip "Since version 0.7r"
    You can now use both relative (`right`, `left`, `front`, `back`, `top`, `bottom`) and cardinal (`north`, `south`, `east`, `west`, `up`, `down`) directions for the `direction` argument.
    
    ```lua linenums="1"
    local bridge = peripheral.find("meBridge")
    
    -- Imports 32 dirt from the container above into the system
    bridge.importItem({name="minecraft:dirt", count=1}, "up")
    ```
    
    ---
    
    ### exportItem
    ```
    exportItem(item: table, direction: string) -> number
    ```
    
    Exports an `item` to a container in the `direction` from the RS bridge block.  
    Returns the number of the `item` exported into the container.
    
    ```lua linenums="1"
    local bridge = peripheral.find("meBridge")
    
    -- Exports 1 "Protection I" book into the container above
    bridge.exportItem({name="minecraft:enchanted_book", count=1, nbt="ae70053c97f877de546b0248b9ddf525"}, "up")
    ```
    
    ---
    
    ### importItemFromPeripheral
    ```
    importItemFromPeripheral(item: table, container: string) -> number
    ```
    
    Similar to [`importItem()`](#importitem) it imports an `item` from a container which is connected to the peripheral network.  
    `container` should be the exact name of the container peripheral on the network.  
    Returns the number of the `item` imported from the container.
    
    ---
    
    ### exportItemToPeripheral
    ```
    exportItemToPeripheral(item: table, container: string) -> number
    ```
    
    Similar to [`exportItem()`](#exportitem) it exports an `item` to a container which is connected to the peripheral network.  
    `container` should be the exact name of the container peripheral on the network.  
    Returns the number of the `item` exported into the container.
    
    ---
    
    ### getMaxItemDiskStorage
    ```
    getMaxItemDiskStorage() -> number
    ```
    
    !!! success "Added in version 0.7.3r"
    
    Returns the total amount of available item disk storage.
    
    ---
    
    ### getMaxFluidDiskStorage
    ```
    getMaxItemDiskStorage() -> number
    ```
    
    !!! success "Added in version 0.7.3r"
    
    Returns the total amount of available fluid disk storage.
    
    ---
    
    ### getMaxItemExternalStorage
    ```
    getMaxItemExternalStorage() -> number
    ```
    
    !!! success "Added in version 0.7.3r"
    
    Returns the total amount of available external item disk storage.
    
    ---
    
    ### getMaxFluidExternalStorage
    ```
    getMaxFluidExternalStorage() -> number
    ```
    
    !!! success "Added in version 0.7.3r"
    
    Returns the total amount of available external fluid disk storage.
    
    ---
    
    ### getEnergyStorage
    ```
    getEnergyStorage() -> number
    ```
    
    Returns the stored energy of the whole RS System in FE.
    
    ---
    
    ### getMaxEnergyStorage
    ```
    getMaxEnergyStorage() -> number
    ```
    
    Returns the maximum energy storage capacity of the whole RS system in FE.
    
    ---
    
    ### getEnergyUsage
    ```
    getEnergyUsage() -> number
    ```
    
    Returns the energy usage of the whole RS System in FE/t.
    
    ---
    
    ### getPattern
    ```
    getPattern(item: table) -> table | nil, string
    ```
    
    !!! success "Added in version 0.7.3r"
    
    Returns the crafting pattern for the `item` if one exists.
    
    #### Properties
    
    | pattern               | Description                                             |
    | --------------------- | ------------------------------------------------------- |
    | inputs: `table`       | A list of all the input items                           |
    | outputs: `table`      | A list of all of the output items                       |
    | byproducts: `table`   | A list of any byproduct items                           |
    | processing: `boolean` | If the pattern is currently being used in crafting      |
    
    ---
    
    ### isItemCrafting
    ```
    isItemCrafting(item: table) -> boolean
    ```
    
    Returns true if a crafting job for the `item` exists.
    
    ---
    
    ### isItemCraftable
    ```
    isItemCraftable(item: table) -> boolean
    ```
    
    !!! success "Added in version 0.7.3r"
    
    Returns true if the `item` is craftable.
    
    ---
    
    ### listCraftableItems
    ```
    listCraftableItems() -> table
    ```
    
    !!! danger "Does not exist in versions >=0.7.3r, <0.7.10b"
    
    Returns a list of information about all craftable items
    
    #### Properties
    
    | item / fluid           | Description                                             |
    | ---------------------- | ------------------------------------------------------- |
    | name: `string`         | The registry name of the item                           |
    | fingerprint: `string?` | A unique fingerprint which identifies the item to craft |
    | amount: `number`       | The amount of the item in the system                    |
    | displayName: `string`  | The display name for the item                           |
    | isCraftable: `boolean` | Whether the item has a crafting pattern or not          |
    | nbt: `string?`         | NBT to match the item on                                |
    | tags: `table`          | A list of all of the item tags                          |
    
    ```lua linenums="1"
    local bridge = peripheral.find("meBridge")
    
    -- print out all craftable items
    craftableItems = bridge.listCraftableItems()
    for _, item in pairs(craftableItems) do
        print(item.name)
    end
    ```
    
    ---
    
    ### listCraftableFluids
    ```
    listCraftableFluids() -> table
    ```
    
    !!! danger "Does not exist in versions >=0.7.3r, <0.7.10b"
    
    Returns a list of information about all craftable fluids
    
    ---
    
    ### listItems
    ```
    listItems() -> table
    ```
    
    Returns a list of information about all items in the RS System.
    
    ---
    
    ### listFluids
    ```
    listFluids() -> table
    ```
    
    Returns a list of information about all fluids in the RS System.
    
    ---

    </div>

=== "1.21.1-0.7 and newer"
    <div class="result" markdown>
    
    !!! info
        If you are playing on 0.7 for the minecraft version 1.20.1 and older, please use the content tab for "1.20.1-0.7 and older".
        The following documentation also works for the canary 0.8 version.

        The new ME and RS Bridge systems will eventually be back ported to 1.20.1 and 1.19.2 with 0.8.

    ## Functionality
    
    The RS and ME Bridge now share the same functionality. Check [this Guide](../guides/storage_system_functions.md) for the whole documentation for every available feature.

    </div>

---

## Examples

### Requester

The requester is a successor for the old "Automatic Autocrafting" script which uses the old ME Bridge functions.
It currently only works with AP on 1.21.1 or on 1.19.2 0.8 and supports both the ME and the RS Bridge at the same time.

This script automatically schedules crafting jobs for pre-defined items, fluids and mekanism chemicals
Do you want 500 glass in your me system at all times? Add glass to the list and the script will craft it for you.
No need for level emitters or crafting cards!

You can find instructions on how to install the script [here](https://github.com/SirEndii/Lua-Projects/tree/master)

![Requester example script preview](../img/bridge_requester.png)

### Automatic Autocrafting

This script automatically crafts items in a list.
Do you want 500 glass in your me system at all times? Add glass to the list and the script will craft it for you.
No need for level emitters or crafting cards!

You can find instructions on how to install the script [here](https://github.com/SirEndii/Lua-Projects/tree/master)

![Automatic autocrafting example script preview](../img/me_bridge/autocraft_example.png)

### ME Crafting CPUs

This script shows you some statistics about the ME crafting cpus.

You can find instructions on how to install the script [here](https://github.com/SirEndii/Lua-Projects/tree/master)

![Me system crafting cpu example script preview](../img/me_bridge/mecpus_example.png)

---

## Changelog/Trivia

**0.7r**  
The ME Bridge does uses computercraft relative and cardinal directions.
We also changed some function names.

**0.4b**  
Reworked the system of the ME Bridge, it now has more features and a new system for the `item` parameter.

**0.3.9b**  
Added the `importItem` and `exportItem` from container functions.

**0.3b**  
Added the ME Bridge with a good amount of features.
