---
title: Building game
permalink: /docs/building-game/
---

# Building game

At the moment there are difficulties with the automatic build of the game, so you need to build it manually.

Instructions:
1. Download the engine:
 - [Windows](https://github.com/godotengine/godot/releases/download/3.5.3-stable/Godot_v3.5.3-stable_win64.exe.zip);
 - [Linux](https://github.com/godotengine/godot/releases/download/3.5.3-stable/Godot_v3.5.3-stable_x11.64.zip);
 - [Mac OS X](https://github.com/godotengine/godot/releases/download/3.5.3-stable/Godot_v3.5.3-stable_osx.universal.zip);
2. Download the sources:
 - [master](https://github.com/GREAT-DNG/Futureal/archive/refs/heads/master.zip);
 - [develop](https://github.com/GREAT-DNG/Futureal/archive/refs/heads/develop.zip);
3. Unpack the archives;
4. Launch Godot;
5. Click *Import* and select the path to the *project.godot* file. There may be errors in the output, but in most cases it is not critical;
6. Open *Editor* > *Manage Export Templates*, then click *Download and Install*;
7. Open *Project* > *Export...*, click *Add...* and select the required platform. Set the settings as desired;
8. Click *Export Project...*, select the file path and press *Save*;

To properly design the build, also add an icon using [Godot Icon Plugin](https://github.com/pkowal1982/godoticonplugin) and copy the *LICENSE* file to the folder with the build.

More information about the build process can be found on [the engine documentation website](https://docs.godotengine.org/en/3.5/tutorials/export/index.html).