---
title: jMonkeyEngine SDK: Importing and Viewing Models
---
<h1 class="sectionedit1" id="jmonkeyengine_sdkimporting_and_viewing_models">jMonkeyEngine SDK: Importing and Viewing Models</h1>
<div class="level1">

<p>
The jMonkeyEngine SDK imports models from your project and stores them in the assets folder. The imported models are converted to a jME3 compatible binary format called .j3o. Double-click .j3o files in the jMonkeyEngine SDK to display them in the SceneViewer, or load them in-game using the AssetManager.
</p>

<p>
Presently, <a href="http://www.blender.org/" class="urlextern" title="http://www.blender.org/" rel="nofollow">Blender 3D</a> is the preferred modelling tool for jME3 as it is also Open-Source Software and an exporter for OgreXML files exists. There is a direct .blend file importer available in the SDK and you can directly import or store blend files in your project to convert them. If for some reason your version of blender is not compatible, you can use the default OgreXML format. Note that the OgreXML exporter is not compatible with Blender 2.49 or before!
</p>

<p>
Also, see this <a href="http://www.youtube.com/watch?v=nL7woH40i5c" class="urlextern" title="http://www.youtube.com/watch?v=nL7woH40i5c" rel="nofollow">demo video</a> on importing models.
</p>

</div>
<!-- EDIT1 SECTION "jMonkeyEngine SDK: Importing and Viewing Models" [1-955] -->
<h3 class="sectionedit2" id="installing_the_ogrexml_exporter_in_blender">Installing the OgreXML Exporter in Blender</h3>
<div class="level3">

<p>
The jMonkeyEngine SDK includes a tool to install the correct exporter tools in Blender to export OgreXML files. To install the exporter, do the following:
</p>
<ol>
<li class="level1"><div class="li"> Select “Tools”→“OgreXML”→“Install Blender OgreXML” in the jMonkeyEngine SDK Menu</div>
</li>
<li class="level1"><div class="li"> If you are presented a filechooser, select the folder where your blender scripts reside</div>
</li>
<li class="level1"><div class="li"> Press “Install” in the window that opens</div>
</li>
</ol>

<p>
Also check out <a href="/jme3/external/blender.html" class="wikilink1" title="jme3:external:blender">how to create compatible models in blender</a> and <a href="/jme3/intermediate/multi-media_asset_pipeline.html" class="wikilink1" title="jme3:intermediate:multi-media_asset_pipeline">how to organize your assets</a>.
</p>

</div>
<!-- EDIT2 SECTION "Installing the OgreXML Exporter in Blender" [956-1555] -->
<h2 class="sectionedit3" id="importing_and_viewing_a_model">Importing and Viewing a Model</h2>
<div class="level2">

</div>
<!-- EDIT3 SECTION "Importing and Viewing a Model" [1556-1597] -->
<h3 class="sectionedit4" id="using_the_model_importer_tool">Using the Model Importer Tool</h3>
<div class="level3">

<p>
jMonkeyEngine SDK includes a model importer tool that allows you to preview and import supported models into your jMonkeyEngine3 project.
</p>

<p>
<a href="/resources/wp-uploads-2010-11-jmonkeyplatform003-300x117.jpg" class="media wikilink2" title="wp-uploads:2010:11:jmonkeyplatform003-300x117.jpg"><img src="/resources/wp-uploads-2010-11-jmonkeyplatform003-300x117.jpg" class="media" title="jmonkeyplatform003-300x117.jpg" alt="jmonkeyplatform003-300x117.jpg" /></a>
<a href="/resources/wp-uploads-2010-11-jmonkeyplatform002-300x218.jpg" class="media wikilink2" title="wp-uploads:2010:11:jmonkeyplatform002-300x218.jpg"><img src="/resources/wp-uploads-2010-11-jmonkeyplatform002-300x218.jpg" class="mediaright" title="jmonkeyplatform002-300x218.jpg" alt="jmonkeyplatform002-300x218.jpg" /></a>
</p>
<ol>
<li class="level1"><div class="li"> Select the project you want to import your model to</div>
</li>
<li class="level1"><div class="li"> Click the “Import Model” button in the toolbar</div>
</li>
<li class="level1"><div class="li"> Click “open model..” and select the main model file</div>
</li>
<li class="level1"><div class="li"> Check the preview and file list and press “Next”</div>
</li>
<li class="level1"><div class="li"> Check and change the import path if necessary</div>
</li>
<li class="level1"><div class="li"> If you want to copy the original model files as well, check the checkbox</div>
</li>
<li class="level1"><div class="li"> Press “finish”</div>
</li>
</ol>

<p>
The model is converted to j3o and all necessary files are copied to the project assets folder. If you have specified the corresponding option, all original model files will also be copied to your assets folder.
</p>

</div>
<!-- EDIT4 SECTION "Using the Model Importer Tool" [1598-2463] -->
<h3 class="sectionedit5" id="using_the_model_files_directly">Using the model files directly</h3>
<div class="level3">

<p>
<a href="/resources/sdk-jmonkeyplatform-docu-2.png" class="media" title="sdk:jmonkeyplatform-docu-2.png"><img src="/resources/sdk-jmonkeyplatform-docu-2.png" class="mediaright" alt="" width="421" height="298" /></a>
</p>
<ol>
<li class="level1"><div class="li"> Create a separate folder for each model in the <code>assets</code> folder of your project.</div>
</li>
<li class="level1"><div class="li"> Save the model created in Blender (.blend) <strong>in the <code>asset</code> folder of your project</strong>, </div>
</li>
<li class="level1"><div class="li"> Make sure that no textures are packed in the .blend file.</div>
</li>
<li class="level1"><div class="li"> Make sure all textures used in the .blend file are in the assets folder of the project.</div>
</li>
<li class="level1"><div class="li"> In the Projects Explorer Assets node, select the model that you want to import.</div>
</li>
<li class="level1"><div class="li"> Double-click the model or right-click and select “Convert to JME binary” from the context-menu.</div>
</li>
<li class="level1"><div class="li"> In the Projects Explorer Assets node you should see your model j3o file.</div>
</li>
<li class="level1"><div class="li"> Double-click it to view it in the SceneViewer.</div>
</li>
<li class="level1"><div class="li"> Click on the lightbulb to turn on the light if you cannot see your model.</div>
</li>
</ol>

<p>
Note: It is important that you copy the model file and its textures to the correct assets folder before creating the j3o file because the paths for textures (and possibly other things) will be stored as absolute (to the assets folder root) when you convert that model. This means the texture location should not change after the import.
</p>

<p>
Note: If the SceneViewer doesn't work refer to <a href="/sdk/troubleshooting.html" class="wikilink1" title="sdk:troubleshooting">Troubleshooting jMonkeyEngine3 SDK</a>.
</p>

</div>
<!-- EDIT5 SECTION "Using the model files directly" [2464-3719] -->
<h2 class="sectionedit6" id="working_with_a_model">Working With a Model</h2>
<div class="level2">
<ul>
<li class="level1"><div class="li"> Open Windows&gt;SceneExplorer to view sub-nodes of the model</div>
</li>
<li class="level1"><div class="li"> Open Windows&gt;Properties to view the properties of the model's nodes.</div>
</li>
<li class="level1"><div class="li"> Click the cube button in the SceneViewer to toggle between Wireframe mode and Textured mode.</div>
</li>
<li class="level1"><div class="li"> Click the lightbulb to view Materials that require a light source</div>
</li>
</ul>

</div>
<!-- EDIT6 SECTION "Working With a Model" [3720-4055] -->
<h2 class="sectionedit7" id="notes_about_model_assets">Notes About Model Assets</h2>
<div class="level2">

<p>
The original OgreXML <code>.mesh.xml</code>, <code>.scene</code>, <code>.material</code>, <code>.skeleton.xml</code> and <code>.blend</code> model files <strong>will not be included</strong> in the distribution <code>assets.jar</code> file of your distributed game, they are only available in the assets folder so you are able to recreate the <code>.j3o</code> file from the original if you ever come to change it in blender and have to export it again.
</p>

</div>
<!-- EDIT7 SECTION "Notes About Model Assets" [4056-4472] -->
<h2 class="sectionedit8" id="about_the_sceneviewer_and_sceneexplorer_window">About the SceneViewer and SceneExplorer window</h2>
<div class="level2">

<p>
The SceneViewer and SceneExplorer windows are shared among plugins to save system resources. This means that you will have to keep an eye on what plugin is using the scene right now and what you are actually modifying in these windows.
</p>

<p>
Most plugins will deliver their own UI elements to modify the scene so the SceneExplorer is more of a global tool. The simple SceneComposer however heavily relies on its functions as other plugins might too in the future.
</p>

</div>
<!-- EDIT8 SECTION "About the SceneViewer and SceneExplorer window" [4473-4992] -->
<h3 class="sectionedit9" id="about_the_projects_assetmanager">About the projects AssetManager</h3>
<div class="level3">

<p>
Each jMonkeyEngine SDK project has its own internal AssetManager that has the projects assets folder registered as a FileLocator. When the project is run, the assets folder is compressed into a jar file and added to the projects main jar classpath. This way the editors in jMonkeyEngine SDK and the running game have the same asset folder structure.
</p>

<p>
You might wonder why jMonkeyEngine SDK requires you to copy the model that is to be converted to j3o into the assets folder before. The Model Import Tool also copies the model and associated files to the project directory before converting. To load the model it needs to be in a folder (or jar etc..) that belongs to the projects AssetManager root. To load a model from some other folder of the filesystem, that folder would have to be added to the AssetManager root. If every folder that contains a model was in the root of the AssetManager, all textures named “hull.jpg” for example would be the same for the AssetManager and it would only deliver the texture of the first model folder that was added.
</p>

<p>
To have a valid jME3 object, the paths to textures and other assets belonging to the model have to be read with the correct, final path that can then be stored in the j3o object. The j3o object will use those paths when it is loaded with the AssetManager and it requires the AssetManager to deliver the assets on those paths, this is why the folder structure while converting has to be the same as when loading.
</p>
<div class="tags"><span>
	<a href="/tag/documentation.html" class="wikilink1" title="tag:documentation" rel="tag">documentation</a>,
	<a href="/tag/sdk.html" class="wikilink1" title="tag:sdk" rel="tag">sdk</a>,
	<a href="/tag/tool.html" class="wikilink1" title="tag:tool" rel="tag">tool</a>,
	<a href="/tag/asset.html" class="wikilink1" title="tag:asset" rel="tag">asset</a>,
	<a href="/tag/scene.html" class="wikilink1" title="tag:scene" rel="tag">scene</a>
</span></div>

</div>
<!-- EDIT9 SECTION "About the projects AssetManager" [4993-] -->
