---
layout: post
title: The Scene Manager
date: 2020-01-15T13:19:00.000Z
description: Our implementation of a scene manager
published: true
category: technical
tags:
- project 237
- c++
- low level programming
- scene manager
---

Following instruction from our Game Engine Architecture module and by our tutor we were given as a requirement the use of Manager classes, specifically a Scene Manager as a minimum, to better structure our code and implement systems in our game in a sensible and practical manner.

My main understanding of Scene Managers came from using Unity, where the Scene Manager is responsible for loading Scenes - effectively game levels or screens such as the main menu, level selection... effectively it manages the different game states and ensures data is being processed appropriately and the respective screens rendered properly, in order. At times for example several scenes may be active at once - such as a game level and a pause screen - and the scene manager can maintain control of both and ensure they are loaded or unloaded when required.

As I understood things the Scene Manager would effectively be the root of the game, owner of any objects that represented scenes such as the level and UI, and controlling the update and render functions of each to manage what data was being processed and what was being shown on screen.

First I implemented a GameState enum to track what the condition of the game; e.g. in the main menu or ingame. I also gave the scene manager ownership of the Level object which would contain, effectively, the entire map and all gameobjects within it which would be a part of the game scene. The SceneManager would initialise the Level when the game began and destroy it when the player returned to the main menu. Depending on the difficulty selected by the player, the Level's own difficulty setting would be assigned appropriately as well, which could then be passed on to all objects that behaved according to the difficulty chosen.

Because the Scene Manager in this structure acts as the root of all other objects, it seemed sensible for it to store data regarding the current key presses; it would need these for one to process changes in state when the player moved through menus or paused the game, and could pass them on to the scenes' update functions where they would be needed (e.g. to move the player). This was stored as a bitset which simply stored whether that key was currently pressed (updated by the keyhandler function in the base game.cpp).

Each frame the manager checks its current state; if the appropriate key or keys are pressed to change state it updates appropriately, else if the game is running it passes on the need to call the level's update and render functions in order to process and display the level's owned objects (while those objects remain out of scope for the manager itself). This could in theory be expanded to simply call the update function of whatever scene is loaded.

Implemented, the scene manager has made it practical and intuitive to control how the game updates and displays relevant information; it was, compared to previous projects, relatively easy to implement pausing for example, and player-controlled transition between different difficulties or exiting the game.