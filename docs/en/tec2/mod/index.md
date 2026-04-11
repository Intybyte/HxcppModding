I will rewrite the objective here in case the Reverse Engineering section hard resetted someone's head (it kinds of does that, not very easy topics).

> The objective is adding custom items to the game, each item has a picture, but for the sake of simplifying for now we will target only adding items themselves and maybe recycle the image assets of other items.

So we can handle this in a lot of different ways.

Q: Do we reimplement XML parsing ourselves or do we hook to the native functions?

A: I am lazy, let's just hook to the XML parse function.

Q: So when do we actually parse the stuff? When the dll is loaded said section wasn't been run yet, and probably the GLOBAL_REGISTRY with all items is not yet alive.

A: Slighly before the end of the `tec2::Deserialize::allItemDefinitions` function, because I don't understand what is going on at the very end.

![Hooking preview](../../../img/tec2/mod/hooking_preview.png)

We are going to add items from a XML file format, the files will be located in `/Mods/Assets/*.xml`.

Let's get started!