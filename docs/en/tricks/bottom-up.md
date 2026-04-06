In case you don't understand the high level logic that is going on, just go lower level.

Examples:

You can track down basic functions like `hx::InternalNew` and now you have a basic idea of
where the allocations are taking places.

You can track where arrays are created and now you have a good idea what sections of the code are
using arrays, without having to figure out much about some vtable calls.

Once you understand the basic stuff, you build your way up and get a solid idea of where the haxe
internals and lib internals, and once you have figured those out you can move up to the actual
game's logic with more context.