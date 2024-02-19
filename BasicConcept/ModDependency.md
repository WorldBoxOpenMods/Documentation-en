Mod Dependencies in NML are divided into two categories: Hard dependency and soft dependency.

# Hard Dependency

It is also called neccessary dependency. A mod will be loaded only when all of its hard dependencies are loaded.

You can declare your mod hard dependent to some mods, and add reference to compiled DLL of them in project file(.csproj file) to make IDE give correct code analysis.

# Soft Dependency

It is also called optional dependency. A mod will be loaded no matter how many its soft dependencies loaded succefully. When a mod with soft dependencies are failed to compile, NML will try to compile it again without any soft dependencies.

To implement it, NML uses macro to control compilation.

When a soft dependent mod exists, NML will add its ID as macro when compiling your mod.

The following is in ModExample(soft dependent on "一米_中文名"). It implements the function of adding different name generators according to whether "一米_中文名" exists or not.

In above, "一米_中文名" is a Chinese mod for Chinese name generator. Because name rule in Chinese is distinct with Romance language family.

Name generator is used in naming custom creatures, custom items and custom races' kingdom, city, culture and so on. It is an important part in game.

```csharp
using System.IO;
// Uses macro to wrap all soft dependencies' code. "一米_中文名" is the ID of the soft dependency. Chinese_Name is a namespace provided by the mod. As shown below.
#if 一米_中文名
using Chinese_Name;
#endif

namespace ExampleMod.Content;

internal static class ExampleNameGenerators
{
    public static void init()
    {
        // If Chinese Name mod is compiled successfully, initialize Chinese name generators. Otherwise, initialize vanilla name generators
#if 一米_中文名
        init_chinese_name_generators();
#else
        init_vanilla_name_generators();
#endif
    }
    private static void init_chinese_name_generators()
    {
        string mod_folder = ExampleModMain.Instance.GetDeclaration().FolderPath;
        // Because the classes and methods are provided by ChineseName, you should wrap them with macro
#if 一米_中文名
        WordLibraryManager.SubmitDirectoryToLoad(Path.Combine(mod_folder,
            "additional_resources/word_libraries"));
        CN_NameGeneratorLibrary.SubmitDirectoryToLoad(Path.Combine(mod_folder,
            "additional_resources/name_generators"));
#endif
    }
    private static void init_vanilla_name_generators()
    {
        // No content yet
    }
}
```

For IDE code analysis, you should add reference to dependent mods' DLL. And you need to add mod's ID as predefined constants(All of the line is based on the fact that you want to use full features of IDE)

[Related Example Code](https://github.com/WorldBoxOpenMods/ModExample/blob/master/content/ExampleNameGenerators.cs)

[Related Example mod.json](https://github.com/WorldBoxOpenMods/ModExample/blob/master/mod.json)

[Related Predefined constant](https://github.com/WorldBoxOpenMods/ModExample/blob/master/ExampleMod.csproj#L7)

# How to reference to dependent mods

[Related example](https://github.com/WorldBoxOpenMods/ModExample/blob/master/ExampleMod.csproj#L44-L46)

## DLL reference

All files you need to reference are in `worldbox_Data/StreamingAssets/mods/NML/CompiledMods`. They are named as "ModID.dll"

## Project reference

If released dependent mod contains project file(.csproj), you can reference to it directly(You need to search methods in the web)