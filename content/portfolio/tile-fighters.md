+++
categories = ["game-dev", "unreal", "cplus"]
coders = []
date = 2021-05-05T23:00:00Z
description = "Complete, Programmer (Unreal Engine 4, Blueprints, C++) - 3D Online Multiplayer Unit Management Game with Custom Tilemap Editor"
github = ["https://github.com/devmcclu/tile-fighters"]
image = "https://i.imgur.com/rkWANUk.png"
title = "Tile Fighters"
type = "post"
[[tech]]
logo = "https://public.boxcloud.com/api/2.0/internal_files/492919699086/versions/521865489486/representations/png_paged_2048x2048/content/1.png?access_token=1!84BJcfICAN9seKZhNUlCPyOS234aSa5_WvHkUWFlTvsmgfZ1kwUy7y6PbFon-o4Hh5Hk8oktKSyguQckZoLBsW_X7FixX4AXm97A-iZXXFqFJ23AuGmFUUkXKDlzlhvFNWjqr1AAdSGOkiGtcSx9ngzOw_0wjeqw-Hfy09MfGQg3FBt02AnwenTg0ScFrgB5iG4LYckplOewjC9Lnc-Uw_Qh7LCL035UjUsz47YejoxKiug__45omh_X_kqq-IXpWbekRJqbIvnSYziWQoULc-hlmB_pfjlmshkvloKkYSjS4vYrVQSY_fDrS_msqGuCZxVghihBwrpc9vuaB9YCHRdsCwshYYONuw8Nv4k7Skou8WzIDR9tXaNLUxMYMh7Vefjimyytj5COcaUhjSn3migPuA1-ze4-rrhQul4tuWBts0H3Y0uA9SV765t3AnkIbrkNZRXuM63oN-zaezg68zjY9MwcNZ-xbjKxcRG1fKVxCzxXijuEXWi-Gac93vlHsSw2WDmsjLvM4EnbsvxsDRgQMMgL_sIC9NdRwOXCoogPOOVxOKBnGkVkDLqsy-TyRA..&shared_link=https%3A%2F%2Fepicgames.ent.box.com%2Fs%2Fr5xk6a6ch44qng7bsjfqkvqryartjhlv&box_client_name=box-content-preview&box_client_version=2.60.0"
name = "Unreal Engine 4"
url = "https://www.unrealengine.com/"

+++
March 2021 to May 2021

Solo Project

A project focusing on creating tools and expanding the use of Unreal Engine for a 3D unit management simultanious networked multiplayer game. In this, I explored ways developers can mix the use of C++ and Blueprints in a project and how to best spend time when building a game and other tools.

## Features
* Simultanious networked multiplayer
* [3D Tilemap Editing Tool]({{< ref "tile-fighters.md#tilemap-editor" >}} "Tilemap Editor")
* [Custom C++ and Blueprint data types]({{< ref "tile-fighters.md#c-and-blueprints" >}} "C++ and Blueprints")

## Tilemap Editor
### Purpose
Making grid based games in 2D has been done fairly well, in tools such as Tiled and the build in Tilemap tools in Unity and Godot. Doing so in a 3D game is a little more tricky, as there aren’t as many tools readily available. [Some exist for Unity](https://assetstore.unity.com/packages/tools/utilities/map-maker-3d-tile-tool-49819), but there does not seem to be any available for Unreal Engine (or Godot). Since I needed an easy way to construct levels in a 3D space with cube shaped models, a 3D tilemap tool was my first priority. I gave myself 4 weeks to do so.

### Process
Something like clicking on the level to place a tile seemed out of the question for the time frame of the project. So I needed to break down the basics of a map tool. In order to get the tilemap tool working, I needed at least four things: selection of the tiles, the position of the tiles, the size of the tiles in the map, and the ability to place a tile in the level. To get the tiles, I created a Primary Data Asset to hold the tile model and an icon to show the user the tiles they can choose from. These Tile Assets can be loaded on demand to create new buttons for choosing the tile to place.
The position of the tile, size of the tile, and ability to place the tile in the level are all tied together. The user supplies the size of the tile, and every time the user places a new tile by clicking the button, the Y position is incremented by the size of the tiles. The text in the text box is updated to reflect the change. The user can also arbitrarily change the position of where the tile will be placed. There didn’t seem to be a good way to keep track of these values if the tool was closed and reopened, however, so the user has to input the position of where they last left off or where they want to be.

![Spawning Tiles](https://i.imgur.com/f2sn4BG.png)
*Blueprints of how tiles are spawned*

![Tilemap Editor](https://i.imgur.com/rkWANUk.png)
*Tilemap Editor UI*

### Result
The final UI of the tool was wrapped up as a Utility Blueprint that the user can launch at anytime. It ticks all the checkboxes that were needed for this tool to hit its minimum viable product. While not perfect, this is room for this tool to grow and become something for other people to use for their own games.

![Tilemap in action](https://thumbs.gfycat.com/DelightfulMammothFlyingsquirrel-size_restricted.gif)
*The final Tilemap in action*

## C++ and Blueprints

### Purpose
Blueprints is a great tool for making games in Unreal fast, but C++ can result in more readable code if done right. C++ can also be used to create new data types in the engine for other users to create Blueprints from. Thus, I went into the project trying to understand the best uses of C++ and Blueprints in the same project and where I should spend my time.

### Process
The first tool that I set out to build entirely in C++ was the 3D tilemap editor. Unreal has a UI framework called [Slate](https://docs.unrealengine.com/en-US/ProgrammingAndScripting/Slate/index.html) which is used for creating editor tools, and also is what most of the engine is built with. Slate has some good examples on how to create UI, however I quickly realized that the amount of work required to quickly iterate on the layout and functions of the tool would require more time than I had to spend. Therefore, I used Unreal's Editor Utility Widget Blueprint to build out the UI for the Tilemap editor visually. This was a good choice, as I didn't have to worry about the specifics of placing items using code. All of the functionality of the buttons and text fields is done in Blueprint scripting, which for the most part didn't require me to make new methods.

When it came to getting the icon and mesh for the tiles, I realized that Blueprint classes would not be a good use of storing the information. I found Primary Data Assets were great for what I needed, since all I needed was references to data. Making a simple C++ class with public references to a Static Mesh and a UI is all that was needed for this information. 

![Tile Data Asset UI](https://i.imgur.com/6nXPhcO.png)
*Example Tile Data Asset UI*
![Tile Data Code](https://i.imgur.com/2lNMizH.png)
*All of the code needed for the Tile Data Asset*

Placing the tiles in the level uses Blueprints and references the information that is in the Tile Data Assets. More information about the functions of the Tilemap Editor, which are created in Blueprints, can be found [above]({{< ref "tile-fighters.md#tilemap-editor" >}} "Tilemap Editor").

When it came to gameplay, C++ and Blueprints seemed like they would be used interchangably. Spawning the units that the player controlls was thing I tackled in gameplay ++, and it was the easiest in terms of implementation, with good examples of spawning actors in the Unreal documentation and community posts.

![Spawn Fighter Code](https://i.imgur.com/MgaWgmP.png)
*Code for spawning in the units that the player controls*

When it came to building the Player Controller, C++ seemed like the reasonable choice but as I went on I found myself running into issues with referencing my custom pawn used for the units that the player controls in Blueprint functions that I was using. I tried for days to fix the issues I was experiencing setting and getting the current unit being controlled and all the units that the player can control in the game, but came to the conclussion that for this project that all of the control of gameplay should be controlled by Blueprint scripting. This led to gameplay functions being built in Blueprints during the latter half of the project.

![Player Controller](https://i.imgur.com/oO8uhuW.png)
*Part of the Player Controller's Blueprints*

### Result
In Unreal Engine, there is a lot of flexibility when it comes to using Blueprints and C++. In this project, I found that data and class variables were best held in C++, as they usually don't change too much throughout a project which reduces compile times and doesn't break any Blueprints which rely on the class. Class methods that stay relatively constant also tend to work well in a C++ project for this same reason. Blueprints are a great tool for prototyping gameplay that might be changing at a rapid pace in the design process or for elements that are easier to change visually. Some custom data types and classes also don't translate well from C++ to Blueprints which can make it difficult or impossible to modify variables, so creating these structure in Blueprints makes sense as well.