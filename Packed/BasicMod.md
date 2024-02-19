Basic Mod is exactly class `BasicMod`. If you want these features, you should make your mod main class inherit from `BasicMod` instead of `MonoBehaviour` and `IMod`.

# Mod Loading

`BasicMod` is different with `IMod` in modder's layer. BasicMod implements `OnLoad` in IMod, and call `OnModLoad` to initialize mod. You should implement OnModLoad in BasicMod instead of OnLoad.

# Multilingual

`BasicMod` loads files under folder `Locales` automatically. `cz.json` is Simplified Chinese, `en.json` is English, `ch.json` is Tranditional Chinese.

The following is an example of localization for Simplified Chinese in JSON format.
```jsonc
// cz.json
{
    "Humans": "人类",
    "Orcs": "兽人"
}
```

Except of `.json` file, you can also use `.csv` to make localization.

The following is an example `lang.csv`
```csv
key,cz,en,ch
Humans,人类,Humans,人類
Orcs,兽人,Orcs,獸人
```

File name for `.csv` is not important.

# Mod Configuration

`BasicMod` provides default mod configuration file(`default_config.json` under mod's folder) and consistent user's mod configuration.

You can write `default_config.json` refer to [Mod Configuration](../BasicConcept/ModConfiguration.md)

## Default mod configuration file

It provides format of mod configuration and default values for them.

### When add/remove configuration item(excluding modifying default value)

Consistent user's mod configuration will add/remove corresponding items with new default values.