---
title: Multithreading Bullet Physics in jme3
---
<h1 class="sectionedit1" id="multithreading_bullet_physics_in_jme3">Multithreading Bullet Physics in jme3</h1>
<div class="level1">

</div>
<!-- EDIT1 SECTION "Multithreading Bullet Physics in jme3" [1-53] -->
<h2 class="sectionedit2" id="introduction">Introduction</h2>
<div class="level2">

<p>
Since bullet is not (yet) multithreaded or GPU accelerated, the jME3 implementation allows to run each physics space on a separate thread that is executed in parallel to rendering.
</p>

</div>
<!-- EDIT2 SECTION "Introduction" [54-261] -->
<h2 class="sectionedit3" id="how_is_it_handled_in_jme3_and_bullet">How is it handled in jme3 and bullet?</h2>
<div class="level2">

<p>
A SimpleApplication with a BulletAppState allows setting the threading type via 
</p>
<pre class="code">setThreadingType(ThreadingType type);</pre>

<p>
 where ThreadingType can be either SEQUENTIAL or PARALLEL. By default, it's SEQUENTIAL.
</p>

<p>
You can activate PARALLEL threading in the simpleInitApp() method:
</p>
<pre class="code java">bulletAppState <span class="sy0">=</span> <span class="kw1">new</span> BulletAppState<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
bulletAppState.<span class="me1">setThreadingType</span><span class="br0">(</span>BulletAppState.<span class="me1">ThreadingType</span>.<span class="me1">PARALLEL</span><span class="br0">)</span><span class="sy0">;</span>
stateManager.<span class="me1">attach</span><span class="br0">(</span>bulletAppState<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
Now the physics update happens in parallel to render(), that is, after the user's changes in the update() call have been applied. During update() the physics update loop pauses. This way the loop logic is still maintained: the user can set and change values in physics and scenegraph objects before render() and physicsUpdate() are called in parallel. This allows you to use physics methods in update() as if it was single-threaded.
</p>
<div class="table sectionedit4"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0">PARALLEL</th><th class="col1">SEQUENTIAL</th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0">1. update(), 2. render() and physics update().</td><td class="col1 leftalign">1. update(), 2. render(), 3. physics update().  </td>
	</tr>
	<tr class="row2">
		<td class="col0">Physics Debug View is rendered inaccurately (out of sync)</td><td class="col1">Physics Debug View is rendered accurately.</td>
	</tr>
</table></div>
<!-- EDIT4 TABLE [1202-1424] -->
<p>
</p><p></p><div class="notetip">You can add more physics spaces by using multiple PARALLEL bulletAppStates. You would do that if you have sets physical objects that never collide (for example, underground bolders and flying cannon balls above ground), so you put those into separate physics spaces, which improves performances (less collisions to check!). 
</div>

<div class="tags"><span>
	<a href="/tag/documentation.html" class="wikilink1" title="tag:documentation" rel="tag">documentation</a>,
	<a href="/tag/physics.html" class="wikilink1" title="tag:physics" rel="tag">physics</a>,
	<a href="/tag/threading.html" class="wikilink1" title="tag:threading" rel="tag">threading</a>
</span></div>

</div>
<!-- EDIT3 SECTION "How is it handled in jme3 and bullet?" [262-] -->
