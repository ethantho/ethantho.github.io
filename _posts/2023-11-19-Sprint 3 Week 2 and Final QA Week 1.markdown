---
layout: post
title:  "Sprint 3 Week 2 and Final QA Week 1 , Ending November 19 2023"
date:   2023-11-19   15:00 -0400
categories: studio update
---
## Week 1: Sprint 3 Week 2 (12 hours)

# Weekly Meeting (2 hours)
This meeting ended on time and I didn't have to stay afterwards for anything extra.

# Repairing Tutorial Mission 1 After Merges (1 hours)
Although the basic sequence of Tutorial Mission 1 had been working last week (assuming the player followed directions absolutely perfectly), merging the mission into the master branch had made it unplayable. The master branch as a whole was actually in a pretty chaotic state immediately following the weekly meeting, but thankfully Howard, Nikhil, and Eli managed to get it back into a useable state. Once this was done, I was able to go into Tutorial Mission 1 and make some slight changes to make it as functional as the previous week.

# Implementing Tutorial Mission 2 (4 hours)
Since this was the last feature implementation week, I had the task of getting both Tutorial Mission 2 and 3 into the game in some form. Anything that wasn't in the game by the end of the week was supposed to be cut, so my goal was to get these missions in, even if they are buggy. Then I could work on them more in the QA sprint. Tutorial Mission 2 has the shortest scripted section of the three tutorials, so by following the example of tutorial mission 1 I was able to implement this. All of the dialogue is a placeholder to make the tutorial testable until the design team has written more "flavorful" dialogue to use.
<video muted autoplay controls width="600">
    <source src="{{ site.my-media-path }}/3media/TutorialMission2WorksKinda.mp4" type="video/mp4">
</video>


# Implementing Tutorial Mission 3 (5 hours)
Tutorial Mission 3 ended up being more time consuming to implement than Tutorial Mission 2, despite the scripted section of the level being shorter than 2's. The War Balloon unit is very important to this mission, but unfortunately it did not have a model while I was working this week. A video of Tutorial Mission 3's scripted sequence can be found below, but it is somewhat confusing to watch since such an important unit is invisible.
<video muted autoplay controls width="600">
    <source src="{{ site.my-media-path }}/3media/TutorialMission3WorksKinda.mp4" type="video/mp4">
</video>









## Week 2: Final QA Week 1 (12.5 hours)

# Weekly Meeting (2.5 hours)
I attended this week's meeting remotely since I was sick. However, we ended up going overtime a bit at the programming meeting since there was a lot to discuss.

# Bug 1: Player unit in Tutorial 1 cannot be clicked on (2 hours)
Working on this week's bugs ended up being very time consuming. Me and several other programmers have been dealing with an issue where the debugger takes forever to get working. It usually takes a few attempts of restarting the debugger to have the editor even allow me to click the play button, and even when it works it takes a few minutes for the game to run when the debugger is enabled. I eventually managed to figure out what was causing this bug however and I made some minor tweaks to the TutorialMission1Runner.cs to make the unit moveable.


# Bug 2: Unit Interaction System is not Working as Intended (1 hour)
During testing I discovered that the unit interaction system in our game was still not properly replicating Wargroove. A few weeks back some designers and programmers had discussed the issue of accidently using up a unit's movement ability by double clicking. While a few ideas were bounced around, the final decision was to simply copy Wargroove's unit control flow. However, as of the start of this week this was not implemented. Additionally, there was a task assigned to Morgan that seemed to suggest that we were using a completely different unit interaction system. It turned out that Morgan knew what should actually be implemented and the description of that task was just written incorrectly. After some discussion we clarified everything and now we know for sure how the unit interaction system should work.

# Bug 3: Wizard in Tutorial 3 Cannot Attack War Balloon (4 hours)
This is an issue that I discovered this week and still have not managed to fix, despite spending a lot of time investigating it. Last week, as seen in the video of tutorial mission 2, the wizard was able to attack the war balloon just fine. However, this week a number of issues have broken this part of the tutorial sequence. When attempting to perform this attack, sometimes the action menu would not show up at all. This turned out to be an issue with how we check if a unit has moved. Units that cannot move and attack in the same turn still need to choose to move to their own square in order to open the menu, but doing so still marks them as "moved". The fix to this issue was simply tracking how far a unit has moved in a turn, rather than whether or not it selected a tile to move to. 

After solving this issue, an even more confusing bug appeared. The action menu would appear when it was supposed to, and clicking "Attack" would cause the available attack tiles to highlight. However, the action menu would still stay open, and then I could not select a tile to attack. What I think is part of issue was that the fix to make the unit interaction more like wargroove did not take into consideration the fact that some units can only choose to move or choose to attack in a single turn (they cannot do both). The wizard is one of these units since it is a reskin of the old ballista unit, so after some communication with Morgan and Nikhil we were able to assign fixing this as a task for someone.

# Bug 4: Moving the wizard too fast breaks Tutorial 3 (1 hour)
After working on the previous bug for a while, I decided to focus on an easier bug that I was confident I could get in this week. Tutorial Mission 3 starts with the enemy attacking a unit, but someone discovered that you are not prevented from moving your wizard while this takes place, which breaks the tutorial sequence. This turned out to be not too difficult of a bug to fix, since hard coded ai moves don't control which player is set as the "current player" in TurnPlayerManager.cs. By simply setting this at the start of the round, and changing it again once the ai moves were complete, I was able to prevent this issue.

# Tile Highlight Improvement (2 hours)
I decided to use the last of my time this week to investigate why the tutorial tile highlight system wasn't working. Since it quit working after integrating tutorial mission 1 with the rest of the game, I didn't even bother using it yet in tutorial missions 2 and 3. However, it could be very useful for helping the player know exactly what to do without just listing out grid coordinates. I investigated why it quit working for a while (and struggled with getting the debugger to run for longer than I'd like to admit) and was able make it work again in tutorial mission 1. Now when the tutorial tells you to move to a tile, that tile is highlighted. I would like to make the tile highlight cursor a bit more visible in the future, but for now I duplicated the cursor and have it hover a bit above the tile to highlight.





## Conclusion
Overall these two weeks were quite productive. However, I am a bit concerned about how quickly the end of the cycle is approaching. The tutorial designer gave me a new design for tutorial mission 1 on saturday evening, which will likely be quite time consuming to implement, along with fixing all the other issues with the current tutorial missions. I will likely have to work a bit over Thanksgiving break in order to ensure that I have time to finish everything, since no other programmers are assigned to work on the tutorials at all. Still, I am hopeful that I can get everything done, and Nikhil told me some new ways to run the tutorials which should be helpful in the tutorial 1 rewrite.


# Total Time Commitment for this Sprint: 24.5 Hours

