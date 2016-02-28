---
title: Atom framework's Managers
---
<h3 class="sectionedit1" id="atom_framework_s_managers">Atom framework's Managers</h3>
<div class="level3">

<p>
Read about the Manager idea here <a href="/jme3/advanced/atom_framework/atomcore.html" class="wikilink1" title="jme3:advanced:atom_framework:atomcore">atomcore</a>
</p>

<p>
Atom also have a lot of Managers. <strong>Here suggestion for implemented one!</strong>, you can call it a convention because it's not forced on you to gain more flexibility.
</p>

<p>
Manager can has SubManagers, as a List or a Map (Hierarchy or not is not forced)
</p>

<p>
Manager can be extended or Singleton or DefaultInstance (can be getDefault() but not a singleton) here and there. Manager all “attend” in a “cycle” but not “obey”. They can implement ICycle to mark they executor as Obey stricly to the Cycle.
</p>

<p>
you can do Main.getManager(Class) if your Main support it, or doing the long reference getManager().getSubManager().
</p>

<p>
You can see it as a hybrid or “no contract yet” – “not stricted to” way of implementing to get “best of both world” out of:
</p>
<ol>
<li class="level1"><div class="li"> singleton vs default vs linked instance</div>
</li>
<li class="level1"><div class="li"> hierarchy vs flatten component base</div>
</li>
<li class="level1"><div class="li"> cycle attend vs a random routine.</div>
</li>
</ol>

<p>
In this implementation, I also try to have a good balance between flexibility and usefulness, clearance and performance. In the near future, when my framework is proved to be statable and useful, I will release it fully.
</p>

</div>
