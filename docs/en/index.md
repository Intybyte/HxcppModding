Haxe is a multiplatform programming language that can compile to many different targets. While this makes it incredibly versatile, it also makes modding Haxe games more challenging. 

To create mods, you often need to work with multiple targets at once, which can require understanding several different platforms, different implementation of the haxe language, and different reverse engineering techniques.

For simplification, this guide focuses on Hxcpp games, even more in the specific, those compiled with Windows, but it can be applied to Linux also, with some minor changes that is.

One of the main challenge is that now, together with having to figure out what sheneningas C++ is pulling with duplicating functions across the code, inlining, virtual table magic, you now also have to deal with Hxcpp converting Haxe code to cpp.

But it can also become and advantage knowing the general structure on how hxcpp transpiles to C++, because we can more easily detect some methods... it doesn't help however that Haxe has inline functions that make everything more messy to read, but once you track them down and categorize them with extreme prejudice, reading the decompiled code gets easier.

This guide provides tools, techniques, and using the game [The Enchanted Cave 2](https://store.steampowered.com/app/368610/The_Enchanted_Cave_2/) as a reference.