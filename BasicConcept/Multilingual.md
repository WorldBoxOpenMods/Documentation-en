# Introduction

NML provides multilingual support for mods. You can switch language in game.

NML supports to load two format locale files: csv and json.

[csv Example](https://github.com/WorldBoxOpenMods/ModExample/blob/master/Locales/items_lang.csv)

[json Example](https://github.com/WorldBoxOpenMods/ModExample/blob/master/Locales/cz.json)

[Load Manually Example](https://github.com/WorldBoxOpenMods/ModExample/blob/master/ExampleModCode.cs#L62)About line 62, in `Reload`, find it yourself.

# Usage

`NeoModLoader.General.LM` provides some utilities to use localization

`LM.Get` is used to get text of a given key in current language
```csharp
LM.Get("Humans"); // It returns "人类" if your game language is Chinese
```

`LM.LoadLocales` is used to load `.csv` format locale file.
```csharp
LM.LoadLocales("path-to-csv-file");
```

`LM.LoadLocale` is used to load `.json` format locale file. To be attention, filename of the file should be target language short name. Such as:

```csharp
LM.LoadLocale("path-to-mod-folder/Locales/en.json"); // Load English locale file
LM.LoadLocale("path-to-mod-folder/Locales/cz.json"); // Load Simplified Chinese locale file
```

`LM.AddToCurrentLocale` is used to add a localization at runtime instantaneously.

```csharp
LM.AddToCurrentLocale("Humans", "New Humans Name Locale");
```

`LM.Add` is used to add a localization at runtime for a given language.

```csharp
LM.Add("en", "Humans", "New Humans Name Locale");
```

`LM.ApplyLocale` applies all changes

```csharp
LM.ApplyLocale(); // Apply changes of current language and update all LocalizedText
LM.ApplyLocale(False); // Apply changes of current language but not update all LocalizedText
LM.ApplyLocale("cz"); // Apply changes of Simplified Chinese and update all LocalizedText
LM.ApplyLocale("cz", False); // Apply changes of Simplified Chinese but not update all LocalizedText
```

## csv format locale file

The following is an example of `lang.csv`
```csv
key,cz,en,ch
Humans,人类,Humans,人類
Orcs,兽人,Orcs,獸人
```
Filename of csv format file is not important

## json format locale file

The following is an example for Simplified Chinese
```jsonc
// cz.json
{
    "Humans": "人类",
    "Orcs": "兽人"
}
```
Filename of json format file should be correspond to its language.

# Automatically load

You need to implements `ILocalizable` interface for you mod main class. `GetLocaleFilesDirectory` returns path to locale files' folder. `.csv` and `.json` files in the folder will be loaded before your mod's loading.