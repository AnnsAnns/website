+++
author = "tomGER"
title = "Farmulty - Progress Report #1"
date = "2021-05-31"
description = "The first progress report about my Farming Gaming Farmulty"
tags = [
    "progress-report",
    "game",
    "godot"
]
images = ["header.png"]
+++

{{< figure src="header.png" alt="Farmulty logo" height="70%" width="70%" class="text-center">}}

Farmulty is my attempt at a farming game with some special twists that I have been working on daily for over a month now. Midway through May I posted the first alpha of it on my twitter and the response to it was much bigger than I expected. However, I quickly realized that the way I originally planned to release snapshots of the game made it nearly impossible to commit to larger changes for the project. The fear of breaking something before releasing another snapshot caused me to become ever more worried about adding anything that I couldn't finish within a few hours or that might require me to rewrite major portions of already existing code.

{{< figure src="parabel.png" alt="Chart showcasing productivity" height="40%" width="40%" class="text-center" caption="*This was basically the productivity leading up to releases*">}}

Given the mentioned problems with weekly snapshots I decided that I'd much rather focus on improving the code long-term and only showcasing my current progress in progress reports, such as this one :) Especially after the extremely positive and honestly unexpected reaction to my first alpha release, I want to create a game that I can be proud of in the long-run and not one that is full of buggy YandereDev code that is focussed on shoving as many features as possible into the releases.

So without further ado, let us look into the progress I have made since the last (literally) alpha build.

## Saving and Loading

{{< figure src="saving.gif" alt="GIF showcasing saving a game" height="70%" width="70%" class="text-center">}}

Saving and Loading a game is surprisingly complicated and hard to implement. The process of serializing and deserializing all the required data requires quite a lot of planning and as such this feature was one that I always tried to shove to the side but after nearly one month saving and loading is fully working, albeit I must admit that there are still some minor bugs when loading games but those will only require some minor changes to fix :)

This is by far the most important and complex feature I implemented so far but given that nobody wants to play a farming game in a single sitting and then loose all their progress, it was something that was critical in order to change the games status from "Proof of Concept" into something I'd call playable.

## Redesign Shovel Logic

{{< figure src="shovel.gif" alt="GIF showcasing shovel" height="70%" width="70%" class="text-center">}}

One of the worst offenders of rushed code was the shovel logic, there were many weird bugs and rushed lines in the code and as such I felt like the shovel was extremely inconsistent and unenjoyable to use. The new shovel logic now follows a very specific algorithm (which is even showcased to the user through a grid box) and improved the previous code drastically by fixing many hacky solutions such as the way it spawned areas that the character can plant in. Previously the area would always be spawned for one frame before the system picked up on it and checked whether it was properly placed. Not only did that look ugly but it also confused players.

The new system now clearly indicates which spaces the shovel can be used on and fixes nearly all instances a one-frame-entity would have been spawned.

## Redesign Main Menu

{{< figure src="mainmenu.gif" alt="GIF showcasing main menu" height="90%" width="90%" class="text-center" caption="*Old Main Menu vs New Main Menu*">}}

The previous main menu was the literal text book example of an main menu that you would find in alpha releases. I felt like this didn't do the game justice and as such drastically improved it. Adding nicer buttons, nicer font and generally making it look more presentable.

## Player Customization and Layered Sprites

{{< figure src="hair.gif" alt="GIF showcasing customization" height="70%" width="70%" class="text-center">}}

This feature is one of the features that look so easy to implement and barely change anything but actually require extremely complicated state handling in order to layer sprites together into one single character. Before implementing this, the character sprite was a single AnimatedSprite node, which is basically just like one single video player that handles everything for you. However, this also means that I can't simply customize something like the hair without adding hair, body and hands together for each single option beforehand, which would mean thousands of different sprites.

To support customization we have our own implementation of this AnimatedSprite node called "HumanSprite" (Yes, I am creative with my naming). This allows all NPCs, the player and so on to easily customize their looks while hiding all the complicated logic behind an abstraction layer.

And all that just so you can customize yourself and feel more immersed.

## Watering Can

{{< figure src="watering.gif" alt="GIF showcasing watering can" height="70%" width="70%" class="text-center">}}

Something that is standard in every farming game is that you have to water your crops in order to add that extra *r e a l i s m*. As such I have recently started working on the watering can. It still has a lot of things that are left to do but the basic system works perfectly.

In the future the watering can will either speed crop growth up or be mandatory in order to not have dead bushes left on the next day. It will also likely require refill at the sea or some well.

## FTAIBNSITTRTOSS

Short for **Features That Are Important But Not So Important That They Require Their Own Section Section** ;)

#### Dialog:

{{< figure src="dialog.png" alt="GIF showcasing main menu" height="90%" width="90%" class="text-center" caption="*Old Dialog vs New Dialog*">}}
- Aside from the design changes, each NPC can now also have their own button/dialog color, use rich text formatting such as *italic* or **bold** and dynamically update buttons at runtime :)

#### Time:

Time is now tracked properly, aside from that, there are now also days that are being tracked in order to create seasons or other events.

#### Sound Handler:

All SFX / Music now goes through a unified bus in order to easily change global volumes and so on. This would also allow me to add effects to sounds / music if the need ever arises to do that. Aside from that, there is now support for hourly music.

If you want to listen to one of the banger songs included by Dezphos, visit: https://youtu.be/YpdjDyiG5zE

#### Inventory Overhaul

{{< figure src="inventory.png" alt="GIF showcasing inventory" height="90%" width="90%" class="text-center" caption="*New Inventory vs Old Inventory*">}}

I drastically improved the look of the inventory while implementing support for saving/load, though my twitter followers might have already known that ;)

#### New Crop, Cabbage

Not much to say about it honestly, for now it serves no use but to look fancy.

#### A lot of bugfixes

General system stability improvements to enhance the user's experience. ;^)


## Next Features

I'm eager to start working on long-term goals for users. In order to provide incentive to plant and harvest crops, players need to have some way to sell their crops and gain some currency from them. This would require an actual merchant instead of the current plant lover alpha NPC.

There are also 2 major goals that I want to accomplish in the near future, one being online interactivity (Which I will likely talk more about when I get there since it is quite the unique vision for the game) and the other one being a proper time system.

At first I aimed to make this game real-time but the fact that seasons in rl are 3 months long is quite suboptimal and boring for something like a farming game. As such I'm currently experimenting with some systems that would allow the game to still be connected to real-time but not cause the player to feel like they have nothing to do for the entire season of winter. Once again, I'll likely talk about this in much further detail once I get to that point or decide to write a blog post about my vision for the game.


## Steam, Donations and Releasing

With (all) music, the game currently sits around 350MB which makes it extremely inconvenient to share it over GitHub. All together, I don't want to make GitHub my platform of choice when it comes to game releases. Given that it has been a huge dream to me and that I see a lot of potential in a Steam release, I decided to make this my platform of choice for the beta releases before the final launch (Unless some other game store wants to slide into my e-mails *cough farmulty@tomGER.eu cough*)

To accomplish this goal, I hoped to fund 50% of the required submission fee on Steam through donations. If you have any interest in this game and want to support me, please consider donating to me so I can put the game onto Steam. I have already put hundreds of hours into the game and I know that I'll likely never make that back but at least somewhat covering costs such as these would help me more than you could imagine:

{{< rawhtml >}}
<script type='text/javascript' src='https://storage.ko-fi.com/cdn/widget/Widget_2.js'></script><script type='text/javascript'>kofiwidget2.init('Donate to me on Ko-Fi!', '#29abe0', 'G2G418XJS');kofiwidget2.draw();</script>
{{< /rawhtml >}}

<br><br>

Thank you for reading my progress report :) You can also follow the development on my Twitter: https://www.twitter.com/_tomGER
