---
title: jMonkeyEngine SDK: Scene Explorer
---
<h1 class="sectionedit1" id="jmonkeyengine_sdkscene_explorer">jMonkeyEngine SDK: Scene Explorer</h1>
<div class="level1">

<p>
<a href="/resources/sdk-jmonkeyplatform-sceneexplorer-add.jpg" class="media" title="sdk:jmonkeyplatform-sceneexplorer-add.jpg"><img src="/resources/sdk-jmonkeyplatform-sceneexplorer-add.jpg" class="mediacenter" title="jmonkeyplatform-sceneexplorer-add.jpg" alt="jmonkeyplatform-sceneexplorer-add.jpg" /></a>
</p>

</div>
<!-- EDIT1 SECTION "jMonkeyEngine SDK: Scene Explorer" [1-98] -->
<h2 class="sectionedit2" id="about_the_sceneexplorer_window">About the SceneExplorer window</h2>
<div class="level2">

<p>
The SceneExplorer gives you a structural overview of the currently edited scene and is active among all plugins
</p>

<p>
Most plugins will deliver their own UI elements to modify the scene so the SceneExplorer is more of a global tool. The simple SceneComposer however heavily relies on its functions as other plugins might too in the future.
</p>

</div>
<!-- EDIT2 SECTION "About the SceneExplorer window" [99-477] -->
<h2 class="sectionedit3" id="using_the_sceneexplorer">Using the SceneExplorer</h2>
<div class="level2">

<p>
The SceneExplorer displays Nodes in a tree that represents the tree of Spatials in your scene. Spatial controls, lights and geometry meshes are also displayed in the tree.
</p>

<p>
SceneExplorer works in conjunction with SceneComposer, the default editor for J3O files in the jMonkeyEngine IDE.  If SceneExplorer doesn't appear when you select “Edit in SceneComposer”, choose Window → SceneExplorer from the menu bar to reveal the window.
</p>

</div>
<!-- EDIT3 SECTION "Using the SceneExplorer" [478-947] -->
<h3 class="sectionedit4" id="editing_objects_in_the_scene">Editing Objects in the scene</h3>
<div class="level3">
<ol>
<li class="level1"><div class="li"> Select a node in the SceneExplorer window (Open via Window→SceneExplorer if not open)</div>
</li>
<li class="level1"><div class="li"> Edit the node in the Properties window (Open via Window→Properties if not open)</div>
</li>
<li class="level1"><div class="li"> You can rename a Spatial by right clicking it or by slowly double-clicking the node</div>
</li>
</ol>

</div>
<!-- EDIT4 SECTION "Editing Objects in the scene" [948-1252] -->
<h3 class="sectionedit5" id="reorganizing_objects_in_the_scene">Reorganizing Objects in the scene</h3>
<div class="level3">
<ol>
<li class="level1"><div class="li"> You can cut, copy and paste Nodes in the SceneExplorer with the normal keyboard commands or the right-click menu of the Nodes</div>
</li>
<li class="level1"><div class="li"> You can move single object within the SceneExplorer tree by dragging&amp;dropping them</div>
</li>
</ol>

</div>
<!-- EDIT5 SECTION "Reorganizing Objects in the scene" [1253-1515] -->
<h3 class="sectionedit6" id="adding_objects_to_the_scene">Adding Objects to the scene</h3>
<div class="level3">

<p>
Right-click a Spatial or Node in the SceneExplorer to add other Spatials like ParticleEmitters or Lights, you can also add UserData to a Spatial that can be read during runtime.
</p>
<div class="tags"><span>
	<a href="/tag/documentation.html" class="wikilink1" title="tag:documentation" rel="tag">documentation</a>,
	<a href="/tag/sdk.html" class="wikilink1" title="tag:sdk" rel="tag">sdk</a>,
	<a href="/tag/tool.html" class="wikilink1" title="tag:tool" rel="tag">tool</a>,
	<a href="/tag/scene.html" class="wikilink1" title="tag:scene" rel="tag">scene</a>,
	<a href="/tag/node.html" class="wikilink1" title="tag:node" rel="tag">node</a>
</span></div>

</div>
<!-- EDIT6 SECTION "Adding Objects to the scene" [1516-] -->
