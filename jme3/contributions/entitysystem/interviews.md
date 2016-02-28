---
title: ES Approaches
---
<h2 class="sectionedit1" id="es_approaches">ES Approaches</h2>
<div class="level2">

<p>
Entity System implementations are various! 
</p>

<p>
As said, we are talking about Component oriented programming Entity System, implemented in Object oriented programming language and enviroment like Java!
</p>

<p>
So,we are
</p>
<ul>
<li class="level1"><div class="li"> <strong>not talking</strong> about Groovy, Scala, Closure.. or any Java extension!</div>
</li>
<li class="level1"><div class="li"> <strong>not talking</strong> about Entity system in any scope other than in a real-time application!</div>
</li>
<li class="level1"><div class="li"> <strong>focusing</strong> in 'core' features, which exclude many specific usecases</div>
</li>
<li class="level1"><div class="li"> <strong>trying</strong> to be unprejudiced , impersonal to make equitable judge.</div>
</li>
</ul>

</div>
<!-- EDIT1 SECTION "ES Approaches" [1-547] -->
<h3 class="sectionedit2" id="outline">Outline</h3>
<div class="level3">
<ol>
<li class="level1"><div class="li"> Initial philosophy</div>
</li>
<li class="level1"><div class="li"> Pure data or not?</div>
</li>
<li class="level1"><div class="li"> Multi-threading, concurency enable or not?</div>
</li>
<li class="level1"><div class="li"> Communication: Event messaging enable or not?</div>
</li>
<li class="level1"><div class="li"> Is database (and other kind of persistent) friendly or not?</div>
</li>
<li class="level1"><div class="li"> Is enterprise friendly (expanable/ extensible/ modulizable) or not?</div>
</li>
<li class="level1"><div class="li"> Script possibilities?</div>
</li>
<li class="level1"><div class="li"> Restrictions and limitation</div>
</li>
<li class="level1"><div class="li"> Dependencies</div>
</li>
<li class="level1"><div class="li"> Current status: Long term, stable, community?</div>
</li>
</ol>

<p>
The comparasions will focus in these below points, follow with the scope, status of each projects
Detail explanation of abbove points <a href="/jme3/contributions/entitysystem/points.html" class="wikilink1" title="jme3:contributions:entitysystem:points">points</a>
</p>

</div>
<!-- EDIT2 SECTION "Outline" [548-1144] -->
<h2 class="sectionedit3" id="es_projects_interviews">ES projects interviews</h2>
<div class="level2">

<p>
These interviews are short but focus dicussion to help you get a clear view of underlying implementation of each project.
</p>

</div>
<!-- EDIT3 SECTION "ES projects interviews" [1145-1300] -->
<h3 class="sectionedit4" id="artemisgeneral">Artemis: General</h3>
<div class="level3">

<p>
GoogleCode: <a href="https://code.google.com/p/artemis-framework/" class="urlextern" title="https://code.google.com/p/artemis-framework/" rel="nofollow">https://code.google.com/p/artemis-framework/</a>
</p>

<p>
Website: <a href="http://gamadu.com/artemis/index.html" class="urlextern" title="http://gamadu.com/artemis/index.html" rel="nofollow">http://gamadu.com/artemis/index.html</a>
</p>

<p>
Wiki: <a href="http://entity-systems.wikidot.com/artemis-entity-system-framework" class="urlextern" title="http://entity-systems.wikidot.com/artemis-entity-system-framework" rel="nofollow">http://entity-systems.wikidot.com/artemis-entity-system-framework</a>
</p>

<p>
</p><p></p><div class="noteimportant">Review: HERE! <a href="/doku.php/jme3:contributions:entitysystem:interviews:artemis" class="wikilink2" title="jme3:contributions:entitysystem:interviews:artemis" rel="nofollow">artemis</a> because I can not contact with author of Artemis at the moment so I will have a short review of it with some of my experience working on it and base on its source code!
</div>


</div>

<h4 id="short_conclusion">Short conclusion</h4>
<div class="level4">

<p>
Artemis approach
</p>
<ol>
<li class="level1"><div class="li"> Initial philosophy : Lightweight, small footprint and 1.5+</div>
</li>
<li class="level1"><div class="li"> Pure data: No</div>
</li>
<li class="level1"><div class="li"> Multi-threading, concurency: with care</div>
</li>
<li class="level1"><div class="li"> Communication: Event messaging enable or not? No implementation yet</div>
</li>
<li class="level1"><div class="li"> Is database (and other kind of persistent) friendly or not? No implementation yet</div>
</li>
<li class="level1"><div class="li"> Is enterprise friendly (expanable/ extensible/ modulizable) or not? Not clear but because not pure data, consider Yes</div>
</li>
<li class="level1"><div class="li"> Script possibilities? Yes</div>
</li>
<li class="level1"><div class="li"> Restrictions and limitation: Custom System has to be extends base System; Processor base; Aspect base, Has documented about Dependencies between System</div>
</li>
<li class="level1"><div class="li"> External library dependencies : No</div>
</li>
<li class="level1"><div class="li"> Current status: Long term, stable, community? The most early Java ES, more than 3 years, kind of unactive, has a forum. </div>
</li>
</ol>

<p>
Read the full review for details
</p>

</div>
<!-- EDIT4 SECTION "Artemis: General" [1301-2598] -->
<h3 class="sectionedit5" id="zay-espspeed">Zay-ES : @pspeed</h3>
<div class="level3">

<p>
Forum : <a href="http://hub.jmonkeyengine.org/forum/board/projects/zay-es/" class="urlextern" title="http://hub.jmonkeyengine.org/forum/board/projects/zay-es/" rel="nofollow">http://hub.jmonkeyengine.org/forum/board/projects/zay-es/</a>
</p>

<p>
Wiki: <a href="http://hub.jmonkeyengine.org/wiki/doku.php/jme3:contributions:entitysystem" class="urlextern" title="http://hub.jmonkeyengine.org/wiki/doku.php/jme3:contributions:entitysystem" rel="nofollow">http://hub.jmonkeyengine.org/wiki/doku.php/jme3:contributions:entitysystem</a>
</p>

<p>
Links: <a href="http://hub.jmonkeyengine.org/forum/topic/zay-es-links/" class="urlextern" title="http://hub.jmonkeyengine.org/forum/topic/zay-es-links/" rel="nofollow">http://hub.jmonkeyengine.org/forum/topic/zay-es-links/</a>
</p>

<p>
Interview: <a href="/doku.php/jme3:contributions:entitysystem:interviews:zay-es" class="wikilink2" title="jme3:contributions:entitysystem:interviews:zay-es" rel="nofollow">zay-es</a>
</p><p></p><div class="noteimportant">In my POV, Zay-ES has the most active development status and also the maintainer is a core JME3 dev, that's why all its functions and wisdoms are close to JME3!
</div>


</div>

<h4 id="short_conclusion1">Short conclusion</h4>
<div class="level4">

<p>
Zay-ES approach
</p>
<ol>
<li class="level1"><div class="li"> Initial philosophy : Lightweight, small footprint and 1.5+</div>
</li>
<li class="level1"><div class="li"> Pure data: Yes</div>
</li>
<li class="level1"><div class="li"> Multi-threading, concurency: free, by design, but still <em>need better design contract</em></div>
</li>
<li class="level1"><div class="li"> Communication: Event messaging enable or not? No implementation yet</div>
</li>
<li class="level1"><div class="li"> Is database (and other kind of persistent) friendly or not? No implementation yet</div>
</li>
<li class="level1"><div class="li"> Is enterprise friendly (expanable/ extensible/ modulizable) or not? Not clear, <em>lack of design contract</em></div>
</li>
<li class="level1"><div class="li"> Script possibilities? Yes</div>
</li>
<li class="level1"><div class="li"> Restrictions and limitation: Free of System implementation, but <em>lack of design contract</em></div>
</li>
<li class="level1"><div class="li"> External library dependencies : No</div>
</li>
<li class="level1"><div class="li"> Current status: Long term, stable, community? more than 2 years, open source recently, active, has a forum in Jmonkey's hub. </div>
</li>
</ol>

<p>
Read the full review for details
</p>

</div>
<!-- EDIT5 SECTION "Zay-ES : @pspeed" [2599-3896] -->
<h3 class="sectionedit6" id="entitymonkeyzzuegg">EntityMonkey : @zzuegg</h3>
<div class="level3">

<p>
Post: <a href="http://hub.jmonkeyengine.org/forum/topic/entitymonkey-a-simple-entity-system-for-jme/" class="urlextern" title="http://hub.jmonkeyengine.org/forum/topic/entitymonkey-a-simple-entity-system-for-jme/" rel="nofollow">http://hub.jmonkeyengine.org/forum/topic/entitymonkey-a-simple-entity-system-for-jme/</a>
</p>

<p>
Interview: <a href="/doku.php/jme3:contributions:entitysystem:interviews:em-es" class="wikilink2" title="jme3:contributions:entitysystem:interviews:em-es" rel="nofollow">em-es</a>
</p>

</div>
<!-- EDIT6 SECTION "EntityMonkey : @zzuegg" [3897-4085] -->
<h3 class="sectionedit7" id="privateempire_phoenix">Private : @Empire phoenix</h3>
<div class="level3">

<p>
Interview: <a href="/doku.php/jme3:contributions:entitysystem:interviews:emp-es" class="wikilink2" title="jme3:contributions:entitysystem:interviews:emp-es" rel="nofollow">emp-es</a>
</p>

</div>
<!-- EDIT7 SECTION "Private : @Empire phoenix" [4086-4186] -->
<h2 class="sectionedit8" id="others">Others</h2>
<div class="level2">

</div>
<!-- EDIT8 SECTION "Others" [4187-4205] -->
<h3 class="sectionedit9" id="java_java_extension">Java &amp; Java extension</h3>
<div class="level3">

</div>

<h4 id="spartanused_for_slick_abandoned">Spartan: [used for Slick. abandoned]</h4>
<div class="level4">

<p>
GoogleCode: <a href="http://code.google.com/p/spartanframework/" class="urlextern" title="http://code.google.com/p/spartanframework/" rel="nofollow">http://code.google.com/p/spartanframework/</a>
</p>

</div>
<!-- EDIT9 SECTION "Java & Java extension" [4206-4338] -->
<h3 class="sectionedit10" id="not_java">Not Java</h3>
<div class="level3">

</div>

<h4 id="c">C++</h4>
<div class="level4">

</div>

<h4 id="javascript">JavaScript</h4>
<div class="level4">

</div>

<h4 id="c1">C#</h4>
<div class="level4">

</div>

<h4 id="actionscript">ActionScript</h4>
<div class="level4">

</div>
<!-- EDIT10 SECTION "Not Java" [4339-] -->
