---
title: JMonkey Entity System Usage
---
<h1 class="sectionedit1" id="jmonkey_entity_system_usage">JMonkey Entity System Usage</h1>
<div class="level1">

</div>
<!-- EDIT1 SECTION "JMonkey Entity System Usage" [1-41] -->
<h3 class="sectionedit2" id="initialize_the_entity_system">Initialize the Entity System</h3>
<div class="level3">
<pre class="code java">EntitySystem entitySystem <span class="sy0">=</span> <span class="kw1">new</span> EntitySystem<span class="br0">(</span><span class="kw1">new</span> DefaultEntityData<span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span></pre>

</div>
<!-- EDIT2 SECTION "Initialize the Entity System" [42-170] -->
<h3 class="sectionedit3" id="writing_an_own_component">Writing an own Component</h3>
<div class="level3">
<pre class="code java"><span class="kw1">public</span> <span class="kw1">class</span> MovementComponent <span class="kw1">extends</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+component"><span class="kw3">Component</span></a> <span class="br0">{</span>
 
    <span class="kw1">private</span> Vector3f movement<span class="sy0">;</span>
 
    <span class="kw1">public</span> MovementComponent<span class="br0">(</span>Vector3f movement<span class="br0">)</span>
    <span class="br0">{</span>
        <span class="kw1">this</span>.<span class="me1">movement</span><span class="sy0">=</span>movement<span class="sy0">;</span>
    <span class="br0">}</span>
 
    <span class="kw1">public</span> Vector3f getMovement<span class="br0">(</span><span class="br0">)</span>
    <span class="br0">{</span>
        <span class="kw1">return</span> movement<span class="sy0">;</span>
    <span class="br0">}</span>
<span class="br0">}</span></pre>

</div>
<!-- EDIT3 SECTION "Writing an own Component" [171-483] -->
<h3 class="sectionedit4" id="adding_a_new_entity">Adding a new Entity</h3>
<div class="level3">
<pre class="code java"><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+component"><span class="kw3">Component</span></a><span class="br0">[</span><span class="br0">]</span> components <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+component"><span class="kw3">Component</span></a><span class="br0">[</span><span class="nu0">6</span><span class="br0">]</span><span class="sy0">;</span>
 
components<span class="br0">[</span><span class="nu0">0</span><span class="br0">]</span> <span class="sy0">=</span> <span class="kw1">new</span> VisualRepComponent<span class="br0">(</span><span class="st0">"Models/HoverTank/Tank2.mesh.xml"</span><span class="br0">)</span><span class="sy0">;</span>     
components<span class="br0">[</span><span class="nu0">1</span><span class="br0">]</span> <span class="sy0">=</span> <span class="kw1">new</span> PositionComponent<span class="br0">(</span>v3f,<span class="kw1">new</span> Quaternion<span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
components<span class="br0">[</span><span class="nu0">2</span><span class="br0">]</span> <span class="sy0">=</span> <span class="kw1">new</span> MovementComponent<span class="br0">(</span>Vector3f.<span class="me1">ZERO</span><span class="br0">)</span><span class="sy0">;</span>
components<span class="br0">[</span><span class="nu0">3</span><span class="br0">]</span> <span class="sy0">=</span> <span class="kw1">new</span> InSceneComponent<span class="br0">(</span><span class="kw2">true</span><span class="br0">)</span><span class="sy0">;</span>
components<span class="br0">[</span><span class="nu0">4</span><span class="br0">]</span> <span class="sy0">=</span> <span class="kw1">new</span> PlayerComponent<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
components<span class="br0">[</span><span class="nu0">5</span><span class="br0">]</span> <span class="sy0">=</span> <span class="kw1">new</span> CollisionComponent<span class="br0">(</span><span class="nu0">5</span><span class="br0">)</span><span class="sy0">;</span>
 
entitySystem.<span class="me1">newEntity</span><span class="br0">(</span>components<span class="br0">)</span><span class="sy0">;</span></pre>

</div>
<!-- EDIT4 SECTION "Adding a new Entity" [484-943] -->
<h3 class="sectionedit5" id="creating_a_new_entityset">Creating a new EntitySet</h3>
<div class="level3">
<pre class="code java"><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+entity"><span class="kw3">Entity</span></a> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+set"><span class="kw3">Set</span></a> entitySet <span class="sy0">=</span> entitySystem.<span class="me1">getEntitySet</span><span class="br0">(</span>MovementComponent.<span class="kw1">class</span>, PositionComponent.<span class="kw1">class</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
For the single parts of your programm who deal with special components it is recommended to use <a href="/jme3/advanced/application_states.html" class="wikilink1" title="jme3:advanced:application_states">AppStates</a>.
</p>

</div>
<!-- EDIT5 SECTION "Creating a new EntitySet" [944-1242] -->
<h3 class="sectionedit6" id="loop_through_all_entities">Loop through all entities</h3>
<div class="level3">
<pre class="code java">entitySet.<span class="me1">applyChanges</span><span class="br0">(</span><span class="br0">)</span>
 
Iterator<span class="sy0">&lt;</span>Entity<span class="sy0">&gt;</span> iterator <span class="sy0">=</span> entitySet.<span class="me1">getIterator</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
<span class="kw1">while</span> <span class="br0">(</span>iterator.<span class="me1">hasNext</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
      <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+entity"><span class="kw3">Entity</span></a> entity <span class="sy0">=</span> iterator.<span class="me1">next</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
	<span class="co1">//do something</span>
<span class="br0">}</span></pre>

</div>
<!-- EDIT6 SECTION "Loop through all entities" [1243-1462] -->
<h3 class="sectionedit7" id="only_get_changed_entities">Only get changed Entities</h3>
<div class="level3">
<pre class="code java"><span class="kw1">if</span><span class="br0">(</span>entitySet.<span class="me1">applyChanges</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span>
<span class="br0">{</span>
 	entitySet.<span class="me1">getAddedEntities</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">//Get the Set of new added entities</span>
        entitySet.<span class="me1">getChangedEntities</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">//Get the Set of changed entities</span>
        entitySet.<span class="me1">getRemovedEntities</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">//Get the Set of removed entities</span>
<span class="br0">}</span></pre>

</div>
<!-- EDIT7 SECTION "Only get changed Entities" [1463-1766] -->
<h3 class="sectionedit8" id="update_a_component">Update a component</h3>
<div class="level3">
<pre class="code java">entity.<span class="me1">setComponent</span><span class="br0">(</span><span class="kw1">new</span> PositionComponent<span class="br0">(</span><span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span></pre>

</div>
<!-- EDIT8 SECTION "Update a component" [1767-1874] -->
<h3 class="sectionedit9" id="destroy_an_entity">Destroy an entity</h3>
<div class="level3">
<pre class="code java">entity.<span class="me1">destroy</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span></pre>

</div>
<!-- EDIT9 SECTION "Destroy an entity" [1875-1939] -->
<h3 class="sectionedit10" id="how_to_display_spatials_if_it_not_allowed_to_save_them_into_the_components">How to display Spatials if it not allowed to save them into the components?</h3>
<div class="level3">

<p>
Use an EntityControl class which is able to display Entitys with visual components.
In an AppState with a Map containing Entities and and EntitiyControls they can be merged together and updated.
</p>

<p>
Have a look at the example:
<a href="http://peeeq.de/uploads/ogerlord/EntityTest.rar" class="urlextern" title="http://peeeq.de/uploads/ogerlord/EntityTest.rar" rel="nofollow">http://peeeq.de/uploads/ogerlord/EntityTest.rar</a>
</p>

</div>
<!-- EDIT10 SECTION "How to display Spatials if it not allowed to save them into the components?" [1940-] -->
