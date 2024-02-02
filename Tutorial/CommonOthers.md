# HarmonyPatch

If you want to modifies functions in game or do something before or after a function, you need `HarmonyPatch`

[Documentation](https://harmony.pardeike.net/articles/intro.html)

Using `HarmonyPrefix` to overwrite vanilla function is easy to do, but it may causes incompatible with other mods. 

Here are two approaches to anesis it:

## HarmonyTranspiler

Insert IL code into methods to implement what you want. It has a learning cost, but is quite flexible and has a much more efficient runtime than `HarmonyPrefix`.

## Listener-Handler(Developing)

这是NML引入的一个功能, 简单来说, NML或其他模组提供使用`HarmonyTranspiler`实现的`Listener`来监听原版的函数执行, 并依次调用`Listener`下注册的所有`Handler`来处理.

NML还会捕获`Handler`执行时发生的异常, 当异常数量大于一定值后, 将会停用该`Handler`来保证游戏的正常运行.