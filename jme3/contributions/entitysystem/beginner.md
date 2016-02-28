---
title: Zay-ES Beginner Tutorial
---
<h1 class="sectionedit1" id="zay-es_beginner_tutorial">Zay-ES Beginner Tutorial</h1>
<div class="level1">

<p>
In this article we explain the first steps how to work with Zay-ES and what you should know about the background.
</p>

<p>
If you are new Entity Systems please read the <a href="/jme3/contributions/entitysystem/introduction.html" class="wikilink1" title="jme3:contributions:entitysystem:introduction">Entity System Introduction</a> first.
</p>

</div>
<!-- EDIT1 SECTION "Zay-ES Beginner Tutorial" [1-287] -->
<h3 class="sectionedit2" id="sample_code">Sample Code</h3>
<div class="level3">
<pre class="code java"><span class="kw1">import</span> <span class="co2">com.simsilica.es.Entity</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.simsilica.es.EntityData</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.simsilica.es.EntityId</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.simsilica.es.base.DefaultEntityData</span><span class="sy0">;</span>
 
<span class="kw1">public</span> <span class="kw1">class</span> Main <span class="br0">{</span>
 
    <span class="kw1">public</span> <span class="kw1">static</span> <span class="kw4">void</span> main<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a><span class="br0">[</span><span class="br0">]</span> args<span class="br0">)</span> <span class="br0">{</span>
 
        <span class="co1">//Creating the EntityData</span>
        EntityData entityData <span class="sy0">=</span> <span class="kw1">new</span> DefaultEntityData<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
 
        <span class="co1">//Creates a new EntityId, the id is handled as an object to prevent botching</span>
        EntityId entityId <span class="sy0">=</span> entityData.<span class="me1">createEntity</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="co1">//A new TestComponent is added to the Entity</span>
        entityData.<span class="me1">setComponent</span><span class="br0">(</span>entityId, <span class="kw1">new</span> TestComponent<span class="br0">(</span><span class="st0">"Hello World"</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
 
        <span class="co1">//Get a new Entity Object with TestComponents</span>
        <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+entity"><span class="kw3">Entity</span></a> entity <span class="sy0">=</span> entityData.<span class="me1">getEntity</span><span class="br0">(</span>entityId, TestComponent.<span class="kw1">class</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="co1">//Get the Component and display the value</span>
        TestComponent testComponent <span class="sy0">=</span> entity.<span class="me1">get</span><span class="br0">(</span>TestComponent.<span class="kw1">class</span><span class="br0">)</span><span class="sy0">;</span>
        <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+system"><span class="kw3">System</span></a>.<span class="me1">out</span>.<span class="me1">println</span><span class="br0">(</span>testComponent.<span class="me1">getValue</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
 
        <span class="co1">//Overwrite the existing component</span>
        entity.<span class="me1">set</span><span class="br0">(</span><span class="kw1">new</span> TestComponent<span class="br0">(</span><span class="st0">"New Value"</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
        <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+system"><span class="kw3">System</span></a>.<span class="me1">out</span>.<span class="me1">println</span><span class="br0">(</span>testComponent.<span class="me1">getValue</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
 
        <span class="co1">//Remove the Entity from the data</span>
        entityData.<span class="me1">removeEntity</span><span class="br0">(</span>entity.<span class="me1">getId</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
<span class="br0">}</span></pre>

</div>
<!-- EDIT2 SECTION "Sample Code" [288-1483] -->
<h2 class="sectionedit3" id="description_of_the_sample">Description of the sample</h2>
<div class="level2">

</div>
<!-- EDIT3 SECTION "Description of the sample" [1484-1521] -->
<h3 class="sectionedit4" id="create_a_component_class">Create a Component Class</h3>
<div class="level3">

<p>
You simply create a component by implementing the EntityComponent interface:
</p>
<pre class="code java"><span class="kw1">public</span> <span class="kw1">class</span> TestComponent <span class="kw1">implements</span> EntityComponent <span class="br0">{</span>
 
    <span class="kw1">private</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> value<span class="sy0">;</span>
 
    <span class="kw1">public</span> TestComponent<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> value<span class="br0">)</span>
    <span class="br0">{</span>
        <span class="kw1">this</span>.<span class="me1">value</span><span class="sy0">=</span>value<span class="sy0">;</span>
    <span class="br0">}</span>
 
    <span class="kw1">public</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> getValue<span class="br0">(</span><span class="br0">)</span>
    <span class="br0">{</span>
        <span class="kw1">return</span> value<span class="sy0">;</span>
    <span class="br0">}</span>
<span class="br0">}</span></pre>

<p>
But there are some rules you must consider:
Components only have a constructor and getter.
It is important that you only store pure data in the components because otherwise you would no longer know where you can find the logic and the approach of a clear software design would get lost.
Besides an entity can only have one component of the same class.
</p><p></p><div class="noteimportant">
Beginners tend to add large objects like spatials and geometries to a component.
This is a big mistake because such objects contain logic and in our approach components are data only. Abstract it to a general level or store it completely in the systems.
</div>


<p>
</p><p></p><div class="noteimportant">
Never subclass Component classes. 
</div>


</div>
<!-- EDIT4 SECTION "Create a Component Class" [1522-2582] -->
<h3 class="sectionedit5" id="initialize_the_entity_system">Initialize the Entity System</h3>
<div class="level3">
<pre class="code java"> EntityData entityData <span class="sy0">=</span> <span class="kw1">new</span> DefaultEntityData<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
The EntityData is the main class of the entity system.  All the data are stored here.
</p>

<p>
How the entityData works:
</p>

<p>
For every component class a new Hashmap is created which contains the entityId as a key and the component as a value. Therefore, if you need to know all entities which own a component of a certain type, the system will search in these Hashmaps for the required entityIds.
</p>

</div>
<!-- EDIT5 SECTION "Initialize the Entity System" [2583-3079] -->
<h3 class="sectionedit6" id="creating_entitys_and_adding_components">Creating Entitys and adding Components</h3>
<div class="level3">
<pre class="code java"><span class="co1">//Creates a new EntityId, the id is handled as an object to prevent botching</span>
EntityId entityId <span class="sy0">=</span> entityData.<span class="me1">createEntity</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
<span class="co1">//A new TestComponent is added to the Entity</span>
entityData.<span class="me1">setComponent</span><span class="br0">(</span>entityId, <span class="kw1">new</span> TestComponent<span class="br0">(</span><span class="st0">"Hello World"</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
EntityIds are a objects which contain a long value. Zay-ES uses this objects to prevent users from writing dirty code.
</p>

<p>
Every entity has a unique id which is a long.
Ids are not reused because, if they were, they would not be unique anymore, which would cause a huge penalty.
</p>

<p>
</p><p></p><div class="notetip">
Often people are scared that they will run out of ids:
If you create a new entity every nano second, you would need roughly 585 years before it wraps. 

</div>


</div>
<!-- EDIT6 SECTION "Creating Entitys and adding Components" [3080-3833] -->
<h3 class="sectionedit7" id="the_entity_class">The Entity Class</h3>
<div class="level3">
<pre class="code java"><span class="co1">//Get a new Entity Object with TestComponents</span>
<a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+entity"><span class="kw3">Entity</span></a> entity <span class="sy0">=</span> entityData.<span class="me1">getEntity</span><span class="br0">(</span>entityId, TestComponent.<span class="kw1">class</span><span class="br0">)</span><span class="sy0">;</span>
<span class="co1">//Get the Component and display the value</span>
TestComponent testComponent <span class="sy0">=</span> entity.<span class="me1">get</span><span class="br0">(</span>TestComponent.<span class="kw1">class</span><span class="br0">)</span><span class="sy0">;</span>
<a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+system"><span class="kw3">System</span></a>.<span class="me1">out</span>.<span class="me1">println</span><span class="br0">(</span>testComponent.<span class="me1">getValue</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
If you want to work with entities, the EntityData is able to create Entity objects. This objects contains
all the Components of the classes you are interested in. In this example it is only the TestComponent.class.
You can have multiple Entity objects for the same entity.
</p>

<p>
</p><p></p><div class="noteimportant">The data of this Entity objects will not be updated if other classes change the components for this entity
</div>


</div>
<!-- EDIT7 SECTION "The Entity Class" [3834-4558] -->
<h3 class="sectionedit8" id="replacing_a_component">Replacing a component</h3>
<div class="level3">
<pre class="code java"><span class="co1">//Overwrite the existing component</span>
entity.<span class="me1">set</span><span class="br0">(</span><span class="kw1">new</span> TestComponent<span class="br0">(</span><span class="st0">"New Value"</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
<a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+system"><span class="kw3">System</span></a>.<span class="me1">out</span>.<span class="me1">println</span><span class="br0">(</span>testComponent.<span class="me1">getValue</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span></pre>

</div>
<!-- EDIT8 SECTION "Replacing a component" [4559-4735] -->
<h3 class="sectionedit9" id="delete_an_entity">Delete an entity</h3>
<div class="level3">
<pre class="code java"><span class="co1">//Remove the Entity from the data</span>
entityData.<span class="me1">removeEntity</span><span class="br0">(</span>entity.<span class="me1">getId</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span></pre>

</div>
<!-- EDIT9 SECTION "Delete an entity" [4736-4858] -->
<h2 class="sectionedit10" id="entity_sets">Entity Sets</h2>
<div class="level2">

<p>
The most important feature of Zay-ES are the Entity Sets.
It is strongly recommended that you read the <a href="/jme3/contributions/entitysystem/entityset.html" class="wikilink1" title="jme3:contributions:entitysystem:entityset">Entity Set tutorial</a> after reading this article.
</p>

<p>
</p><p></p><div class="noteimportant">Read the <a href="/jme3/contributions/entitysystem/entityset.html" class="wikilink1" title="jme3:contributions:entitysystem:entityset">tutorial</a> about entity sets
</div>


</div>
<!-- EDIT10 SECTION "Entity Sets" [4859-] -->
