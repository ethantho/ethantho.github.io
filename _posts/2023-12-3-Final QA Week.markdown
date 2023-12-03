---
layout: post
title:  "Final QA Week , Ending December 3 2023"
date:   2023-12-3   15:00 -0400
categories: studio update
---
## Week 1: Thanksgiving Break (2 hours)

# Weekly Meeting (2 hours)
The meeting ended at the usual time this week.

# Rest of the Week (0 hours)
I was originally planning on working this week even though it wasn't required, but I ended up being very busy at home during Thanksgiving break.

## Week 2: Final QA Week (12 hours)
There was no weekly meeting this week due to Thanksgiving break.

# Tutorial Mission 1 Rewrite (6 hours)
During the last sprint, a new design for tutorial mission 1 was uploaded to Confluence. Since the sequence of the tutorial was changing anyways, I decided to completely rewrite tutorial mission 1 using a Unity feature that Nikhil had told me about: Custom Yield Instructions. Rather than being an abomination of switch statements with an int to track which stage the tutorial was on, using CustomYieldInstructions I could write very readable and modifiable tutorial sequences, with the entire tutorial being a coroutine. 

After creating some CustomYieldInstructions like "WaitForUnitAtTile" and "WaitForUnitHealthChange", I was able to begin working on a complete rewrite of Tutorial Mission 1. This went fairly smoothly compared to previous versions of the tutorials, and the resulting code is far simpler.

# Tutorial 1 Troubleshooting: Allied Unit Moves during AI Turn (1 hours)
While the rewrite of Tutorial 1 worked far better than the old version right off the bat, I still ran into several issues along the way. The first of which was allied units being moved during the enemy AI turn. This turned out to be an issue with the way that tiles track what unit is on them, since hard coded AI moves access the unit to move through the tile that they are on. If the information contained in a tile is outdated, then a unit that was previously on this tile could end up being moved. I fixed this with a small addition to Unit.cs which makes sure that the tile that a unit is standing on knows that it is standing on it.

# Tutorial 1 Troubleshooting: Freeform Section Doesn't Start (2 hours)
After the scripted section of Tutorial Mission 1, the game is supposed to simply play out as if it was a normal singleplayer match. However, various issues were preventing this from working. Because Tutorial Mission 1 does not contain an enemy commander unit, I had to add a workaround to prevent nullpointers if the AI tries calculating a strategy involving the commander. I originally planned to use the restricted AI system to simply remove the AI's ability to even attempt strategies such as "Move Towards Commander", but over the course of the past couple of weeks the restricted AI system broke and I do not have time to fix it.

# Tutorial 2 Rewrite (3 hours)
Since I liked the way Tutorial Mission 1's rewrite turned out, and Tutorial Mission 2 still had some issues, I decided to start working on rewriting Tutorial Mission 2 in the same way, using CustomYieldInstructions. This is going fairly smoothly, and is all scripted out already. In the next couple days it just needs to be tested and have the new dialogue added.

## Conclusion
Overall this week went fairly smoothly. While I was a bit frustrated at first to have to completely rework Tutorial Mission 1 to fit the new spec, I am glad that it gave me the opportunity to rewrite the tutorials in a cleaner way. This will be much more expandable and modifiable in the future, and should allow me to fix all the issues with Tutorial Mission 3 in the next couple of days. To be honest, I wish I had known about writing the tutorials this way much earlier, since then it might not have taken so much time to make and debug them in previous sprints.

# Total Time Commitment for this Sprint: 14 Hours

