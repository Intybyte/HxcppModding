When doing certain operations you need to keep in mind that the game's code and context uphold certain "expectations".

For example I once tried to run a thread in an Haxe game, and then call a function, bad idea, basically Haxe to handle garbage collection stores in the TLS a stack context pointer, used to handle the allocated data. Making a new thread from C code doesn't automatically create such stack context and everything blows up.

In some functions, probably hxcpp's internals, some data is used before the actual data type, in decompilers it will show up as `var[-1]` which might make you go insane, thinking you made some mistake, and no, you didn't, it generally has information about the object's hash or class type, but I am not sure myself, if you dig more information about it, feel free to PR here or make a page in the Haxe documentation or something similar. 99% of anything that has to do with Haxe is largely undocumented.

Upholding certain "expectations" might be complex depending on what you are trying to do. But keep in mind that if something breaks, it can also be some of these expectations being broken.