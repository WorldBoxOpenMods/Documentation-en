# Introduction

This can be said to be the most technical aspect of the entire NML, but its usage is very simple.

You only need to add `[Hotfixable]` for a method and set `Config.isEditor=true` and then click button.

The function is often used to debug. Consider such a scene:

```
Here is a bug. It needs a lot of time to trigger.

The bug will disappear after save-load.

The bug will keep a long time after appearing.
```

If you add log and restart game once and once again to get information of the bug, it wastes a lot of time.

If you uses the function, you can pause game, and modify your mod code, add log or even try to fix the bug. Then click button to reload your mod, you can see result.

Except above, you can use it on UI designing.

# Usage

1. Implement `IReloadable` and set `Config.isEditor=true`
2. Launch game
3. Meet problem
4. Add `Hotfixable` attribute to methods to modify
5. Modify methods
6. Click Reload Button of your mod
   
# Example

No video now.

[Example Part 1](https://github.com/WorldBoxOpenMods/ModExample/blob/master/content/ExampleTraits.cs)

[Example Part 2](https://github.com/WorldBoxOpenMods/ModExample/blob/master/ExampleModCode.cs#L55)

# Tips

1. You cannot add `Hotfixable` to `MonoBehaviour`'s methods such as `Awake`,`Update`
2. You cannot add `Hotfixable` to constructor or deconstructor of a class
3. You can add `Hotfixable` to `Reload`
4. You can add `Hotfixable` at runtime
5. You can create a new method at runtime through `Hotfixable`
6. You can add `Hotfixable` to lambda method, like below:

```csharp
trait.action_special_effect = [Hotfixable] (pTarget, pTile) =>
{
    LogService.LogInfo("Before hotfixed trait action");
}
```
