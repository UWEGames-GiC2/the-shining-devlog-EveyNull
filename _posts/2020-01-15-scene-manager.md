---
layout: post
title: Project 237 - A game concept
date: 2019-12-18T13:19:00.000Z
description: Concept & design
published: true
category: design
tags:
- project 237
- c++
- low level programming
- design
---

For our second assignment this year we were tasked with designing and developing a full game in C++, inspired by the film 'The Shining' by Stanley Kubrick.

Our focus quickly went to the maze scene, where the enraged Jack pursues his son through a hedge maze in the cold. We took inspiration from games like Slender and pac-man; the former for its semi-random item distribution in a level with the player seeking them throughout the area - the latter for its claustrophobic maze layout and varied A.I. making gameplay fastpaced and frantic.

In a combination of the two ideas our original concept was a game where you must hide in the maze while pursued by Jack, who is intelligent and follows your footprints left in the snow. The goal was to elude him long enough for him to become worn down and give in to the cold, at which point you were free to exit the maze.

Also as a concept was the 'Shining' ability, allowing the player to see where Jack was as well as the exit, so long as they stood still for a few seconds. We wanted to ensure the player did not get totally lost in the maze while also making it a trade-off in that they risked Jack catching up further if they used the ability.

Finally in homage to the game 'Slender' our idea was to have unlockable pieces of writing or lore scattered throughout the maze, which the player could collect. Once found these would be permanently unlocked in the main menu and over multiple plays the player could eventually complete their collection as long as they kept finding the hidden collectibles.

After presenting this concept the feedback we received was for one that it seemed unintuitive that the player could not simply escape the maze straight away and had to face what was seen as an arbitrary timer countdown. As well as this it seemed too simple a gameplay loop; the only mechanic was to run away and hide, which while worked well with the horror genre just did not offer enough to remain interesting for very long.

Our developed design therefore introduced new gameplay elements; now rather than eluding Jack at all times the goal was to find items inside the maze that could harm or slow him, and set them up as traps. This added extra dimensions to the gameplay; the player was not just running around without aim but instead had something to seek and pursue, while at the same time they needed to at times risk coming into close encounters with Jack in order to bait him into the traps they set. There was more of a risk/reward dynamic at play, with the player wishing to stay far away enough to be safe while not so close that they would get caught.

We also added further incentive to playing multiple times at different difficulties; the unlockable writings would now vary depending on the difficulty selected by the player and therefore to unlock all of them the player would need to try the game at all levels of difficulty. We wanted to encourage the player to try the harder modes even though they may be significantly challenging.

Overall our main selling points were the unlockables, the random maze generation and the AI pathfinding ability, tracking both the player's nearby location and being able to follow their footprints in the snow. These were likely to be challenging to program but certainly not above our ability - we had a good idea how it might all be done and were confident we could achieve our goals.