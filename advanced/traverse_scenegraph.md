---
title: Traverse the SceneGraph
---
<h1 class="sectionedit1" id="traverse_the_scenegraph">Traverse the SceneGraph</h1>
<div class="level1">

<p>
You can run a search across the whole scene graph and search for individual Spatials (<code>Nodes</code> and <code>Geometry</code>s) by custom criteria, such as the Spatial's name, or the Spatial's class, or the Spatial's user data, or Spatial's Controls. You do this when you want modify  the found nodes (move them, call a method, etc) but you don't have a local variable for them.
</p>

</div>
<!-- EDIT1 SECTION "Traverse the SceneGraph" [1-406] -->
<h2 class="sectionedit2" id="example_use_cases">Example Use Cases</h2>
<div class="level2">

<p>
<strong>Example 1:</strong>
</p>
<ol>
<li class="level1"><div class="li"> You have created a procedural scene with lots of dynamically generated elements.</div>
</li>
<li class="level1"><div class="li"> You want to find individual Spatials under ever-changing conditions and modify their state. </div>
</li>
</ol>

<p>
<strong>Example 2:</strong>
</p>
<ol>
<li class="level1"><div class="li"> You created a mostly static scene in the jMonkeyEngine SDK and exported it as .j3o file. <br />
The scene also contains interactive objects, for example a particle emitter, spatials with user data, or spatials with custom controls. </div>
</li>
<li class="level1"><div class="li"> You load the .j3o scene using the assetManager. </div>
</li>
<li class="level1"><div class="li"> You want to interact with one of the loaded interactive scene elements in your Java code. <br />
For example, you want to call <code>emitAllParticles()</code> on the particle emitter. Or you want to find all NPC's Geometries with a custom CivilianControl, and call the CivilianControl method that makes them start acting their role.</div>
</li>
</ol>

<p>
In this case, you can use a SceneGraphVisitorAdapter to identify and access the Spatials in question.
</p>

</div>
<!-- EDIT2 SECTION "Example Use Cases" [407-1364] -->
<h2 class="sectionedit3" id="code_sample">Code Sample</h2>
<div class="level2">

<p>
For each search, you create a <code>com.jme3.scene.SceneGraphVisitorAdapter</code> that defines your search criteria and what you want to do with the found Spatials. Then you call the <code>depthFirstTraversal(visitor)</code> or <code>breadthFirstTraversal(visitor)</code> method of the Spatial (e.g. the rootNode, or better, a subnode) to start the search.
</p>
<pre class="code java">SceneGraphVisitor visitor <span class="sy0">=</span> <span class="kw1">new</span> SceneGraphVisitor<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
 
  @Override
  <span class="kw1">public</span> <span class="kw4">void</span> visit<span class="br0">(</span>Spatial spat<span class="br0">)</span> <span class="br0">{</span>
    <span class="co1">// search criterion can be control class:</span>
    MyControl control <span class="sy0">=</span> spatial.<span class="me1">getControl</span><span class="br0">(</span>MyControl.<span class="kw1">class</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="kw1">if</span> <span class="br0">(</span>control <span class="sy0">!=</span> <span class="kw2">null</span><span class="br0">)</span> <span class="br0">{</span>
      <span class="co1">// you have access to any method, e.g. name.</span>
      <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+system"><span class="kw3">System</span></a>.<span class="me1">out</span>.<span class="me1">println</span><span class="br0">(</span><span class="st0">"Instance of "</span> <span class="sy0">+</span> control.<span class="me1">getClass</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">getName</span><span class="br0">(</span><span class="br0">)</span> 
                       <span class="sy0">+</span> <span class="st0">" found for "</span> <span class="sy0">+</span> spatial.<span class="me1">getName</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
  <span class="br0">}</span>
 
<span class="br0">}</span><span class="sy0">;</span>
 
<span class="co1">// Now scan the tree either depth first...</span>
rootNode.<span class="me1">depthFirstTraversal</span><span class="br0">(</span>visitor<span class="br0">)</span><span class="sy0">;</span>
<span class="co1">// ... or scan it breadth first.</span>
rootNode.<span class="me1">breadthFirstTraversal</span><span class="br0">(</span>visitor<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
Which of the two methods is faster depends on how you designed the scengraph, and what tree element you are looking for. If you are searching for one single Geometry that is a “leaf” of the tree, and then stop searching, depth-first may be faster. If you search for a high-level grouping Node, breadth-first may be faster. 
</p>

<p>
The choice of depth- vs breadth-first also influences the order in which found elements are returned (children first or parents first). If you want to modify user data that is inherited from the parent node (e.g. transformations), the order of application is important, because the side-effects add up.
</p>

<p>
You can use the SceneGraphVisitorAdapter class to scan separately for Geometry and Nodes.
</p>

</div>
<!-- EDIT3 SECTION "Code Sample" [1365-3055] -->
<h2 class="sectionedit4" id="see_also">See Also</h2>
<div class="level2">
<ul>
<li class="level1"><div class="li"> <a href="/jme3/the_scene_graph.html" class="wikilink1" title="jme3:the_scene_graph">The Scene Graph</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/advanced/spatial.html" class="wikilink1" title="jme3:advanced:spatial">Spatial</a></div>
</li>
</ul>
<div class="tags"><span>
	<a href="/tag/spatial.html" class="wikilink1" title="tag:spatial" rel="tag">spatial</a>,
	<a href="/tag/node.html" class="wikilink1" title="tag:node" rel="tag">node</a>,
	<a href="/tag/mesh.html" class="wikilink1" title="tag:mesh" rel="tag">mesh</a>,
	<a href="/tag/geometry.html" class="wikilink1" title="tag:geometry" rel="tag">geometry</a>,
	<a href="/tag/scenegraph.html" class="wikilink1" title="tag:scenegraph" rel="tag">scenegraph</a>
</span></div>

</div>
<!-- EDIT4 SECTION "See Also" [3056-] -->
