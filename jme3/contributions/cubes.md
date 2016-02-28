---
title: Cubes - A Block World Framework
---
<h1 class="sectionedit1" id="cubes_-_a_block_world_framework">Cubes - A Block World Framework</h1>
<div class="level1">

<p>
<a href="/resources/fetch.php" class="media" title="http://destroflyer.mania-community.de/other/imagehost/cubes/header.png"><img src="/resources/fetch.php" class="mediacenter" alt="" width="650" /></a>
</p>

<p>
</p><p></p><div class="noteimportant">This framework is still <strong>work-in-progress</strong> - I'll keep you up-to-date about modifications. :)
</div>


<p>
As the title says, “Cubes” is a framework for block worlds (also called “bloxel” or “minecraft-like”) - It offers an easy way to add/remove blocks, block skinning, useful tools and user-specific behaviours. “Cubes” itself will not contain tools for creating crafting or RPG functionalities, it will <strong>only</strong> help you managing the block system.
</p>

</div>
<!-- EDIT1 SECTION "Cubes - A Block World Framework" [1-603] -->
<h2 class="sectionedit2" id="the_origin">The origin</h2>
<div class="level2">

<p>
In the summer of 2011, I (destroflyer) started a little minecraft clone (like almost every jMonkey) - nothing special, I just wanted a little block world in which players can walk around, place or remove blocks and the ability to save those maps. It didn't take long until I stumbled across the “batch-boxes-to-improve-performance”, texture atlas and mesh optimization things - Luckily, I managed to get those to run, played a few rounds with a friend and that was it. The code was really quick 'n dirty and at this time, my studies at the university began. The “game” was never started anymore and was hidden in the jME-projects folder - Until a few days ago.
</p>

<p>
Almost every two days, a new thread in the forum appears, where people talk about “bloxel” worlds, mesh optimization, batching and so on… As the discussions about the <abbr title="Graphical User Interface">GUI</abbr> frameworks (Nifty and its upcoming alternatives) began, I thought: “Why don't you create a block-world-framework, that the people can use easily?” :)
</p>

<p>
I read my old code (mainly the chunk management and the mesh optimizer) again and started to code the named framework from scratch - After a few hours, I made the block world run and after 2 days it seemed to work in the way I like it to work.
</p>

<p>
At the moment, the “block engine” includes all necessary features for a minecraft-like world and even a few useful tools (e.g. loading blocks from heightmaps, noises, …) - Time to publish a first preview. :)
</p>

</div>
<!-- EDIT2 SECTION "The origin" [604-2069] -->
<h2 class="sectionedit3" id="how_it_works">How it works</h2>
<div class="level2">

<p>
The vertex buffers, UV coordinates, chunk management, block faces, … … … … nah, just kidding. :P I think, everyone who knows about this topic, knows how bloxel-engines work. And in case you don't - There are sooo many topics about this in the forum and even articles on the internet… I don't want to explain everything, that was already explained by persons, who can do it much better than me.
</p>

<p>
Nevertheless, here are the basics: Blocks are merged to chunks (e.g. 16x256x16 blocks), so only the according chunks need to be updated when the block is added/removed/whatever. The tricky thing when rendering is to only render the visible faces - If you have a huge mountain of blocks, you only need to render the blocks on the surface. And even in this case, only the faces that point outwards. ;)
The framework does all this for you, no need to worry. You, as user, can just add/remove blocks as you wish without knowing about the chunks, the optimized geometries etc. etc.
</p>

<p>
⇒ You add a block ⇒ You see the block :)
</p>

</div>
<!-- EDIT3 SECTION "How it works" [2070-3122] -->
<h2 class="sectionedit4" id="performance">Performance</h2>
<div class="level2">

<p>
The performance is good I think - In a test case I had a scene with 1.350.000 blocks (in 4x1x4 chunks of the size 16x256x16) and 20 movements of a block per second - The result was 1200 FPS. The average time to generate the optimized geometry for a chunk was 5ms.
</p>

<p>
Of course, there are cases when every face has to be rendered - But even in generated worst cases I never fell under 300-400 FPS, so it <em>should</em> be fine for this stage of development (More about possible improvements later).
</p>

</div>
<!-- EDIT4 SECTION "Performance" [3123-3640] -->
<h2 class="sectionedit5" id="usage">Usage</h2>
<div class="level2">

<p>
Enough boring words about theory - Here's how you use the framework. :) This happens in different parts:
</p>
<ol>
<li class="level1"><div class="li"> <a href="/jme3/contributions/cubes/settings.html" class="wikilink1" title="jme3:contributions:cubes:settings">Settings</a></div>
</li>
<li class="level2"><div class="li"> <a href="/jme3/contributions/cubes/register_your_blocks.html" class="wikilink1" title="jme3:contributions:cubes:register_your_blocks">Register Your Blocks</a></div>
</li>
<li class="level2"><div class="li"> <a href="/jme3/contributions/cubes/build_your_block_world.html" class="wikilink1" title="jme3:contributions:cubes:build_your_block_world">Build Your Block World</a></div>
</li>
</ol>

<p>
After executing these steps, you should come up with an application like the <a href="/jme3/contributions/cubes/basic_example.html" class="wikilink1" title="jme3:contributions:cubes:basic_example">Basic Example</a>.
</p>

</div>
<!-- EDIT5 SECTION "Usage" [3641-4044] -->
<h2 class="sectionedit6" id="screenshots">Screenshots</h2>
<div class="level2">

<p>
Those are just some random screenshots that I made while creating and testing the block engine - They show in a nice way, what you can expect from the framework.
</p>

<p>
<a href="/resources/fetch.php" class="media" title="http://destroflyer.mania-community.de/other/imagehost/cubes/test_physics.png"><img src="/resources/fetch.php" class="media" alt="" width="800" /></a>
</p>

<p>
<a href="/resources/fetch.php" class="media" title="http://destroflyer.mania-community.de/other/imagehost/cubes/etherblocks_third_person.jpg"><img src="/resources/fetch.php" class="media" title="destroflyer.mania-community.de_other_imagehost_cubes_etherblocks_third_person.jpg" alt="destroflyer.mania-community.de_other_imagehost_cubes_etherblocks_third_person.jpg" width="800" /></a>
</p>

<p>
<a href="/resources/fetch.php" class="media" title="http://destroflyer.mania-community.de/other/imagehost/cubes/wireframe_view.png"><img src="/resources/fetch.php" class="media" alt="" width="800" /></a>
</p>

<p>
<a href="/resources/fetch.php" class="media" title="http://destroflyer.mania-community.de/other/imagehost/cubes/test_shapes.png"><img src="/resources/fetch.php" class="media" alt="" width="800" /></a>
</p>

<p>
<a href="/resources/fetch.php" class="media" title="http://destroflyer.mania-community.de/other/imagehost/cubes/scene_mountains.png"><img src="/resources/fetch.php" class="media" alt="" width="800" /></a>
</p>

</div>
<!-- EDIT6 SECTION "Screenshots" [4045-4722] -->
<h2 class="sectionedit7" id="tools">Tools</h2>
<div class="level2">

<p>
The framework offers several tools to play around with your blockworld:
</p>
<ul>
<li class="level1"><div class="li"> <a href="/jme3/contributions/cubes/tools/heightmaps.html" class="wikilink1" title="jme3:contributions:cubes:tools:heightmaps">Heightmaps</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/contributions/cubes/tools/noise.html" class="wikilink1" title="jme3:contributions:cubes:tools:noise">Noise</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/contributions/cubes/tools/picking.html" class="wikilink1" title="jme3:contributions:cubes:tools:picking">Picking</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/contributions/cubes/tools/serialization.html" class="wikilink1" title="jme3:contributions:cubes:tools:serialization">Serialization</a></div>
</li>
</ul>

</div>
<!-- EDIT7 SECTION "Tools" [4723-5009] -->
<h2 class="sectionedit8" id="further_improvements_work-in-progress_things">Further improvements / "Work-In-Progress" things</h2>
<div class="level2">

<p>
The following list contains things, that are <strong>not yet</strong> (!) part of the framework, but are considered as useful. If you have any ideas what's missing or what could be a cool feature, please tell me and (hopefully) it will be on the to-do list. :)
</p>
<ul>
<li class="level1"><div class="li"> <strong>Wiki:</strong> List the included test applications (Tutorial, Heightmap, Noise, Modifications, …)</div>
</li>
<li class="level1"><div class="li"> <strong>Wiki:</strong> List the included test data (Assets, Blocks, …)</div>
</li>
<li class="level1"><div class="li"> <strong>Wiki:</strong> Write the missing instructions for some tools (e.g. how to create custom block shapes)</div>
</li>
<li class="level1"><div class="li"> <strong>BlockTerrain:</strong> Support for dynamic counts of chunks (Automatically add chunks if an out-of-bounds block is added)</div>
</li>
<li class="level1"><div class="li"> <strong>Lights:</strong> Implement a performant way to calculate if a block is affected by a “light block” and modify its texture accordingly</div>
</li>
</ul>

</div>
<!-- EDIT8 SECTION "Further improvements / Work-In-Progress things" [5010-5838] -->
<h2 class="sectionedit9" id="where_is_this_available">Where is this available?</h2>
<div class="level2">

<p>
This framework is available as plugin in the jMonkeyEngine SDK (“Tools” → “Plugins”), so users are able to download and integrate the library easily.
</p>

<p>
Hopefully, this thing will help some of you guys, when it's released - Any ideas, hints and comments on this are appreciated. :)
</p>

</div>
<!-- EDIT9 SECTION "Where is this available?" [5839-] -->
