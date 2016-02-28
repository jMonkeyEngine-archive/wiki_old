---
title: Picking
---
<h1 class="sectionedit1" id="picking">Picking</h1>
<div class="level1">

<p>
You already found out how to create a world block and modify it from your code. But wouldn't it be nice to have a “click-and-build” functionality? (Minecraft says hello)
</p>

<p>
The framework helps you to get the block location which is e.g. pointed by your mouse - When receiving the coordinates, you can use them to add or remove a block there.
</p>

</div>
<!-- EDIT1 SECTION "Picking" [1-365] -->
<h2 class="sectionedit2" id="blocknavigator">BlockNavigator</h2>
<div class="level2">

<p>
The <code>BlockNavigator</code> class contains various methods to help you navigate through your blockworld without having to trouble with coordinates, type casts or chunks. The method we need for (mouse) picking is this one:
</p>
<pre class="code java"><span class="kw1">public</span> <span class="kw1">static</span> Vector3Int getPointedBlockLocation<span class="br0">(</span>BlockTerrain blockTerrain, Vector3f collisionContactPoint, <span class="kw4">boolean</span> getNeighborLocation<span class="br0">)</span><span class="br0">{</span>
    <span class="co1">//Some mysterious code that returns the location</span>
    <span class="co1">//of the block in the terrain, which is placed</span>
    <span class="co1">//at the specified collisionContactPoint (world coordinates)</span>
    <span class="co1">//If you set getNeighborLocation to true, you can</span>
    <span class="co1">//get the empty block gap, in the direction towards you</span>
    <span class="co1">//(e.g. if you want to add a block to the block you've clicked)</span>
<span class="br0">}</span></pre>

</div>
<!-- EDIT2 SECTION "BlockNavigator" [366-1120] -->
<h2 class="sectionedit3" id="get_the_cursor-pointed_location_raycasting">Get the cursor-pointed location / RayCasting</h2>
<div class="level2">

<p>
So, the above method needs a collisionContactPoint - This is the point you've clicked in your world. Luckily, jMonkeyEngine offers raycasting, which lets you get exactly this point.
</p>

<p>
</p><p></p><div class="noteimportant">I recommend to read the <a href="/jme3/beginner/hello_picking.html" class="wikilink1" title="jme3:beginner:hello_picking">Hello Picking</a> tutorial first, since the rest of this chapter has nothing to do with the “Cubes” framework itself.
</div>


<p>
This is a method I've created while creating a test case for mouse picking in the blockworld - It returns the CollisionResults of the mouse cursor and a specified node: (Generally, this will be the BlockTerrain's node)
</p>
<pre class="code java"><span class="kw1">private</span> CollisionResults getRayCastingResults<span class="br0">(</span>Node node<span class="br0">)</span><span class="br0">{</span>
    Vector3f origin <span class="sy0">=</span> cam.<span class="me1">getWorldCoordinates</span><span class="br0">(</span><span class="kw1">new</span> Vector2f<span class="br0">(</span><span class="br0">(</span>settings.<span class="me1">getWidth</span><span class="br0">(</span><span class="br0">)</span> <span class="sy0">/</span> <span class="nu0">2</span><span class="br0">)</span>, <span class="br0">(</span>settings.<span class="me1">getHeight</span><span class="br0">(</span><span class="br0">)</span> <span class="sy0">/</span> <span class="nu0">2</span><span class="br0">)</span><span class="br0">)</span>, 0.0f<span class="br0">)</span><span class="sy0">;</span>
    Vector3f direction <span class="sy0">=</span> cam.<span class="me1">getWorldCoordinates</span><span class="br0">(</span><span class="kw1">new</span> Vector2f<span class="br0">(</span><span class="br0">(</span>settings.<span class="me1">getWidth</span><span class="br0">(</span><span class="br0">)</span> <span class="sy0">/</span> <span class="nu0">2</span><span class="br0">)</span>, <span class="br0">(</span>settings.<span class="me1">getHeight</span><span class="br0">(</span><span class="br0">)</span> <span class="sy0">/</span> <span class="nu0">2</span><span class="br0">)</span><span class="br0">)</span>, 0.3f<span class="br0">)</span><span class="sy0">;</span>
    direction.<span class="me1">subtractLocal</span><span class="br0">(</span>origin<span class="br0">)</span>.<span class="me1">normalizeLocal</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    Ray ray <span class="sy0">=</span> <span class="kw1">new</span> Ray<span class="br0">(</span>origin, direction<span class="br0">)</span><span class="sy0">;</span>
    CollisionResults results <span class="sy0">=</span> <span class="kw1">new</span> CollisionResults<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    node.<span class="me1">collideWith</span><span class="br0">(</span>ray, results<span class="br0">)</span><span class="sy0">;</span>
    <span class="kw1">return</span> results<span class="sy0">;</span>
<span class="br0">}</span></pre>

<p>
You can use the closest CollisionResult to receive the collisionContactPoint with your BlockTerrain and to finally get the “pointed” block location:
</p>
<pre class="code java"><span class="kw1">private</span> Vector3Int getCurrentPointedBlockLocation<span class="br0">(</span><span class="kw4">boolean</span> getNeighborLocation<span class="br0">)</span><span class="br0">{</span>
    CollisionResults results <span class="sy0">=</span> getRayCastingResults<span class="br0">(</span>terrainNode<span class="br0">)</span><span class="sy0">;</span>
    <span class="kw1">if</span><span class="br0">(</span>results.<span class="me1">size</span><span class="br0">(</span><span class="br0">)</span> <span class="sy0">&gt;</span> <span class="nu0">0</span><span class="br0">)</span><span class="br0">{</span>
        Vector3f collisionContactPoint <span class="sy0">=</span> results.<span class="me1">getClosestCollision</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">getContactPoint</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="kw1">return</span> BlockNavigator.<span class="me1">getPointedBlockLocation</span><span class="br0">(</span>blockTerrain, collisionContactPoint, getNeighborLocation<span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
    <span class="kw1">return</span> <span class="kw2">null</span><span class="sy0">;</span>
<span class="br0">}</span></pre>

<p>
Time to sum up: You can now get the current block location that you point with your mouse at any time you want. :)
</p>

</div>
<!-- EDIT3 SECTION "Get the cursor-pointed location / RayCasting" [1121-2993] -->
<h2 class="sectionedit4" id="woah_-_let_s_build_minecraft">Woah - Let's build Minecraft!</h2>
<div class="level2">

<p>
One nice example would be to register a mouse-listener (See <a href="/jme3/beginner/hello_input_system.html" class="wikilink1" title="jme3:beginner:hello_input_system">Hello Input</a>) and to execute the following code when the user clicks:
</p>
<pre class="code java"><span class="co1">//Get the free block gap, to which the user is loooking...</span>
Vector3Int blockLocation <span class="sy0">=</span> getCurrentPointedBlockLocation<span class="br0">(</span><span class="kw2">true</span><span class="br0">)</span><span class="sy0">;</span>
<span class="co1">//(The block location is null, if the user looks in the sky or out of the map)</span>
<span class="kw1">if</span><span class="br0">(</span>blockLocation <span class="sy0">!=</span> <span class="kw2">null</span><span class="br0">)</span><span class="br0">{</span>
    <span class="co1">//... and place a block there :)</span>
    blockTerrain.<span class="me1">setBlock</span><span class="br0">(</span>blockLocation, CubesTestAssets.<span class="me1">BLOCK_WOOD</span><span class="br0">)</span><span class="sy0">;</span>
<span class="br0">}</span></pre>

<p>
And that's it - You just created your own minecraft-like blockworld-editor. Give yourself a challenge and implement the other mouse button to remove the pointed block (Look out for the <code>getNeighborLocation</code> parameter).
</p>

<p>
<a href="/resources/fetch.php" class="media" title="http://destroflyer.mania-community.de/other/imagehost/cubes/test_picking.png"><img src="/resources/fetch.php" class="media" alt="" width="800" /></a>
</p>

</div>
<!-- EDIT4 SECTION "Woah - Let's build Minecraft!" [2994-3877] -->
<h2 class="sectionedit5" id="further_improvements">Further improvements</h2>
<div class="level2">
<ul>
<li class="level1"><div class="li"> Create different types of interactions between player and block (Open a door, turn a switch, destroy a block, …) and a way to define own interactions</div>
</li>
</ul>

</div>
<!-- EDIT5 SECTION "Further improvements" [3878-] -->
