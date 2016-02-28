---
title: ES Design goals explained
---
<h2 class="sectionedit1" id="es_design_goals_explained">ES Design goals explained</h2>
<div class="level2">

<p>
This page revive and explain more about points of design goals and implementations for an ES and its usefulness (means features) to corporate with other Java and game software techs and layers.
</p>

<p>
Theoricaly an Java ES done right should be:
</p>
<ol>
<li class="level1"><div class="li"> Pure data : very debatable</div>
<ol>
<li class="level2"><div class="li"> Mutable : as bean with setter and getter</div>
</li>
<li class="level2"><div class="li"> Immutate : as bean with getter, should be replace if changed.</div>
</li>
</ol>
</li>
<li class="level1"><div class="li"> Multi-threading, concurency enable : very debatable</div>
<ol>
<li class="level2"><div class="li"> As my experience, pure data or not is not clear contract to multi-threading success. Consider other things happen outside of ES scope, so it not an solid waranty that those component will not be touched by any other thread.</div>
</li>
<li class="level2"><div class="li"> Also if there is a contract that no other thread touching those data, in Java style via synchonization or other paradigm like actor… multi-threading also consider success but just more complicated!</div>
</li>
</ol>
</li>
<li class="level1"><div class="li"> Communication: very debatable</div>
<ol>
<li class="level2"><div class="li"> Event messaging enable</div>
</li>
<li class="level2"><div class="li"> No event or messaging : update beat, no need of inter-com or events. How can we do network messaging?</div>
</li>
</ol>
</li>
<li class="level1"><div class="li"> Is database (and other kind of persistent) friendly</div>
<ol>
<li class="level2"><div class="li"> Save to XML (file, serialized)?</div>
</li>
<li class="level2"><div class="li"> Send over network?</div>
</li>
<li class="level2"><div class="li"> Change sets are resembling Databse concept, what about tranactions?</div>
</li>
</ol>
</li>
<li class="level1"><div class="li"> Is enterprise friendly (expanable/ extensible/ modulizable)</div>
<ol>
<li class="level2"><div class="li"> Spring, as lazy loaded, injected?</div>
</li>
</ol>
</li>
<li class="level1"><div class="li"> Script possibilities</div>
<ol>
<li class="level2"><div class="li"> Can be script, non trivial work in pure data!</div>
</li>
<li class="level2"><div class="li"> Can be use with other JVM language than java like groovy, or scala, jython?</div>
</li>
</ol>
</li>
<li class="level1"><div class="li"> Restrictions and limitation</div>
<ol>
<li class="level2"><div class="li"> No dynamic Java object methods in Component ? What about Entities and Systems ( Processors)</div>
</li>
<li class="level2"><div class="li"> An overal way to manage and config Systems, freely chose? How to hook to its routine?</div>
</li>
</ol>
</li>
<li class="level1"><div class="li"> Depedencies</div>
<ol>
<li class="level2"><div class="li"> The separation of components are clear, as no dependencies at all. Hard cored, scripted or injected will break the overal contract!</div>
</li>
<li class="level2"><div class="li"> The separation of Entities. What about depedencies of entities? Ex: parent/ child relationship in JME spatial. How the framework handle that?</div>
</li>
<li class="level2"><div class="li"> The separation of Systems. Ex: any contract about that?</div>
</li>
</ol>
</li>
</ol>

</div>
<div class="level3">

</div>
