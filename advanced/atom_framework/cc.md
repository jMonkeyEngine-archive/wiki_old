---
title: Character customization Introduction
---
<h2 class="sectionedit1" id="character_customization_introduction">Character customization Introduction</h2>
<div class="level2">

<p>
This is an introduction of Character customization tool of Atom framework
</p>

<p>
</p><p></p><div class="notetip">Go to <a href="/doku.php/jme3:advanced:atom_framework:quickstart" class="wikilink2" title="jme3:advanced:atom_framework:quickstart" rel="nofollow">quickstart</a> if you on a rush!
</div>


</div>
<!-- EDIT1 SECTION "Character customization Introduction" [1-181] -->
<h3 class="sectionedit2" id="ideas_features">Ideas &amp; Features</h3>
<div class="level3">

</div>

<h4 id="ideas">Ideas</h4>
<div class="level4">

<p>
The initial idea of Character customization is: We (human) are soooo <strong>similiar</strong>!! 
</p>

<p>
The second idea: <strong>resuable</strong> and <strong>composable</strong>!
</p>
<ol>
<li class="level1"><div class="li"> Cloths, skins, 3dmodels, animation.. are components of a whole, which made up character</div>
</li>
<li class="level1"><div class="li"> The same ideas with component oriented architecture</div>
</li>
</ol>

<p>
So to reduce a very big workload of data and assets need for a game with vast data of character (football players, etc…) More over we can support and encourage gamer to “build” their own character! This is how we handle the situations, similiar scenario can happen in a MMOs.
</p>

</div>

<h4 id="features">Features</h4>
<div class="level4">
<ul>
<li class="level1"><div class="li"> Customize parts of characters (body, face, weapon) in gender | race (male - female, human - animal…), various height, weight!</div>
</li>
<li class="level1"><div class="li"> Customize cloths ( shirt, skirt) and their appearance (color, decal) . The cloth will fit its wearers!</div>
</li>
<li class="level1"><div class="li"> Customize the face with animation, emotions ( eyes, nose, mouth ) with (smile, angry …) goto <a href="/jme3/advanced/atom_framework/facial.html" class="wikilink1" title="jme3:advanced:atom_framework:facial">facial</a></div>
</li>
<li class="level1"><div class="li"> As close as seen in current AAA games, open to MMORPG and social games.</div>
</li>
</ul>

<p>
</p><p></p><div class="noteimportant">Go to alternatives and researches if you want to go further than Atom!
</div>


<p>
</p><p></p><div class="notetip">Try some example in Football game's character cusomization <a href="/jme3/atomixtuts/kickgame/cc.html" class="wikilink1" title="jme3:atomixtuts:kickgame:cc">cc</a>
</div>


</div>
<!-- EDIT2 SECTION "Ideas & Features" [182-1429] -->
<h2 class="sectionedit3" id="atomfacial_framework_-_first_look">AtomFacial framework - First look</h2>
<div class="level2">

</div>
<!-- EDIT3 SECTION "AtomFacial framework - First look" [1430-1474] -->
<h3 class="sectionedit4" id="features1">Features</h3>
<div class="level3">
<ol>
<li class="level1"><div class="li"> Template: Slot, Part are “place” and “item” just like textbox, choicebox in a form.</div>
</li>
<li class="level1"><div class="li"> Composing: Provide Node base way to define Customable parts, material and assets for CC. A mesh can be stiched together again after composing.</div>
</li>
<li class="level1"><div class="li"> Optimization : Compress texture space, mesh verticles</div>
</li>
<li class="level1"><div class="li"> Transformation: Provide way to include mesh morph or bone transformation can be describle in Blender, Free form deformation to make fitable clothes.</div>
</li>
<li class="level1"><div class="li"> Paint and Projection: support layered paint and decal projection (box, cylinder, sphere) in mesh surface, can be baked afterward.</div>
</li>
</ol>

</div>
<!-- EDIT4 SECTION "Features" [1475-2073] -->
<h3 class="sectionedit5" id="screenshots_video">Screenshots &amp; Video</h3>
<div class="level3">

<p>
<a href="/lib/exe/fetch.php/jme3:advanced:atom_framework:youtube_fcf6grenolg" class="media mediafile mf_ wikilink2" title="jme3:advanced:atom_framework:youtube_fcf6grenolg">youtube_fcf6grenolg</a>
</p>

</div>
<!-- EDIT5 SECTION "Screenshots & Video" [2074-2133] -->
<h3 class="sectionedit6" id="techniques">Techniques</h3>
<div class="level3">

<p>
<strong>1) Blend shape</strong> : 
</p>

<p>
<strong>2) Bone</strong> : 
</p>

<p>
<strong>3) Free form deformation</strong>: 
</p>

</div>
<!-- EDIT6 SECTION "Techniques" [2134-2225] -->
<h3 class="sectionedit7" id="problems">Problems</h3>
<div class="level3">

<p>
<strong>1) Blend shape</strong> : 
</p>

<p>
I saw that going to be added into the core soon. So exciting, that will help a tons, as soon as finish, I will make a patch to help import blend shape from blender too. One thing I still have to consider is: Can we make a type of Mesh that save a whole topology from Blender or other CAD and then become the base mesh for futher manipulate?
</p>

<p>
<strong>2) Bone</strong> : 
</p>

<p>
I saw the current behavior of Bone, SkeletonControl are quite limited. I remember once @nehon explain that we don’t save the Length of the bone, but the trans/rot/scale just like a mat4… In fact, we can save more information in a Bone, and it will help tons when it come to a situation that someone want to manipulate the bone his self.
</p>

<p>
<em>setUserControl</em> didn’t sastify me cause I force me to patch the whole animation system just because I want to scale a bone up and down (ex: bigger nose for a character), and sync that with the existed animation. You can say it’s just my very own problem but …
</p>

<p>
<strong>3) Free form deformation</strong>: 
</p>

<p>
For the need of cloth customization, I made my self a quick FFD system, in fact, it works extactly like a set of bones still have lengths and envelops on them. But in the end, once again I have to hack into the Mesh class and other things, just because a lot of private and final methods… It’s kind of sad that it should not be that hard for the engine users to add more features to the engine if the user want to.
</p>

<p>
At the end, I just want what I want, that mean I just want things work if it’s really easy, silly me. So is there another way around to make those 2 simple things?
</p>

<p>
1) Scale/Translate/Rotate a bonebut preseved the current animation. ⇒ If yes, go for Characer custumization and facial…
</p>

<p>
2) The mesh class is the center of the system, we should provide a way for people to build in from scratch or preseved topology. May be another type of Mesh, like HalfEdge mesh. If the answer it’s No need for now just consider it once in the future (We are not just making game for the moment)!
</p>

</div>
<!-- EDIT7 SECTION "Problems" [2226-4279] -->
<h3 class="sectionedit8" id="architecture">Architecture</h3>
<div class="level3">

</div>
<!-- EDIT8 SECTION "Architecture" [4280-4302] -->
<h3 class="sectionedit9" id="components">Components</h3>
<div class="level3">

</div>
<!-- EDIT9 SECTION "Components" [4303-4323] -->
<h2 class="sectionedit10" id="manuals">Manuals</h2>
<div class="level2">

<p>
Go Quick 
</p>

<p>
Go in depth
</p>

</div>
<!-- EDIT10 SECTION "Manuals" [4324-4367] -->
<h3 class="sectionedit11" id="basic_video_tutorials">Basic video tutorials</h3>
<div class="level3">

</div>
<!-- EDIT11 SECTION "Basic video tutorials" [4368-4400] -->
<h3 class="sectionedit12" id="in_depth">In depth</h3>
<div class="level3">

</div>

<h4 id="quickstart">Quickstart</h4>
<div class="level4">

</div>

<h4 id="asset_making">Asset making</h4>
<div class="level4">

</div>

<h4 id="programming">Programming</h4>
<div class="level4">

</div>
<!-- EDIT12 SECTION "In depth" [4401-4481] -->
<h2 class="sectionedit13" id="researches_papers">Researches &amp; Papers</h2>
<div class="level2">

<p>
This is a short list of Researches &amp; Papers
</p>

<p>
I have a Character customization system which i've plan to be quite complete. I reviewed a fews character system including:
<a href="http://www.youtube.com/watch?v=RO8GIoRLGa0" class="urlextern" title="http://www.youtube.com/watch?v=RO8GIoRLGa0" rel="nofollow">http://www.youtube.com/watch?v=RO8GIoRLGa0</a>
</p>
<ul>
<li class="level1"><div class="li"> Perfect World</div>
</li>
<li class="level1"><div class="li"> APB: Reloaded</div>
</li>
<li class="level1"><div class="li"> Aion</div>
</li>
<li class="level1"><div class="li"> Star Trek Online</div>
</li>
<li class="level1"><div class="li"> Champions Online</div>
</li>
</ul>

<p>
Some technical articles:
</p>
<ul>
<li class="level1"><div class="li"><a href="http://www.heroengine.com/heroengine/dynamic-character-systems/" class="urlextern" title="http://www.heroengine.com/heroengine/dynamic-character-systems/" rel="nofollow">http://www.heroengine.com/heroengine/dynamic-character-systems/</a></div>
</li>
<li class="level1"><div class="li"><a href="http://hewiki.heroengine.com/wiki/Character_Design_and_Development" class="urlextern" title="http://hewiki.heroengine.com/wiki/Character_Design_and_Development" rel="nofollow">http://hewiki.heroengine.com/wiki/Character_Design_and_Development</a></div>
</li>
<li class="level1"><div class="li"><a href="http://anticto.com/" class="urlextern" title="http://anticto.com/" rel="nofollow">http://anticto.com/</a></div>
</li>
</ul>

</div>
<!-- EDIT13 SECTION "Researches & Papers" [4482-4999] -->
<h2 class="sectionedit14" id="alternatives">Alternatives</h2>
<div class="level2">

</div>
<!-- EDIT14 SECTION "Alternatives" [5000-5023] -->
<h3 class="sectionedit15" id="opensource">Opensource</h3>
<div class="level3">

</div>
<!-- EDIT15 SECTION "Opensource" [5024-5044] -->
<h3 class="sectionedit16" id="commercial">Commercial</h3>
<div class="level3">

</div>
<!-- EDIT16 SECTION "Commercial" [5045-] -->
