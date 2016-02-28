---
title: JMonkey Entity System Advanced
---
<h1 class="sectionedit1" id="jmonkey_entity_system_advanced">JMonkey Entity System Advanced</h1>
<div class="level1">

<p>
In this article we explain how the JMonkey Entity System looks like and why.
</p>

<p>
If you are new to this subject please read the <a href="/jme3/contributions/entitysystem/introduction.html" class="wikilink1" title="jme3:contributions:entitysystem:introduction">Entity System Introduction</a> first.
</p>

</div>
<!-- EDIT1 SECTION "JMonkey Entity System Advanced" [1-254] -->
<h1 class="sectionedit2" id="multithreading">Multithreading</h1>
<div class="level1">

<p>
One difference between the JMonkey Entity System and other Entity Systems is that you are allowed to access the system from various threads. This can give your game a huge performance boost because costly task can easily separated in an own thread.
This leads to an unique design of the components and the introduction to Entity Sets.
</p>

</div>
<!-- EDIT2 SECTION "Multithreading" [255-619] -->
<h3 class="sectionedit3" id="entity_sets">Entity Sets</h3>
<div class="level3">

<p>
One part of this special approach are the Entity Sets. Most of the time you want to work with Entities you create an Entity Set and add the class names of the components you are interested in to the constructor.
In the background the Entity Set now creates Entity objects for all entities that contain the passed component classes.
This Entities <strong>only</strong> hold the the components the Set is interested in.
This means different Entity Sets have two different Entity objects for the same entity.
Therefore changes of one entity must be synchronized with the other entity sets.
This works with events created for every change and passed to the other entity sets.
With the method applyChanges() this entity Set will update all of their entities or remove/add new ones.
Besides after this method call you have a direct access to all added,changed and removed entities separately and there is no need to loop through all entities.
</p>

</div>
<!-- EDIT3 SECTION "Entity Sets" [620-1567] -->
<h3 class="sectionedit4" id="components">Components</h3>
<div class="level3">

<p>
Because components have no other methods except the getter, changes are made by replacing the component of an entity with a new one. Therefore an entity can only have one component of the same class. If a component would have a setter no event would fired and parallel processing would not be possible anymore. 
It is important that you only store pure data in the components because otherwise you would no longer know where you can find the logic and the approach of a clear software design would get lost.
</p>

<p>
</p><p></p><div class="noteimportant">
Beginners tend to add large objects like spatials and geometries to a component.
This is a big mistake because such objects contain logic and in our approach components are data only. Abstract it to a general level or store it completely in the systems.
</div>


<p>
</p><p></p><div class="noteimportant">
Never subclass Component classes. 
</div>


</div>
<!-- EDIT4 SECTION "Components" [1568-2437] -->
<h3 class="sectionedit5" id="what_are_systems">What are Systems?</h3>
<div class="level3">

<p>
Simply all objects that use entities/components can be called a system.
For example <a href="/jme3/advanced/application_states.html" class="wikilink1" title="jme3:advanced:application_states">AppStates</a> can deal with different components and can easily be added to the Application.
</p>

<p>
</p><p></p><div class="noteimportant">Never modify the same component from different systems.
</div>
If two systems are modifying the same components then there is a design flaw. 
This is a sign that there is a missing component or system.


</div>
<!-- EDIT5 SECTION "What are Systems?" [2438-2896] -->
<h1 class="sectionedit6" id="the_back_end">The Back End</h1>
<div class="level1">

<p>
There are two different ways of storing the information:
</p>

</div>
<!-- EDIT6 SECTION "The Back End" [2897-2983] -->
<h3 class="sectionedit7" id="hashmaps">Hashmaps</h3>
<div class="level3">

<p>
For every component class a new Hashmap is created which contains the entityId as a key and the component as a value. Therefore if you need to get to know all entities which owns components of a 
certain type the system will search in these Hashmaps for same entityIds.
</p>

</div>
<!-- EDIT7 SECTION "Hashmaps" [2984-3275] -->
<h3 class="sectionedit8" id="sql">SQL</h3>
<div class="level3">

<p>
All information of the components are stored in an SQL Database, this is done via reflection.
Therefore all Components need an empty constructor when they are stored in a database.
Otherwise it is not possible to load the Component.
</p>

<p>
Because SQL librarys can be different this Entity System only concentrate on working with hsqldb.
<a href="http://hsqldb.org/" class="urlextern" title="http://hsqldb.org/" rel="nofollow">http://hsqldb.org/</a>
</p>

</div>
<!-- EDIT8 SECTION "SQL" [3276-3640] -->
<h3 class="sectionedit9" id="hybrid">Hybrid</h3>
<div class="level3">

<p>
Because saving/loading the component objects from a SQL Database is slow this does not work for components who are changed recently. (PositionComponent)
On the other hand checking weather an entity owns a special component ist faster in a SQL database.
To keep both benefits there is the Hybrid approach:
</p>
<ul>
<li class="level1"><div class="li"> Components are put into a Hashmap.</div>
</li>
</ul>
<ul>
<li class="level1"><div class="li"> Persistent Components are stored in the SQL database.</div>
</li>
</ul>

</div>
<!-- EDIT9 SECTION "Hybrid" [3641-4061] -->
<h3 class="sectionedit10" id="id_generation">Id Generation</h3>
<div class="level3">

<p>
Every entity has a unique id which is a long.
Ids are not reused because afterward they would not be unique anymore which would cause a huge penalty.
</p>

<p>
</p><p></p><div class="notetip">
Often people are scared that they would ran out of ids:
If you create a new entity every nano second you would need roughly 585 years before it wraps. 

</div>


</div>
<!-- EDIT10 SECTION "Id Generation" [4062-] -->
