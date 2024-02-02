# Introduction

NML does not load BepInEx, give everything to BepInEx. NML provides:
1. Recognize BepInEx mod and uploading approach
2. Link BepInEx mod to local BepInEx's `plugins` folder
3. Install BepInEx automatically when BepInEx does not exist

So there is not tutorial about how to make BepInEx mod, only related standard.

For NML to recognize information of your BepInEx mod, you should follow the below appointment:

1. `AssemblyTitleAttribute` annotates mod name
2. `AssemblyCompanyAttribute` annotates mod author
3. `AssemblyVersionAttribute` annotates mod version
4. `AssemblyDescriptionAttribute` annotates mod description

In addition, structure of your mod should be

```
BepInEx
    |---plugins
    |       |---Mod folder
    |       |       |---The only main DLL file
    |       |       |---icon.png(as mod icon)
    |       |       |---other not-DLL files
    |       |       |---other folders
```

At last, a DLL file will be recognized as a mod only when it references `Assembly-CSharp.dll`.