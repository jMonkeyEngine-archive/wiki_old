---
title: EntitySets
---
<h1 class="sectionedit1" id="entitysets">EntitySets</h1>
<div class="level1">

</div>
<!-- EDIT1 SECTION "EntitySets" [1-26] -->
<h1 class="sectionedit2" id="introduction">Introduction</h1>
<div class="level1">

<p>
One difference between Zay-ES and other Entity Systems is that you are allowed to access the system from various threads. This can give your game a huge performance boost because costly tasks can easily be separated out into their own thread.
This leads to a unique design of the components and the introduction to Entity Sets.
</p>

</div>
<!-- EDIT2 SECTION "Introduction" [27-383] -->
<h1 class="sectionedit3" id="why_entitysets">Why EntitySets?</h1>
<div class="level1">

<p>
One huge benefit of Zay-ES is that you are able to create a separate class for each job.
This leads to clean code and you always know which class is responsible for bugs.
For example you can have a class for Collision, Movement, Enemies, PlayerInput,….
All of these classes are only interested in entities which have special components.
</p>

</div>
<!-- EDIT3 SECTION "Why EntitySets?" [384-754] -->
<h1 class="sectionedit4" id="how_to_use_them">How to use them</h1>
<div class="level1">

</div>
<!-- EDIT4 SECTION "How to use them" [755-785] -->
<h2 class="sectionedit5" id="create_an_entityset">Create an EntitySet</h2>
<div class="level2">
<pre class="code java"><span class="co1">//This set is interested in entities with a TestComponent</span>
EntitySet entitySet <span class="sy0">=</span> entityData.<span class="me1">getEntities</span><span class="br0">(</span>TestComponent.<span class="kw1">class</span><span class="br0">)</span><span class="sy0">;</span></pre>

</div>
<!-- EDIT5 SECTION "Create an EntitySet" [786-962] -->
<h2 class="sectionedit6" id="update_an_entityset">Update an EntitySet</h2>
<div class="level2">
<pre class="code java"> <span class="co1">//Apply all new changes to the EntitySet and return false if nothing changed</span>
<span class="kw1">if</span><span class="br0">(</span>entitySet.<span class="me1">applyChanges</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span>
<span class="br0">{</span>
    entitySet.<span class="me1">getAddedEntities</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    entitySet.<span class="me1">getChangedEntities</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    entitySet.<span class="me1">getRemovedEntities</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>        
<span class="br0">}</span></pre>

</div>
<!-- EDIT6 SECTION "Update an EntitySet" [963-] -->
