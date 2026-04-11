Let's start with the basics, the games is x64 so we are going to target that, let's make a mod loader and mod launcher.

I made the mod launcher copying some of the code from the [CubeWorldModLauncher Alpha](https://github.com/ToufouMaster/Cube-World-Mod-Launcher), you can find the launcher at [TEC2ModLauncher](https://github.com/Intybyte/TEC2ModLauncher).

For the mod loader, I made a simplified one mostly by myself, basing myself again on CubeWorld's mod loader, but this game is in x64 unlike the previous one and I had to look for a good place where to start the logic.

I found a function called slighly after what seems like setting the title to the application, it is the function at `FUN_14049cce0`, which to be honest, I have no idea what this function does, but it seems to be a solid hooking spot at least for now.

I also track down the `__boot_all` method, which doesn't seem a good place to hook, as sometimes stuff aren't executed here, not sure why, the `__boot_all` was at `FUN_140032980`.

By starting the ".exe" with my launcher, which in turn loads the mod loader, we now have a basic structure going, and there seems to be some extra output on screen, seems to be `hx::trace` doing something, these informations may become useful later.   

You can find the mod loader at [TEC2ModLoader](https://github.com/Intybyte/TEC2ModLoader/)