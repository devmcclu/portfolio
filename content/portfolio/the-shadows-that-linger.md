+++
categories = ["game-dev", "unity", "csharp"]
coders = []
date = 2020-06-19T23:00:00Z
description = "Released, Programmer (Unity, C#) - Narrative Adventure Murder Mystery"
github = []
image = "https://i.imgur.com/cIFLKSz.jpeg"
title = "The Shadows That Linger"
type = "post"
[[tech]]
logo = "https://i.imgur.com/v03jzFC.png"
name = "Unity"
url = "https://unity.com/"
[[tech]]
logo = "https://www.inklestudios.com/ink/img/ink-logo.png"
name = "ink"
url = "https://www.inklestudios.com/ink/"

+++
January 2020 - Present

Released March 17, 2021

Programmer - [Crimson Ink Games](https://www.theshadowsthatlinger.com/), Team Size 6

Download the game: https://crimson-ink-games-llc.itch.io/the-shadows-that-linger

Can provide code on request

## About The Game
 Play as a medium named Ilana in this spooky mystery and solve your sister's murder on behalf of her lingering shadow. With time running out before her restless spirit becomes lost in purgatory forever, converse with your newly acquainted in-laws to gather leads in tense dialogues, explore their picturesque estate, and use your crystal ball to peer into the realm of shadows and discover clues with spiritual connections. After collecting sufficient evidence, accuse whom you believe the murderer is to get one step closer to saving your sister's soul.

## Implemented
* Branching Narrative structure built upon ink Framework
* Notification system for important in-game events
* Scriptable Object based system design


The Shadows That Linger is a very dialog heavy game, so one of the first things that had to be nailed down was how the player interacts with the characters. We could just write our own dialog system, but people have already made great systems before that allow for simple choice based actions. After some research, I landed on the tool [ink](https://www.inklestudios.com/ink/). Ink works great for us because it has an official Unity plugin so we don’t have to go around using some third-party tool for Unity integration. You could build your whole game using nothing but Ink scripts and some simple sprite changes!

![ink website image](https://i.imgur.com/PQ2x7L0.png)

Shadows is more complex than that, so thankfully ink makes it relatively easy to access and modify variables in an ink script so they can react to things the player has found, who they have talked to, or have the game state react based on the player’s conversations. The clues that you find in the game are a large part of what we track in the game partially due to the dialog, so being able to access that info was another thing that had to be figured out. Almost everything in the game that we track is done so using custom Scriptable Objects. Unity’s Scriptable Objects are a great fit, as they give the designers a visual representation of the data we need, are easy to create in the editor, and make getting the data super simple.

![Clue object snippit](https://i.imgur.com/8n0GITU.png)
*A code snippit of the Clue Objects*

To make things just a little simpler, I put all of the Clue Scriptable Objects inside of another Scriptable Object whose sole purpose is to hold the Clues after we realized that we need to be able to access multiple (or all) of the clues in dialog and other systems in the game. Scriptable Objects also serialize well, so they are partially used in the game’s automatic save system.



![Almost all the Scriptable Objects used in dialog](https://i.imgur.com/RsRk9TD.png)
*Almost all the Scriptable Objects used in dialog*

When it comes to actually showing dialog though, not much magic is happening here. We based our system off of the [ink example game](https://github.com/inkle/the-intercept), with some modifications based on the variables that need to be tracked in and out of dialog. Overall, I think it looks good and I hope you do too.

{{< youtube id="wFKf9JH5APw" autoplay="false" >}}