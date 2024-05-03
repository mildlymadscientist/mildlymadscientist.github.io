# mildlymadscientist.github.io

IMGD 4000 instructed by Charlie Roberts
Cozy Coast Game Portfolio
Eliza Hackler

Role: My role on this Project was as a Programmer and Game Feature Designer, designing many key features alongside my team and assisting in Programming movement, our diving game, and invisible boundaries, as well as testing some inventory concepts, sourcing, editing and implementing audio, and implementing particles effects. 

Team Experience: Our teamed formed based on compatible levels of experience. We had two experienced Game Programmers - one with some Unreal experience, one with some Unity experience -  and two programmers who only had experience designing conceptual games and boardgames, and had experience programming in C++. We met with a variety of art teams, and joined with a team who also was interest in making a cozy game. I pitched a fishing game, and my team was enthusiastic about the idea. We did most of our work together in the school lab, allowing us to work mostly together, and even when not taking the lead on researching and implementing we could see how each tech feature was created. 

Design: We evaluated resources like online tutorials, advice from the teaching assistant based on our plans, and our own programming skills, and while we were all experienced in C++ we were very interested in learning Blueprints in Unreal 5. We chose to make our game using Blueprints so we could utilize the extensive Blueprint tutorials online. 
I concepted a overhead diving minigame, where the player would look down on the bird and control it’s shadow using WASD, then intersect a fish’s shadow and dive. When we decided we also wanted to be able to play as a human, I came up with some plans for a fish shop, we conceptualized the island with the art team, and started on the game. 

Structure: The game is comprised of a few main tech features. Which have the player view, where one can navigate the island and interact with NPCs, we have an NPC dialogue system, and the UI system using widgets. As the bird, we have a separate movement system, a dive mechanic with a spam minigame, and the complex fish spawning system. 

Movement: I worked on the character movement first, starting with a simple WASD movement where the character moves only one direction at a time, either on the x or y, using input mapping. 


![Screenshot 2024-05-03 160501](https://github.com/mildlymadscientist/mildlymadscientist.github.io/assets/117318083/26fd9945-b587-42a5-acb6-d4d9a4da0730)
![Screenshot 2024-05-03 160456](https://github.com/mildlymadscientist/mildlymadscientist.github.io/assets/117318083/69262f8c-3602-477f-86d7-b5956d3d3b1e)
![Screenshot 2024-05-03 144827](https://github.com/mildlymadscientist/mildlymadscientist.github.io/assets/117318083/1116065b-100b-400b-9fc3-a3d8e272bbf8)




Then using some of the built in Unreal features, turned off Character Rotation yaw and turned on Orient Character to movement so the character could move on a the 45 degree angles for enhanced movement and orient the mesh so it would face the direction the character was going. At this point, me and another programmer experimented with omnidirectional movement, where A and D were turning left and right, and W and S were forward and backwards, but since our camera was fixed in place, there was no need to add complication. 
The bird movement was similar, so we used the same input mapping, locked the map and attached a camera from above. We planned out a system to flip the bird back the way it came but when we did playtesting, based off instructor feedback, we chose to simply have the bird spiral around the screen and control a reticle in the water with WASD, ending up very similar to my original design of controlling a shadow. 

Dive Event: Because the swimming patterns of the fish were so complicated, we didn’t want to make it any more difficult to catch them, so in the original the check for collisions happened at the beginning, then the fish descended down the the fish spawning plane, and during that gave the player a quick time event of spamming space. If the player completes it, the fish is returned. While I worked less on the dive after playtesting, the bird was changed to a moving reticle, and the fish, or special item, is now checked off in quest progress. 

 ![Screenshot 2024-05-03 164016](https://github.com/mildlymadscientist/mildlymadscientist.github.io/assets/117318083/d345c27e-d570-4c6a-a53f-d778193bc9f5)


Scrapped ideas: There were few features that didn’t serve our game at all, but one was my  system to first carry the fish over to a barrel on the dock after catching it, and only then would the fish be returned, if it collided with the barrel (or was close enough). It ended up being very redundant and tedious to just catch one fish, because there was already a dive event and a minigame. 

Audio and Particles: I sourced all audio from Freesound, save a few sound that I synthesize, or edited greatly, using Emmisions Control 2 and Audacity. While in the future I have plans to synthesize and record every sound myself or with the team, it served the purpose in being cohesive enough and indiacting game events to the player. In Unreal, the ambient sound object only worked for on of our 4 ambient sounds, the wave and wind track. The music track stopped too abruptly, so me and the ui programmer attached it to an always running UI widget, and then when the music wouldn’t stop in the Unreal editor, we made sure to deconstruct the widget upon shutdown. The other two ambient tracks were based on location, and played when the player entered the trigger boxes. Initially this was simply done by using play sound, which we quickly realized meant it would not stop upon leaving the area. 

We instead spawned in both sounds (and stopped them playing as when spawned the audio starts). 

![Screenshot 2024-05-03 165746](https://github.com/mildlymadscientist/mildlymadscientist.github.io/assets/117318083/febe9a25-4a06-469b-8d7e-6cc5299624ef)

 
When the player enters a triggerbox, that sound variable is played, when they leave it stops. 

![Screenshot 2024-05-03 165734](https://github.com/mildlymadscientist/mildlymadscientist.github.io/assets/117318083/ebcb9813-c2d5-49e4-94f9-473643fd421b)

 
The Particles were created using the Niagara system. For the different footstep materials, material classes were added in the project settings, and the physical material overrides were added to each object the player could walk on. While I initially used the Play sound and Play particle notifies, the particles would not scale properly, so I added notifies to the animations, and referenced them in the ABP. 
 
I used line trace to detect a collision with the material type, then based on that play the appropriate sound and particle effect at location. Because the particles don’t spawn fast enough, they are about a whole footstep late, so I used the actor’s transform and forward vector to calculate the actor’s direction, then play each particle 75 pixels forward in the direction of the character’s movement. 
Boundaries: To keep the character from being able to step off cliffs into the water and have to walk all the way around the island to the beach, the “can step off cliffs” needed to be disabled. To avoid revealing that the water was a solid object in our Alpha, I also turned off collisions with the water to the engine treated it as a cliff and made it uninteractable. When our environmental artist added ground underneath the shallow water of the beaches this stopped working, and I wanted to show off that the water looked good with the character walking in it, so I simply made a system of invisible walls around the beaches, and anywhere the character could make their way to the water. It allowed more flexibility than having the artists building some big single attached wall, so I was able to play with the shape more. 

Version Control: We chose to use Github’s large file sharing service, Git LFS, as we had a lot of big files. It mostly worked as expected, but I experienced it getting struck a few times and taking excessively long to download, or not showing it was dowloading at all, just waiting until you fetched again and showing how many more files had changed based on how long it had been. 

Github Desktop was used by all of us but the one Linux user in our group, which caused no problems. To avoid working with the same file, we worked on separate versions of the island, and combined the features when we got the time together in the lab. 

Conclusion: As the most amatuer programmer on the team, my goal was to learn as mcu about Unreal Engine as I could for my own experience, so working together and being to see and understand every element of our project was awesome. It went so well, we hope to be able to continue our work, as we feel we are close to having a working game!
