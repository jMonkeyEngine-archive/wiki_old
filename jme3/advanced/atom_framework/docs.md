---
title: Atom Framework Documentations
---
<h2 class="sectionedit1" id="atom_framework_documentations">Atom Framework Documentations</h2>
<div class="level2">

<p>
Welcome this is the main entrance of Atom framework documentation. Here you will find all the resource you need to start developing with Atom framework. First take a look at the structure of the documentation.
</p>

</div>
<!-- EDIT1 SECTION "Atom Framework Documentations" [1-252] -->
<h3 class="sectionedit2" id="structure_of_the_documentations">Structure of the Documentations</h3>
<div class="level3">
<ol>
<li class="level1"><div class="li"> Architecture Design</div>
</li>
<li class="level1"><div class="li"> General docs</div>
<ol>
<li class="level2"><div class="li"> Setup</div>
</li>
<li class="level2"><div class="li"> Coding and project structure convention</div>
</li>
<li class="level2"><div class="li"> Usages of SDK</div>
</li>
</ol>
</li>
<li class="level1"><div class="li"> Component's docs</div>
<ol>
<li class="level2"><div class="li"> AtomCore</div>
</li>
<li class="level2"><div class="li"> AtomEx</div>
</li>
<li class="level2"><div class="li"> AtomSDK</div>
</li>
<li class="level2"><div class="li"> TeeHee .. others</div>
</li>
</ol>
</li>
</ol>

</div>
<!-- EDIT2 SECTION "Structure of the Documentations" [253-497] -->
<h2 class="sectionedit3" id="download_and_setup">Download and Setup</h2>
<div class="level2">

<p>
<a href="/jme3/advanced/atom_framework/docs/setup.html" class="wikilink1" title="jme3:advanced:atom_framework:docs:setup">Download and Setup instructions</a>
</p>

</div>
<!-- EDIT3 SECTION "Download and Setup" [498-604] -->
<h2 class="sectionedit4" id="design_documentation">Design documentation</h2>
<div class="level2">

<p>
Design &amp; Architecture documentation page: 
<a href="/jme3/advanced/atom_framework/design.html" class="wikilink1" title="jme3:advanced:atom_framework:design">design</a>
</p>

</div>
<!-- EDIT4 SECTION "Design documentation" [605-720] -->
<h2 class="sectionedit5" id="the_code">The Code</h2>
<div class="level2">

<p>
</p><p></p><div class="noteimportant">Make sure that you've read and understanded Atom's Design part
</div>


</div>
<!-- EDIT5 SECTION "The Code" [721-827] -->
<h3 class="sectionedit6" id="programming_aspects">Programming aspects</h3>
<div class="level3">
<ul>
<li class="level1"><div class="li"> Java</div>
</li>
<li class="level1"><div class="li"> Groovy</div>
</li>
<li class="level1"><div class="li"> XML</div>
</li>
</ul>

</div>
<!-- EDIT6 SECTION "Programming aspects" [828-885] -->
<h3 class="sectionedit7" id="polygot_programming">Polygot programming</h3>
<div class="level3">

<p>
AtomCore (pure Java) supports:
</p>
<ul>
<li class="level1"><div class="li"> Functional reactive programming</div>
</li>
<li class="level1"><div class="li"> Flow based programming</div>
</li>
<li class="level1"><div class="li"> Component based programming</div>
</li>
<li class="level1"><div class="li"> Composite based programming</div>
</li>
<li class="level1"><div class="li"> Data-driven &amp; Model-driven &amp; Domain-driven</div>
</li>
</ul>

<p>
Because AtomScripting and others use Groovy, so it inherit (a lot of) polygot capacity from Groovy.
</p>

<p>
Read: <a href="http://groovy.codehaus.org/Polyglot+Programming+with+Groovy" class="urlextern" title="http://groovy.codehaus.org/Polyglot+Programming+with+Groovy" rel="nofollow">http://groovy.codehaus.org/Polyglot+Programming+with+Groovy</a>
</p>

</div>
<!-- EDIT7 SECTION "Polygot programming" [886-1290] -->
<h3 class="sectionedit8" id="how_can_i_structure_my_code">How can I structure my code?</h3>
<div class="level3">
<pre class="code">How can I structure my code in Atom framework and in JME3 games. What is the best practices, some patterns, pros cons and caveat?</pre>

<p>
<a href="http://hub.jmonkeyengine.org/forum/topic/how-to-structure-the-game-code/" class="urlextern" title="http://hub.jmonkeyengine.org/forum/topic/how-to-structure-the-game-code/" rel="nofollow">http://hub.jmonkeyengine.org/forum/topic/how-to-structure-the-game-code/</a>
</p>

<p>
More detailed, <a href="/jme3/advanced/atom_framework/docs/code/structure.html" class="wikilink1" title="jme3:advanced:atom_framework:docs:code:structure">Code structure explained</a>
</p>

<p>
You can also find a better examples here in my game examples:
<a href="/jme3/atomixtuts.html" class="wikilink1" title="jme3:atomixtuts"> Atomix's tutorials games</a>
</p>

</div>
<!-- EDIT8 SECTION "How can I structure my code?" [1291-1740] -->
<h3 class="sectionedit9" id="code_generation">Code generation</h3>
<div class="level3">

<p>
<a href="http://en.wikipedia.org/wiki/Code_generation_%28compiler%29" class="urlextern" title="http://en.wikipedia.org/wiki/Code_generation_%28compiler%29" rel="nofollow">http://en.wikipedia.org/wiki/Code_generation_%28compiler%29</a>
</p>

<p>
Atom support code generation from multiple sources and to various targets to help speed up and unite production pipeline. <a href="/jme3/advanced/atom_framework/codegen.html" class="wikilink1" title="jme3:advanced:atom_framework:codegen">CodeGen</a> - Ultimate tools for code genration corporate with <a href="/jme3/advanced/atom_framework/atomexasset.html" class="wikilink1" title="jme3:advanced:atom_framework:atomexasset">AtomExAsset</a> - Ultimate tools for game assets management is 2 facilities in charge for the job.
</p>

</div>

<h5 id="sources">Sources</h5>
<div class="level5">
<ul>
<li class="level1"><div class="li"> UML</div>
</li>
<li class="level1"><div class="li"> ECore</div>
</li>
<li class="level1"><div class="li"> Java code or Java classes with annotations</div>
</li>
<li class="level1"><div class="li"> Code gen diagrams (modified UML diagrams for games)</div>
</li>
<li class="level1"><div class="li"> 3D Model and assets</div>
</li>
</ul>

</div>

<h5 id="targets">Targets</h5>
<div class="level5">
<ul>
<li class="level1"><div class="li"> Other Model format - via ECore, UML</div>
</li>
<li class="level1"><div class="li"> Groovy or Java - via ECore, UML, ANTLR</div>
</li>
<li class="level1"><div class="li"> Java bytecode - via instrument and transformation ASM</div>
</li>
<li class="level1"><div class="li"> JavaScript - via GWT, ANTLR (supervisor translation)</div>
</li>
<li class="level1"><div class="li"> StringTemplate, XML, Text, Configurations … and other textbased - via StringTemplate</div>
</li>
<li class="level1"><div class="li"> Assetpack and other kind of assets - via processing pipeline</div>
</li>
</ul>

</div>
<!-- EDIT9 SECTION "Code generation" [1741-2715] -->
<h3 class="sectionedit10" id="more_coding_convention">More coding convention</h3>
<div class="level3">

</div>
<!-- EDIT10 SECTION "More coding convention" [2716-2749] -->
<h3 class="sectionedit11" id="configurations">Configurations</h3>
<div class="level3">

<p>
Atom support configs based in Apache Commons Configurations:
<a href="http://commons.apache.org/proper/commons-configuration/" class="urlextern" title="http://commons.apache.org/proper/commons-configuration/" rel="nofollow">http://commons.apache.org/proper/commons-configuration/</a>
</p>

<p>
Apache Commons Configurations supported configuration format:
</p>
<ul>
<li class="level1"><div class="li"> Properties </div>
</li>
<li class="level1"><div class="li"> XML</div>
</li>
<li class="level1"><div class="li"> JMX</div>
</li>
</ul>

<p>
Additionally Atom support configuration via:
</p>
<ul>
<li class="level1"><div class="li"> Java Annotations </div>
</li>
<li class="level1"><div class="li"> GroovyConfigs</div>
</li>
</ul>

</div>
<!-- EDIT11 SECTION "Configurations" [2750-3073] -->
<h3 class="sectionedit12" id="scripting">Scripting</h3>
<div class="level3">

<p>
Default scripting language of Atom framework is Groovy. 
</p>

<p>
Some optional groovy facilities are also included (gpars, ASM, ANTLR…) 
</p>

<p>
</p><p></p><div class="noteimportant">But note that AtomCore is not depend in Groovy.
</div>


<p>
You can also do scripting in other Java scripting frameworks like BeanScript or JavaScript.
</p>

<p>
Scripting leverage game programming a lot. You can stay inside the running game and make changes into the game enviroment (is just one small advantage aside of other super cool features!). So read about how to do scripting here:
</p>

<p>
<a href="http://hub.jmonkeyengine.org/wiki/doku.php/jme3:advanced:atom_framework:atomscripting" class="urlextern" title="http://hub.jmonkeyengine.org/wiki/doku.php/jme3:advanced:atom_framework:atomscripting" rel="nofollow">http://hub.jmonkeyengine.org/wiki/doku.php/jme3:advanced:atom_framework:atomscripting</a>
</p>

<p>
<a href="http://hub.jmonkeyengine.org/wiki/doku.php/jme3:scripting" class="urlextern" title="http://hub.jmonkeyengine.org/wiki/doku.php/jme3:scripting" rel="nofollow">http://hub.jmonkeyengine.org/wiki/doku.php/jme3:scripting</a>
</p>

</div>
<!-- EDIT12 SECTION "Scripting" [3074-3768] -->
<h2 class="sectionedit13" id="the_project">The Project</h2>
<div class="level2">

<p>
Atom provide two editing facilities : AtomEditor for ingame editing and AtomSDK for desktop swing based in Netbean. Both of them working with a Project format and structure defined in AtomEditor structure.
</p>

<p>
The main format to save Project informations is XML. With default settings format is normal XML, it can be set to used a multiversion XML tree (imagine git but effective in XML).
</p>

<p>
<a href="/jme3/advanced/atom_framework/docs/project.html" class="wikilink1" title="jme3:advanced:atom_framework:docs:project">Project details</a>
</p>

</div>
<!-- EDIT13 SECTION "The Project" [3769-4242] -->
<h3 class="sectionedit14" id="project_structure">Project structure</h3>
<div class="level3">

<p>
The project also has a folder structure (directories and files) convention just like JME3. Aware of that when coding or making assets.
</p>

<p>
<a href="/doku.php/jme3:advanced:atom_framework:docs:project:structure" class="wikilink2" title="jme3:advanced:atom_framework:docs:project:structure" rel="nofollow">Project structure</a>
</p>

</div>
<!-- EDIT14 SECTION "Project structure" [4243-4479] -->
<h3 class="sectionedit15" id="code_or_data">Code or Data?</h3>
<div class="level3">

<p>
First take a look at how Atom manage Data…
</p>

<p>
<a href="/jme3/advanced/atom_framework/atomexasset.html" class="wikilink1" title="jme3:advanced:atom_framework:atomexasset">AtomExAsset</a>
</p>

<p>
<strong>One question you may ask: if Atom was so Data+Model-driven and generative. Is code still code or is Data?</strong>
</p>
<ol>
<li class="level1"><div class="li"> Code is still code in almost every situations. </div>
</li>
<li class="level1"><div class="li"> Till it's sent into generation pipelines (when you hit build or so), the new code and assets are generated.</div>
</li>
<li class="level1"><div class="li"> In pakaging phase, code (as byte code or scripts) are packed completely in jar (or packages format). Some of them are ofucased, zipped then translate via network. They are now data.</div>
</li>
<li class="level1"><div class="li"> In the run-time enviroment again, they are data of the JVM to execute which instruct the machine to do something (your games)</div>
</li>
<li class="level1"><div class="li"> Some of data are still data the whole time :Images or 3D Models and almost Assets for examples. But because some user data can be embeded in j3o (script for example) so they are also code in other perspective.</div>
</li>
</ol>

<p>
The distingish between data and code just need to be clear if you like to process on them. As long as you don't, they are same bit, forget about the differencies totally - who give a $%it!
</p>

</div>
<!-- EDIT15 SECTION "Code or Data?" [4480-5602] -->
<h3 class="sectionedit16" id="project_settings">Project settings</h3>
<div class="level3">

</div>
<!-- EDIT16 SECTION "Project settings" [5603-5630] -->
<h2 class="sectionedit17" id="usage_of_sdk">Usage of SDK</h2>
<div class="level2">

</div>
<!-- EDIT17 SECTION "Usage of SDK" [5631-5655] -->
<h3 class="sectionedit18" id="for_3d_editing">For 3D editing</h3>
<div class="level3">

</div>
<!-- EDIT18 SECTION "For 3D editing" [5656-5681] -->
<h3 class="sectionedit19" id="for_project_management">For project management</h3>
<div class="level3">

</div>
<!-- EDIT19 SECTION "For project management" [5682-5714] -->
<h3 class="sectionedit20" id="for_code_generation">For code generation</h3>
<div class="level3">

</div>
<!-- EDIT20 SECTION "For code generation" [5715-5746] -->
<h2 class="sectionedit21" id="components_documentations">Components documentations</h2>
<div class="level2">

</div>
<!-- EDIT21 SECTION "Components documentations" [5747-5783] -->
<h3 class="sectionedit22" id="atom_libraries">Atom Libraries</h3>
<div class="level3">

<p>
AtomCore
</p>

<p>
AtomSripting
</p>

<p>
AtomEditor
</p>

<p>
Atom2D
</p>

<p>
Atom2DEditor
</p>

<p>
CodeGen
</p>

<p>
CityGen
</p>

<p>
AtomEx
</p>

<p>
AtomExAsset
</p>

<p>
AtomLight
</p>

<p>
AtomAnim
</p>

<p>
AtomAI
</p>

<p>
AtomTestbed
</p>

</div>
<!-- EDIT22 SECTION "Atom Libraries" [5784-5949] -->
<h3 class="sectionedit23" id="inside_atomsdk">Inside AtomSDK</h3>
<div class="level3">

<p>
TeeHeeComposer
</p>

<p>
CharacterCreator
</p>

<p>
MMO-Machines
</p>

</div>
<!-- EDIT23 SECTION "Inside AtomSDK" [5950-] -->
