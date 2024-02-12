# HarmonyPatch

If you want to modifies functions in game or do something before or after a function, you need `HarmonyPatch`

[Documentation](https://harmony.pardeike.net/articles/intro.html)

Using `HarmonyPrefix` to overwrite vanilla function is easy to do, but it may causes incompatible with other mods. 

Here are two approaches to anesis it:

## HarmonyTranspiler

Insert IL code into methods to implement what you want. It has a learning cost, but is quite flexible and has a much more efficient runtime than `HarmonyPrefix`.

## Listener-Handler(Developing)

It is a feature provided by NML. Simply speaking, NML uses `HarmonyTranspiler` to implement `Listener`s listening to vanilla functions and call all registered and related `Handler` to handle the event. 

NML also catches exceptions when `Handler` excuting. When the number of exceptions is greater than a certain value, the Handler will be deactivated to ensure the normal operation of the game.