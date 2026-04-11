Assign a meaningful namespace to each function, for instance if it is a haxe call you can use:

`hx::<package>::<class>::<method-name>`

If it is some internal call to Haxe's language implementation, like for instance the GC is handled using a `hx::StackContext` on the TLS you should use `hxcpp` to better separate the two. 

If it is some library call you can use:

`<lib-name>::<package>::<class>::<method-name>`

If you are certain that it is custom custom from the game you can use:

`<game-acronym>::<package>::<class>::<method-name>`

Use a namespace regarding the game only if you are sure that said function is a custom one defined by the game, and as always try to "safely guess" what and where the method might be, you are going to hit some constructors so it is better to consider the OOP aspect while you are at it and.

For instance instead of making a function like `allocateItemData`, it would make more sense to name it something like `tec2::ItemData::new` for instance \(you might want to add package namespacing if you see a lot of xml related stuff for instance, but that is very subjective for these cases\).