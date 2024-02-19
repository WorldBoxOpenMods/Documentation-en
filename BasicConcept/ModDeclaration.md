# Introduction

To keep consistent with NCMS mod, NML uses `mod.json` to contain meta information of a mod. And NML will search `mod.json` recursively and use the parent folder of `mod.json` as mod's folder.

[mod.json Example](https://github.com/WorldBoxOpenMods/ModExample/blob/master/mod.json)

mod.json file will be deserialized as below class through JSON

```csharp
public class ModDeclare
{
    public string name;                      // Name
    public string author;                    // Author
    public string version;                   // Version
    public string description;               // Simple description
    public string iconPath;                  // Icon path(related to folder of mod.json)
    public string GUID;                      // GUID of mod
    public string RepoUrl;                   // Url to repository
    public string[] Dependencies;            // Hard dependencies
    public string[] OptionalDependencies;    // Soft dependencies
    public string[] IncompatibleWith;        // Incompatible mods(Not implement yet)
}
```

If `GUID` is empty, NML uses captalization of "Author\_ModName" as mod's ID, non letter or numeric characters belonging to ASCII will be replaced with underscores. For example: 

<table><thead><tr><th width="172">Author</th><th width="186">Mod Name</th><th>ID</th></tr></thead><tbody><tr><td>Nikon#7777</td><td>Example Mod</td><td>NIKON_7777_EXAMPLE_MOD</td></tr><tr><td>一米</td><td>中文名</td><td>一米_中文名</td></tr></tbody></table>

"一米" and "中文名" are not belonging to ASCII, so they are not replaced.

## Url to Repository

You can keep it empty. It used for users to report bug/suggestions.


## Hard dependencies

It should be an array of mods' ID. NML tries to load mod only when all of its hard dependencies compiled successfully.

Mods can directly access the public content of dependent mods

## Soft dependencies

It should be an array of mods' ID. NML load mod no matter how many its soft dependencies compiled successfully. NML will add mods' ID as macro(predefined constants) to mark what soft dependent mods compiled successfully.



## Incompatible

It should be an array of mods' ID. It has not been completed yet.

## Icon path

Related to mod folder(folder of `mod.json`). It can be empty. When it is empty, icon of your mod will be icon of NML.

# Usage in mod

When a mod's `OnLoad` is called, its `ModDeclare` has been processed by NML. You can access its content according to the following definition of `ModDeclare`:

```csharp
public class ModDeclare
{
    // Mod name
    [JsonProperty("name")] 
    public string Name { get; private set; }
    // Mod ID
    public string UID { get; private set; }
    // Author
    [JsonProperty("author")] 
    public string Author { get; private set; }
    // Version
    [JsonProperty("version")] 
    public string Version { get; private set; }
    // Simple description
    [JsonProperty("description")] 
    public string Description { get; private set; }
    // Url to repository
    [JsonProperty("RepoUrl")] 
    public string RepoUrl { get; private set; }
    // Array of hard dependencies' ID
    [JsonProperty("Dependencies")] 
    public string[] Dependencies { get; private set; }
    // Array of soft dependencies' ID
    [JsonProperty("OptionalDependencies")] 
    public string[] OptionalDependencies { get; private set; }
    // Array of incompatible mods' ID
    [JsonProperty("IncompatibleWith")] 
    public string[] IncompatibleWith { get; private set; }
    // Path of the folder of mod.json
    public string FolderPath { get; private set; } = null!;
    // Path to mod's icon file(related to FolderPath)
    [JsonProperty("iconPath")] 
    public string IconPath { get; private set; }
}
```
