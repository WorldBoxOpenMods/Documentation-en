---
description: Basic development configuration
layout:
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

We configure development environment in the section.

# People

1. You need to be intellectually complete and have the ability to think for yourself
2. In order To better solve The problems you will encounter, it is recommended to first read [How To Ask Questions The Smart Way](http://www.catb.org/~esr/faqs/smart-questions.html)
3. Then you need to master [the most basic CSharp knowledge](https://www.w3schools.com/cs/index.php)
4. If you can, it is recommended to master [basic Git usage].(https://www.w3schools.com/git/)



# Basic Environment

* Worldbox Game
* Install NeoModLoader



# Code Editor
Here are a few options, in order of recommendation:

1. `Rider`. Paid, but student certification/open source project available
2. `Visual Studio Community`. Free
3. `Visual Studio Code`. Free, lightweight, but cumbersome for beginners to configure
4. `Notepad`. Free, lightweight, no-configuration, just dumb



# Game Source Code

Here, I recommend both of them

* `ILSpy` gets readable code and exports symbolic files (.pdb)
* `DnSpy` UI is nice, the buttons are highlighted when you hover over them (ILSpy is not), and when you look at the IL code you see the index directly



# Game Resources

* `AssetRipper` exports game as a Unity project



# Debug

* `BepInEx` Enable `Logging.Console` in `BepInEx\config\BepInEx.cfg`, console built in game is terrible.
* `UnityExplorer` a BepInEx plugin. You should search for what it can do by yourself.

# Example Code

There are some open NeoMod repositories:

* [ModExample](https://github.com/WorldBoxOpenMods/ModExample/) A pure example code repository. It will include all content in the documentation