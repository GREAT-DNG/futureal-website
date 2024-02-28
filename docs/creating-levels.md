---
title: Creating levels
permalink: /docs/creating-levels/
---

# Creating levels

This article is intended for those who have minimal knowledge of the principles of the Godot engine.

To create a level you need the engine and the game sources, opened in the engine (see points 1-5 in [the article about building the game](building-game.md)). Use already created levels as examples (see `res://Scenes/Levels/`). Don't forget to save your progress. When arranging objects, prefer round numbers in positions.

## Preparation

1. Inherit or copy the contents from the `res://Scenes/Levels/BasicSingleplayerLevel.tscn` or `res://Scenes/Levels/BasicMultilayerLevel.tscn` (depending on the level's play mode) scene to the new scene;
2. Remove the editor description in the root node (`BasicLevel`);
3. Rename the root node (`BasicLevel`) to the name of your level. It is recommended to use `PascalCase` in node naming;

### For the singleplayer mode:

In the root node properties (`BasicLevel`), specify the level number and the next level.

Save the level file separately from the project, loading will be done via the `Load` button in the `Play` menu.

### For the multiplayer mode:

Add the following constant to the `res://Scripts/Utilities/MultiplayerManager.gd` script:
```
const LEVEL_NAME: Dictionary = {
	"max_players": number,
	"spawn_positions": [Vector2(x, y), Vector2(x, y) ... ],
	"used_spawn_positions": [],
	}
```
And replace `number` with the maximum number of players. Also write the players' spawn points by changing `x` and `y`.

Also add your level to the list by changing the `LEVELS` constant:
```
const LEVELS: Dictionary = {
	...
	"LevelFileName": LEVEL_NAME,
	}
```

## Creating an environment

1. Create the walls and floors of the level in the `BlocksTileMap` tile map. Recommendations:
- Compose the tiles so that the line on them is on the player's side;
- Create floors under the guides;
2. Create a background in the `EnvironmentTileMap` tile map. Recommendations (the tile numbers correspond to the file names (starting from zero) in `res://Sprites/Environment/` and the order in the tileset):
- Use the first tile for the outdoor floor;
- Use the second tile for the background walls inside the room;
- Use the third tile for transitions from indoors to outdoors;
- Use the fourth tile for floor separations;
- Use the fifth tile for something unusual, such as secret rooms;
- Use the sixth tile for where the level starts (the player's spawn point);
- Use the seventh tile in front of enemy spawners or other unexpected hazards;
- Use the eighth tile for the background walls of a room with a portal to the next level;

## Adding light

Select the type of light (0 - general, 1 - directional) and make the scene instance `res://Scenes/Lamps/Lamp + type.tscn` in `/Lamps/type/`. Change the `Texture Scale` if necessary, don't forget to fix the `Offset` when using directional light.

## Adding items

To add an item, select the desired type (`Gun`, `MedChest` or `BulletsPack`) make the scene instance `res://Scenes/Items/type.tscn` to `/type + s/` and change the properties.

General properties of items:
- `Respawning` - toggles the ability of the item to reappear after capture, needed in multiplayer;
- `Respawning Time` - time in seconds after which the item will appear after capture;

Properties `Guns`:
- `Gun ID` - the weapon the player receives when taking it. For convenience of selection in the inspector id's are replaced by names;

`MedChest` properties:
- `Heal Power` - renewable amount of health;

Properties `BulletsPack`:
- `Clips` - the number of clips received by the player;

## Customizing enemies (singleplayer mode only)

Select the enemy type (0 to 2), make the scene instance `res://Scenes/Enemies/Enemy + type.tscn` to `/Enemies/type/` and change the properties.

Enemy Properties:
- `Health` - enemy's health;
- `Health Difference` - the number subtracted from `Health` at an easy difficulty level and added at a hard difficult level;
- `Speed` - speed of movement;
- `Lethargy` - slowness when shooting;
- `Gun ID` - enemy's weapon. For convenience of selection in the inspector id's are replaced by names;
- `Path` - the path on which the enemy will walk, is an array of coordinates. If you do not specify the array the enemy will stand still;
- `Shot Always` - toggles eternal shooting. By default, the enemy shoots only if it sees the player;
- `Mode` - mode of enemy actions when seeing the player:
	- `Follow path` - the enemy will follow the path no matter what the circumstances;
	- `Follow player` - the enemy will follow the player. Hence specifying `Path` is meaningless;
	- `Follow player after seen` - the enemy will follow the path, but if he sees the player he will follow him;

## Customizing enemy spawners (singleplayer mode only)

Make the scene instance `res://Scenes/Items/EnemySpawner.tscn` into `/EnemySpawners/` and change the properties.

`EnemySpawner` properties:
- `Spawn Position` - enemy spawn position;
- `One Shot` - switches one-shot triggering of the spawner;
- `Enemy Type` - the type of enemy that will be spawned;
- The rest of the properties are related to the enemy that will be spawned, see "Customizing Enemies";