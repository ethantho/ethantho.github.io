---
layout: post
title:  "QA 1 And Sprint 2 Week 1 , Ending October 22 2023"
date:   2023-10-07   22:00 -0400
categories: studio update
---
## Week 1: QA 1 (12.5 hours)

# Weekly Meeting (2.5 hours)
As usual I had to stay after the meeting for a bit to talk about the project with programmers from other squads and make sure we could use each other's systems. We discussed ideas for how to fix some of the bugs we were assigned as well.

# First Bug to Fix: Enemy AI Attacks Aeronauts with Ground Units  (2 hours)
My first task was fixing the issue of AI ground units that cannot reach aerial units still attempting to attack aeronauts. I struggled to test this since at the start of the week the AI did not attack my units at all. They simply all piled up on the unclaimed city closest to them, and captured it for my team. I ended up struggling a bit trying to see if there was an easy fix for this myself, but later in the week the AI was working again and I discovered that the AI already avoids attacking aeronauts, so it was already fixed.

# Spawning Canvas (1 hour)
I was not assigned to this, but I ended up spending a bit of time seeing if there was an easy fix to the spawning UI being constantly on since it was making it difficult to test my tasks. The issue turned out to be more complex than I expected and I decided to just wait for this bug to be fixed.

# Soldier Crit (1 hour)
During the meeting I found out that I had implemented the soldier crit condition incorrectly. The intended behavior was that once a soldier attacks a unit, that unit is flagged for a turn and any other soldiers that attack it will land a critical hit. I had mistakenly made it so that if any unit (not just a soldier) attacks another unit, the flag is set. This was a fairly quick fix, but took a bit of time to test.

# Commander Exhaust (0.5 hours)
The next issue I had to fix was that moving your commander on the first turn (which should exhaust it) does not result in your turn being automatically ended. In the course of fixing this I discovered another issue in which the first turn that you have enough credits to purchase a unit, the cities are still marked as exhausted. I fixed the commander issue by moving the ExhaustSystem's subscription to the "OnRoundStart" event to the Awake() method rather than Start(), ensuring that it happens on the first turn. The city issue was fixed by making the exhaust system consider the income that will occur at the start of the turn before exhausting cities. If the player's current money + the income that will be received that turn is less than the price of the cheapest unit, then the cities are marked as exhausted at the start of the turn.

# Wargroove Style Movement (5.5 hours)
My last task for the week was less of a bugfix and more of a new feature implementation. At the start of the week our unit control flow worked like this:

- Select a unit
- Select "attack" to attack from that square, or Select "Wait" to move (which was very confusing)
- If "Wait" was selected, show the movement preview
- Click the square you want to move to
- If you didnt already attack, you can now click the unit again to attack

However, the designers told me that they wanted a similar movement system as Wargroove. Wargroove's system works like this:
- select a unit
- move that unit to a square
- once you select what square to move it to, the three choices show up: attack, wait, and cancel

- Attack: prompts you to select a unit to attack
- Wait: move the the square you selected and exhaust the unit without attacking
- Cancel: undoes the move you selected and starts over

This system is much more inuitive, and closely matches what other tactics games use. It also allows a player to change their mind on moving a unit to a square if they view the battle preview and decide not to attack.

Since this was a fairly major change, this ended up taking quite a while to implement and I went a bit over the 12 hours per week limit finishing it up. However, I think it was a very worthwhile change because of the useful "cancel" feature. Here is a video of it working:

<video muted autoplay controls>
    <source src="{{ site.my-media-path }}/NewUnitMove.mp4" type="video/mp4">
</video>
