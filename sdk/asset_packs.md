---
title: jMonkeyEngine SDK: AssetPacks and AssetPack Browser
---
<h1 class="sectionedit1" id="jmonkeyengine_sdkassetpacks_and_assetpack_browser">jMonkeyEngine SDK: AssetPacks and AssetPack Browser</h1>
<div class="level1">

<p>
AssetPacks are a way to package jME3 compatible assets (like models, textures, sounds and whole scenes!) into a package that contains publisher info, license info, descriptions etc. for all of the assets. An AssetPack basically consists of an <code>assetpack.xml</code> file that describes the content and an <code>assets</code> folder that contains the content. The integrated browser in the jMonkeyEngine SDK allows you to add the assets from installed AssetPacks to any jme3 project scene you are working on. 
</p>

</div>
<!-- EDIT1 SECTION "jMonkeyEngine SDK: AssetPacks and AssetPack Browser" [1-563] -->
<h2 class="sectionedit2" id="the_assetpack_browser">The AssetPack Browser</h2>
<div class="level2">

<p>
<a href="/resources/sdk-assetpackbrowser-300x166.jpg" class="media" title="sdk:assetpackbrowser-300x166.jpg"><img src="/resources/sdk-assetpackbrowser-300x166.jpg" class="mediaright" alt="" /></a>
</p>

</div>
<!-- EDIT2 SECTION "The AssetPack Browser" [564-638] -->
<h3 class="sectionedit3" id="browsing_assets">Browsing Assets</h3>
<div class="level3">

<p>
The AssetPack browser in jMonkeyEngine SDK makes browsing the installed AssetPacks easy. Browse categories, search for tags and find the right asset for your project. When you have found it, you can add it with one click to your current scene. The AssetPack manager will automagically copy all needed textures, sounds etc. to your projects assets folder.
</p>

<p>
</p><p></p><div class="notetip">You can also browse a selection of online assetpacks that are available on jMonkeyEngine.org for download and install them to your jMonkeyEngine SDK's AssetPack browser.
</div>


<p>
The AssetPack browser uses a predefined directory to store the AssetPacks which is also used for new AssetPack projects. You can see and change the folder path in the AssetPack preferences (jMonkeyEngine SDK→Settings).
</p>

</div>
<!-- EDIT3 SECTION "Browsing Assets" [639-1430] -->
<h3 class="sectionedit4" id="adding_assets_to_your_scene">Adding Assets to Your Scene</h3>
<div class="level3">

<p>
To preview a model from the browser, right-click it and select “Preview Asset”
</p>

<p>
To add a model from the AssetPack browser to a scene do the following:
</p>
<ol>
<li class="level1"><div class="li"> Create a new scene (j3o) file or use an existing one</div>
</li>
<li class="level1"><div class="li"> Open it in the SceneComposer by right-clicking it and selecting “Edit in SceneComposer”</div>
</li>
<li class="level1"><div class="li"> Select the root node of the scene (or another node you want to add the model to)</div>
</li>
<li class="level1"><div class="li"> Right-click a model in the AssetBrowser and select “Add to SceneComposer”</div>
</li>
</ol>

<p>
The model will be added to your scene and all needed texture files will be copied to your projects assets folder.
</p>

</div>
<!-- EDIT4 SECTION "Adding Assets to Your Scene" [1431-2047] -->
<h2 class="sectionedit5" id="create_your_own_assetpack_project">Create Your Own AssetPack Project</h2>
<div class="level2">

<p>
AssetPack projects are a way to create your own AssetPacks, either for personal use or for publishing. With this project type in jMonkeyEngine SDK you can create a library of assets on your computer that you can use in any of your projects via the AssetPack browser.
Editing of asset and project info, adding of new assets and setting their properties, everything you need to create and publish your AssetPacks is there.
</p>
<ol>
<li class="level1"><div class="li"> Choose “File → New Project” from the menu</div>
</li>
<li class="level1"><div class="li"> Choose “AssetPack Project”</div>
</li>
<li class="level1"><div class="li"> Fill in the project info and press “finish”</div>
</li>
</ol>

<p>
You can access and change the project properties by right-clicking the project and selecting “Properties”.
</p>

</div>
<!-- EDIT5 SECTION "Create Your Own AssetPack Project" [2048-2751] -->
<h3 class="sectionedit6" id="add_your_own_assets">Add Your Own Assets</h3>
<div class="level3">

<p>
<a href="/resources/sdk-assetpackimport-300x222.jpg" class="media" title="sdk:assetpackimport-300x222.jpg"><img src="/resources/sdk-assetpackimport-300x222.jpg" class="mediaright" alt="" /></a>
</p>

<p>
To add new assets to your AssetPack do the following:
</p>
<ol>
<li class="level1"><div class="li"> Right-Click the “Assets” node of the AssetPack project</div>
</li>
<li class="level1"><div class="li"> Select “Add Asset..”</div>
</li>
<li class="level1"><div class="li"> Specify the info about your asset and press Next</div>
</li>
<li class="level1"><div class="li"> Press the “add files” button and select all files belonging to your asset</div>
</li>
<li class="level1"><div class="li"> Select the “main” checkbox for the main model file if your asset is a model file</div>
</li>
<li class="level1"><div class="li"> Change the asset paths and types if needed and press “finish”</div>
</li>
</ol>

<p>
The global asset type can be “model”, “scene”, “texture”, “sound”, “shader” or “other”
</p>

<p>
With the “model” or “scene” types, the AssetPack browser will try to load and add a model file from the selected assets when the user selects “Add to SceneComposer”. Specify the “load this model with material” flag for the model file that should be loaded via the AssetManager, you can also specify multiple mesh or scene files to be loaded. All texture and other needed files will be copied to the users project folder.
</p>

<p>
On the “Add Files” page you define the path of the files in the AssetPack. The importer tries to generate a proper path from the info entered on the first page. Note that for j3o binary models, the texture paths have to be exactly like they were during conversion. The given paths will also be used when copying the data to the users “assets” folder.
</p>

<p>
With the “add files” button you can open a file browser to select files from your harddisk that will be copied into the <code>assets/</code> folder of the AssetPack project. With the “add existing” button you can add a file thats already in your AssetPack assets folder to a new asset item. This way you can reuse e.g. textures for asset items or make items for an existing collection of asset files that you copied to the projects assets folder.
</p>

<p>
<a href="/resources/sdk-assetpackimport2-300x179.jpg" class="media" title="sdk:assetpackimport2-300x179.jpg"><img src="/resources/sdk-assetpackimport2-300x179.jpg" class="mediaright" alt="" /></a>
</p>

<p>
You can specify a specific material to be used for the single mesh/scene files, just select it in the dropdown below the mesh or scene file. If you don't select a material file here, the first found material file is used or none if none is found.
</p>

<p>
If the material file is an Ogre material file (.material) it will be used for loading an Ogre scene or mesh file. If it is a jMonkeyEngine3 material file (.j3m), it will be applied to the mesh regardless of model type. Note that for j3o models you don't need material files as the material is stored inside the j3o file.
</p>

<p>
</p><p></p><div class="notetip">In your AssetPack Project, right-click each asset and select “preview asset” to see your model. Verify hat it looks correctly, because then it should work for other users as well.
</div>


<p>
You can change the single assets properties in the properties window after you have added them. Just select an asset and open the properties window (Windows→Properties).
</p>

<p>
Supported formats for models (main files) are:
</p>
<ol>
<li class="level1"><div class="li"> OgreXML .mesh.xml / .scene</div>
</li>
<li class="level1"><div class="li"> Wavefront .obj</div>
</li>
<li class="level1"><div class="li"> jMonkeyEngine3 .j3o</div>
</li>
<li class="level1"><div class="li"> Blender .blend (unpack textures)</div>
</li>
</ol>

</div>
<!-- EDIT6 SECTION "Add Your Own Assets" [2752-5683] -->
<h3 class="sectionedit7" id="assetpack_publishing">AssetPack Publishing</h3>
<div class="level3">

<p>
<a href="/resources/sdk-assetpackdownload-263x300.jpg" class="media" title="sdk:assetpackdownload-263x300.jpg"><img src="/resources/sdk-assetpackdownload-263x300.jpg" class="media" alt="" /></a>
</p>

<p>
You can publish your AssetPacks either as a zip file or directly to jmonkeyengine.org, using your website user name and login. <strong>This means other jMonkeyEngine SDK users can download your AssetPacks and install them to their local database right off the AssetPack online packages browser.</strong>
</p>

<p>
</p><p></p><div class="noteimportant">To make sure you can upload, you have to be registered on jmonkeyengine.org, and have to enter your login info in the AssetPack preferences: jMonkeyEngine SDK→Options→Asset Packs first.
</div>

<ol>
<li class="level1"><div class="li"> Right-Click your AssetPack project in the SDK and select “Publish AssetPack…”</div>
</li>
<li class="level1"><div class="li"> Check the description etc. settings, and press “Next”.</div>
</li>
<li class="level1"><div class="li"> Select the checkbox for online and/or local publishing and press “finish”.</div>
</li>
</ol>
<div class="tags"><span>
	<a href="/tag/documentation.html" class="wikilink1" title="tag:documentation" rel="tag">documentation</a>,
	<a href="/tag/sdk.html" class="wikilink1" title="tag:sdk" rel="tag">sdk</a>,
	<a href="/tag/asset.html" class="wikilink1" title="tag:asset" rel="tag">asset</a>
</span></div>

</div>
<!-- EDIT7 SECTION "AssetPack Publishing" [5684-] -->
