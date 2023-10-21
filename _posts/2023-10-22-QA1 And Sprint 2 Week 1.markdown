---
layout: post
title:  "QA 1 And Sprint 2 Week 1 , Ending October 22 2023"
date:   2023-10-21   17:00 -0400
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

## Week 2: Sprint 2 Week 1 (12 hours)

# Weekly Meeting (2 hours)
This meeting was remote and finished on time. I found out during this meeting that I was being moved to the Singleplayer squad for the sprint to work on the tutorial more. My task for the entire week was to make as much progress as I could on implementing the tutorial missions, as outlined in the design documents.

# Helping Jackson with Unity Setup (0.5 hours)
Jackson messaged me near the start of this week for help cloning the project so that he could modify unit stats for balance. I helped him with this and showed him where the scene for testing and the ScriptableObjects to modify are located.

# Roadblock : Scene Management (2 hours)
After creating a new scene for the first tutorial mission, I attempted to launch the game in the editor from this scene but was confused by the fact that the old tutorial scene I had made last sprint was loaded instead. It took a while, but I had to re-learn how I had made this original tutorial scene work two weeks ago. The biggest problem was that due to a confusion between two scenes, I had accidently written code that infinitely loaded a scene which loaded itself infinitely, causing the game to never actually start. Whenever I would click the play button in Unity the game would load forever and the only way to cancel it was to close Unity from the task manager. This made it very difficult to test this issue and discover what was wrong, but then Nikhil discovered the problem and I was able to move on.

# Playtest With Chimeric (1 hour)
I joined the call for the first playtest with Chimeric and took notes of the issues he brought up. These notes are at the end of this devblog.

# Slow Progress on Tutorial Mission 1 (5 hours)
After Nikhil helped fix my problem with scene management, I began work on the content of the first mission. Progress on this was very slow. Originally when I made the sample tutorial scene, I had the code call the devconsole's SpawnUnit command to spawn in the units for each stage of the tutorial. I realized this week that this was not a good solution since it was hard to refer to units spawned this way in code due to the timing of when commands happen. Because of this, I started using UnitSpawner.cs to spawn tutorial units, and I had to slightly modify the method that does this. I added an optional arguement of whether or not the unit that is spawned in is immediately marked as exhausted. In normal gameplay when a city spawns a unit that unit should be marked as exhausted, but for the purpose of the tutorial I needed to be able to spawn a unit and have to player immediately move it.

The other major slowdown for implementing the tutorial was that the design documents for the tutorial missions were not fully developed yet. There were general outlines for what each tutorial should do, but I had to guess on unit locations, city locations, and other features, in order to make the events of the tutorial take the intended number of turns. This took a lot of testing and experimenting, leading to very slow progress actually implementing the first tutorial mission. I found out on saturday that a designer was currently working on specific map layouts for the first couple missions, but would not be done until sunday. 

# Attacking Bugfix (1.5 hours)
Since I was waiting on more specific tutorial mission designs, I still needed to do a bit more work for the week. While working on Tutorial Mission 1 I discovered that I always had to try attacking a unit twice, and it would always work on the second try. I discovered that with the way my tutorial was working, the ValidAttacks list for the attacking unit was not being updated until I attempted to attack once. I tried adding code to update the list in the Start() method, but this still didn't work. The potential Attacks list in the inspector listed the tile that I was trying to attack, but it always took two tries to attack it.

I was very confused by this situation so I tried out the gameplay scene and discovered that the bug exists here too. It is hard to recognize though since a player might just think they misclicked the first time. My next idea was maybe it had something to do with whether the attack button appeared due to finishing a move or appeared due to the unit being clicked on.

After working on this for a while and hitting my 12 hour time limit, I put out a bug report for this issue. I then found out that this exact issue was being worked on by Zade, who had submitted a pull request for this a couple minutes prior. The pull request had not been approved yet, but Nikhil says it fixes this issue so I unfortunately had wasted my time.

## Conclusion
These two weeks were a very mixed bag. The QA week was very productive for me and lead to some very good progress. But the week after that, a significant chunk of time was spent stuck on tough bugs. I am hoping that in next week will be very productive since the singleplayer squad's designers will have exact map layouts of the missions I have to implement. This should let me quickly follow the design docs rather than trying to piece together how to make a mission fitting them.

# Total Time Commitment for this Sprint: 24.5 Hours

## Extra: Playtesting Notes
- Need turn indicator

- Wasd camera panning would help

- Escape to leave menu

- No buy indicator until click green square is unintuitive

- Money indicator in buy menu

- Indicator that turn ended automatically

- Units randomly exhausted?

- Need more style unity for art

- Use old element indicator as team indicator?

- Right click confirmed move?

- Need more music variety on main screen, song doesnt loop well

- Candle indicator is confusing

- Chimeric was confused by units changing colors (exhausting)

- Range? Reach?

- Team clarity is very confusing

- Unit hover takes too long

- Aeronauts need a good visual indicator

- Units balance is extremely important

- Archer didnt change color for exhaust?