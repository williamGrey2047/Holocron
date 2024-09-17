
> [!important] View the assessment on Google Classroom for specific details.

# Technical Report

For suggestions on how to structure your report, see this page:

[Technical Report Writing](_sharedContent/technicalReportWriting.md)

# Assessable Topics 

These are the details you are to cover in the topics in Assessment 2. More Specific Details will be added later in the document.

![assessment2Topics](ISD/2%20-%20Digital%20Applications/2024S2/_images/assessment2Topics.png)

![[_sharedContent/Assessments2024S2/Task 2#Project Overview|Task 2]]

![[_sharedContent/Assessments2024S2/Task 2#Code|Task 2]]

![[_sharedContent/Assessments2024S2/Task 2#Data|Task 2]]

![[_sharedContent/Assessments2024S2/Task 2#Development Process|Task 2]]

Example: 

For the project there are 3 main components that needed to be created from a development standpoint. Those 3 components were the Environments, Player, and Enemies. While other components were required the remaining components were for the most part a result of developing the 3 main components.

Initially a texture-less grey box was created using Godot's 3 shape creation and editing space. These were given collision physics using `CollisionShape3D` child nodes which will be later used to ensure the player and enemy don't move through the walls and floors. This environment was created for the purposes of testing out the functionality of the game actions as they are developed. Once the game has a working engine and functionality the environment will be updated for variety and flavour. 

A player was created as a formless, texture-less, capsule-shape and given a `CollisionShape3d` for the purposes of movement and detection. A `Camera3D` was attached to the player model at the appropriate height through which the player will view the game and a `RayCast3D` was attached project forward both for detecting objects immediately in front of the player.
Movement was added to the `player.gd` script to allow for movement by defining speed and then adding variables that track input direction based on player inputs and then change the `velocity` of the player-model to the current speed in the direction that was input. This was tested in the environment along with a togglable speed increase to add a sprint functionality, a jump function that prevented continual escalation by checking if the player-model is on the floor. This all interacted with a statement that added gravity to the player-model to ensure they stay on the ground.
This formed the basis for the player-model and interactions with the environment. Raycasting was tested against the walls using a `print()` function to show when the walls and floors were in the raycast. A bullet model was created and a spawn point was created for the bullets to come out of the players camera along the raycast and similarly a `print()` function was used to test when the bullets collide with walls and floors.

An enemy model was created and some scripting was used to give the enemies the functionality to follow the player around. This was tested in the basic environment. The enemy models movement utilised a lot of the same physics functions that the player did to keep them on the ground but utilised library functions to find it's own location, the player's location and then increase the enemies `velocity` in the direction of the player.
A function was added to the enemies to detect when a bullet made contact with them. This used similar syntax and logic as the functions that detected bullet collision with the environment but required some iteration to add in an enemy health value that would be reduced and remove the enemy once they had 0 health. 

A health value was added to the player that would reduce when colliding with the enemies. Variables were then added to keep track of the player health and the number of enemies. These two variables served as the win and loss conditions. If the player health reached 0 then the player lost and the game would display a lose screen that was created using Godot's 2D modelling space. If the number of enemies reached 0 then the game was set up to progress the player to the next level.

With these 3 main components completely implemented and tested the game was then ready to be refined. Function was working and now flavour needed to be added. First the levels were made more interesting with environments that better reflected the gameplay. With small maze-like structures to encourage a slow methodical progression and then some long catwalks to encourage a full on, fast-paced section. Textures were imported using seamless png images and applied to the environment. Royalty free enemy models were sourced from online and used to better represent the enemies.

This development continued with 2 additional levels and all levels were tested for bugs, enemy dead-spaces (areas where the player could sit without enemies getting to them), wall-glitches. Where these were found small fixes were made in the environment design mostly by adding additional `CollisionShapes3D` that prevented access to those areas.  


![[_sharedContent/Assessments2024S2/Task 2#Technical Analysis|Task 2]]



![[_sharedContent/Assessments2024S2/Task 2#Work Skills|Task 2]]
