---
title: jMonkeyEngine SDK: Scene Composer
---
<h1 class="sectionedit1" id="jmonkeyengine_sdkscene_composer">jMonkeyEngine SDK: Scene Composer</h1>
<div class="level1">

<p>
SceneComposer allows you to edit scenes stored in j3o files and add content or modify existing content. Please note that the Scene Composer and Explorer are a work in progress and will provide more powerful functions in the future. Also other plugins will allow creation of more specific game type scenes in jMonkeyEngine SDK.
</p>

<p>
Most buttons in the SceneComposer have tooltips that appear when you hover the mouse over the button for a short while.
</p>

</div>
<!-- EDIT1 SECTION "jMonkeyEngine SDK: Scene Composer" [1-498] -->
<h3 class="sectionedit2" id="mouse_cursor_controls">Mouse/Cursor Controls</h3>
<div class="level3">
<ul>
<li class="level1"><div class="li"> Left-click and drag to rotate the camera around the cam center</div>
</li>
<li class="level1"><div class="li"> Right-click and drag to move the cam center</div>
</li>
<li class="level1"><div class="li"> Scoll the mouse wheel to zoom in/out the cam center</div>
</li>
<li class="level1"><div class="li"> Left-click a geometry to select it</div>
</li>
<li class="level1"><div class="li"> Right-click a geometry to place the cursor</div>
</li>
</ul>

<p>
In the SceneComposer toolbar are buttons to snap the camera to the cursor, snap the cursor to the selection and etc.
</p>

</div>
<!-- EDIT2 SECTION "Mouse/Cursor Controls" [499-907] -->
<h3 class="sectionedit3" id="creating_a_scene_file">Creating a scene file</h3>
<div class="level3">

<p>
The jMonkeyEngine SDK stores the scene in a j3o file, this binary file contains the whole scenegraph including all settings for spatials, materials, physics, effects etc. Textures are not stored in the j3o file but as absolute locators to the textures.
</p>

<p>
To create a blank scene file do the following:
</p>
<ol>
<li class="level1"><div class="li"> Right click the “Scenes” folder in your Project Assets and select “New→Other”</div>
</li>
<li class="level1"><div class="li"> Select “Scene” to the left then select “Empty jME3 Scene” and press “Next”</div>
</li>
<li class="level1"><div class="li"> Enter a file name for your scene like “MyScene” and press “OK”</div>
</li>
</ol>

</div>
<!-- EDIT3 SECTION "Creating a scene file" [908-1471] -->
<h3 class="sectionedit4" id="loading_the_scene">Loading the scene</h3>
<div class="level3">

<p>
<a href="/resources/sdk-jmonkeyplatform-docu-2.png" class="media" title="sdk:jmonkeyplatform-docu-2.png"><img src="/resources/sdk-jmonkeyplatform-docu-2.png" class="mediaright" alt="" width="421" height="298" /></a>
</p>

<p>
To open a scene
</p>
<ol>
<li class="level1"><div class="li"> In the Project Explorer, right-click the *.j3o file of the scene</div>
</li>
<li class="level1"><div class="li"> Choose “Open in SceneComposer”</div>
</li>
</ol>

<p>
Now the SceneComposer window opens at the bottom and displays the scene in the SceneViewer. The SceneExplorer displays the contained scene graph as a tree and when selecting a node, you can edit the properties of the corresponding scene graph object in the Properties window.
</p>

<p>
For now, you only see the cursor in the SceneViewer and a single node (the root node of the scene) in the SceneExplorer.
</p>

</div>
<!-- EDIT4 SECTION "Loading the scene" [1472-2066] -->
<h3 class="sectionedit5" id="adding_light_to_the_scene">Adding light to the scene</h3>
<div class="level3">
<ol>
<li class="level1"><div class="li"> Select the root node in the SceneExplorer</div>
</li>
<li class="level1"><div class="li"> Select “Directional Light” in the SceneComposer window</div>
</li>
<li class="level1"><div class="li"> Press the “+” button in the SceneComposer window</div>
</li>
</ol>

<p>
A directional light has been added to your scene, you can see it in the SceneExplorer.
</p>

</div>
<!-- EDIT5 SECTION "Adding light to the scene" [2067-2350] -->
<h3 class="sectionedit6" id="adding_effects_etc_to_the_scene">Adding effects etc. to the scene</h3>
<div class="level3">

<p>
You can add a variety of special objects with the SceneComposer, including lights, effects, audio etc.
</p>
<ol>
<li class="level1"><div class="li"> Select root Node in the SceneExplorer</div>
</li>
<li class="level1"><div class="li"> Select the object type in the list displayed in the SceneComposer window</div>
</li>
<li class="level1"><div class="li"> Press the “+ cursor” button in the SceneComposer window</div>
</li>
</ol>

</div>
<!-- EDIT6 SECTION "Adding effects etc. to the scene" [2351-2678] -->
<h3 class="sectionedit7" id="adding_models_to_the_scene">Adding Models to the scene</h3>
<div class="level3">

<p>
<a href="/resources/sdk-jmonkeyplatform-docu-3.png" class="media" title="sdk:jmonkeyplatform-docu-3.png"><img src="/resources/sdk-jmonkeyplatform-docu-3.png" class="mediaright" alt="" width="421" height="298" /></a>
</p>

<p>
You can directly import 3d models to your scene so that they will be part of your scene file. To be able to import for example an OgreXML file, first export it from your 3D editor to a separate folder in the assets folder of your project (e.g. assets/Models/MyModel/).
</p>
<ol>
<li class="level1"><div class="li"> Place the SceneComposer cursor where you want the model to be</div>
</li>
<li class="level1"><div class="li"> Select the parent Node for the model in the SceneExplorer</div>
</li>
<li class="level1"><div class="li"> In the Project Explorer right-click the model file you want to import</div>
</li>
<li class="level1"><div class="li"> Choose “Add to SceneComposer”</div>
</li>
</ol>

<p>
Note that when importing a model the texture paths are stored absolute, so the folder you import the model from will later only be a textures folder because the original model file is not included in the release.
</p>

<p>
Also note that when adding models this way, changes in the original model file will not be reflected in the scene file as its a complete copy of the original file. If you change the original model, delete the models node from the scene and import it again.
</p>

</div>
<!-- EDIT7 SECTION "Adding Models to the scene" [2679-3741] -->
<h3 class="sectionedit8" id="linking_models_to_the_scene">Linking Models to the scene</h3>
<div class="level3">

<p>
You can also link models/objects into your scene, this way they are reloaded dynamically from the other/original file.
</p>
<ol>
<li class="level1"><div class="li"> Place the SceneComposer cursor where you want the model to be</div>
</li>
<li class="level1"><div class="li"> Select the parent Node for the model in the SceneExplorer</div>
</li>
<li class="level1"><div class="li"> In the Project Explorer right-click the model file you want to link</div>
</li>
<li class="level1"><div class="li"> Choose “Link in SceneComposer”</div>
</li>
</ol>

<p>
Note that when linking objects this way, you cannot edit them as part of the scene. To change the model you have to change the original j3o file.
</p>

<p>
Also note that although it its possible to directly link external model files (OgreXML, OBJ etc.), this is not recommended. Convert the original file to a j3o file by right-clicking it and selecting “Convert to jME Binary” before linking it. This is required because the original model files are not included in the release version of the application.
</p>

</div>
<!-- EDIT8 SECTION "Linking Models to the scene" [3742-4636] -->
<h3 class="sectionedit9" id="saving_the_scene">Saving the Scene</h3>
<div class="level3">
<ol>
<li class="level1"><div class="li"> When a scene has been changed, press the “save” button in the main toolbar or press [Ctrl-S] / [Apple-S] to save it.</div>
</li>
</ol>
<div class="tags"><span>
	<a href="/tag/documentation.html" class="wikilink1" title="tag:documentation" rel="tag">documentation</a>,
	<a href="/tag/sdk.html" class="wikilink1" title="tag:sdk" rel="tag">sdk</a>,
	<a href="/tag/scene.html" class="wikilink1" title="tag:scene" rel="tag">scene</a>,
	<a href="/tag/node.html" class="wikilink1" title="tag:node" rel="tag">node</a>,
	<a href="/tag/asset.html" class="wikilink1" title="tag:asset" rel="tag">asset</a>,
	<a href="/tag/light.html" class="wikilink1" title="tag:light" rel="tag">light</a>,
	<a href="/tag/effect.html" class="wikilink1" title="tag:effect" rel="tag">effect</a>
</span></div>

</div>
<!-- EDIT9 SECTION "Saving the Scene" [4637-] -->
