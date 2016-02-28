---
title: Level of Detail (LOD) Optimization
---
<h1 class="sectionedit1" id="level_of_detail_lod_optimization">Level of Detail (LOD) Optimization</h1>
<div class="level1">

<p>
A mesh with a high level of detail has lots of polygons and looks good close up. But when the mesh is further away (and the detail is not visible), the high-polygon count slows down performance unnecessarily. 
</p>

<p>
One solution for this problem is to use high-detail meshes for objects close to the camera, and low-detail meshes for objects far from the camera. As the player moves through the scene, you must keep replacing close objects by more detailed meshes, and far objects by less detailed meshes. The goal is to keep few high-quality slow-rendering objects in the foreground, and many low-quality fast-rendering objects in the background. (Experienced users can compare this approach to <a href="/jme3/advanced/terrain.html" class="wikilink1" title="jme3:advanced:terrain">JME's TerraMonkey terrain system</a>, which internally uses the specialized GeoMipMapping algorithm to generate a terrain's Levels of Detail.)
</p>

<p>
You see now why you may want to be able to generate Levels of Detail for complex Geometries automatically. JME3 supports a Java implementation of the Ogre engine's LOD generator (originally by Péter Szücs and Stan Melax): You use <a href="https://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/tools/jme3tools/optimize/LodGenerator.java" class="urlextern" title="https://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/tools/jme3tools/optimize/LodGenerator.java" rel="nofollow">jme3tools.optimize.LodGenerator</a> in conjunction with <a href="https://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/core/com/jme3/scene/control/LodControl.java" class="urlextern" title="https://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/core/com/jme3/scene/control/LodControl.java" rel="nofollow">com.jme3.scene.control.LodControl</a>. 
</p>

<p>
For a demo, run <a href="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/stress/TestLodGeneration.java" class="urlextern" title="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/stress/TestLodGeneration.java" rel="nofollow">TestLodGeneration.java</a> from <a href="/sdk/sample_code.html" class="wikilink1" title="sdk:sample_code">JmeTests</a>, then press +/- and spacebar to experiment. The following screenshots show a monkey model with three reduced Levels of Detail: 
<a href="/resources/jme3-advanced-jmonkey-lod.gif" class="media" title="jme3:advanced:jmonkey-lod.gif"><img src="/resources/jme3-advanced-jmonkey-lod.gif" class="mediacenter" alt="" /></a>
</p>

</div>
<!-- EDIT1 SECTION "Level of Detail (LOD) Optimization" [1-1821] -->
<h2 class="sectionedit2" id="usage">Usage</h2>
<div class="level2">

<p>
To activate this optimization:
</p>
<ol>
<li class="level1"><div class="li"> Pick a reduction method and values for the Geometry. (Trial and error…)</div>
</li>
<li class="level1"><div class="li"> Generate LODs for the Geometry, either in the SDK or in code.</div>
</li>
<li class="level1"><div class="li"> Add an LOD control to the Geometry.</div>
</li>
</ol>

</div>
<!-- EDIT2 SECTION "Usage" [1822-2056] -->
<h2 class="sectionedit3" id="pick_reduction_methods_and_values">Pick Reduction Methods and Values</h2>
<div class="level2">

<p>
There are several reduction methods to generate a low-polygon version from a high-polygon model. Don't worry, the reduction does not modify the original model.
</p>
<div class="table sectionedit4"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0">Reduction Method</th><th class="col1">Description</th><th class="col2">Reduction Value</th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0">LodGenerator.TriangleReductionMethod.COLLAPSE_COST</td><td class="col1">Collapses polygon vertices from the mesh until the reduction cost (= amount of ugly artifacts caused) exceeds the given threshold.</td><td class="col2">0.0f - 1.0f</td>
	</tr>
	<tr class="row2">
		<td class="col0">LodGenerator.TriangleReductionMethod.PROPORTIONAL</td><td class="col1">Removes the given percentage of polygons from the mesh.</td><td class="col2"> 0.0f - 1.0f </td>
	</tr>
	<tr class="row3">
		<td class="col0">LodGenerator.TriangleReductionMethod.CONSTANT</td><td class="col1">Removes the given number of polygons from the mesh.</td><td class="col2"> integer </td>
	</tr>
</table></div>
<!-- EDIT4 TABLE [2262-2738] -->
<p>
If you don't know which to choose, experiment. For example start by trying COLLAPSE_COST and .5f-.9f.
</p>

</div>
<!-- EDIT3 SECTION "Pick Reduction Methods and Values" [2057-2841] -->
<h2 class="sectionedit5" id="generate_lod">Generate LOD</h2>
<div class="level2">

<p>
You must generate and cache several LODs for each mesh, ranging from many to few polygons. The LOD generator algorithm attempts to collaps vertices automatically, while avoiding ugly artifacts. The LOD generator doesn't generate new meshes, it only creates separate reduced index buffers for the more highly reduced levels.
</p>
<ul>
<li class="level1"><div class="li"> If you create geometries manually (3D models), use the SDK to generate LODs. </div>
</li>
<li class="level1"><div class="li"> If you create geometries programmatically, generate LODs from your Java code.</div>
</li>
</ul>

</div>
<!-- EDIT5 SECTION "Generate LOD" [2842-3360] -->
<h3 class="sectionedit6" id="generating_lods_in_the_sdk">Generating LODs in the SDK</h3>
<div class="level3">

<p>
The SDK contains a user-friendly interface to generate LODs for a model (.j3o file).
</p>
<ol>
<li class="level1"><div class="li"> Open the Projects or Files window.</div>
</li>
<li class="level1"><div class="li"> Select the .j3o file in the Project Assets &gt; Models directory.</div>
</li>
<li class="level1"><div class="li"> Choose Window&gt;SceneExplorer if the SceneExplorer is not open. Info about the selected model is now displayed in the SceneExplorer.</div>
</li>
<li class="level1"><div class="li"> Right-click the model in SceneExplorer. Choose the “Tools &gt; Generate Levels of Detail” menu. <br />
<a href="/resources/jme3-advanced-jme-sdk-generate-lod-menu.png" class="media" title="jme3:advanced:jme-sdk-generate-lod-menu.png"><img src="/resources/jme3-advanced-jme-sdk-generate-lod-menu.png" class="media" title="The &quot;Tools&gt;Generate LOD&quot; context menu in the SceneExplorer" alt="The &quot;Tools&gt;Generate LOD&quot; context menu in the SceneExplorer" width="300" height="180" /></a></div>
</li>
<li class="level1"><div class="li"> The “Generate LOD” settings wizard opens: <br />
 <a href="/resources/jme3-advanced-jme-sdk-generate-lod-window.png" class="media" title="jme3:advanced:jme-sdk-generate-lod-window.png"><img src="/resources/jme3-advanced-jme-sdk-generate-lod-window.png" class="media" title="The &quot;Generate LOD&quot; settings wizard" alt="The &quot;Generate LOD&quot; settings wizard" width="300" height="150" /></a></div>
</li>
<li class="level1"><div class="li"> Choose a reduction method and reduction values for one or more levels. <br />
Tip: Enter higher reduction values for higher levels. </div>
</li>
<li class="level1"><div class="li"> Click Finish to generate the LODs for this model.</div>
</li>
</ol>

<p>
The LODs are saved in the .j3o model file.
</p>

<p>
</p><p></p><div class="notetip">Choose Window&gt;Properties if the Properties window is not open. Choose the generated LODs from the dropdown in the Properties window, and verify their quality in the SceneComposer.
</div>


<p>
<a href="/resources/jme3-advanced-jme-sdk-generate-lod-full.png" class="media" title="jme3:advanced:jme-sdk-generate-lod-full.png"><img src="/resources/jme3-advanced-jme-sdk-generate-lod-full.png" class="mediacenter" alt="" /></a>
</p>

</div>
<!-- EDIT6 SECTION "Generating LODs in the SDK" [3361-4570] -->
<h3 class="sectionedit7" id="generating_lods_in_code">Generating LODs in Code</h3>
<div class="level3">

<p>
The <code>jme3tools.optimize.LodGenerator</code> utility class helps you generate LODs for an arbitrary mesh (a Geometry object) programmatically from your Java code. You create and bake one LodGenerator for each Geometry. 
</p>
<pre class="code java">LodGenerator lod <span class="sy0">=</span> <span class="kw1">new</span> LodGenerator<span class="br0">(</span>geometry<span class="br0">)</span><span class="sy0">;</span>
lod.<span class="me1">bakeLods</span><span class="br0">(</span>reductionMethod,reductionValue<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
The LODs are stored inside the Geometry object. 
</p>

<p>
<strong>Example:</strong> How to generate an LOD of myPrettyGeo's mesh with 50% fewer polygons:
</p>
<pre class="code java">LodGenerator lod <span class="sy0">=</span> <span class="kw1">new</span> LodGenerator<span class="br0">(</span>myPrettyGeo<span class="br0">)</span><span class="sy0">;</span>
lod.<span class="me1">bakeLods</span><span class="br0">(</span>LodGenerator.<span class="me1">TriangleReductionMethod</span>.<span class="me1">PROPORTIONAL</span>,0.5f<span class="br0">)</span><span class="sy0">;</span></pre>

</div>
<!-- EDIT7 SECTION "Generating LODs in Code" [4571-5204] -->
<h2 class="sectionedit8" id="activate_the_lod_control">Activate the LOD Control</h2>
<div class="level2">

<p>
After generating the LODs for the geometry, you create and add a <code>com.jme3.scene.control.LodControl</code> to the geometry. Adding the LodControl activates the LOD optimizaton for this geometry. 
</p>
<pre class="code java">LodControl lc <span class="sy0">=</span> <span class="kw1">new</span> LodControl<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
myPrettyGeo.<span class="me1">addControl</span><span class="br0">(</span>lc<span class="br0">)</span><span class="sy0">;</span>
rootNode.<span class="me1">attachChild</span><span class="br0">(</span>myPrettyGeo<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
The LodControl internally gets the camera from the game's viewport to calculate the distance to this geometry. Depending on the distance, the LodControl selects an appropriate level of detail, and passes more (or less) detailed vertex data to the renderer. 
</p>

</div>
<!-- EDIT8 SECTION "Activate the LOD Control" [5205-5808] -->
<h2 class="sectionedit9" id="impact_on_quality_and_speed">Impact on Quality and Speed</h2>
<div class="level2">
<div class="table sectionedit10"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0">Level number</th><th class="col1">Purpose</th><th class="col2">Distance</th><th class="col3">Rendering Speed</th><th class="col4">Rendering Quality</th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0">“Level 0”</td><td class="col1">The original mesh is used automatically for close-ups, and it's the default if no LODs have been generated.</td><td class="col2">Closest</td><td class="col3">Slowest.</td><td class="col4">Best.</td>
	</tr>
	<tr class="row2">
		<td class="col0">“Level 1” <br />
“Level 2” <br />
“Level 3” <br />
…</td><td class="col1">If you generated LODs, JME3 uses them automatically as soon as the object moves into the background.</td><td class="col2">The higher the level, <br />
the further away.</td><td class="col3">The higher the level, <br />
the faster.</td><td class="col4">The higher the level, <br />
the lower the quality.</td>
	</tr>
</table></div>
<!-- EDIT10 TABLE [5848-6330] -->
</div>
<!-- EDIT9 SECTION "Impact on Quality and Speed" [5809-6330] -->
<h2 class="sectionedit11" id="see_also">See also</h2>
<div class="level2">
<ul>
<li class="level1"><div class="li"> <a href="http://hub.jmonkeyengine.org/forum/topic/brand-new-lod-generator/" class="urlextern" title="http://hub.jmonkeyengine.org/forum/topic/brand-new-lod-generator/" rel="nofollow">http://hub.jmonkeyengine.org/forum/topic/brand-new-lod-generator/</a></div>
</li>
<li class="level1"><div class="li"> <a href="https://github.com/worldforge/ember/tree/master/src/components/ogre/lod" class="urlextern" title="https://github.com/worldforge/ember/tree/master/src/components/ogre/lod" rel="nofollow">https://github.com/worldforge/ember/tree/master/src/components/ogre/lod</a></div>
</li>
<li class="level1"><div class="li"> <a href="http://www.melax.com/polychop" class="urlextern" title="http://www.melax.com/polychop" rel="nofollow">http://www.melax.com/polychop</a></div>
</li>
<li class="level1"><div class="li"> <a href="http://sajty.elementfx.com/progressivemesh/GSoC2012.pdf" class="urlextern" title="http://sajty.elementfx.com/progressivemesh/GSoC2012.pdf" rel="nofollow">http://sajty.elementfx.com/progressivemesh/GSoC2012.pdf</a> </div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/advanced/terrain.html" class="wikilink1" title="jme3:advanced:terrain">JME3 TerraMonkey Terrain</a></div>
</li>
</ul>

</div>
<!-- EDIT11 SECTION "See also" [6331-] -->
