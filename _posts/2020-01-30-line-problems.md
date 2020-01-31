---
layout: post
title: A line in time
date: 2020-01-30T13:19:00.000Z
description: A very tricky puzzle to work out
published: true
category: technical
tags:
- project 237
- c++
- low level programming
- technical
- trigonometry
---
This particular blog covers an interesting issue I encountered while developing the 'Shining' ability for our game.

The original idea behind the game mechanic was that, if the player stood still for a short period, they would be able to see the relative location of the enemy that pursued them via a line that pointed in the appropriate direction.

At first this seemed like not too difficult a task - get the vector of the difference between the player and enemy, then find the appropriate angle for the line that should be drawn and render it as a sprite on the screen.

The first challenge was a bit of GCSE Maths revision... I had barely touched upon trigonometry for years, at least beyond Pythagoras' theorem and so I needed to revisit the rules of SOHCAHTOA. I knew that it was definitely possible to calculate the two other angles of a right-angled triangle, given the lengths of the sides; given that a vector2 essentially represents a right-angled triangle with the origin as the base of the hypotenuse, it would just take a little trig to solve the angle between Hypotenuse and Adjacent. Sure enough, a bit of revision told me that it was as simple as calculating the inverse tan of the vector - tan^1(Y/X).

This gave me the angle in radians which could be fed directly to the sprite, which I'd then render on top of the player. Great!

Except... I hadn't accounted for the way sprites were drawn in ASGE. They're drawn from the top-left, totally reasonable. What I didn't know was that when you rotate a sprite in ASGE, it rotates from the centre of the sprite. Again, quite reasonable in most circumstances, but in this case I wanted to rotate around one end of the line. The results were... not quite what I wanted.

![AI-chase](/assets/badline.png)

Because the sprite was drawn from the top left and then rotated from its middle, its origin and end point were obviously being skewed off from their intended position. It took a lot of work to discover how to properly render this so that the line began from the player and reached out to the enemy.

Firstly it was clear that, depending on whether the enemy was to the left or right of the player, the sprite would actually need to be drawn from the enemy or player's X position; if they're to the left of the enemy, the sprite needs to be drawn from the top left corner between the two, which would be the player's x position and conversely, the enemy's x position if the enemy is to the left.

This didn't quite solve it however; noticeably because the sprite was being drawn as a horizontal line and then rotated, the biggest effect was when the Y-position of the two entities varied. When the vector between the player and enemy was perpendicular to the sprite's original rotation, i.e. when the player was directly above the enemy, the offset was at its greatest; when they were level on the Y-axis the line was actually exactly in the correct position.

A good step forwards was correcting the Y-position by the average Y position of the two; when the two matched Y-positions the line was not corrected at all, but when they were apart it just bumped the line down just enough to originate from the centre of the player. However here the x-position was still off just slightly, and again it varied only when the y-positions of the two varied.

At this point I got assistance from someone a little better at maths than me... and as I understood things it was a matter of imagining the situation as within a circle.

![AI-chase](/assets/sincostan.png)

If O is the origin, i.e. the player, and the enemy vector represented a point on the circumference of a circle surrounding the player, and the line itself a line between the two, we tried adjusting the xPos of the line by its Cos(angleinradians). This was actually close but not quite right... because the player wasn't actually at O, but at a position slightly left of it. It's hard to prove the maths fully, in writing, right now, but the solution was to adjust the position by 1-cos(angle). Cue applause...

![AI-chase](/assets/goodline.png)

Given this was such a task and something perhaps worth storing in its own class, I made a Line.h class to keep hold of this work. I'm sure it'll come in very handy some time in future...