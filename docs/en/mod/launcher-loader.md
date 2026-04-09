If you want to create mods, you first need to create a mod launcher and a mod loader.

The easiest way is creating the mod launcher and loader separate, so:

- Create a "launcher.exe" program that launches the game in a suspended state.
- Make the launcher load the "loader.dll" inside the game's address space.
- Make the "loader.dll" assembly hook to the game to acquire the correct context.
- Make the "loader.dll" load some `dll` files from a Mods folder 
- The launcher waits until the libary is loaded, then runs the program normally.

The loader can also have some useful stuff for people that Mod the game, handling some versioning, expose some game structures, expose some events.