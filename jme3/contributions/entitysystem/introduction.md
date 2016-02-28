---
title: Entity System Introduction
---
<h1 class="sectionedit1" id="entity_system_introduction">Entity System Introduction</h1>
<div class="level1">

<p>
Every experienced programer knows that planning a huge project is difficult.
You need to know exactly what you want your program to do and which
things should be possible to add later.
If you do not do this you get unclean code, lose the clear view over the project
and have to rewrite large parts again.
Because game development is a dynamic process, sometimes it can be difficult to 
decide in which direction the game will develop)
(Maybe you already compared alpha screenshots of a game with the final result)
</p>

</div>
<div class="level2">

<p>
<a href="/resources/fetch.php" class="media" title="http://media.moddb.com/images/articles/1/116/115301/auto/shjWa.png"><img src="/resources/fetch.php" class="mediacenter" alt="" /></a>
In this example we suddenly want a new unit, an armored robot.
This is not possible with our structure and therefore we would need to rewrite the code.
At this point, the idea for an Entity System starts.
</p>

</div>
<!-- EDIT1 SECTION "Entity System Introduction" [1-841] -->
<h1 class="sectionedit2" id="entity_system">Entity System</h1>
<div class="level1">

<p>
There are various concepts for Entity Systems and they all have some differences.
In this article we concentrate on the way the jMonkey Entity System works.
</p>

</div>
<!-- EDIT2 SECTION "Entity System" [842-1027] -->
<h3 class="sectionedit3" id="entity">Entity</h3>
<div class="level3">

<p>
An Entity is simply an unique Id. 
Every Unit, Item, Bullet, etc. in your game will be represented by one of these entity Ids.
</p>

</div>
<!-- EDIT3 SECTION "Entity" [1028-1172] -->
<h3 class="sectionedit4" id="component">Component</h3>
<div class="level3">

<p>
A Component is a class which only contains data.
This means it has a constructor and <strong>only</strong> getter methods.
Examples for Components can be:
</p>

</div>
<div class="level2">
<ul>
<li class="level1"><div class="li"> PositionComponent</div>
</li>
<li class="level1"><div class="li"> MovementComponent</div>
</li>
<li class="level1"><div class="li"> CollsisionComponent</div>
</li>
</ul>

<p>
Components are added to the Entities.
</p><p></p><div class="noteimportant"> At any particular time, there can be only one component of the same class for one entity.
</div>


<p>
As you can see Entities are flexibly made up of different Components.
You need your Armored Robot? No Problem, you only need to combine the right components.
Besides, you are able to remove/change/add components during the game which is a huge benefit of Entity Systems.
</p>

<p>
<a href="/resources/fetch.php" class="media" title="http://media.moddb.com/images/articles/1/116/115301/auto/0WoEb.png"><img src="/resources/fetch.php" class="mediacenter" alt="" /></a>
</p>

</div>
<!-- EDIT4 SECTION "Component" [1173-1909] -->
<h3 class="sectionedit5" id="systems">Systems</h3>
<div class="level3">

<p>
Simply put, any classes other than the components and the entities can be considered as systems.
You need to pay attention when you read about other Entity Systems
because they can have different ideas of what a system is.
</p>

<p>
In the systems, you can request all Entities which have special components.
For example you can say that you want all entities who have a position and a movement component,
and then calculate the new position for these Entities by overwriting the old position component with a new one.
</p>

<p>
This leads automatically to many classes that only perform a single task, like the movement.
As a result the project becomes clear and in case of bugs, you directly know which class is responsible for these components.
</p>

<p>
For a more detailed and technical view, have a look at the <a href="/jme3/contributions/entitysystem/advanced.html" class="wikilink1" title="jme3:contributions:entitysystem:advanced">Entity System Advanced</a> article
</p>

</div>
<!-- EDIT5 SECTION "Systems" [1910-2795] -->
<h3 class="sectionedit6" id="pros_and_cons">Pros and Cons</h3>
<div class="level3">

<p>
Pro:
</p>
<ul>
<li class="level1"><div class="li"> good overview</div>
</li>
<li class="level1"><div class="li"> flexibility</div>
</li>
<li class="level1"><div class="li"> modularity</div>
</li>
</ul>

<p>
Con:
</p>
<ul>
<li class="level1"><div class="li"> performance</div>
</li>
<li class="level1"><div class="li"> unfamiliar</div>
</li>
<li class="level1"><div class="li"> a bit risky</div>
</li>
</ul>

<p>
As mentioned above, the System has many benefits.  Now lets focus on the cons:
The performance is slightly slower because you have more classes and more calculations are needed in the background.
This point is not so significant anymore because computers are becoming faster and faster.
A more critical point is that, until now, only a few projects have employed entity systems. One example of a project which uses a similar Entity System is the adventure Mythruna.
<a href="http://mythruna.com/" class="urlextern" title="http://mythruna.com/" rel="nofollow">http://mythruna.com/</a>
</p>

<p>
Some say that it is not guaranteed that the Entity System will always work in practice.  This may be true depending on the projects structure.  Therefore project structure and layout is an important consideration when using an entity system.
</p>

</div>
<!-- EDIT6 SECTION "Pros and Cons" [2796-3658] -->
<h3 class="sectionedit7" id="difficulty">Difficulty</h3>
<div class="level3">

<p>
It can be hard to adapt to the style of Entity System Programming if you are used to OOP.
Therefore you need to pay attention that you in no way mix both styles together.
Like other software architectures, you lose all benefits if you are not consistent.
</p>

</div>
<!-- EDIT7 SECTION "Difficulty" [3659-3936] -->
<h3 class="sectionedit8" id="should_i_use_an_entity_system">Should I use an Entity System?</h3>
<div class="level3">

</div>
<div class="level2">
<ul>
<li class="level1"><div class="li"> Make sure that you want to take the risk of using a very new concept</div>
</li>
<li class="level1"><div class="li"> It is better if you have good programming experience</div>
</li>
<li class="level1"><div class="li"> An entity system can make it easier to add new content as your game project grows.</div>
</li>
<li class="level1"><div class="li"> Entity Systems are recommended for MMOs, but can be used for practically any game project.</div>
</li>
</ul>

</div>
<!-- EDIT8 SECTION "Should I use an Entity System?" [3937-4297] -->
<h3 class="sectionedit9" id="sources">Sources:</h3>
<div class="level3">

</div>
<div class="level2">
<ul>
<li class="level1"><div class="li"> <a href="http://www.indiedb.com/games/attack-of-the-gelatinous-blob/news/the-entity-system" class="urlextern" title="http://www.indiedb.com/games/attack-of-the-gelatinous-blob/news/the-entity-system" rel="nofollow">http://www.indiedb.com/games/attack-of-the-gelatinous-blob/news/the-entity-system</a></div>
</li>
<li class="level1"><div class="li"> <a href="http://t-machine.org/index.php/2007/09/03/entity-systems-are-the-future-of-mmog-development-part-1/" class="urlextern" title="http://t-machine.org/index.php/2007/09/03/entity-systems-are-the-future-of-mmog-development-part-1/" rel="nofollow">http://t-machine.org/index.php/2007/09/03/entity-systems-are-the-future-of-mmog-development-part-1/</a></div>
</li>
</ul>

</div>
<!-- EDIT9 SECTION "Sources:" [4298-] -->
