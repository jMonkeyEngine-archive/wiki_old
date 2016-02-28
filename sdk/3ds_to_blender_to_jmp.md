---
title: Using Blender as a Intermediator Between 3dMax and the jMonkeyEngine SDK
---
<h1 class="sectionedit1" id="using_blender_as_a_intermediator_between_3dmax_and_the_jmonkeyengine_sdk">Using Blender as a Intermediator Between 3dMax and the jMonkeyEngine SDK</h1>
<div class="level1">

<p>
The jMonkeyEngine SDK supports .blend files and can convert them to jMonkeyEngine's .j3o format. This means you can use Blender to convert, for example, a 3dMax file to .j3o format.
</p>

</div>
<!-- EDIT1 SECTION "Using Blender as a Intermediator Between 3dMax and the jMonkeyEngine SDK" [1-271] -->
<h2 class="sectionedit2" id="importing_the_3ds_file_to_blender">Importing the .3ds file to Blender</h2>
<div class="level2">

<p>
I'm using the blender 2.59 at this tutorial, but if you blender 2.49b, no problem ;).
After you saved your .3ds file in 3dmax, open the blender, delete the default cube,
and import your .3ds file via File—→Import—–&gt;3D Studio.
</p>

<p>
<a href="/resources/fetch.php" class="media" title="http://farm7.static.flickr.com/6088/6137146239_d38ee89f5e_b.jpg"><img src="/resources/fetch.php" class="mediacenter" title="farm7.static.flickr.com_6088_6137146239_d38ee89f5e_b.jpg" alt="farm7.static.flickr.com_6088_6137146239_d38ee89f5e_b.jpg" /></a>
</p>

</div>
<!-- EDIT2 SECTION "Importing the .3ds file to Blender" [272-623] -->
<h2 class="sectionedit3" id="saving_the_blend_file">Saving the .blend file</h2>
<div class="level2">

<p>
Now save your .blend file so you can load it into the jMonkeyEngine SDK.
</p>

<p>
<a href="/resources/fetch.php" class="media" title="http://farm7.static.flickr.com/6063/6137146285_7e5e994702_b.jpg"><img src="/resources/fetch.php" class="mediacenter" title="farm7.static.flickr.com_6063_6137146285_7e5e994702_b.jpg" alt="farm7.static.flickr.com_6063_6137146285_7e5e994702_b.jpg" /></a>
</p>

</div>
<!-- EDIT3 SECTION "Saving the .blend file" [624-804] -->
<h2 class="sectionedit4" id="importing_the_blend_file_to_the_sdk_by_using_the_modelimporter_and_blendersupport_plugins">Importing the .blend file to the SDK by using the ModelImporter and BlenderSupport plugins</h2>
<div class="level2">

<p>
Click on Import Model button and then click on Open Model button to open the .blend file. Click next, select the checkbox to import a copy from .blend file, and click finish.
</p>

<p>
<a href="/resources/fetch.php" class="media" title="http://farm7.static.flickr.com/6081/6137146313_9b2987b231_b.jpg"><img src="/resources/fetch.php" class="mediacenter" title="farm7.static.flickr.com_6081_6137146313_9b2987b231_b.jpg" alt="farm7.static.flickr.com_6081_6137146313_9b2987b231_b.jpg" /></a>
</p>

</div>
<!-- EDIT4 SECTION "Importing the .blend file to the SDK by using the ModelImporter and BlenderSupport plugins" [805-1153] -->
<h2 class="sectionedit5" id="edit_your_model_in_scenecomposer_and_voila">Edit your model in SceneComposer and "VOILA"</h2>
<div class="level2">

<p>
As you can see, the .blend model was automatically converted to .j3o binary format. Now, you are able to edit it in SceneComposer ;D.
</p>

<p>
<a href="/resources/fetch.php" class="media" title="http://farm7.static.flickr.com/6076/6137146323_ae6275602c_b.jpg"><img src="/resources/fetch.php" class="mediacenter" title="farm7.static.flickr.com_6076_6137146323_ae6275602c_b.jpg" alt="farm7.static.flickr.com_6076_6137146323_ae6275602c_b.jpg" /></a>
</p>

</div>
<!-- EDIT5 SECTION "Edit your model in SceneComposer and VOILA" [1154-] -->
