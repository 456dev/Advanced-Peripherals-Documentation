---
comments: true
---

# RS Bridge

!!! picture inline end
    ![!Image of the RS Bridge block](../img/previews/rs_bridge.png){ align=right }

The RS Bridge is able to interact with Refined Storage.
You can retrieve items, craft items, get all items as a list and more.

!!! warning "Requirement"
    Requires the [Refined Storage](https://www.curseforge.com/minecraft/mc-mods/refined-storage) mod to be installed

<p class="picture-spacing" style="--ps:0.6rem;"></p>

---

<div class="center-table" markdown>

| Peripheral Name | Interfaces with | Has events | Introduced in |
| --------------- | --------------- | ---------- | ------------- |
| rsBridge        | Refined Storage | No         | 0.3.6b        |

</div>

---

## Functions

The RS and ME Bridge now share the same functionality. Check [this Guide](../guides/storage_system_functions) for the whole documentation for every available feature.

## Examples

### Autocrafting script

Here is a script to craft items, the computer will re-craft every item needed (a specified amount) in the RS system. Everything is adjustable.

[Click here](https://gist.github.com/Seniorendi/26bd8ecaec400146f2e38790faceead8) to view the script

!!! bug
    This script does not work on versions above 0.4b

---

## Changelog/Trivia

**0.7.10b**  
Ported RS Bridge to 1.18.1.
Added `listCraftableItems` and `listCraftableFluids` back.

**0.7.3r**  
Added `getMaxItemDiskStorage`, `getMaxFluidDiskStorage`, `getMaxItemExternalStorage`, `getMaxFluidExternalStorage`, `getPattern` and `isItemCraftable`.
Removed `listCraftableItems` and `listCraftableFluids`.

**0.7r**  
The RS Bridge does uses computercraft relative and cardinal directions.
We also changed some function names.

**0.4b**  
Reworked the system of the RS Bridge, it has now more features and a new system for the `item` parameter.

**0.3.9b**  
Added the `importItem` and `exportItem` from container functions.

**0.3.6b**  
Added the RS Bridge with a good amount of features.
