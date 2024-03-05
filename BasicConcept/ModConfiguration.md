# Introduction

NML provides a user friendly interface for `ModConfig`, like below:

![ModConfig](../.gitbook/assets/MODCONFIG.png)

[Corresponding config file Example](https://github.com/WorldBoxOpenMods/ModExample/blob/master/default_config.json)

There are two ways of setting up your project to use this window.

If your main class implements `IMod`, you need to implement the `IConfigurable` interface with the same class. Return an instance of `ModConfig` to pass and receive the configuration result through your main class' `GetConfig()` method.

If your main class implements `BasicMod<T>`, you do not need to implement `IConfigurable`. You only need to create a file named `default_config.json` under your mod folder.([ModTemplate](https://github.com/WorldBoxOpenMods/ModTemplate/tree/master) provides a default one), and edit/add to it.

[Example of using `GetConfig()` with `BasicMod<T>`](https://github.com/WorldBoxOpenMods/ModTemplate/blob/master/ModClass.cs#L13)

`default_config.json` is an abstract serialized `ModConfig`. It provides the format and default values for configuration. The user's configuration will be saved in another file consistently.

# Edit default_config.json

`default_config.json` is a JSON file.

The file will be deserialized into an instance of `Dictionary<string, Dictionary<string, ModConfigItem>>`, which is retrieved with `ModConfig.GetConfig()`. 

The first `string` is the `groupId` of the config group. In the example default_config.json in ModTemplate the groupId is `"Default"`. The second string is the `Id` of the config item, while `ModConfigItem` is a class which contains methods for getting and setting the value of the config item. 

Note that `ModConfigItem` always returns an `object` so you will need to cast the result of `ModConfigItem.GetValue()` to the intended data type.

For `ModConfigItem`, you need provide:

1. `Id`: Unique identifier of the item in the group. It is used to get value of the item in your code.
2. `Type`: Type of configuration item. These are valid: `SWITCH`, `SLIDER`, `TEXT`(text edit).
3. `IconPath`: Path of item icon, it will be loaded through `Resources.Load`. You can leave it empty if you do not need icon for it.
4. `TextVal`: If `Type`=="TEXT", you need to fill the item(string) as default value of text edit.
5. `FloatVal`: If `Type`=="SLIDER", you need to fill the item(float) as default value of slider.
6. `BoolVal`: If `Type`=="SWITCH", you need to fill the item(bool) as default value of switch button.
7. `MinFloatVal`: If `Type`=="SLIDER", you can fill the item(float) as minimum value of slider, default to be 0.
8. `MaxFloatVal`: If `Type`=="SLIDER", you can fill the item(float) as maximum value of slider, default to be 1.
9. `Callback`: Callback method name. It's optional.

For `Callback`, you need to define a static method, the method accepts a parameter(Type of the parameter should be the type of `ModConfigItem`'s value). For such a `ModConfigItem`:

```json
{
    "Id": "Example",
    "Type": "SLIDER",
    "FloatVal": 0.5,
    "Callback": "ExampleType:ExampleCallbackMethod"
}
```

You need to implement such a method below

```csharp
namespace ANYNAMESPACE;

class ExampleType
{
    void ExampleCallbackMethod(float pUpdatedValue)
    {
        // Your callback method's code
    }
}

```

[Callback Example](https://github.com/WorldBoxOpenMods/ModExample/blob/master/content/ExampleActions.cs)

Please note, in-game changes to the mod configuration will be applied after you close the configuration window, not in real-time.

Except above, you need to provide locale definitions for `groupId` and `Id`. Please see [Multilingual](Multilingual.md) for how to provide locale definitions.
