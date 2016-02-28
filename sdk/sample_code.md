---
title: jMonkeyEngine SDK: Sample Code
---
<h1 class="sectionedit1" id="jmonkeyengine_sdksample_code">jMonkeyEngine SDK: Sample Code</h1>
<div class="level1">

<p>
You can run example code by opening an included JME3Tests project and included assets. You can also search the built-in documentation or drag and drop code snippets from the Palette in the SDK to get short code sample.
</p>

</div>
<!-- EDIT1 SECTION "jMonkeyEngine SDK: Sample Code" [1-266] -->
<h2 class="sectionedit2" id="code_palette_and_samples_in_the_sdk">Code Palette and Samples in the SDK</h2>
<div class="level2">
<ul>
<li class="level1"><div class="li"> Type a keyword into the search box in the SDK or press F1 to search the built-in help for sample code.</div>
</li>
<li class="level1"><div class="li"> <a href="/sdk/code_editor.html" class="wikilink1" title="sdk:code_editor">SDK code editor and palette</a></div>
</li>
</ul>

</div>
<!-- EDIT2 SECTION "Code Palette and Samples in the SDK" [267-477] -->
<h2 class="sectionedit3" id="the_jme3tests_project_template">The JME3Tests Project Template</h2>
<div class="level2">

<p>
The jMonkeyEngine SDK contains a Test Project with lots of sample code and assets. The Test Project is all set up and ready to run, and it's easy to use for beginners (no need to mess with classpaths or libraries).
</p>
<ol>
<li class="level1"><div class="li"> Install and Open the jMonkeyEngine <a href="/doku.php/sdk:sdk" class="wikilink2" title="sdk:sdk" rel="nofollow">SDK</a></div>
</li>
<li class="level1"><div class="li"> Go to File→New Project</div>
</li>
<li class="level1"><div class="li"> In the New Project Wizard, select <code>JME3 Tests</code> from the <code>JME3</code> category. Click Next.</div>
</li>
<li class="level1"><div class="li"> Specify a location, e.g. create a jMonkeyProjects directory in your home directory. Click Finish.</div>
</li>
</ol>

<p>
This default project template creates a project called <code>JmeTests</code>. It contains all test classes and examples from the jme3 source repository. Feel free to modify the code samples and experiment! In the unlikely event that you should break the project, <img src="/lib/images/smileys/icon_smile.gif" class="icon" alt=":-)" /> you can always recreate all packaged samples by creating another project from the New Project wizard's <code>JME3 Tests</code> template.
</p>

<p>
</p><p></p><div class="noteimportant">Press Shift-F6 to run a class that is open in the editor, or right-click a class in the Project window and choose Run File. 
</div>


</div>
<!-- EDIT3 SECTION "The JME3Tests Project Template" [478-1544] -->
<h2 class="sectionedit4" id="jme3testdata_assets">JME3TestData Assets</h2>
<div class="level2">

<p>
You may want access to some sample assets, such as 3D models or textures, in one of your projects. A common situation for this would be while going through the <a href="/jme3/beginner.html" class="wikilink1" title="jme3:beginner">beginner tutorials</a>.
</p>
<ol>
<li class="level1"><div class="li"> Right-click an existing jME3 project in the <a href="/doku.php/sdk:sdk" class="wikilink2" title="sdk:sdk" rel="nofollow">SDK</a>, and select Properties.</div>
</li>
<li class="level1"><div class="li"> In the Properties window, select the Libraries section. Go to the Compile tab, it contains compile-time libraries.</div>
</li>
<li class="level1"><div class="li"> Click the Add Library… button and select the pre-defined <code>jme3-test-data</code>. Click OK.</div>
</li>
<li class="level1"><div class="li"> Click OK to save and close the Properties.</div>
</li>
</ol>

<p>
The project's assetManager now has access to sample files from the <code>jme3-test-data.jar</code> file. This JAR library contains
</p>
<ul>
<li class="level1"><div class="li"> Ogre XML Models: Ninja.mesh.xml, Oto.mesh.xml, HoverTank.mesh.xml, Sinbad.mesh.xml, and many more</div>
</li>
<li class="level1"><div class="li"> Blender models</div>
</li>
<li class="level1"><div class="li"> Materials and Textures</div>
<ul>
<li class="level2"><div class="li"> Terrain, sky, rock, brick, pond…</div>
</li>
<li class="level2"><div class="li"> Particle effect textures</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Sounds</div>
</li>
<li class="level1"><div class="li"> And more…</div>
</li>
</ul>

</div>
<!-- EDIT4 SECTION "JME3TestData Assets" [1545-2486] -->
<h2 class="sectionedit5" id="assetpacks">AssetPacks</h2>
<div class="level2">

<p>
<a href="/resources/fetch.php" class="media" title="http://jmonkeyengine.org/wp-content/uploads/2010/10/assetpackbrowser-300x166.jpg"><img src="/resources/fetch.php" class="mediaright" title="jmonkeyengine.org_wp-content_uploads_2010_10_assetpackbrowser-300x166.jpg" alt="jmonkeyengine.org_wp-content_uploads_2010_10_assetpackbrowser-300x166.jpg" /></a>
If you need sample 3D models, don't miss the opportunity to download our community-provided <a href="/sdk/asset_packs.html" class="wikilink1" title="sdk:asset_packs">Asset Packs</a>!
</p>

<p>
In the SDK:
</p>
<ul>
<li class="level1"><div class="li"> Open the AssetPackBrowser from the Windows menu</div>
</li>
<li class="level1"><div class="li"> In the AssetPackBrowser, click the Online AssetPacks button</div>
</li>
<li class="level1"><div class="li"> Click install on the AssetPack of your choice. The SDK downloads it and makes the assets accessible in your AssetPack Library.</div>
</li>
<li class="level1"><div class="li"> Click the View Library button and open the Assets node. </div>
</li>
<li class="level1"><div class="li"> Right-click an asset to</div>
<ul>
<li class="level2"><div class="li"> Preview it</div>
</li>
<li class="level2"><div class="li"> Add it to the SceneComposer</div>
</li>
<li class="level2"><div class="li"> Add it to a game project's assets directory </div>
</li>
</ul>
</li>
</ul>

<p>
Read more about <a href="/sdk/asset_packs.html" class="wikilink1" title="sdk:asset_packs">Asset Packs</a> and how you can share your own collection with the community.
</p>
<div class="tags"><span>
	<a href="/tag/documentation.html" class="wikilink1" title="tag:documentation" rel="tag">documentation</a>,
	<a href="/tag/sdk.html" class="wikilink1" title="tag:sdk" rel="tag">sdk</a>,
	<a href="/tag/asset.html" class="wikilink1" title="tag:asset" rel="tag">asset</a>,
	<a href="/tag/project.html" class="wikilink1" title="tag:project" rel="tag">project</a>
</span></div>

</div>
<!-- EDIT5 SECTION "AssetPacks" [2487-] -->
