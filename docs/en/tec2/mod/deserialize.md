So normally what the deserialize function does is:

- Use the string parameter (I called it `stringFile`) as a reference where to data from.
- It gets passed to many wrappers of `lime::Assets::getAsset` which then give a String containing the xml contents.
- The haxe class Xml in Std processes it.
- The function extracts the xml attributes and loads it into a custom object (we will call it `itemData`)
- `itemData` gets added to the `GLOBAL_REGISTRY` and to an output parameter

So what we can do is intercept the first wrapper call of `lime::Assets::getAsset` (I called it ` getTextAssetObj2StrW`), replace it with our own logic that checks if the string start with some prefix normally unused, for instance I am using `file@`. 

If it doesn't start with the prefix, continue as if nothing happened, just use ` getTextAssetObj2StrW`.

[Here the ASM File](https://github.com/Intybyte/TEC2AssetAdder/blob/master/TEC2AssetAdder/asm_xml_file_support.asm)

First we define `isAssetIdFile` that just does a string check to see if it has the prefix. Then restore all the volatile functions, as if nothing happened. And then the logic is as explained, our own function that handles the custom files will be called `HandleXmlFileSupport`.

??? warning

    As a cautionary tale, make the functions empty at the beginning, or make them behave the same way they would normally, just to check if you are hooking properly. 
    
    After confirming that your patch is the correct size and everything you are doing makes sense, you can start to fill up the your functions with the real logic.