Ok now the base deserialize function supports file, all that is left is passing these files in the format we just defined.

[The ASM file](https://github.com/Intybyte/TEC2AssetAdder/blob/master/TEC2AssetAdder/asm_xml_file_load.asm)

The assembly hook is way simpler in this case, we are not using many references from our C code, and we are just making a call with no arguments, no return values, no nothing.

The LoadAllAssets:

- Gets every file with the `.xml` extension
- The file names should be a number, which will be the `offsetId` of the fucntion
- Passes to the original function (which is now patched) `file@<path>`

??? note
    The offsetId is used to determine the item type of the item 

There were some problems when implementing this, because I was trying to use the specific registries for the offsets, but it looks like they are more like temporary static variables, or the GC removed them after the use, I am unsure, but using them crashed the game as it wouldn't find valid vftables entries.

So I had to use the `hx::ArrayBase::__new` function to create a temporary array and dump everything there. Anyways the GLOBAL_REGISTRY will register them just fine.

The game works and here it is a file I used for testing:

```xml
<?xml version="1.0" encoding="utf-8" ?>
<data>
    <item id="1" picID="0" name="Chunk of Vaanium" value="40" min="0" max="90" e1="exp" e1power="1" e2="defFire" e2power="3" desc="Fossilized suffering" />
</data>
```

It is based on the `Chunk of Amber` item, it is basically the same but the floor spawn range is bigger.