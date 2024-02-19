# Introduction

## Mod Main Class Interface

### Different with NCMS

NCMS uses `ModEntry` attribute to locate mod's entry. NML recognizes mod main class by `IMod` interface.

### Same with NCMS

Mod main class needs to be child class of `MonoBehaviour`.

## Mod Function Interface

Except `IMod`, NML provides `IConfigurable`(Mod configuration), `ILocalizable`(Auto multigual), `IReloadable`(Method hotfix) and so on(more interfaces will be added in the future).

## Interface Packed

It is hard to implement too many interfaces. So there is [`BasicMod`](../Packed/BasicMod.md) which implements `IMod`, `IConfigurable`, `ILocalizable` already and provides some useful functions.

[Related Example](https://github.com/WorldBoxOpenMods/ModExample/blob/master/ExampleModCode.cs#L11)

# IMod

It is always used for mod main class. If you implements it manually, the class should also inherit from `MonoBehaviour`.

`IMod` requires to implement the following four methods

```csharp
/// <summary>
/// Get declaration of your mod
/// </summary>
public ModDeclare GetDeclaration();
/// <summary>
/// Get gameObject of your mod
/// </summary>
public GameObject GetGameObject();
/// <summary>
/// Get repository url of your mod
/// </summary>
public string GetUrl();
/// <summary>
/// This will be called when mod is loaded, even earlier than Awake, Start, OnEnable.
/// You can initialize your mod here.
/// </summary>
/// <param name="pModDecl">Declaration of the mod(It is initialized by NML already, record it by yourself)</param>
/// <param name="pGameObject">Instance of the mod(It is nearly a useless parameter for most mods)</param>
public void OnLoad(ModDeclare pModDecl, GameObject pGameObject);
```


# IConfigurable

If a mod's main class implements `IConfigurable`, you can see an entry button of configuration window for the mod.

`IConfigurable` requires to implement the following method

```csharp
/// <summary>
/// The methods will be called later than OnLoad, you need to return an instance ModConfig, you can create one temporarily or read from file. When configuration window is closed, all changes will be applied to the instance you created.
/// </summary>
public ModConfig GetConfig();
```

See more about `ModConfig` in [Mod Configuration](./ModConfiguration.md)

# ILocalizable

If a mod's main class implements `ILocalizable`, NML will load its locales text before `OnLoad`

`ILocalizable` requires to implement the following method
```csharp
/// <returns>The folder of locale files to load. It is "Locales" in BasicMod</returns>
public string GetLocaleFilesDirectory(ModDeclare pModDeclare);
```

# IReloadable

If a mod's main class implements `IReloadable` and set `Config.isEditor=true`, you can see a reload button for your mod.

Limit `Config.isEditor=true` is to avoid users to click reload button carelessly.

`IReloadable` requires to implement the following method

```csharp
/// <summary>
/// Mod reload order: Click Reload Button, recompile mod, hotfix methods, call Reload method
/// Because of limit of unity 2020, you need to control what to reload manually.
/// </summary>
public void Reload();
```

Except `IReloadable`, NML also provides `Hotfixable` attribute for method. It marks what method to be hotfixed. See more in [Mod Reload](../AdvancedTech/ModReload.md)