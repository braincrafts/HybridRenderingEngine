# HRE :: Hybrid (Clustered Forward/Deferred) Rendering Engine 

[![GitHub license](https://img.shields.io/github/license/Angelo1211/HybridRenderingEngine.svg)](https://github.com/Angelo1211/HybridRenderingEngine/blob/master/LICENSE)
[![GitHub issues](https://img.shields.io/github/issues/Angelo1211/HybridRenderingEngine.svg)](https://github.com/Angelo1211/HybridRenderingEngine/issues)

HRE was a real-time, Physically based, Clustered renderer built with OpenGL and based on the techniques described on the paper [Clustered Deferred and Forward shading](http://www.cse.chalmers.se/~uffe/clustered_shading_preprint.pdf) by Ola Olsson, Markus Billeter and Ulf Assarsson. The aim of this project is to build a testing framework to showcase deferred and forward graphics techniques (hence the hybrid part) and to examine the strengths of Clustered shading. I wrote a lengthy blog post full of cool animations that can serve as an introduction to efficient rendering algorithms as well as a detailed guide of my implementation of Clustered Shading, so make sure to check it out [here!](http://www.aortiz.me/2018/12/21/CG.html)

This algorithm was selected for its two major benefits over traditional deferred/tiled solutions: it allows for more freedom to choose forward or deferred shading paths as desired and is a better long term fit for the modern GPU performance trends. It has already been succesfully implemented in some of the best looking games of the last couple of years, with some notable examples being: [DOOM 2016](https://www.slideshare.net/TiagoAlexSousa/siggraph2016-the-devil-is-in-the-details-idtech-666), [Just Cause 3](http://www.humus.name/Articles/PracticalClusteredShading.pdf) and [Detroit: Become Human](https://www.gdcvault.com/play/1025420/Cluster-Forward-Rendering-and-Anti). 

### Project is now on hold :(

Unfortunately this project is no longer maintained. I got hired to work at Rockstar Games as a Graphics Programmer shortly after posting this and don't have the time to work on a sideproject of this size anymore. I plan on keeping it up (as well as my other major graphics project [SSGE](https://github.com/Angelo1211/SoftwareRenderer)) so others can see what it took me to break into the industry. I will still be helping anyone who runs into any issues with it or has any questions about it. Feel free to reach me here or at [my twitter](https://twitter.com/aortizelguero) about this or any other GFX topic you'd like to talk about! Thanks to everyone who checked this project out! :D 

## Download

Stable builds can be found on the [HRE releases](https://github.com/Angelo1211/HybridRenderingEngine/releases) page. 

Currently only Windows platforms are supported.

## Render Samples
![helmetcrop](https://user-images.githubusercontent.com/11263073/49331372-01e09980-f59c-11e8-93af-c706c0571fb4.PNG)

![waterbottlefixed](https://user-images.githubusercontent.com/11263073/49331375-01e09980-f59c-11e8-9b62-34c7b8e5a986.PNG)

![metallicspheres](https://user-images.githubusercontent.com/11263073/49331373-01e09980-f59c-11e8-87c1-63c320ec9e3b.PNG)

![sponza](https://user-images.githubusercontent.com/11263073/49331374-01e09980-f59c-11e8-9306-beaec08e8ad6.PNG)
![correct colors](https://user-images.githubusercontent.com/11263073/49331468-ad3e1e00-f59d-11e8-9a1a-86813ea4f85e.PNG)

<center> <h4>Cluster z slices</h4> </center>

## Main Features

### Rendering 

* Clustered Forward/Deferred Renderer
* Physically Based shading
* Image Based Lighting
* Metallic workflow
* Cook-Torrance specular BRDF (w/ lambert diffuse)
* Ambient Occlusion & Emissive mapping
* Tangent space normal mapping
* HDR/linear lighting
* HDR/LDR skyboxes
* Exposure based tone mapping
* Bloom
* Multisample Anti-aliasing (MSAA)
* Directional & point light sources
* Compute shader based light culling
* Alpha tested foliage (sponza atrium)
* Directional light dynamic shadow mapping
* Static Omnidirectional Shadow Mapping for Point Lights
* Forward, Tiled Forward and Deferred rendering implementations
    * Located in other branches of the repo. Only clustered rendering is actively being developed.

### Engine
* OpenGL 4.5+
* SDL2 backend 
* JSON Parsing via Nlohmann: JSON for C++
* Model Loading via ASSIMP (OBJ, FBX, gLTF2.0 etc)
* Scene contents clearly outlined in JSON file
* Multiple image loading paths via stb-image and GLI
* Immediate mode GUI for debugging via ImGUI
* Fully commented for future referencing
* Environment map generation on load for IBL and skyboxes
* Free flight camera

## Development Timeline & Planned Features 

### Alas, I am unfortunately unable to work on this project anymore and won't be updating it any time soon. I am still keeping this section in here as a record in case I ever do return and as proof of my naive optimism. Thanks to everyone who checked out this project! :) 

The first development cycle began September 2018 and concluded December 2018 with the inclusion of Image Based Lighting and the release of the first stable version: HRE 0.01 "Aachen". For the next couple of months I'll be tackling the issues outlined in the [Projects section](https://github.com/Angelo1211/HybridRenderingEngine/projects) beginning with fixes for the remaining non-critical bugs and then moving on to a major re-write of the material system. The following is a a list of the engine features I aim to include over the coming months, it's obviously subject to change and all that stuff. 

#### Update #1: Materials & Shadow Mapping
 * Full material system re-write to decouple mesh & textures.
 * Implementing a shadow mapping atlas and automatic shadow map reuse.
 * Fix some unneccessary STL calls.

#### Update #2: Deferred / Screen Space Effects
* Rewriting screen space fragment shaders as compute shaders
* Screen Space Ambient Occlusion
* Screen Space Reflections
* Temporal AA
* Improved Color Grading & Tone Mapping

#### Update #3: Cluster Optimizations
* Large amounts of lights via BVH construction
* Advanced environment mapping
* View Frustum culling
* Compute shader based particles
* Include Approaching Zero Driver Overhead (AZDO) principles 

I'll be writing accompanying blog posts at the end of each major milestone, outlining the new features and their implementations and any complications I found along the way. Meanwhile, [Here's the first post](http://www.aortiz.me/2018/12/21/CG.html) which contains an overview of other traditional rendering algorithms and builds the case for Clustered rendering. 

## Repository structure

```bash
Hybrid Rendering Engine
|-- assets              
|   |-- models              # Meshes and textures
|   |-- scenes              # Scene description files in JSON format
|   |-- shaders             
|   |   |-- computeShaders  # Compute shaders for clustered forward
|   |   |-- OldShaders      # Shaders not currently in use
|   |   `-- currentShaders  # Shaders for the current rendering pipeline
|   `-- skyboxes            # Skyboxes in either cubemap or equirectangular map form
|-- build                   # CMake compile  
|-- include                 # Project header files
|-- libs                    # Check dependencies section for descriptions & links
|   |-- ASSIMP               
|   |-- Dear imgui           
|   |-- Glad 
|   |-- Json c++            
|   |-- GLI 
|   |-- GLM 
|   |-- stb_image 
|   `-- SDL2 
|-- modules                 # CMake lib setup scripts
|-- src                     # C++ implementation files
`-- CMakeLists.txt          # CMake build script
```

## Dependencies 

In my previous project, [SSGE](https://github.com/Angelo1211/SoftwareRenderer), I made an effort to reduce the amount of dependencies to a minimum. This time however, the pendulum has swung the other way and I've made no restriction whatsoever (within reason) as to what libraries I could include in the project. I did this because I wanted to get more comfortable with the process of including and working with external libraries in C++.

Here's a list of the libraries currently included in the project:

* [ASSIMP](https://github.com/assimp/assimp): Mesh and material loading.
* [dear imgui,](https://github.com/ocornut/imgui): Immediate Mode GUI.
* [glad](https://github.com/Dav1dde/glad): GL loader-generator.
* [JSON for Modern C++](https://github.com/nlohmann/json): Scene description and serialization.
* [OpenGL Image (GLI)](https://github.com/g-truc/gli): Image loading for DDS files.
* [OpenGL Mathematics (GLM)](https://glm.g-truc.net/0.9.9/index.html): Linear algebra / matrix library.
* [SDL2](https://www.libsdl.org/download-2.0.php): Hardware abstraction layer.
* [stb_image](https://github.com/nothings/stb): Image loading/decoding for JPG, PNG, HDR.

Here's a list of the libraries **not** included:

* [CMake](https://github.com/Kitware/CMake): Build generation.
* [OpenGL](https://www.opengl.org/): All things GPU & graphics.

All included libraries are represented here under their respective licenses which can be found in the links above or in the licenses.txt doc in the libs folder.

## References

There's a comprehensive indexed list of references for the project that I keep more or less up to date in this [page of the wiki](https://github.com/Angelo1211/HybridRenderingEngine/wiki/References). However, I find myself constantly returning to a subset of them for further reading or when I need inspiration, so I've added links below to share them and spread the word of their awesomeness. Check them out! 

* [Learn OpenGL](https://learnopengl.com/Introduction): OpenGL tutorials and general introduction to 3D graphics concepts.
* [Parallel Computer Architecture and Programming](http://15418.courses.cs.cmu.edu/tsinghua2017/home) : Intro to the GPU programming model. 
* [Doom(2016) - Graphics Study](http://www.adriancourreges.com/blog/2016/09/09/doom-2016-graphics-study/): Dissection of a frame in the id Tech 6 engine.
* [Siggraph2016 - The Devil is in the Details: idTech 666](https://www.slideshare.net/TiagoAlexSousa/siggraph2016-the-devil-is-in-the-details-idtech-666?next_slideshow=1): A behind-the scenes look into the renderer tech of DOOM 2016. Probably the biggest inspiration in terms of features and overall quality level that I'm striving for.  
* [Efficient Real-Time Shading with Many Lights](https://www.zora.uzh.ch/id/eprint/107598/1/a11-olsson.pdf): An introduction to clustered shading directly from the writers of the original paper. Also outlines some practical tips from industry veterans.
* [Real Shading in Unreal Engine 4](https://blog.selfshadow.com/publications/s2013-shading-course/karis/s2013_pbs_epic_notes_v2.pdf): The principles and implementation details behind UE4 physically based shading model. Includes shader code!
* [Forward vs Deferred vs Forward+ Rendering with DirectX 11](https://www.3dgep.com/forward-plus/): Detailed overview of different rendering algorithms.

## Acknowledgements
### Models & Textures

* [Sponza (gLTF2 Version)](https://github.com/KhronosGroup/glTF-Sample-Models/tree/master/2.0/Sponza)
: Original model: [Frank Meinl](https://www.artstation.com/artwork/K5bEr), First modified by: [Morgan McGuire](http://casual-effects.com/data/index.html), PBR Textures: [Alexandre-pestana](http://www.alexandre-pestana.com/pbr-textures-sponza/).
* [Barcelona Sunrise (HDR Map)](http://www.hdrlabs.com/sibl/archive.html): by [@Blochi](https://twitter.com/Blochi)
* [Battle Damaged Sci-fi Helmet (PBR)](https://github.com/KhronosGroup/glTF-Sample-Models/tree/master/2.0/DamagedHelmet): by [@theblueturtle_](https://sketchfab.com/theblueturtle_)
* [Metal Rough Test Spheres (PBR)](https://github.com/KhronosGroup/glTF-Sample-Models/tree/master/2.0/MetalRoughSpheres): by Ed Mackey.
* [gLTF Sample Model Repository](https://github.com/KhronosGroup/glTF-Sample-Models): All other models & textures.
* [sIBL Archive](http://www.hdrlabs.com/sibl/archive.html): All other HDR maps & skyboxes.
* [Default Skybox](http://www.custommapmakers.org/skyboxes.php)

Thank you to all the 3D & texture artists who have made their assets free to use and so beautiful to look at. If it weren't for you guys I'd probably still be staring at the same old boring utah teapot all damn day!  

If I've mis-acknowledged, misattributed, or missed any references, please, create a new GitHub issue or send me a DM on Twitter and I'll make sure to fix it immediately.

### Graphics Programming Community <3

Shout-out to Kostas Anagnostou and Eric Arnebäck for taking the time to answer all of my questions for the last couple of months, your explanations made understanding every daunting topic so much easier!

## License

MIT License

Copyright (c) 2018 Angel Ortiz

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.




## 🌐 Web Resources & Interactive Index
- [FIDGET TOYS POP IT](https://studyplayings.pages.dev/fidget-toys-pop-it.html)
- [FASHION BATTLE FOR SURVIVAL](https://studyquests.github.io/fashion-battle-for-survival.html)
- [ENGLISH CHECKERS](https://themindplay.github.io/english-checkers.html)
- [WORD CLASH](https://themindplaying.web.app/word-clash.html)
- [BUBBLE SHOOTER REMASTERED](https://themindskillplayplay.pages.dev/bubble-shooter-remastered.html)
- [HOOK MASTER MAFIA CITY](https://skillplay.github.io/hook-master-mafia-city.html)
- [CATEGORY TOP DOWN248](https://themindskillplayplay.pages.dev/category-top-down248.html)
- [BATTLEDUDES IO](https://skillplay.github.io/battledudes-io.html)
- [FAIRY WINGERELLA](https://themindskillplayplay.pages.dev/fairy-wingerella.html)
- [STICKMAN IN SPACE](https://themindskillplayplay.pages.dev/stickman-in-space.html)
- [EGGY BEATS](https://skillplay.github.io/eggy-beats.html)
- [MERGE WAR](https://skillplay.github.io/merge-war.html)
- [MY FARM](https://themindskillplayplay.pages.dev/my-farm.html)
- [CATEGORY PLATFORM260](https://themindskillplayplay.pages.dev/category-platform260.html)
- [PLAYGROUND PARKOUR](https://themindskillplayplay.pages.dev/playground-parkour.html)
- [DEFENDERS OF THE REALM AN EPIC WAR](https://themindskillplayplay.pages.dev/defenders-of-the-realm-an-epic-war.html)
- [CATEGORY SNIPER39](https://themindskillplayplay.pages.dev/category-sniper39.html)
- [MONEY MAKER](https://iskillplay.web.app/money-maker.html)
- [CONNECT 2 CARS](https://skillplay.github.io/connect-2-cars.html)
- [WEST FRONTIER SHARPSHOOTER 3D](https://iskillplay.web.app/west-frontier-sharpshooter-3d.html)
- [CATEGORY SIMULATION 2](https://themindskillplayplay.pages.dev/category-simulation-2.html)
- [CODE RUNNER BINARY CONFUSION](https://themindskillplayplay.pages.dev/code-runner-binary-confusion.html)
- [HOME PIN 2](https://iskillplay.web.app/home-pin-2.html)
- [LABUBU JETPACK RUSH](https://skillplay.github.io/labubu-jetpack-rush.html)
- [PAINT MASTER](https://themindskillplayplay.pages.dev/paint-master.html)
- [STICKMAN SANTA](https://iskillplay.web.app/stickman-santa.html)
- [MERGE 3D MATCH 3 BALLOONS](https://skillplay.github.io/merge-3d-match-3-balloons.html)
- [GOBATTLEIO](https://themindskillplayplay.pages.dev/gobattleio.html)
- [FEET DOCTOR URGENCY CARE](https://skillplay.github.io/feet-doctor-urgency-care.html)
- [ROBBIE STAND ON THE RIGHT COLOR](https://iskillplay.web.app/robbie-stand-on-the-right-color.html)
- [BATTLE RACING STARS](https://iskillplay.web.app/battle-racing-stars.html)
- [OKAY](https://skillplay.github.io/okay.html)
- [CS COMMAND SNIPERS](https://themindskillplayplay.pages.dev/cs-command-snipers.html)
- [TRIAL XTREME](https://skillplay.github.io/trial-xtreme.html)
- [BLOCK PUZZLE TRAVEL](https://skillplay.github.io/block-puzzle-travel.html)
- [SNIPER VS SNIPER](https://iskillplay.web.app/sniper-vs-sniper.html)
- [CATEGORY MINECRAFT 3](https://themindskillplayplay.pages.dev/category-minecraft-3.html)
- [ERASE THE EXTRA ELEMENT](https://skillplay.github.io/erase-the-extra-element.html)
- [ASTRO KITTY RUSH](https://iskillplay.web.app/astro-kitty-rush.html)
- [COLOR RACE OBBY](https://iskillplay.web.app/color-race-obby.html)
- [CATEGORY PUZZLE 6](https://themindskillplayplay.pages.dev/category-puzzle-6.html)
- [CATEGORY SURVIVAL365](https://themindskillplayplay.pages.dev/category-survival365.html)
- [REAL RACING 3D](https://themindskillplayplay.pages.dev/real-racing-3d.html)
- [ZOMBIE CHASE](https://iskillplay.web.app/zombie-chase.html)
- [CATEGORY POOL17](https://themindskillplayplay.pages.dev/category-pool17.html)
- [BANG BANG MAHJONG](https://iskillplay.web.app/bang-bang-mahjong.html)
- [ATLANTIC SKY HUNTER XTREME](https://iskillplay.web.app/atlantic-sky-hunter-xtreme.html)
- [CATEGORY QUIZ](https://themindskillplayplay.pages.dev/category-quiz.html)
- [ARROW SHIFT LOGIC TREE](https://iskillplay.web.app/arrow-shift-logic-tree.html)
- [ARMY FIGHT 3D](https://themindskillplayplay.pages.dev/army-fight-3d.html)
- [UPHILL RUSH 13](https://iskillplay.web.app/uphill-rush-13.html)
- [AVATAR MAKE UP](https://themindskillplayplay.pages.dev/avatar-make-up.html)
- [ACCURATE 2D](https://skillplay.github.io/accurate-2d.html)
- [AIDAN IN DANGER](https://skillplay.github.io/aidan-in-danger.html)
- [STELLAR STYLE SPECTACLE FASHION](https://skillplay.github.io/stellar-style-spectacle-fashion.html)
- [NINJA WARS BATTLE SIMULATOR](https://skillplay.github.io/ninja-wars-battle-simulator.html)
- [CATEGORY SOLITAIRE27](https://themindskillplayplay.pages.dev/category-solitaire27.html)
- [CRIME THEFT GANGSTER PARADISE](https://themindskillplayplay.pages.dev/crime-theft-gangster-paradise.html)
- [CATEGORY RACING127](https://themindskillplayplay.pages.dev/category-racing127.html)
- [IDLE PIZZA BUSINESS](https://iskillplay.web.app/idle-pizza-business.html)
- [CATEGORY STICKMAN 3](https://themindskillplayplay.pages.dev/category-stickman-3.html)
- [DIGIT SHOOTER](https://themindskillplayplay.pages.dev/digit-shooter.html)
- [PICK BRAINROT 3D BATTLE](https://themindskillplayplay.pages.dev/pick-brainrot-3d-battle.html)
- [SNIPER WARS FIND THE CRIMINAL](https://themindskillplayplay.pages.dev/sniper-wars-find-the-criminal.html)
- [CATEGORY STRATEGY 2](https://themindskillplayplay.pages.dev/category-strategy-2.html)
- [STUMBLE GUYS](https://iskillplay.web.app/stumble-guys.html)
- [BREAK THE BLOCK THERE BRAINROT](https://iskillplay.web.app/break-the-block-there-brainrot.html)
- [OBBY PRISON CRAFT ESCAPE](https://iskillplay.web.app/obby-prison-craft-escape.html)
- [FARM MERGE HARVEST](https://iskillplay.web.app/farm-merge-harvest.html)
- [STICKER PUZZLE BOOK](https://iskillplay.web.app/sticker-puzzle-book.html)
- [MAZEAN COM](https://themindskillplayplay.pages.dev/mazean-com.html)
- [CATEGORY FPS 2](https://theskillquest.pages.dev/category-fps-2.html)
- [FISHING FISHES](https://iskillplay.web.app/fishing-fishes.html)
- [TANK ATTACK 5](https://iskillquest.pages.dev/tank-attack-5.html)
- [HELIX CRUSH](https://theskillquest.pages.dev/helix-crush.html)
- [CUDDLE MONSTER FUSION](https://themindskillplayplay.pages.dev/cuddle-monster-fusion.html)
- [SQUID ESCAPE GAME](https://themindskillplayplay.pages.dev/squid-escape-game.html)
- [DESTRUCTION SIMULATOR](https://themindzone.pages.dev/destruction-simulator.html)
- [CATEGORY TOWER DEFENSE](https://themindzone.pages.dev/category-tower-defense.html)
- [CATEGORY CAN T STOP PLAYING212](https://theskillquest.pages.dev/category-can-t-stop-playing212.html)
- [COLOR DODGE](https://studyquests.github.io/color-dodge.html)
- [CATEGORY PHYSICS371](https://studyplayings.pages.dev/category-physics371.html)
- [PUZZLE BLOCKS](https://iskillplay.web.app/puzzle-blocks.html)
- [TRIVIA NATION](https://studyplayings.web.app/trivia-nation.html)
- [CATEGORY MOUSE1 707](https://quizverses.pages.dev/category-mouse1-707.html)
- [HIDDEN OBJECTS STORY](https://studyplayings.pages.dev/hidden-objects-story.html)
- [CATEGORY MOBILE2 112 2](https://themindskillplayplay.pages.dev/category-mobile2-112-2.html)
- [SUPER STAR ANIMAL SALON](https://learnquester.github.io/super-star-animal-salon.html)
- [FIRESIDE SOLITAIRE](https://studyplaying.github.io/fireside-solitaire.html)
- [CATEGORY CASUAL](https://learnquester.github.io/category-casual.html)
- [PIRATES MAHJONG](https://quizverses.pages.dev/pirates-mahjong.html)
- [CATEGORY MATCH 3117](https://quizverses.pages.dev/category-match-3117.html)
- [CATEGORY MEDIEVAL15](https://quizverses.pages.dev/category-medieval15.html)
- [LOVE IN STYLE](https://iskillplay.web.app/love-in-style.html)
- [CATEGORY STICKMAN175](https://quizverses.pages.dev/category-stickman175.html)
- [CATEGORY FLASH](https://studyplayings.pages.dev/category-flash.html)
- [BUBBLE BLITZ GALAXY](https://theskillquest.pages.dev/bubble-blitz-galaxy.html)
- [APOCALYPSE SHELTER](https://iskillplay.web.app/apocalypse-shelter.html)
- [CATEGORY BIKE](https://quizverses.pages.dev/category-bike.html)
- [CATEGORY COOKING46](https://quizverses.pages.dev/category-cooking46.html)
- [TINY FARM](https://quizverses.pages.dev/tiny-farm.html)
- [SAVE STRANDING FISH](https://thequizzone.pages.dev/save-stranding-fish.html)
- [STICKMAN SHOOTER BROS](https://studyplayings.pages.dev/stickman-shooter-bros.html)
- [CATEGORY STICKMAN 2](https://quizverses.pages.dev/category-stickman-2.html)
- [MILITARY CUBES 2048](https://iskillplay.web.app/military-cubes-2048.html)
- [CATEGORY SHOP49](https://themindskillplayplay.pages.dev/category-shop49.html)
- [REAL DRIVE 3D](https://learnquester.github.io/real-drive-3d.html)
- [ENERGY SUPERMAN 3D](https://thelearnquester.web.app/energy-superman-3d.html)
- [SOLITAIRE FARM SEASONS 3](https://iskillquest.pages.dev/solitaire-farm-seasons-3.html)
- [CATEGORY LANSCHOOL](https://studyplaying.github.io/category-lanschool.html)
- [COLLEGE GIRL COLORING DRESS UP](https://iskillplay.web.app/college-girl-coloring-dress-up.html)
- [VORTEX BALL](https://studyplayings.web.app/vortex-ball.html)
- [CATEGORY STICKMAN](https://studyquests.pages.dev/category-stickman.html)
- [ONLY UP BALLS](https://themindskillplayplay.pages.dev/only-up-balls.html)
- [CATEGORY DRAGON22](https://iskillplay.web.app/category-dragon22.html)
- [BRAINROT MEMORY](https://thequizzone.pages.dev/brainrot-memory.html)
- [HERO PIPE](https://studyquests.github.io/hero-pipe.html)
- [CATEGORY CAR](https://quizverses.pages.dev/category-car.html)
- [BOUNCY BLOB RACE OBSTACLE COURSE](https://themindzone.pages.dev/bouncy-blob-race-obstacle-course.html)
- [WORDS WITH OWL](https://learnquester.github.io/words-with-owl.html)
- [2 CARS RUN](https://theskillquest.pages.dev/2-cars-run.html)
- [CRYPTOWORD](https://studyplayings.web.app/cryptoword.html)
- [FASHION WORLD SIMULATOR](https://themindskillplayplay.pages.dev/fashion-world-simulator.html)
- [LIVE 100 DAYS](https://skillplay.github.io/live-100-days.html)
- [CATEGORY ESCAPE](https://iskillplay.web.app/category-escape.html)
- [CUT THE ROPE TIME TRAVEL](https://learnquester.github.io/cut-the-rope-time-travel.html)
- [CATEGORY MAHJONG CONNECT](https://themindskillplayplay.pages.dev/category-mahjong-connect.html)
- [OHPEACH IT](https://themindskillplayplay.pages.dev/ohpeach-it.html)
- [SANDBOX ISLAND WAR](https://themindskillplayplay.pages.dev/sandbox-island-war.html)
- [CATEGORY BOARDGAMES](https://theskillquest.pages.dev/category-boardgames.html)
