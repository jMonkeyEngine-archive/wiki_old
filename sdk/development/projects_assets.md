---
title: Projects and Assets
---
<h1 class="sectionedit1" id="projects_and_assets">Projects and Assets</h1>
<div class="level1">

<p>
The SDK heavily uses the systems provided by the base platform for the handling of assets and projects and extends the system with jME3 specific features.
</p>

</div>
<!-- EDIT1 SECTION "Projects and Assets" [1-189] -->
<h2 class="sectionedit2" id="projectassetmanager">ProjectAssetManager</h2>
<div class="level2">

<p>
All AssetDataObjects and SceneExplorerNodes allow access to the ProjectAssetManager of the project they were loaded from.
</p>
<pre class="code java">ProjectAssetManager pm <span class="sy0">=</span> node.<span class="me1">getLookup</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">lookup</span><span class="br0">(</span>ProjectAssetManager.<span class="kw1">class</span><span class="br0">)</span></pre>

<p>
The ProjectAssetManager is basically a normal DesktopAssetManager for each project with some added functionality:
</p>
<ul>
<li class="level1"><div class="li"> Access to the FileObject of the assets folder of the project to load and save data</div>
</li>
<li class="level1"><div class="li"> Convert absolute file paths to relative asset paths and vice versa</div>
</li>
<li class="level1"><div class="li"> Get lists of all textures, materials etc. in the project</div>
</li>
<li class="level1"><div class="li"> more convenient stuff.. :)</div>
</li>
</ul>

</div>
<!-- EDIT2 SECTION "ProjectAssetManager" [190-801] -->
<h2 class="sectionedit3" id="assetdataobject">AssetDataObject</h2>
<div class="level2">

<p>
Most “files” that you encounter in the SDK come in the form of AssetDataObjects. All Nodes that you encounter contain the AssetDataObject they were loaded from. It provides not just access to the FileObject of the specific file but also an AssetData object that allows access to jME specific properties and data. The AssetData object also allows loading the object via the jME3 assetManager. It is accessible via the lookup of the Node or AssetDataObject:
</p>
<pre class="code java">assetDataObject.<span class="me1">getLookup</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">lookup</span><span class="br0">(</span>AssetData.<span class="kw1">class</span><span class="br0">)</span></pre>

</div>
<!-- EDIT3 SECTION "AssetDataObject" [802-1355] -->
<h2 class="sectionedit4" id="new_asset_file_types">New Asset File Types</h2>
<div class="level2">

<p>
When you add a new file type for a model format or other asset file that can be loaded in jME3 you can start by using new file type template (New File→Module Development→File Type). Change the DataObject to extend AssetDataObject (general), SpatialAssetDataObject (some type of model) or BinaryModelDataObject (basically a j3o savable file). And possibly override the loadAsset and saveAsset methods which are used by the AssetData object to return the correct AssetKey type (needed for import properties to work).
</p>
<pre class="code java"><span class="kw1">public</span> <span class="kw1">class</span> BlenderDataObject <span class="kw1">extends</span> SpatialAssetDataObject <span class="br0">{</span>
    <span class="kw1">public</span> BlenderDataObject<span class="br0">(</span>FileObject pf, MultiFileLoader loader<span class="br0">)</span> <span class="kw1">throws</span> DataObjectExistsException, <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+ioexception"><span class="kw3">IOException</span></a> <span class="br0">{</span>
        <span class="kw1">super</span><span class="br0">(</span>pf, loader<span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
<span class="br0">}</span></pre>

<p>
An AssetManagerConfigurator class can be created to configure the assetManager of the projects and model importer to use the new asset type:
</p>
<pre class="code java">@org.<span class="me1">openide</span>.<span class="me1">util</span>.<span class="me1">lookup</span>.<span class="me1">ServiceProvider</span><span class="br0">(</span>service <span class="sy0">=</span> AssetManagerConfigurator.<span class="kw1">class</span><span class="br0">)</span>
<span class="kw1">public</span> <span class="kw1">class</span> BlenderAssetManagerConfigurator <span class="kw1">implements</span> AssetManagerConfigurator <span class="br0">{</span>
    <span class="kw1">public</span> <span class="kw4">void</span> prepareManager<span class="br0">(</span>AssetManager manager<span class="br0">)</span> <span class="br0">{</span>
        manager.<span class="me1">registerLoader</span><span class="br0">(</span>com.<span class="me1">jme3</span>.<span class="me1">scene</span>.<span class="me1">plugins</span>.<span class="me1">blender</span>.<span class="me1">BlenderModelLoader</span>.<span class="kw1">class</span>, <span class="st0">"blend"</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
<span class="br0">}</span></pre>

</div>
<!-- EDIT4 SECTION "New Asset File Types" [1356-] -->
