Not all values will be clear from decompiling the game, you might need to figure out some values by running the program and seeing the values stored in some pointers, or maybe you need more clarity on what exactly some vtable pointers point to.

## Debuggers

There are tools like WinDbg that allow you to launch the program in a suspended state, apply breakpoint and then run the programs, they are essential if you want to know what some startup functions do or when they are called.

### WinDbg Usage

Generally you are going to inspect the registers at a breakpoint, then use another program to better view the memory structure at said point, or if you need to inspect vtables, subtract that value to the base and use the decompiler to go there.

The main commands you are going to use are:

- bp \<module\> + \<offset\> : Adds Breakpoints
- bl : Lists breakpoints
- r : Shows registers
- ? \<expression\> : Expression operator to do calculations, useful when you need to compute the relative offset of an address

Examples:

- bp ApplicationMain+0xcafebabe
- ? rip - ApplicationMain

There are many more commands you can use, a good 5min search will give you most of the answers.

### Debugging a Mod

Let's say you completed everything and you now want to check why your mod crashes. Then you will need to launch WinDbg with the correct path and point it to your launcher.

You will need to hook to the child process spawned by the launcher, to do so you will need to run these commands after starting to debug:

- `.childdbg 1` : Enables child process debugging
- `sxe cpr` : Break on process creation

Your objective is using break points in the main game itself.

## Cheat Engine

A program that allows you track memory changes so that you can find values and pointers more easly that you can later link to your decompiler's output. While I hate the fact that downloading this piece of software has you walk a landmine of adware softwares in the installation process, it is very useful and worth it.

### Usage

Essentially Cheat Engine allows you to track memory values, and the included debugger help you to also keep track of what is writing/accessing a certian memory value.

So for instance if you want to mod the HP for a game, like probably the tutorial of CE shows you,
\(not sure, did it a long ago, it is a pretty solid tutorial\), you might want to debug based on
write access and see what writes to it, you might find the game's way of handling HP, maybe a
damage or heal function, or something that does both.

Most of the times you are going to use the write debugger breakpoint, as the access of course 
gives a lot of stuff you might not be interested in.

### DYOR

I will not give you a tutorial on this section about Cheat Engine, and I am going to assume that
if you got this far in reading this, you are capable enough to find such info and tutorials that 
explain the topic in a better way I could convey myself on a glorified notepad.

### Other

For the sake of alternatives, there is Squalr that is getting developed that might be an 
alternative, but there are probably similar programs out there, in a finished state,
that might do something similar, Cheat Engine is the one most are familiar with.

As a general note, any good Dynamic Analysis tool/toolset is needed.