---
title: Codegen Introduction
---
<h2 class="sectionedit1" id="codegen_introduction">Codegen Introduction</h2>
<div class="level2">

<p>
Code generator for various - cross platform programming languages and paradims. All in one!
</p>

<p>
Powered by AtomCore and JME3.
</p>

</div>

<h4 id="inspired_by">Inspired by</h4>
<div class="level4">

<p>
ECore
</p>

<p>
UML
</p>

<p>
MetaWidget
</p>

<p>
Other game engines and editor: UDK, Unity, Blender, GameMaker…
</p>

<p>
Other node base editor: 
</p>

<p>
Web world: 
</p>

</div>
<!-- EDIT1 SECTION "Codegen Introduction" [1-304] -->
<h3 class="sectionedit2" id="features">Features</h3>
<div class="level3">

<p>
Node &amp; Flow &amp; Graph base
</p>

<p>
Model base
</p>

<p>
Scope &amp; Instruction &amp; Control base
</p>

</div>
<!-- EDIT2 SECTION "Features" [305-397] -->
<h3 class="sectionedit3" id="comparasion">Comparasion</h3>
<div class="level3">

</div>

<h4 id="vs_metawidget_oim">VS MetaWidget OIM</h4>
<div class="level4">

<p>
<a href="http://metawidget.org/" class="urlextern" title="http://metawidget.org/" rel="nofollow">http://metawidget.org/</a>
</p>

<p>
is for generating UI from objects. 
</p>

<p>
<strong>CodeGen</strong> is for generating data (objects) from (data) objects.
</p>

</div>

<h4 id="vs_emf">VS EMF</h4>
<div class="level4">

<p>
<a href="https://www.eclipse.org/modeling/emf/" class="urlextern" title="https://www.eclipse.org/modeling/emf/" rel="nofollow">https://www.eclipse.org/modeling/emf/</a>
</p>

<p>
<a href="http://www.eclipse.org/ecoretools/" class="urlextern" title="http://www.eclipse.org/ecoretools/" rel="nofollow">http://www.eclipse.org/ecoretools/</a>
</p>

<p>
is for model based generation.
</p>

<p>
<strong>CodeGen</strong> works upon EMF and also support others: flow base - scope base paradigm.
</p>

<p>
CodeGen tools toward Netbean instead of Eclipse to suite with JME3's SDK. Also CodeGen toward Games, not general applications!
</p>

</div>

<h4 id="vs_morph_beanmapping_orm">VS Morph/ BeanMapping / ORM</h4>
<div class="level4">

<p>
Work in higher level than those.
</p>

<p>
That's said!
</p>

<p>
<strong>CodeGen</strong> work in higher level, solve other problems and depends on MetaWidget, EMF, Morph, BeanMapping and ORM.
</p>

</div>
<!-- EDIT3 SECTION "Comparasion" [398-1110] -->
<h2 class="sectionedit4" id="first_look">First look</h2>
<div class="level2">

</div>
<!-- EDIT4 SECTION "First look" [1111-1134] -->
<h3 class="sectionedit5" id="generation">Generation</h3>
<div class="level3">

<p>
<a href="http://en.wikipedia.org/wiki/Code_generation_%28compiler%29" class="urlextern" title="http://en.wikipedia.org/wiki/Code_generation_%28compiler%29" rel="nofollow">http://en.wikipedia.org/wiki/Code_generation_%28compiler%29</a>
</p>

<p>
Atom support code generation from multiple sources and to various targets to help speed up and unite production pipeline. CodeGen - Ultimate tools for code genration corporate with AtomExAsset - Ultimate tools for game assets management is 2 facilities in charge for the job.
</p>

<p>
Sources
</p>
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

<p>
Targets
</p>
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
<!-- EDIT5 SECTION "Generation" [1135-2012] -->
<h3 class="sectionedit6" id="simulation">Simulation</h3>
<div class="level3">

</div>
<!-- EDIT6 SECTION "Simulation" [2013-2034] -->
<h2 class="sectionedit7" id="architecture_designs">Architecture &amp; Designs</h2>
<div class="level2">

</div>
<!-- EDIT7 SECTION "Architecture & Designs" [2035-2069] -->
<h3 class="sectionedit8" id="metawidget_architecture">MetaWidget Architecture</h3>
<div class="level3">

<p>
<a href="http://metawidget.sourceforge.net/doc/reference/en/html/ch02.html" class="urlextern" title="http://metawidget.sourceforge.net/doc/reference/en/html/ch02.html" rel="nofollow">http://metawidget.sourceforge.net/doc/reference/en/html/ch02.html</a>
</p>

<p>
<a href="http://metawidget.sourceforge.net/elevator.php" class="urlextern" title="http://metawidget.sourceforge.net/elevator.php" rel="nofollow">http://metawidget.sourceforge.net/elevator.php</a>
</p>

<p>
</p><p></p><div class="notetip">MORAL: Object has “similar” semantic with its UI. A thing has conceptal similarties with its representation, if there is a projection from it to the representation.
</div>


</div>
<!-- EDIT8 SECTION "MetaWidget Architecture" [2070-2399] -->
<h3 class="sectionedit9" id="emf_architecture">EMF Architecture</h3>
<div class="level3">

<p>
<a href="http://wiki.eclipse.org/index.php/EMF/FAQ" class="urlextern" title="http://wiki.eclipse.org/index.php/EMF/FAQ" rel="nofollow">http://wiki.eclipse.org/index.php/EMF/FAQ</a>
</p>

<p>
</p><p></p><div class="notetip">MORAL: 
</div>


</div>
<!-- EDIT9 SECTION "EMF Architecture" [2400-2492] -->
<h3 class="sectionedit10" id="codegen_architecture">CodeGen Architecture</h3>
<div class="level3">

<p>
The initial idea of CodeGen is “there is similarity between two, there is a transform available”, learnt from above.
</p>

<p>
Also take a look at wisdoms and <a href="/jme3/advanced/atom_framework/atomcore/algorithms.html" class="wikilink1" title="jme3:advanced:atom_framework:atomcore:algorithms">Algorithms</a> which AtomCore sketchs for Generation:
</p>
<ul>
<li class="level1"><div class="li"> [Math] A function from one set to another set.</div>
</li>
<li class="level1"><div class="li"> [Physics] Energy from one form to another.</div>
</li>
<li class="level1"><div class="li"> [Language] Translate sematic from one to another language need a dictionary.</div>
</li>
<li class="level1"><div class="li"> [Art] Nothing new, just a cover</div>
</li>
<li class="level1"><div class="li"> [Computing] Template is a good abstraction of algorimths.</div>
</li>
<li class="level1"><div class="li"> [Programming] DRY and open source. </div>
</li>
<li class="level1"><div class="li"> [New techs &amp; trends] Topology and well defined network actually a virtue. </div>
</li>
</ul>

</div>
<!-- EDIT10 SECTION "CodeGen Architecture" [2493-3173] -->
<h3 class="sectionedit11" id="layouts">Layouts</h3>
<div class="level3">

<p>
GraphLayout
</p>

</div>
<!-- EDIT11 SECTION "Layouts" [3174-3202] -->
<h3 class="sectionedit12" id="builders">Builders</h3>
<div class="level3">

<p>
BlockBuilder
</p>

</div>
<!-- EDIT12 SECTION "Builders" [3203-3233] -->
<h3 class="sectionedit13" id="blocks">Blocks</h3>
<div class="level3">

<p>
CodeBlock
</p>

<p>
PlaceHolderBlock
</p>

</div>
<!-- EDIT13 SECTION "Blocks" [3234-3278] -->
<h2 class="sectionedit14" id="documentation">Documentation</h2>
<div class="level2">

</div>
<!-- EDIT14 SECTION "Documentation" [3279-] -->
