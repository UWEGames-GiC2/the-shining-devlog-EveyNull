---
layout: post
title: Developing an artificial intelligence...
date: 2020-01-28T13:19:00.000Z
description: Multiple layers of intelligence & pathfinding
published: true
category: technical
tags:
- project 237
- c++
- low level programming
- technical
- artificial intelligence
---
With our maze generation looking good and a functional scene manager to handle transitions between levels and menus, the next task I took on was to develop the Artificial Intelligence to drive the enemy in our game.

We'd originally identified several behaviours the A.I. would need to have depending on the selected difficulty level:

-EASY

The enemy would wander randomly, travelling in a constant direction until he met a junction. He'd then pick a direction at random and continue.

If he found a set of footprints left by the player he'd begin to follow them, tracking them until he either met the player or ran out of tracks to pursue.

Upon obtaining sight of the player the enemy would immediately switch to chasing the player, until he reached the spot they last saw them.

-MEDIUM

The above behaviours would apply, however, if the player moved within a certain range of the enemy, close enough to be 'heard', the enemy would be able to immediately identify the quickest path to where they last heard the player.

Otherwise the above behaviours would apply.

-HARD

The enemy would be capable of tracking the player's location constantly, and would always know and follow the shortest path to reach them.

-------------

With these requirements in mind I could begin to draw up a priority list for the AI calculations:

If the player is in sight, set destination tile to their location
Otherwise:
  If difficulty is set to hard,
  OR if difficulty is medium and the player is within range,
    Identify the shortest route to the player's location
    Find the furthest visible tile in that route and set that as the destination tile
  Otherwise:
	If current tile is also the current destination tile:
	  If current tile possesses footprints, set destination tile to the next tile in the prints' direction
	  Otherwise:
	    If next tile in our current direction is walkable set that as destination tile
		Otherwise pick a random other walkable direction and set that as our current direction, pick the next tile in that direction as our destination.
		
-------------

The main challenge of this would of course be the pathfinding; I was aware that A* is the most recommended pathfinding algorithm and so I looked up a tutorial for implementing it in a game.
For the sake of pathfinding I created a struct to represent tiles which were part of a pathfinding route. These would possess two pairs of coordinates: one which was their own and the other which was those of the previous tile in the current calculated route.
They also contained variables necessary for calculating their relative weight in the algorithm: 'Cost' (the number of steps from the origin) and 'Distance' (their manhattan distance from the destination tile).

The algorithm essentially boiled down to this:

Starting at the current tile, for each adjacent tile, check if the tile is walkable. If so, add their tile to the open list calculating their Weight (Cost + Distance).
  Find the tile in the open list with the lowest weight
    If the tile coordinates match the destination coordinates pathfinding is complete
	Otherwise, add the tile to the closed list && generate its adjacent tiles. If they're walkable add each one to the open list
	Continue generating adjacent tiles and comparing their weights until the destination tile is reached.
	
When the destination is reached, there should be a series of tiles known, each with their own coordinates as well as those of the previous tile in the chain. By following the chain back, we can get a series of steps that the A.I. needs to take to reach its destination.

I decided to stop at the nearest tile that is visible to the enemy (i.e. does not have a wall tile inbetween that tile and the enemy) and set that as the enemy's new destination.

The enemy would pathfind again if the player changed tiles - this was considered an acceptable compromise between pathfinding every frame (costly) and not pathfinding again until the enemy reached its destination, at which point the player may have moved a significant distance. It needs to update semi-frequently in order to stay on top of the player's movements.

-------------

Overall implementing the A.I. was not too bad, I was somewhat apprehensive about how effective it might turn out but during play it's actually very surprising how intelligent he can appear - at times he actually manages to cut you off while you're running from him leading to quite the jumpscare!

![AI-chase](/assets/shining-ai.gif)