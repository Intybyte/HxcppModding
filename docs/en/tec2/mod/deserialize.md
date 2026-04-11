So normally what the deserialize function does is:

- Use the string parameter (I called it `stringFile`) as a reference where to data from.
- It gets passed to many wrappers of (`lime::Assets::getAsset`) which then give a String containing the xml contents.
- The haxe std lib processes it.
- The function extracts the xml attributes and loads it into a custom object (we will call it `itemData`)
- `itemData` gets added to the `GLOBAL_REGISTRY` and to an output parameter

So what we can do is intercept the first wrapper call of `lime::Assets::getAsset` (I called it ` getTextAssetObj2StrW`), replace it with our own logic that checks if the string start with some prefix normally unused, for instance I am using `file@`. 

If it doesn't start with the prefix, continue as if nothing happened, just use ` getTextAssetObj2StrW`.

If it does instead start with `file@` then whatever comes after is the absolute reference to the XML file we want to deserialize, and our own functions will handle it.

[Here the ASM File](https://github.com/Intybyte/TEC2AssetAdder/blob/master/TEC2AssetAdder/asm_xml_file_support.asm)

First we define `isAssetIdFile` that just does a string check to see if it has the prefix. Then restore all the volatile functions, as if nothing happened. And then the logic is as explained, out own function that handles the custom files will be called `HandleXmlFileSupport`.

As a cautionary tale, make the functions empty at the beginning, or make them behave the same way they would at the start, just to check if you are hooking properly, if your patch is the correct size and everything you are doing makes sense. After that start to fill up the your functions with the real logic.