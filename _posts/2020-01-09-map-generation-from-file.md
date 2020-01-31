---
layout: post
title: Map generation - reading maps from file
date: 2020-01-09T13:00:00.000Z
description: Laying the foundations for generation of a randomized maze
published: true
category: technical
tags:
- project 237
- c++
- low level programming
- map generation
---

Our chosen project was a 2D game where the player must navigate a maze, evading an intelligent enemy while searching for items that will allow them to weaken and eventually defeat it. We decided that maps would be randomly generated each time; to do this the map would be generated in blocks with pre-set tile arrangements depending on the position in the maze. For example at the corners of the maze, the corner blocks would pick a tile arrangement from a set of possible 'corner' configurations; the same would go for edges of the maze and the center.

I took on the task of creating a system that would set up a blank 2x2 grid of blocks, and then load in the tile data from different files at generation.

Objects identified were Tiles, Blocks and Levels; a Block would contain a grid of Tiles and a Level a grid of Blocks. I had to consider how to store and manage these data; for example I could use a two-dimensional array where each dimension would be a row and column respectively. This would certainly be the simplest option though accessing data from this might be unintuitive and I would need to manage the data manually. Therefore I considered what objects in the Standard Template Library could be used to better manage this data.

The object I had most familiarity at this point was a two-dimensional std::vector, which would possess the useful qualities of a smart pointer but would still be unintuitive to interact with when setting up data and seemed superfluous given the size of the maze would be fixed once created and therefore the heap management of a vector would not be necessary.

After consideration I decided to store the data as map objects; by using a set of coordinates as a key (e.g. a std::pair<int,int>) objects could be initialised and managed simply by accessing them with their location in the map coordinate system. So for example within a Block, Tiles would be stored in a std::map<std::pair<int,int>, Tile>. I could write helper functions that returned the desired object at a set of grid coordinates which would make interactions from other systems simpler and more intuitive.

When a map is to be generated, the maze generator is provided with the number of blocks in each row & column, the number of tiles in each block row & column, and the size in pixels of each tile's height & width. The generator runs a loop up to the map size creating map blocks; at this point a check is run to see if the block is against one or two edges of the map (i.e. if it is an edge or corner block) and creates a block of the desired size, before emplacing it in the map against a key representing its coordinates in the map.

At block initialisation, the constructor reads from a directory determined by its position in the grid (e.g. /map_blocks/corner/) and picks a random tileset file to read from within that directory. It then reads the file into a buffer, before using a helper function to split the string by its delimeters (newlines and commas) to read each individual tile's state; for example 1 representing a wall, 0 representing walkable ground. Each tile in the block is then initialised using the data read from the file.

In the case that the file fails to open or something else goes wrong in map generation, the system throws an exception which is caught and passed up to inform the game that the level failed to load, which allows exception handling to prevent crashes, potentially allowing the map to attempt generation again a second time.