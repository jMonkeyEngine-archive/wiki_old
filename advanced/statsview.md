---
title: Optimizing Your Game Using Statistics
---
<h1 class="sectionedit1" id="optimizing_your_game_using_statistics">Optimizing Your Game Using Statistics</h1>
<div class="level1">

<p>
When you create a SimpleApplication, you see the default StatsView and FpsView in the left corner. 
The StatsView displays object statistics that are used during development, for example for debugging and optimization.
Below the StatsView is the FpsView that displays the frames that jMonkeyEngine can render per second. 
</p>

<p>
The main use case of these statistics is to find out why the application may be running slow and where to start fixing the performance.
</p>

<p>
The StatsView + FpsView look like this example:
</p>
<pre class="code">FrameBuffers (M) = 2
FrameBuffers (F) = 2
FrameBuffers (S) = 2
Textures (M) = 7 
Textures (F) = 3 
Textures (S) = 3
Shaders (M) = 6
Shaders (F) = 3
Shaders (S) = 4
Objects = 24
Uniforms = 31
Triangles = 582
Vertices = 1148
Frames per Second: 30</pre>

</div>
<!-- EDIT1 SECTION "Optimizing Your Game Using Statistics" [1-823] -->
<h2 class="sectionedit2" id="on_off">On/Off</h2>
<div class="level2">

<p>
You switch the StatsView on an off in the simpleInitApp() method by setting a boolean:
</p>
<pre class="code java">setDisplayFps<span class="br0">(</span><span class="kw2">false</span><span class="br0">)</span><span class="sy0">;</span>       <span class="co1">// to hide the FPS</span>
setDisplayStatView<span class="br0">(</span><span class="kw2">false</span><span class="br0">)</span><span class="sy0">;</span>  <span class="co1">// to hide the statistics </span></pre>

</div>
<!-- EDIT2 SECTION "On/Off" [824-1054] -->
<h2 class="sectionedit3" id="terminology">Terminology</h2>
<div class="level2">

<p>
Types of items counted:
</p>
<ul>
<li class="level1"><div class="li"> FrameBuffers: Total number of rendering surfaces used for off-screen rendering and render-to-texture functionality. </div>
</li>
<li class="level1"><div class="li"> Textures: Total number of distinct textures used in the scene.</div>
</li>
<li class="level1"><div class="li"> Shaders: Total number of shaders used for effects (shading, blur, lighting, glow, etc).</div>
</li>
<li class="level1"><div class="li"> Objects: Total number of objects in the OpenGL pipeline. That is, objects attached to the rootNode and guiNode, etc.</div>
</li>
<li class="level1"><div class="li"> Uniforms: Total number of shader uniforms. Uniforms are predefined variables used as parameters in shader calculations, containing data such as matrices, vectors, time, and colors.</div>
</li>
<li class="level1"><div class="li"> Triangles: Total number of triangles (faces) of the meshes of all objects.</div>
</li>
<li class="level1"><div class="li"> Vertices: Total number of vertices (corner points) of the meshes of all the objects.</div>
</li>
</ul>

<p>
Types of statistics:
</p>
<ul>
<li class="level1"><div class="li"> <strong>(M) = Memory</strong> – Number of items currently in OpenGL memory.</div>
</li>
<li class="level1"><div class="li"> <strong>(F) = Frame </strong> – Number of items used by current frame (visible).</div>
</li>
<li class="level1"><div class="li"> <strong>(S) = Switches</strong> – Number of items that were state switched in the last frame.</div>
</li>
</ul>

<p>
The StatsView does not include any Physics statistics.
</p>

</div>
<!-- EDIT3 SECTION "Terminology" [1055-2163] -->
<h2 class="sectionedit4" id="how_to_interpret_the_fps_when_optimizing">How to Interpret the FPS when Optimizing</h2>
<div class="level2">

<p>
The FPS (frames per second) shows you how fast jME runs the update loop. If the FPS values goes below 30, the game slows down and runs jerky, which makes the game either frustrating or impossible to play. You need either decrease the number of operations in the update loop, or decrease memory usage (object count). 
</p>

<p>
If your application grows more and more sluggish, deactivate or decrease one feature set at a time: Deactivate drop shadows, physics, anti-aliasing… Try fewer light sources, fewer NPCs, fewer samples in spheres (i.e. less smooth spheres). Temporarily replace the scene (or parts of it) with a simpler test scene to check whether the scene has to many triangles, etc. 
</p>

<p>
Keep an eye on FPS and the StatsView and find out which element has the biggest impact on performance. This is where you start optimizing.
</p>

</div>
<!-- EDIT4 SECTION "How to Interpret the FPS when Optimizing" [2164-3046] -->
<h2 class="sectionedit5" id="how_to_interpret_the_statistics">How to Interpret The Statistics</h2>
<div class="level2">

<p>
</p><p></p><div class="noteimportant">To interpret the numbers correctly, consider that the 14 lines of text themselves already count as 14 objects with 914 vertices. You need to subtract these values from the totals for smaller performance experiments.
</div>


<p>
What do you want to avoid?
</p>
<ol>
<li class="level1"><div class="li"> FrameBuffers: If you don't use any post-processing effects (FilterPostProcessor), this count should be zero. The more effects you use, the more FrameBuffers are in use. If this value is high while others are normal, and your game is sluggish, you can speed up the application by using fewer post-processing effects.</div>
</li>
<li class="level1"><div class="li"> The Object Count (Batch Count) is a very important value that indicates how many geometries were rendered in the last frame. In general, if you keep the object count around 100-200, your game will be fast and responsive. If the count is permanently higher, hand-code rules that detach remote objects, or optimize a complex multi-material scene using: <code>GeometryBatchFactory.optimize(complexNode, true);</code> or a <a href="/jme3/advanced/texture_atlas.html" class="wikilink1" title="jme3:advanced:texture_atlas">Texture Atlas</a>.</div>
</li>
<li class="level1"><div class="li"> Triangle Counts. If your game is sluggish and triangle (polygon) count is high, then you are rendering too many, too detailed meshes. Tell your graphic designers to create models with lower polygon counts, or use a <a href="/jme3/advanced/level_of_detail.html" class="wikilink1" title="jme3:advanced:level_of_detail">Level of Detail</a> (LOD) optimization. The limit is around 100'000 vertices for a scene, considering that the slowest currently used graphic cards cannot handle anything beyond that. </div>
</li>
<li class="level1"><div class="li"> Are any counts constantly increasing right before the game slows down or runs out of memory? Check whether you are accidentally adding objects in a loop, instead of only once.</div>
</li>
<li class="level1"><div class="li"> Verify that the numbers are plausible. If you think you generated a test scene out of “a few boxes”, but the StatsView shows ten thousands of triangles, then you probably have extra objects out of sight somewhere (due to barely visible materials, overlapping with other objects, scaled too big or too small to see, etc). </div>
<ul>
<li class="level2"><div class="li"> Example: In a test scene made up of boxes, you'd expect a vertex:triangle:object ratio of 8:12:1. </div>
</li>
<li class="level2"><div class="li"> Terrains, models and spheres have higher counts, depending on their size and <a href="/jme3/advanced/level_of_detail.html" class="wikilink1" title="jme3:advanced:level_of_detail">Level of Detail</a> (LOD). A high-poly model looks pretty in Blender, but you must find a lower-poly, low-LOD compromise if you want several large objects in one scene!</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> If S (objects being switched) are high compared to F (objects used), then you use or generate too many different Materials (etc). You are unnecessarily forcing jME to re-load and re-bind objects (= Switches), which is bad for performance. Also if you have many transparent materials in your scene, this results in more switches, and you should use fewer transparent materials.</div>
</li>
<li class="level1"><div class="li"> If the M values (objects in memory) are high compared to F (objects used), that means a lot more GL objects are kept in memory than are actually used. This can happen in large scenes with many materials. Consider breaking the scene up and detaching objects while they are out of sight, so the built-in culling can optimize the scene.</div>
</li>
</ol>

<p>
What goal are you trying to achieve in general?
</p>
<ol>
<li class="level1"><div class="li"> The values for (M) and (F) should be within the same order of magnitude. This means your code only loads objects that it actually needs, and that the hardware can actually handle.</div>
</li>
<li class="level1"><div class="li"> It's okay if Switches (S) are lower than Used in Current Frame (F).</div>
</li>
<li class="level1"><div class="li"> The FPS should be 30 or more on the slowest hardware that you target.</div>
</li>
<li class="level1"><div class="li"> 10'000-50'000 vertices is a typical average value for a scene.</div>
</li>
</ol>
<hr />

<p>
See also:
</p>
<ul>
<li class="level1"><div class="li"> <a href="http://hub.jmonkeyengine.org/forum/topic/good-triangles-count/" class="urlextern" title="http://hub.jmonkeyengine.org/forum/topic/good-triangles-count/" rel="nofollow">What's a good triangle count?</a> Forum discussion</div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/advanced/level_of_detail.html" class="wikilink1" title="jme3:advanced:level_of_detail">Level of Detail</a></div>
</li>
</ul>

</div>
<!-- EDIT5 SECTION "How to Interpret The Statistics" [3047-] -->
