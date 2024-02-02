# For BasicMod

## Log

`BasicMod` provides three static methods to print log with mod name as prefix: `LogInfo`, `LogWarning`, `LogError`.

## Mod Instance

`BasicMod` provides static property to visit your mod instance directly: `Instance`.

## Mod Info

You can get your mod declaration through `BasicMod:GetDeclaration`. Definition of mod declaration is below:

```csharp
// Some fields are not shown here, see 'Basic Concept/Mod Declaration' for details
public class ModDeclare
{
    // Mod's name
    public string Name { get; private set; }
    // Mod's ID(It should be unique)
    public string UID { get; private set; }
    // Mod's author
    public string Author { get; private set; }
    // Mod's version
    public string Version { get; private set; }
    // Mod's simple description
    public string Description { get; private set; }
    // URL to repository of the mod
    public string RepoUrl { get; private set; }
    // Necessary(hard) dependencies
    public string[] Dependencies { get; private set; }
    // Optional(soft) dependencies
    public string[] OptionalDependencies { get; private set; }
    // Path to the folder of mod.json
    public string FolderPath { get; private set; };
    // Path to mod's icon file(Related to the folder of mod.json)
    public string IconPath { get; private set; }
}
```

## Mod Configuration Window

`BasicMod` is a mod providing configuring. You can get instance of `ModConfig` with `GetConfig`, Detailed see [Mod Configuration](../BasicConcept/ModConfiguration.md)

## Multiligual

Create a folder named `Locales`, and refers to [ModExample](https://github.com/WorldBoxOpenMods/ModExample/tree/master/Locales). Only json and csv files are supported.

# Others Common Features

## Log

`NeoModLoader.services.LogService` provides

* Normal: `LogInfo`,`LogWarning`,`LogError`,
* Print stack trace: `LogStackTraceAsInfo`, `LogStackTraceAsWarning`, `LogStackTraceAsError`
* Used in multiple threads: `LogInfoConcurrent`, `LogWarningConcurrent`, `LogErrorConcurrent`.

## Sprite

Create a folder named `GameResources` under your mod folder. `.png`, `.jpg`, `.jpeg` files will be explained by `sprites.json` or corresponding `.meta` files and loaded into game.

Then you can get them through `Resources.Load`, `SpriteTextureLoader.getSprite` or other related functions.

Detailed see [Resources Overview](../ModResources/Overview.md)

`NeoModLoader.utils.SpriteLoadUtils` provides

* `LoadSingleSprite(string)` to load a single picture file as a Sprite
* `LoadSprites(string)` search related `.meta` file(parsed into a `TextureImporter`, and provides a `SpriteSheet`) or `sprites.json` to load picture(s) at/under a path.