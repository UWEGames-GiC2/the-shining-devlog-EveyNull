---
layout: post
title: Project 237 - Retrospective
date: 2020-01-31T13:19:00.000Z
description: How did it go?
published: true
category: post-mortem
tags:
- project 237
- c++
- low level programming
- post-mortem
---
It took a lot of work and a fair bit of staying up late fixing bugs but the game that came out of it definitely feels well-executed. My initial thoughts when looking at the final product were that it looked pretty good, and feedback we got was that it was fun to play - if lacking in some polish and quality of life improvements that left the experience a little lacking.

So what went well and what didn't?

Early on in the project things felt pretty good overall; we had a pretty well-established concept that was, as far as we could tell at the time, definitely feasible for our current skill level and experience with programming in C++. We identified the major challenge areas early - the A.I., the randomised map generation and the lore unlocks - which meant we had a strong idea of where the most work was going to need to be performed.

With that said, I think one of the big mistakes we made early on was the decision to tackle these aspects of the game before the core gameplay loop was complete.

It was definitely not a poorly-informed decision to get started on work sooner rather than leaving it too late and risking them being incomplete, but the result was also that the most important features - the ones that made the game playable and completable - weren't implemented until much, much later. I joked at one point that we'd actually managed to get a working map generation before our player class was even capable of navigating it (collisions weren't implemented yet), which seemed like running before we could walk.

As a result of this our playtesting was poor - for a long time it was possible to lose the game but impossible to actually win it. Important aspects of the feel for the game, such as the oppressive and claustrophobic atmosphere created from the limited vision radius and sound design, weren't present and so we didn't have an idea what the full player experience would be.

I think this is probably the major failure of our game; our technical work was definitely strong and we achieved a lot from what we did, I was very impressed by what we actually managed to achieve, we were on the ball with testing and bugfixing features and on that level the game was very polished. I think we all came away from the project with greatly improved coding and debugging ability in particular, and I personally benefitted from brushing up on my maths and trigonometry knowledge.

However if I were to do the project again I would reconsider our priorities from early on and playtest, playtest, playtest. I would start small and get things out and playable rather than working at length to make a highly detailed system that isn't merged until it's complete.

This also probably would have spared us our fair share of git troubles, we suffered quite a bit from merge conflicts where work was continued at length on a branch for quite some time before being merged back, at which point things were so out of date we had to go through a painful rebasing process which was responsible for quite a few bugs.

All that aside though I'm happy with what we achieved... there was definitely a little worry at times that we weren't going to make it in time but we pulled it all together in pretty good time. I'm certainly grateful we didn't experience a horrific panicked crunch period right up to the deadline...