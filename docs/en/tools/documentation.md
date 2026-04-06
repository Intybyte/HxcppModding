Your main objective in this phase is Intel, get as much as you can.

Is the developer available? Yes? Ask him which libs he used, did he use Lime? Flixel?

Once you have that, and you know that the game is in Haxe, and some libs, have windows open
with the source code and documentation of each one.

String literals are going to be very useful in this. Example:

You find that a weird function uses a string called "Not sure how to get template: " then you
can search it on Google \(if you think it is a lib call, but you are not sure\), or on the docs, 
find that the "Assets.hx" class in Lime has it, then you now know where you are, that there is
some weird string concatenation function, that the output of concatenating stuff is used in the
throw, and now that half of the functions make sense, you can single out more easily the other
stuff.

