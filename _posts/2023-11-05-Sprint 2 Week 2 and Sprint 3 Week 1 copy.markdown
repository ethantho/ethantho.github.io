---
layout: post
title:  "Sprint 2 Week 2 and Sprint 3 Week 1 , Ending November 5 2023"
date:   2023-11-5   15:00 -0400
categories: studio update
---
## Week 1: Sprint 2 Week 2 (12 hours)

# Weekly Meeting (3 hours)
After this week's meeting I stayed after for a while to discuss the toon shader currently being used in the game with Adam, Henry, and Jordan. Adam explained how the current shader could be quite inefficient and result in weird overlapping outlines due to the way the outline of objects is drawn. After consulting with Jordan, it sounds like the current plan is to replace this shader with something made custom by Adam.

# Helping Jackson Set up Unity, and Other Discussion (1 hours)
One of our designers, Jackson, Contacted me for help with cloning our repository. I helped him set everything up and pointed him to the folders that contain the UnitType ScriptableObjects that he would be modifying.

Later on in the week he contacted me about possibly setting up a meeting to discuss "inconsistencies with unit stats". After some discussion we realized that he hadn't been told that the stats currently in the game were simply placeholders, and his stats still needed to be implemented. We ended up deciding we didn't need to run a meeting after all. Later in the week I also relayed this info to Howard.


# Preparing for Level Designs (5 hours)
Since I was waiting for the first tutorial design to be completed, I was tasked with making sure that I would be able to implement the level fairly quickly once it was designed. I thought a hardcoded AI system where I can tell ai units exactly where to go would be useful for speeding up progress once I received the mission design. I spent quite a while working towards understanding how the existing AI system worked. Once I felt comfortable enough, I created a "Restricted AI" mode where you can specify which types of moves the AI will attempt. For example, you could have the AI only attempt to capture cities and ignore possible attacks. Creating this was fairly difficult however, since my restricted AI system seemed to load the correct strategy types but not execute them. Nikhil and I investigated this and found that there were several cases where (row,column) coordinates were used instead of (x,y) coordinates, which lead to several issues. Fixing these helped work towards the restricted AI system working correctly.

# Working on Implementing Tutorial Level 1 (3 hours)
On saturday I received the design for Tutorial Mission 1 from Cole. I was able to fit in a bit of time working on it that day. Cole had used the terrain editor to design the map for this mission, so I was able to simply use this file to load the map in my branch. Unfortunately, a large portion of the map's tiles were invisible at first, shown below.
![misloaded terrain](/3media/misload.png)
The issue turned out to be that several tile types currently have no graphics. I simply added a placeholder to each tile type with this issue and the level became usable.
This week I also dealt with spawning in Units for the mission in the right locations, and troubleshooting the restricted AI since it quit working once I made a new level. This turned out to be due to yet another (row,column) vs (x,y) coordinates confusion issue.

## Week 2: Sprint 3 Week 1 (12 hours)

# Weekly Meeting (2 hours)
This week I left the meeting right as it ended, so my time investment from it is just 2 hours.

# Main Task: Tutorial Mission 1 (7 hours prior to work session)
Since I received the design for Tutorial Mission 1 a few days prior, this week I was able to implement this design. Since I had already implemented the terrain last week, my task now was all of the behavior of the scripted portion of mission 1. Using the dialogue system I had made previously, I set up a series of 21 "stages" to the mission, based on the outline in the spec. Each of these stages has a condition to be fulfilled to go to the next stage. One example is "enemy unit #3 arrives at this specific grid square". With these stages, a sequence of events where the player is told exactly what to do by the dialog system is carried out.

# Friday Work Session (3 hours)
At the work session I managed to finish up the last few stages of Tutorial Mission 1 and fix some issues I was having like certain stages being skipped. By the time I had to leave, I had submitted a pull request with a somewhat complete version of Tutorial Mission 1. I have attached a video of this below. There are a few features that do not work yet, for example the Old King's special. This special is supposed to spawn a unit next to the Old King, but it did not work in my branch so I simply simulated it with a console command in my demo video, as shown below. Additionally, this tutorial still needs dialogue to be written to replace all the placeholders which simply tell the player exact instructions on what to do.

<video muted autoplay controls width="600">
    <source src="{{ site.my-media-path }}/3media/TutorialMission1WorksKinda.mp4" type="video/mp4">
</video>


## Conclusion
Overall these two weeks were fairly productive for me. It was a bit stressful not knowing when I would receive the final design for mission 1, but once I did, I was able to work whenever I was able to and script out the entire mission. Now that I have completed tutorial mission 1's sequence of events, missions 2 and 3 should be easier and take less time since they have fewer stages. This next week will definitely have a lot of work again, but I am fairly confident that I will have all 3 tutorial missions in the game in some form by the end of sprint 3.

# Total Time Commitment for this Sprint: 24 Hours

