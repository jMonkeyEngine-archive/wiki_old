---
title: Best Practices For jME3 Developers
---
<h1 class="sectionedit1" id="best_practices_for_jme3_developers">Best Practices For jME3 Developers</h1>
<div class="level1">

<p>
Every milestone of a game development project is made up of phases: Planning, development, testing, and release. Every milestone involves updates to multi-media assets and to code.  
</p>

<p>
This “best practices” page is a collection of recommendations and expert tips. Feel free to add your own!
</p>

</div>
<!-- EDIT1 SECTION "Best Practices For jME3 Developers" [1-341] -->
<h2 class="sectionedit2" id="requirements_and_planning">Requirements and Planning</h2>
<div class="level2">

<p>
If you are a beginner, you should first <a href="http://www.hobbygamedev.com/digests/?page=free" class="urlextern" title="http://www.hobbygamedev.com/digests/?page=free" rel="nofollow">read some</a> <a href="http://gamasutra.com/" class="urlextern" title="http://gamasutra.com/" rel="nofollow">articles about</a> <a href="http://www.google.com/search?q=3d+game+development" class="urlextern" title="http://www.google.com/search?q=3d+game+development" rel="nofollow">game development</a>. We cannot cover all general tips here.
</p>

</div>
<!-- EDIT2 SECTION "Requirements and Planning" [342-634] -->
<h3 class="sectionedit3" id="requirements_gathering">Requirements Gathering</h3>
<div class="level3">

<p>
As a quick overview, answer yourself the following questions:
</p>
<ul>
<li class="level1"><div class="li"> Motivation</div>
<ul>
<li class="level2"><div class="li"> Sum up your game idea in one catchy sentence. If you can't, it's too complicated. <br />
E.g. “Craft by day, fight by night!”</div>
</li>
<li class="level2"><div class="li"> Who's the target group? Are you making it for your friends or are you trying to attract the masses?</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Game type</div>
<ul>
<li class="level2"><div class="li"> Point of view (first- or third-person camera)? What characters does the player control? (if applicable)</div>
</li>
<li class="level2"><div class="li"> Time- or turn-based?</div>
</li>
<li class="level2"><div class="li"> Genre (drama, horror, adventure, mystery, comedy, educational, documentary)? </div>
</li>
<li class="level2"><div class="li"> Setting and background story? (historic, fantasy, anime, futuristic, utopia/dystopia, pirate, zombie, vampire…)? </div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Gameplay</div>
<ul>
<li class="level2"><div class="li"> What is the start state, what is the end state? (if applicable)</div>
</li>
<li class="level2"><div class="li"> What resources does the player manage? How are resources gained, transformed, spent? <br />
E.g. “points”, health, speed, gold, xp, mana.</div>
</li>
<li class="level2"><div class="li"> How does the player interact? Define rules, challenges, game mechanics.</div>
</li>
<li class="level2"><div class="li"> What state is considered winning, and what losing, or is it an open world?</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Multi-media assets</div>
<ul>
<li class="level2"><div class="li"> Which media will you need? How will you get this content? <br />
E.g. models, terrains; materials, textures; noises, music, voices; video, cutscenes; spoken/written dialog; level maps, quests, story; AI scripts.</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Interface</div>
<ul>
<li class="level2"><div class="li"> Can you achieve a high degree of input control? (Even minor navigation and interaction glitches make the game unsolvable.)</div>
</li>
<li class="level2"><div class="li"> Decide how to reflect current status, and changes in game states. E.g. health/damage in HUD.</div>
</li>
<li class="level2"><div class="li"> Decide how to reward good moves and discourage bad ones.</div>
</li>
</ul>
</li>
</ul>

</div>
<!-- EDIT3 SECTION "Requirements Gathering" [635-2261] -->
<h3 class="sectionedit4" id="planning_development_milestones">Planning Development Milestones</h3>
<div class="level3">

<p>
Use an <a href="http://en.wikipedia.org/wiki/Issue_tracking_system" class="urlextern" title="http://en.wikipedia.org/wiki/Issue_tracking_system" rel="nofollow">issue and bug tracker</a> to outline what features you want and what components are needed.
</p>
<ol>
<li class="level1"><div class="li"> Pre-Alpha Development</div>
<ul>
<li class="level2"><div class="li"> Artwork: Test asset loading and saving with mock-ups and stock art.</div>
</li>
<li class="level2"><div class="li"> Lay out the overall application flow, i.e. switching between intro / options / game screen, etc.</div>
</li>
<li class="level2"><div class="li"> Get one typical level working before you can announce the Alpha Release. <br />
E.g. if the game is a “Jump'n'Run”, jumping and running must work.</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Alpha Release</div>
</li>
<li class="level1"><div class="li"> Pre-Beta Development</div>
<ul>
<li class="level2"><div class="li"> Artwork: Replace all mock-ups with first drafts of real media and level maps.</div>
</li>
<li class="level2"><div class="li"> Have your team members review and “alpha test” it on various systems, track bugs, debug, optimize.</div>
</li>
<li class="level2"><div class="li"> Declare <a href="http://en.wikipedia.org/wiki/Feature_freeze" class="urlextern" title="http://en.wikipedia.org/wiki/Feature_freeze" rel="nofollow">Feature Freeze</a> before you announce the Beta Release to prevent a bottomless pit of new bugs.</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Beta Release</div>
</li>
<li class="level1"><div class="li"> Post-Beta Development</div>
<ul>
<li class="level2"><div class="li"> Artwork: Fill in the final media and level maps.</div>
</li>
<li class="level2"><div class="li"> Have external people review and “beta test” it, make it easy to report bugs.</div>
</li>
<li class="level2"><div class="li"> Fix high-priority bugs, even out the kinks in code and gameplay, don't add new features for now!</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Gamma Release, Delta Release… = Release Candidates</div>
<ul>
<li class="level2"><div class="li"> Think you're done? Make test runs incl. packaging and distribution. (Order form? download?)</div>
</li>
<li class="level2"><div class="li"> Test the heck out of it. Last chance to find and fix a horrible bug.</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Omega = Final Release</div>
</li>
</ol>

<p>
How you name or number these stages is fully up to your team. Development teams use numbered milestones (m1, m2, m3), Greek letters (e.g. alpha, beta, gamma, delta), <a href="http://en.wikipedia.org/wiki/Software_versioning" class="urlextern" title="http://en.wikipedia.org/wiki/Software_versioning" rel="nofollow">"major.minor.patch-build" version</a> numbering (e.g. “2.7.23-1328”), or combinations thereof. 
</p>

</div>
<!-- EDIT4 SECTION "Planning Development Milestones" [2262-4046] -->
<h3 class="sectionedit5" id="use_file_version_control">Use File Version Control</h3>
<div class="level3">

<p>
Whether you work in a team or alone, keeping a version controlled repository of your code will help you roll-back buggy changes, or recover old code that someone deleted and that is now needed again.
</p>
<ul>
<li class="level1"><div class="li"> Treat commit messages as messages to your future self. “Made some changes” is <em>not</em> a commit message.</div>
</li>
<li class="level1"><div class="li"> The jMonkeyEngine SDK supports Subversion, Mercurial, and Git. <br />
If you don't know which to choose, Subversion is a good choice for starters.</div>
</li>
<li class="level1"><div class="li"> Set up your own local server, or get free remote hosting space from various open-source dev portals like <a href="http://sourceforge.net/" class="urlextern" title="http://sourceforge.net/" rel="nofollow">Sourceforge</a>, <a href="https://github.com/" class="urlextern" title="https://github.com/" rel="nofollow">Github</a>, <a href="https://bitbucket.org/" class="urlextern" title="https://bitbucket.org/" rel="nofollow">bitbucket</a> (supports private projects), <a href="http://home.java.net/create-project" class="urlextern" title="http://home.java.net/create-project" rel="nofollow">Java.net</a>, <a href="https://code.google.com" class="urlextern" title="https://code.google.com" rel="nofollow">Google Code</a>…</div>
</li>
</ul>

</div>
<!-- EDIT5 SECTION "Use File Version Control" [4047-4879] -->
<h2 class="sectionedit6" id="multi-media_asset_pipeline">Multi-Media Asset Pipeline</h2>
<div class="level2">
<div class="table sectionedit7"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0">DO</th><th class="col1">DON'T</th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0"> Save original models+textures into <code>assets/Textures</code>. </td><td class="col1"> Don't reference textures or models outside your JME project. </td>
	</tr>
	<tr class="row2">
		<td class="col0"> Save sounds into <code>assets/Sounds.</code></td><td class="col1"> Don't reference audio files outside your JME project. </td>
	</tr>
	<tr class="row3">
		<td class="col0"> Create simple, low-polygon models. </td><td class="col1"> Don't create high-polygon models, they render too slow to be useful in games. </td>
	</tr>
	<tr class="row4">
		<td class="col0"> Only use Diffuse Map, Normal Map, Glow Map, Specular Map. </td><td class="col1"> Don't use unsupported material properties that are not listed in the <a href="/jme3/advanced/materials_overview.html" class="wikilink1" title="jme3:advanced:materials_overview">Materials Overview</a>.</td>
	</tr>
	<tr class="row5">
		<td class="col0"> Use UV texture / texture atlases / baking for each texture map. </td><td class="col1"> Don't create models based on multiple separate textures, it will break the model into separate meshes.</td>
	</tr>
	<tr class="row6">
		<td class="col0"> Convert Models to j3o format. Move j3o files into <code>assets/Models</code>. </td><td class="col1">Don't reference Blender/Ogre/OBJ files in your load() code, because these unoptimized files are not packaged into the JAR.</td>
	</tr>
</table></div>
<!-- EDIT7 TABLE [4920-5806] -->
<p>
Learn details about the <a href="/jme3/intermediate/multi-media_asset_pipeline.html" class="wikilink1" title="jme3:intermediate:multi-media_asset_pipeline">Multi-Media Asset Pipeline</a> here.
</p>

</div>
<!-- EDIT6 SECTION "Multi-Media Asset Pipeline" [4880-5889] -->
<h2 class="sectionedit8" id="development_phase">Development Phase</h2>
<div class="level2">

<p>
</p><p></p><div class="noteclassic">Many game developers dream of creating their very own “MMORPG with full-physics, AI, post-rendering effects, multi-player networking, procedurally generated maps, and customizable characters”. So why aren't there tons of MMORPGs out there? <br />
Even for large experienced game producers, the creation of such a complex game is time-intensive and failure-prone. How familiar are you with multi-threading, persistence, optimization, client-server synchonization, …? Unless your answer is “very!”, then start with a single-player desktop game, and work your way up – just as the pros did when they started.
</div>


</div>
<!-- EDIT8 SECTION "Development Phase" [5890-6539] -->
<h3 class="sectionedit9" id="extend_simpleapplication">Extend SimpleApplication</h3>
<div class="level3">

<p>
Every jME3 game is centered around one main class that (directly or indirectly) extends com.jme3.app.<a href="/jme3/intermediate/simpleapplication.html" class="wikilink1" title="jme3:intermediate:simpleapplication">SimpleApplication</a>. 
</p>

<p>
</p><p></p><div class="noteimportant">Note that although the “SimpleApplication” name might be misleading, all jME3 applications, including very large projects, are based on this class. The name only implies that this class itself is a simple application already. You make it “non-simple” by extending it!
</div>


<p>
For your future game releases, you will want to rely on your own framework (based on jME): Your custom framework extends jME's SimpleApplication, and includes your custom methods for loading, saving, and arranging your scenes, your custom navigation methods, your inputs for pausing and switching your custom screens, your custom user interface (options screen, HUD, etc), your custom NPC factory, your custom physics properties, your custom networking synchronization, etc. 
</p>

<p>
</p><p></p><div class="notetip">Writing and reusing (extending) your own base framework saves you time. When you update your generic base classes, all your games that extend them benefit from improvements to the base (just as all jME-based games benefit of improvements to the jME framework). <br />
Also, your own framework gives all your games a common look and feel.
</div>


</div>
<!-- EDIT9 SECTION "Extend SimpleApplication" [6540-7823] -->
<h3 class="sectionedit10" id="where_to_start">Where to Start?</h3>
<div class="level3">

<p>
You have a list of features that you want in game, but which one do you implement first? You will keep adding features to a project that grows more and more complex, how can you minimize the amount of rewriting required?
</p>
<ol>
<li class="level1"><div class="li"> Make sure the game's high-level frame (screen switching, network sync, loading/saving) is sound and solid. </div>
</li>
<li class="level1"><div class="li"> Start with implementing the most complex game feature first – the one that imposes most constraints on the structure of your project (for example: multi-player networking, or physics.)</div>
</li>
<li class="level1"><div class="li"> Add only one larger feature at a time. If there are complex interactions (such as “networking + physics”), start with a small test case (“one shared cube”) and work your way up. Starting with a whole scene introduces too many extra sources of error.</div>
</li>
<li class="level1"><div class="li"> Implement low-complexity decorations (audio and visual effects) last.</div>
</li>
<li class="level1"><div class="li"> Test for side-effects on existing code after you add a new feature (regression test).</div>
</li>
</ol>

<p>
</p><p></p><div class="notetip">Acknowledge whether you want a feature because it is necessary for gameplay, or simply because “everyone else has it”. Your goal should be to bring out the essence of your game idea. Don't water down gameplay by attempting to make it “do everything, but better”. Successful high-performance games are the ones where someone made smart decisions what to keep and what to <em>drop</em>.
</div>


</div>
<!-- EDIT10 SECTION "Where to Start?" [7824-9191] -->
<h3 class="sectionedit11" id="the_smart_way_to_add_custom_methods_and_fields">The Smart Way to Add Custom Methods and Fields</h3>
<div class="level3">

<p>
</p><p></p><div class="notewarning"><strong>Avoid the Anti-Pattern:</strong> Don't design complex role-based classes using Java inheritance, it will result in an unmaintainable mess. <br />
Example: You start extending <code>Node</code> –&gt; <code>MyMobileNode</code> –&gt; <code>MyNPC</code>. Then you extend <code>MyFighterNPC</code> (defends, attacks) and <code>MyShopKeeperNPC</code> (trades) from <code>MyNPC</code>. What if you need an NPC that trades and defends itself, but doesn't attack? Do you extend MyShopKeeperNPC and copy and paste the defensive methods from MyFighterNPC? Or do you extend MyFighterNPC and override the attacking methods of its parent? Neither is a clean solution. <br />
Wouldn't it be better if behaviours were a separate “system”, and attributes were separate “components” that you add to the “entity” that needs them?
</div>


<p>
You write Java classes named <code>Controls</code> to implement your Game Entities, and define an Entity's visuals, attributes, and behaviours. In jME, <code>Spatial</code>s (<code>Nodes</code> or <code>Geometry</code>s) are the visual representation of the game entity in the scene graph.
</p>
<ul>
<li class="level1"><div class="li"> Game entities have <strong>attributes</strong> – All Entities are neutral <em>things</em>, only their attributes define what an entity actually <em>is</em> (a person or a brick). In jME, we call these class fields of Spatials “user data”. <br />
Example: Players have <strong>class fields</strong> for <code>id, health, coins, inventory, equipment, profession</code>.</div>
</li>
<li class="level1"><div class="li"> Game entities have <strong>behaviours</strong> – Behaviour systems communicate about the game state and modify attributes. In jME, these game mechanics are implemented in modular <code>update()</code> methods that all hook into the main update loop. <br />
Example: Players have <strong>methods</strong> such as <code>walk(), addGold(), getHealth(), pickUpItem(), dropItem(), useItem(), attack()</code>.</div>
</li>
</ul>

<p>
</p><p></p><div class="notetip"> <strong>Follow the Best Practice:</strong> In general, use composition over inheritance and keep “what an entity does” (behaviour system) separate from “what this entity is” (attributes).

<ul>
<li class="level1"><div class="li"> Use <code><a href="/jme3/advanced/spatial.html" class="wikilink1" title="jme3:advanced:spatial">setUserData()</a></code> to add custom attributes to Spatials.</div>
</li>
<li class="level1"><div class="li"> Use <a href="/jme3/advanced/custom_controls.html" class="wikilink1" title="jme3:advanced:custom_controls">Controls</a> and <a href="/jme3/advanced/application_states.html" class="wikilink1" title="jme3:advanced:application_states">Application States</a> to define custom behaviour systems.</div>
</li>
</ul>

<p>

</p></div>


<p>
If your game is even more complex, you may want to learn about “real” Entity Systems, which form a quite different programming paradigm from object oriented coding but are scalable to very large proportions. Note however that this topic is very unintuitive to handle for an OOP programmer and you should really decide on a case basis if you really need this or not and gather some experiences before diving head first into a MMO project <img src="/lib/images/smileys/icon_smile.gif" class="icon" alt=":-)" />
</p>
<ul>
<li class="level1"><div class="li"> <a href="http://cowboyprogramming.com/2007/01/05/evolve-your-heirachy/" class="urlextern" title="http://cowboyprogramming.com/2007/01/05/evolve-your-heirachy/" rel="nofollow">http://cowboyprogramming.com/2007/01/05/evolve-your-heirachy/</a> </div>
</li>
<li class="level1"><div class="li"> <a href="http://www.gamasutra.com/blogs/MeganFox/20101208/88590/Game_Engines_101_The_EntityComponent_Model.php" class="urlextern" title="http://www.gamasutra.com/blogs/MeganFox/20101208/88590/Game_Engines_101_The_EntityComponent_Model.php" rel="nofollow">http://www.gamasutra.com/blogs/MeganFox/20101208/88590/Game_Engines_101_The_EntityComponent_Model.php</a></div>
</li>
<li class="level1"><div class="li"> <a href="http://gamedev.stackexchange.com/questions/28695/variants-of-entity-component-systems" class="urlextern" title="http://gamedev.stackexchange.com/questions/28695/variants-of-entity-component-systems" rel="nofollow">http://gamedev.stackexchange.com/questions/28695/variants-of-entity-component-systems</a></div>
</li>
<li class="level1"><div class="li"> <a href="http://louisstowasser.com/post/19279778476/entity-component-systems-inheritance-vs-composition" class="urlextern" title="http://louisstowasser.com/post/19279778476/entity-component-systems-inheritance-vs-composition" rel="nofollow">http://louisstowasser.com/post/19279778476/entity-component-systems-inheritance-vs-composition</a></div>
</li>
<li class="level1"><div class="li"> <a href="http://t-machine.org/index.php/2012/03/16/entity-systems-what-makes-good-components-good-entities/" class="urlextern" title="http://t-machine.org/index.php/2012/03/16/entity-systems-what-makes-good-components-good-entities/" rel="nofollow">http://t-machine.org/index.php/2012/03/16/entity-systems-what-makes-good-components-good-entities/</a></div>
</li>
<li class="level1"><div class="li"> <a href="http://entity-systems.wikidot.com/" class="urlextern" title="http://entity-systems.wikidot.com/" rel="nofollow">http://entity-systems.wikidot.com/</a></div>
</li>
</ul>

</div>
<!-- EDIT11 SECTION "The Smart Way to Add Custom Methods and Fields" [9192-12315] -->
<h3 class="sectionedit12" id="the_smart_way_to_access_game_features">The Smart Way to Access Game Features</h3>
<div class="level3">

<p>
<a href="/jme3/intermediate/simpleapplication.html" class="wikilink1" title="jme3:intermediate:simpleapplication">SimpleApplication</a> gives you access to game features such as a the rootNode, assetManager, guiNode, inputManager, audioManager, physicsSpace, viewPort, and the camera. But what if you need this access also from another class? Don't extend SimpleApplication a second time, and don't pass around tons of object references in constructors! Needing access to application level objects is a sign that this class should be designed as an <a href="/jme3/advanced/application_states.html" class="wikilink1" title="jme3:advanced:application_states">AppState</a> (read details there). 
</p>

<p>
An AppState has access to all game features in the SimpleApplication via the <code>this.app</code> and <code>this.stateManager</code> objects. Examples:
</p>
<pre class="code java">Spatial sky <span class="sy0">=</span> SkyFactory.<span class="me1">createSky</span><span class="br0">(</span><span class="kw1">this</span>.<span class="me1">app</span>.<span class="me1">getAssetManager</span><span class="br0">(</span><span class="br0">)</span>, <span class="st0">"sky.dds"</span>, <span class="kw2">false</span><span class="br0">)</span><span class="sy0">;</span>
...
<span class="kw1">this</span>.<span class="me1">app</span>.<span class="me1">getRootNode</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">attachChild</span><span class="br0">(</span> sky <span class="br0">)</span><span class="sy0">;</span></pre>

</div>
<!-- EDIT12 SECTION "The Smart Way to Access Game Features" [12316-13153] -->
<h3 class="sectionedit13" id="the_smart_way_to_implement_game_logic">The Smart Way to Implement Game Logic</h3>
<div class="level3">

<p>
As your SimpleApplication-based game grows more advanced, you find yourself putting more and more interactions in the <code>simpleUpdate()</code> loop, and your <code>simpleInitApp()</code> methods grows longer and longer. It's a best practice to move blocks of game mechanics into reusable component classes of their own. In jME3, these resuable classes are called <code>Controls</code> and <code>AppStates</code>.
</p>
<ul>
<li class="level1"><div class="li"> Use <a href="/jme3/advanced/application_states.html" class="wikilink1" title="jme3:advanced:application_states">AppStates</a> to implement <em>global game mechanics</em>. </div>
<ul>
<li class="level2"><div class="li"> Each AppState calls its own <code>initialize()</code> and <code>cleanup()</code> methods when it is attached to or detached from the game. </div>
</li>
<li class="level2"><div class="li"> Each AppState runs its own <em>thread-safe</em> <code>update()</code> loop that hooks into the main <code>simpleUpdate()</code> loop. </div>
</li>
<li class="level2"><div class="li"> You specify what happens if an AppState is paused/unpaused.</div>
</li>
<li class="level2"><div class="li"> You can use an AppState to switch between sets of AppStates.</div>
</li>
<li class="level2"><div class="li"> An AppState has access to everything in the SimpleApplication (rootNode, AssetManager, StateManager, InputListener, ViewPort, etc). </div>
</li>
</ul>
</li>
</ul>
<ul>
<li class="level1"><div class="li"> Use <a href="/jme3/advanced/custom_controls.html" class="wikilink1" title="jme3:advanced:custom_controls">Controls</a> to implement the <em>behaviour of game entities</em>. </div>
<ul>
<li class="level2"><div class="li"> Controls add a type of behaviour (methods and fields) to an individual Spatial (a player, an NPC). </div>
</li>
<li class="level2"><div class="li"> Each Control runs its own <em>thread-safe</em> <code>controlUpdate()</code> loop that hooks into the main <code>simpleUpdate()</code> loop. </div>
</li>
<li class="level2"><div class="li"> One Spatial can be influenced by several Controls. (!)</div>
</li>
<li class="level2"><div class="li"> Each Spatial needs its own instance of the Control. </div>
</li>
<li class="level2"><div class="li"> A Control only has control over and access to the spatial that it is attached to (and its sub-spatials).</div>
</li>
</ul>
</li>
</ul>

<p>
</p><p></p><div class="noteclassic">A game contains algorithms that do not directly affect spatials (for example, AI pathfinding code that calculates and chooses paths, but does not actually move spatials). You do not need to put such non-spatial code in controls, you can run thse things in a new thread. Only the tranformation code that actually modifies the spatial must be called from a control, or must be enqueue()ed.
</div>


<p>
Controls and AppStates often work together: An AppState can reach up to the application and <code>get</code> all Spatials from the rootNode that carry a specific Control, and perform a global action on them. Example: In BulletPhysics, all physical Spatials that carry RigidBodyControls are steered by the overall BulletAppState.
</p>

<p>
</p><p></p><div class="notetip">AppStates and Controls are extensions to a SimpleApplication. They are your modular building blocks to build a more complex game. In the ideal case, you move all init/update code into Controls and AppStates, and your simpleInitApp() and simpleUpdate() could end up virtually empty. This powerful and modular approach cleans up your code considerably. 
</div>


<p>
Read all about <a href="/jme3/advanced/custom_controls.html" class="wikilink1" title="jme3:advanced:custom_controls">Custom Controls</a> and <a href="/jme3/advanced/application_states.html" class="wikilink1" title="jme3:advanced:application_states">Application States</a> here.
</p>

</div>
<!-- EDIT13 SECTION "The Smart Way to Implement Game Logic" [13154-15956] -->
<h3 class="sectionedit14" id="optimize_application_performance">Optimize Application Performance</h3>
<div class="level3">
<ul>
<li class="level1"><div class="li"> <a href="/jme3/intermediate/optimization.html" class="wikilink1" title="jme3:intermediate:optimization">Optimization</a> – How to avoid wasting cycles</div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/advanced/multithreading.html" class="wikilink1" title="jme3:advanced:multithreading">Multithreading</a> – Use concurrency for long-running background tasks, but don't manipulate the scene graph from outside the main thread (update loop)!</div>
</li>
<li class="level1"><div class="li"> You can add a <a href="/sdk/debugging_profiling_testing.html" class="wikilink1" title="sdk:debugging_profiling_testing">Java Profiler</a> to the jMonkeyEngine SDK via Tools → Plugins → Available. The profiler presents statistics on the lifecycle of methods and objects. Performance problems may be caused by just a few methods that take long, or are called too often (try to cache values to avoid this). If object creation and garbage collection counts keep increasing, you are looking at a memory leak.</div>
</li>
</ul>

</div>
<!-- EDIT14 SECTION "Optimize Application Performance" [15957-16680] -->
<h3 class="sectionedit15" id="don_t_mess_with_geometric_state">Don't Mess With Geometric State</h3>
<div class="level3">

<p>
<strong>These tips are especially important for users who already know jME2.</strong> Automatic handling of the Geometric State has improved in jME3, and it is now a best practice to <em>not</em> mess with it.
</p>
<ul>
<li class="level1"><div class="li"> Do not call <code>updateGeometricState()</code> on anything but the root node!</div>
</li>
<li class="level1"><div class="li"> Do not override or mess with <code>updateGeometricState()</code> at all.</div>
</li>
<li class="level1"><div class="li"> Do not use <code>getLocalTranslation().set()</code> to move a spatial in jME3, always use <code>setLocalTranslation()</code>.</div>
</li>
</ul>

</div>
<!-- EDIT15 SECTION "Don't Mess With Geometric State" [16681-17170] -->
<h3 class="sectionedit16" id="maintain_internal_documentation">Maintain Internal Documentation</h3>
<div class="level3">

<p>
It's unlikely you will fully document <em>every</em> class you write, we hear you. However, you should at least write meaningful javadoc to provide context for your most crucial methods/parameters.
</p>
<ul>
<li class="level1"><div class="li"> What is this? How does it solve its task (input, algorithm used, output, side-effects)? </div>
</li>
<li class="level1"><div class="li"> Write down implicit limits (e.g. min/max values) and defaults while you still remember.</div>
</li>
<li class="level1"><div class="li"> In which situation do I want to use this, is this part of a larger process? Is this step required, or what are the alternatives? </div>
</li>
</ul>

<p>
Treat javadoc as messages to your future self. “genNextVal() generates the next value” and “@param float factor A factor influencing the result” do <em>not</em> count as documentation.
</p>

</div>
<!-- EDIT16 SECTION "Maintain Internal Documentation" [17171-17907] -->
<h2 class="sectionedit17" id="debugging_and_test_phase">Debugging and Test Phase</h2>
<div class="level2">

<p>
<strong>A <a href="/sdk/debugging_profiling_testing.html" class="wikilink1" title="sdk:debugging_profiling_testing">Java Debugger</a></strong> is included in the jMonkeyEngine SDK. It allows you to set a break point in your code near the line of code where an exception happens. Then you step through the execution line by line and watch object and variable states live, to detect where the bug starts.
</p>

<p>
<strong>Use the <a href="/jme3/advanced/logging.html" class="wikilink1" title="jme3:advanced:logging">Logger</a></strong> to print status messages during the development and debugging phase, instead of System.out.println(). The logger can be switched off with one line of code, whereas commenting out all your <code>println()</code>s takes a while.
</p>

<p>
<strong>Unit Testing (<a href="http://download.oracle.com/javase/1.4.2/docs/guide/lang/assert.html" class="urlextern" title="http://download.oracle.com/javase/1.4.2/docs/guide/lang/assert.html" rel="nofollow">Java Assertions</a>)</strong> has a different status in 3D graphics development than in other types of software. You cannot write assertions that automatically test whether the rendered image <em>looks</em> correct, or whether interactions are <em>intuitive</em>. Still you should <a href="/sdk/debugging_profiling_testing.html" class="wikilink1" title="sdk:debugging_profiling_testing">create simple test cases</a> for individual game features such as loaders, content generators, effects. Run the test cases now and then to see whether they still work as intended – or whether they are suffering from regressions or side-effects. Keep the test classes in the <code>test</code> directory of your project, don't include them in the distribution.
</p>

<p>
<strong>Quality Assurance (QA)</strong> means repeatedly checking a certain set of features that must work, but that might be unexpectedly broken as a side-effect. Every game has some crazy bugs somewhere – but basic tasks <em>must work</em>, no excuse. This includes installing and de-installing; saving and loading; changing options; starting, pausing, quitting; basic actions such as walking, fighting, etc. After every milestone, you go through your QA list again and systematically look for regressions or newly introduced bugs. Check the application <em>on every supported operating system and hardware</em> (!) because not all graphic cards support the same features. If you don't find the obvious bugs, your users will, and carelessness will put them off.
</p>

<p>
<strong>Alpha and Beta Testing</strong> means that you ask someone to try to install and run your game. It should be a real user situation, where they are left to figure out the installation and gameplay by themselves–you only can include the usual read-me and help docs. Provide the testers with an easy method to report back what problems they encountered, what they liked best, or why they gave up. Evaluate whether reported problems are one-off glitches, or whether they must be fixed for the game to be playable for everyone.
</p>

</div>
<!-- EDIT17 SECTION "Debugging and Test Phase" [17908-20524] -->
<h2 class="sectionedit18" id="release_phase">Release Phase</h2>
<div class="level2">

</div>
<!-- EDIT18 SECTION "Release Phase" [20525-20551] -->
<h3 class="sectionedit19" id="pre-release_to-do_list">Pre-Release To-Do List</h3>
<div class="level3">
<ul>
<li class="level1"><div class="li"> Prepare a web page, a cool slogan, advertisements, etc</div>
</li>
<li class="level1"><div class="li"> Verify that all assets are up-to-date and converted to .j3o. </div>
</li>
<li class="level1"><div class="li"> Verify that your code loads the optimized .j3o files, and not the original model formats.</div>
</li>
<li class="level1"><div class="li"> Prepare licenses of assets that you use for inclusion. (You <em>did</em> obtain permission to use them, right…?)</div>
</li>
<li class="level1"><div class="li"> Switch off fine <a href="/jme3/advanced/logging.html" class="wikilink1" title="jme3:advanced:logging">logging</a> output.</div>
</li>
<li class="level1"><div class="li"> Prepare promotional art: The most awesome screenshots (in thumbnail, square, vertical, horizontal, and fullscreen formats) and video clips. Include name, contact info, slogan, etc., so future customers can find you.</div>
</li>
<li class="level1"><div class="li"> Prepare a readme.txt file, or installation guide, or handbook – if applicable.</div>
</li>
<li class="level1"><div class="li"> Get a certificate if one is required for your distribution method (see below).</div>
</li>
<li class="level1"><div class="li"> Specify a <a href="http://en.wikipedia.org/wiki/Video_game_content_rating_system#Comparison" class="urlextern" title="http://en.wikipedia.org/wiki/Video_game_content_rating_system#Comparison" rel="nofollow">classification rating</a> (needed for e.g. app stores).</div>
</li>
</ul>

</div>
<!-- EDIT19 SECTION "Pre-Release To-Do List" [20552-21503] -->
<h3 class="sectionedit20" id="distributing_the_executables">Distributing the Executables</h3>
<div class="level3">

<p>
The <a href="/sdk/application_deployment.html" class="wikilink1" title="sdk:application_deployment">jMonkeyEngine SDK helps you with deployment</a>: You specify your branding and deployment options in the Project Properties dialog, and then choose Clean and Build from the context menu. <strong>If you use another IDE, consult this IDE's documentation.</strong>
</p>

<p>
Decide whether you want to release your game as WebStart, desktop JAR, mobile APK, or browser Applet – Each has its pros and cons.
</p>
<div class="table sectionedit21"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0">Distribution</th><th class="col1">Pros</th><th class="col2">Cons</th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0">Desktop Launcher <br />
(.EXE, .app, .jar+.sh)</td><td class="col1">This is the standard way of distributing desktop applications. The jMonkeyEngine SDK can be configured to automatically create zipped launchers for each operating system. </td><td class="col2">You need to offer three separate, platform-dependent downloads.</td>
	</tr>
	<tr class="row2">
		<td class="col0">Desktop Application <br />
(.JAR)</td><td class="col1">Platform independent desktop application. </td><td class="col2">User must have Java configured to run JARs when they are opened; or user must know how to run JARs from command line; or you must provide a custom JAR wrapper.</td>
	</tr>
	<tr class="row3">
		<td class="col0">Web Start <br />
(.JNLP)</td><td class="col1">The user accesses a <abbr title="Uniform Resource Locator">URL</abbr>, saves the game as one executable file. Easy process, no installer required. You can allow the game to be played offline.</td><td class="col2">Users need network connection to install the game. Downloading bigger games takes a while as opposed to running them from a CD. </td>
	</tr>
	<tr class="row4">
		<td class="col0">Browser Applet <br />
(.<abbr title="HyperText Markup Language">HTML</abbr>+.JAR)</td><td class="col1">Easy to access and play game via most web browsers. Userfriendly solution for quick small games.</td><td class="col2">Game only runs in the browser. Game or settings cannot be saved to disk. Some restrictions in default camera navigation (jME cannot capture mouse.)</td>
	</tr>
	<tr class="row5">
		<td class="col0">Android <br />
(.APK)</td><td class="col1">Game runs on Android devices.</td><td class="col2">Android devices do not support post-procesor effects.</td>
	</tr>
</table></div>
<!-- EDIT21 TABLE [21957-23177] -->
<p>
Which ever method you choose, a Java-Application works on the main operating systems: Windows, Mac <abbr title="Operating System">OS</abbr>, Linux, Android.
</p>

<p>
The distribution appears in a newly generated <code>dist</code> directory inside your project directory. These are the files that you upload or burn to CD to distribute to your customers.
</p>
<hr />

<p>
See also:
</p>
<ul>
<li class="level1"><div class="li"> <a href="http://www.gamedev.net/page/resources/_/creative/game-design/developing-your-game-concept-by-making-a-design-document-r3004" class="urlextern" title="http://www.gamedev.net/page/resources/_/creative/game-design/developing-your-game-concept-by-making-a-design-document-r3004" rel="nofollow">gamedev.net: Developing Your Game Concept By Making A Design Document</a></div>
</li>
</ul>

</div>
<!-- EDIT20 SECTION "Distributing the Executables" [21504-] -->
