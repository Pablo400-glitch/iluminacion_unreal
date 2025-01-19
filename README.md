
# Illumination on Unreal Engine

## Introduction 

The game consists of a player who must pick up an object that grants them a special power. This power allows the player to see specific signs that guide them to escape the forest.

The objective of this project is to explore how lighting should function in a video game, experimenting with the game engine to develop a small demo.

## Character

The first thing I wanted to add to this demo was a character. For this game, I found a model of Shadow the Hedgehog and added some animations from Mixamo.

### Model

This model was not available on Mixamo, so I had to find it elsewhere. In this case, I found it on Sketchfab. For my game, I used the ThirdPerson template from Unreal Engine 5. Therefore, I replaced the default model of the template with the one I downloaded from Sketchfab.

![Alt text](/images/Model.png)

*Figure 1: Shadow the Hedgehog Model*

### Animations

For the animations, I imported the model into Mixamo and applied animations directly from there. Mixamo allows me to preview how the animations work with my model and verify if they behave as intended. Once satisfied, I can download the desired animations and integrate them into Unreal Engine 5.

![Alt text](/images/Animations.png)

*Figure 2: Mixamo Animations*

## External Environment

In this section, I will discuss how I created and imported a landscape from Blender into Unreal Engine 5, as well as the three environments and the vegetation added to the level.

### Landscape

Once the character was ready, I moved on to the landscape. The landscape was initially created in Blender, following the steps we learned during the course.

![Alt text](/images/Landscape%20Blender.png)

*Figure 3: Blender Landscape*

To design the landscape, I used Blender's Geometry Nodes utility to generate the terrain without textures, preparing it for the game.

![Alt text](/images/Landscape%20Blender%20-%20Geometry%20Nodes.png)

*Figure 4: Blender Landscape Geometry Nodes*

Finally, I imported the landscape into Unreal Engine 5. Also I had to create a new level for the game, because by default the ThirdPerson template has a level so I had to add a new one for the landscape.

![Alt text](/images/Landscape%20Unreal.png)

*Figure 5: Landscape in Unreal*

#### Materials and Environments

Once the level was created and the landscape was added, I ran the game with the model and the new landscape. However, the landscape lacked textures, so I had to add them.

I needed three environments: a snowy one, a swamp, and a normal forest. Additionally, I required a material for the path the player needs to follow. First, I downloaded four materials from Quixel and created a material with the same number of layers. Once the material was created, I made a material instance, which was then applied to the landscape. Using the paint utility, I was able to paint the textures onto the terrain.

![Alt text](/images/Forrest%20Environment.png)

*Figure 6: Forrest Environment*

![Alt text](/images/Snow%20Environment.png)

*Figure 7: Snow Environment*

![Alt text](/images/Swamp%20Environment.png)

*Figure 8: Swamp Environment*

### Vegetation

For the vegetation I add 3 types of trees, one made by me with tree it, and some rocks and grass.

### Ilumination

For the exterior lighting, I adjusted the position of the sun and added a post-process volume to control the bloom effect of the light. Additionally, I incorporated some fog into the level to enhance the atmosphere.

## Interior Environment

In this section, I will discuss the house created in the environment, the materials used, the lighting, and the reflective material.

![Alt text](/images/House.png)

*Figure 9: House Model*

### Model

To create the house, I used the modeling tools in Unreal Engine 5. The model is divided into multiple parts:

1. The Porch
    - Top
    - Middle
    - Floor
2. The House
    - Roof
    - Walls
    - Floor

I divided it this way to apply different textures to specific parts. Additionally, this approach makes it much easier to modify individual sections if needed, rather than having to edit the entire house.

![Alt text](/images/House%20Model.png)

*Figure 10: House Hierarchy*

### Materials

As before, I downloaded the textures from Quixel. For the interior environment, I used four different materials:  
- **Worn Parquet**: Applied to the floor of the house.  
- **Damaged Brick Wall**: Used for the walls and roof of the house, as well as the roof of the porch.  
- **Demolished Tiles**: Applied to the floor of the porch.  
- **Flaked Paint Walls**: Used for the middle section of the porch.  

### Ilumination and Reflections

#### Ilumination

For the lighting, I added a window to allow natural light to enter the house from the outside. Additionally, I incorporated artificial lighting for another part of the house.

The artificial light has a yellow hue, and that section of the house includes a post-process volume where the bloom effect is significantly reduced.

![Alt text](/images/Interior%20Light.png)

*Figure 11: House Interior Light*

![Alt text](/images/House%20Exterior%20Light.png)

*Figure 12: House Exterior Light*

#### Reflections

For the reflections I add a cube with a texture that can reflect. This cube is scaled to look more like a mirror instead of a cube. 

At first, the reflections were too blurry, so I had to adjust some project settings. I increased the capture resolution of reflections from 148 to 2048. Additionally, I configured Lumen to use hardware ray tracing and set the Ray Lighting Mode to "Hit Lighting for Reflections".

![Alt text](/images/Mirror.png)

*Figure 13: House Mirror*

## Pick Object Mechanic

### Mechanic

I need a mechanic that allows the player to pick up an object, granting them a special power. This power enables the player to see specific signs that guide them on where to go in order to complete the level.

So I add a new input action to the "ThirdPerson" input called **IA_Interact**, and also included it in the Input Mapping Context. Pressing the **E** key, as indicated in the interface that appears when aiming at an interactable object, triggers the **start interact** event. This event executes the logic defined within the Blueprints that use it.
In my case, the logic required was to set the visibility of the signs to true.

For the game, I added a purple orb that activates the player's power.

![Alt text](/images/Orb.png)

*Figure 14: Interactable Orb*

I also want to mention that I had to create an interface to let the player know which objects can be interacted with.

![Alt text](/images/Orb%20Interface.png)

*Figure 15: Interact Interface*

### Sign

For the sign I used a model from Sketchfab.

![Alt text](/images/Sign.png)

*Figure 16: Sign Model*

### Deferred Decal

For the Deferred Decal, I used a texture of yellow paint and created a new texture with some custom configurations. For the material domain, I set it to Deferred Decal and the blend mode to Translucent. I then applied these deferred decals to the different signs that appear at specific locations.

![Alt text](/images/Deferred%20Decal%20Material.png)

*Figure 17: Deferred Decal Material*

![Alt text](/images/Sign%20with%20deferred%20decal.png)

*Figure 18: Sign with Deferred Decal*

## Finish game

To escape from the forest, the player must follow the signs until they find a portal with a glass texture, which allows them to exit the forest.

![alt text](images/EndLevel%20Portal.png)

*Figure 19: End Level Portal*

I created a new material with the blend mode set to Translucent and adjusted the opacity to achieve a better visual effect.

![alt text](images/Glass%20Material.png)

*Figure 20: Glass Material Portal*

When the player interacts with the portal, the level simply ends. This functionality is implemented in the blueprint called "BP_EndLevel".

![alt text](/images/BP_EndLevel.png)

*Figure 20: EndLevel Blueprint*

## Bibliography

https://sketchfab.com/3d-models/ancient-tree-960fb92d7192458daeaf4282cc6193e2 (Ancient Tree)
https://www.fab.com/listings/069a0d0a-bd04-4664-ba5b-14df2c79720c (Quick treeit tree)
https://www.youtube.com/watch?v=28T3rqWyIhs (Video sobre un sistema de interacción simple)
https://sketchfab.com/3d-models/wooden-sign-low-poly-923ce9265cf244558ffa3b8c127d8111 (Wooden Sign Model)
https://www.cleanpng.com/png-computer-icons-color-clip-art-orange-juice-splashi-4048882/ (Yellow Splash)
https://www.youtube.com/watch?v=8ZH5bzQZQaQ (Unity Reflexions)