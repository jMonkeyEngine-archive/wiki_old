---
title: Creating assets in Blender3D
---
<h1 class="sectionedit1" id="creating_assets_in_blender3d">Creating assets in Blender3D</h1>
<div class="level1">

<p>
This section discusses how to create and import models from Blender3D (2.62+, see bottom of page for Blender 2.49 and before) to jME3. Furthermore it explains how you can create various typical game-related assets like normal maps of high-poly models and baked lighting maps.
</p>

</div>
<!-- EDIT1 SECTION "Creating assets in Blender3D" [1-320] -->
<h3 class="sectionedit2" id="asset_management">Asset Management</h3>
<div class="level3">

<p>
For the managing of assets in general, be sure to read the <a href="/jme3/intermediate/multi-media_asset_pipeline.html" class="wikilink1" title="jme3:intermediate:multi-media_asset_pipeline">Asset Pipeline Documentation</a>. It contains vital information on how to manage your asset files.
</p>

</div>
<!-- EDIT2 SECTION "Asset Management" [321-551] -->
<h3 class="sectionedit3" id="creating_models">Creating Models</h3>
<div class="level3">

<p>
Game-compatible models are models that basically only consist of a mesh and UV-mapped textures, in some cases animations. All other material parameters or effects (like particles etc.) can not be expected to be transferred properly and probably would not translate to live rendering very well anyway.
</p>

</div>
<!-- EDIT3 SECTION "Creating Models" [552-879] -->
<h2 class="sectionedit4" id="uv_mapped_textures">UV Mapped Textures</h2>
<div class="level2">

<p>
To successfully import a texture, the texture <strong>has to</strong> be UV-mapped to the model. Heres how to assign diffuse, normal and specular maps:
</p>
<ul>
<li class="level1"><div class="li"> <a href="/resources/jme3-external-blender-material-4.png" class="media" title="jme3:external:blender-material-4.png"><img src="/resources/jme3-external-blender-material-4.png" class="media" alt="" width="300" /></a> <a href="/resources/jme3-external-blender-material-3.png" class="media" title="jme3:external:blender-material-3.png"><img src="/resources/jme3-external-blender-material-3.png" class="media" alt="" width="350" /></a></div>
</li>
<li class="level2"><div class="li"> <a href="/resources/jme3-external-blender-material-2.png" class="media" title="jme3:external:blender-material-2.png"><img src="/resources/jme3-external-blender-material-2.png" class="media" alt="" width="300" /></a> <a href="/resources/jme3-external-blender-material-1.png" class="media" title="jme3:external:blender-material-1.png"><img src="/resources/jme3-external-blender-material-1.png" class="media" alt="" width="150" /></a></div>
</li>
</ul>

<p>
Its important to note that each used texture will create one separate geometry. So its best to either combine the UV maps or use a premade atlas with different texture types from the start and then map the uv coords of the models to the atlas instead of painting on the texture. This works best for large models like cities and space ships.
</p>

</div>
<!-- EDIT4 SECTION "UV Mapped Textures" [880-1593] -->
<h2 class="sectionedit5" id="animations">Animations</h2>
<div class="level2">

<p>
Animations for jME3 have to be bone animations, simple object movement is supported by the blender importer, mesh deformation or other forms of animation are not supported.
</p>

<p>
To create an animation from scratch do the following:
</p>
<ul>
<li class="level1"><div class="li"> Create the model</div>
<ul>
<li class="level2"><div class="li"> Make sure your models location, rotation and scale is applied and zero / one (see “Model Checklist” below)</div>
</li>
<li class="level2"><div class="li"> (Did you know? You can make any model from a box by only using extrusion, this creates very clean meshes)</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Create the armature bones, don't forget to have one root bone!</div>
<ul>
<li class="level2"><div class="li"> Start by placing the cursor at zero</div>
</li>
<li class="level2"><div class="li"> Go to the Add→Armature→Single Bone menu and create the root bone</div>
<ul>
<li class="level3"><div class="li"> <a href="/resources/jme3-external-blender-add-bone.png" class="media" title="jme3:external:blender-add-bone.png"><img src="/resources/jme3-external-blender-add-bone.png" class="media" alt="" /></a></div>
</li>
</ul>
</li>
<li class="level2"><div class="li"> Select the bone and go to edit mode (press tab)</div>
</li>
<li class="level2"><div class="li"> Select the root bone end and press “E” to extrude the bone, then start rigging your model this way</div>
</li>
<li class="level2"><div class="li"> <strong>Make sure your armatures location, rotation and scale is applied (see “Model Checklist” below) before continuing</strong></div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Make the armature the parent of the model</div>
<ul>
<li class="level2"><div class="li"> Make sure you are back in object mode (press tab again)</div>
</li>
<li class="level2"><div class="li"> First select the model object then select the armature object with shift pressed, then press Ctrl-P</div>
</li>
<li class="level2"><div class="li"> When you do this, you can select how the bone groups will be mapped to the model vertices initially</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Set a new armature constraint in the model “Object Modifiers” settings and select the Armature</div>
<ul>
<li class="level2"><div class="li"> <a href="/resources/jme3-external-blender-make-armature.png" class="media" title="jme3:external:blender-make-armature.png"><img src="/resources/jme3-external-blender-make-armature.png" class="media" alt="" /></a></div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Voila, your model should move when you move the bones in pose mode</div>
</li>
<li class="level1"><div class="li"> Go to the “Dope Sheet” window and select the “Action editor”</div>
<ul>
<li class="level2"><div class="li"> <a href="/resources/jme3-external-blender-action-editor.png" class="media" title="jme3:external:blender-action-editor.png"><img src="/resources/jme3-external-blender-action-editor.png" class="media" alt="" /></a></div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Add an action by pressing the plus button</div>
</li>
<li class="level1"><div class="li"> Create the keyframes (select the model armature and press I) along the timeline</div>
<ul>
<li class="level2"><div class="li"> <a href="/resources/jme3-external-blender-add-keyframes.png" class="media" title="jme3:external:blender-add-keyframes.png"><img src="/resources/jme3-external-blender-add-keyframes.png" class="media" alt="" /></a></div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Each action will be an animation available via the animation control in jME after the import</div>
</li>
<li class="level1"><div class="li"> <strong>Press the “F” button next to the action so it will be saved even if theres no references</strong></div>
<ul>
<li class="level2"><div class="li"> The animation would else be deleted if its not the active animation on the armature and the file is saved</div>
</li>
</ul>
</li>
</ul>

</div>
<!-- EDIT5 SECTION "Animations" [1594-3751] -->
<h3 class="sectionedit6" id="model_checklist">Model Checklist</h3>
<div class="level3">

<p>
Sometimes you do not create the model yourself and often times models from the web are not really made for OpenGL live rendering or not completely compatible with the bone system in jME.
</p>

<p>
To export an animated model in Blender make sure the following conditions are met:
</p>
<ul>
<li class="level1"><div class="li"> The animation has to be a <strong>bone animation</strong></div>
</li>
<li class="level1"><div class="li"> Apply Location, Rotation and Scale to the mesh on Blender: On 3D View editor on Blender, select the mesh in Object Mode and go to the 3D View Editor’s header → Object Menu → Apply → Location / Rotation / Scale.</div>
<ul>
<li class="level2"><div class="li"> <a href="/resources/jme3-external-blender_apply_mesh.png" class="media" title="jme3:external:blender_apply_mesh.png"><img src="/resources/jme3-external-blender_apply_mesh.png" class="media" alt="" width="300" /></a></div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Apply Location, Rotation and Scale to the armature on Blender: On 3D View editor on Blender, select the armature in Object Mode and go to the 3D View Editor’s header → Object Menu → Apply → Location / Rotation / Scale.</div>
<ul>
<li class="level2"><div class="li"> <a href="/resources/jme3-external-blender_apply_bones.png" class="media" title="jme3:external:blender_apply_bones.png"><img src="/resources/jme3-external-blender_apply_bones.png" class="media" alt="" width="300" /></a></div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Set the mesh’s origin point in the bottom of the mesh (see the image below).</div>
</li>
<li class="level1"><div class="li"> Set the armature’s origin point in the bottom of the armature (see the image below).</div>
</li>
<li class="level1"><div class="li"> Armature’s origin point and mesh’s origin point must be in the same location(see the image below).</div>
</li>
<li class="level1"><div class="li"> Use a root bone located in the armature’s origin. This root bone must be in vertical position (see the image below) and it is the root bone of the armature. If you rotate the root bone, the the entire armature might be rotate when you import the model into jMonkey (I’m just mentioning the result, I don’t know where is the problem (jMonkey importer or blender’s ogre exporter plugin)).</div>
</li>
<li class="level1"><div class="li"> Uncheck “Bone Envelopes” checkbox on the Armature modifier for the mesh (see the image below).</div>
<ul>
<li class="level2"><div class="li"> <a href="/resources/jme3-external-blender_envelopes.png" class="media" title="jme3:external:blender_envelopes.png"><img src="/resources/jme3-external-blender_envelopes.png" class="media" alt="" width="300" /></a></div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Uncheck “Envelopes” checkbox on the armature (see the image below).</div>
<ul>
<li class="level2"><div class="li"> <a href="/resources/jme3-external-blender_rootbone.png" class="media" title="jme3:external:blender_rootbone.png"><img src="/resources/jme3-external-blender_rootbone.png" class="media" alt="" width="500" /></a></div>
</li>
</ul>
</li>
</ul>

<p>
You can use SkeletonDebugger to show the skeleton on your game in order to check if the mesh and the skeleton are loaded correctly:
</p>
<pre class="code java">    <span class="kw1">final</span> Material soldier2Mat <span class="sy0">=</span> assetManager.<span class="me1">loadMaterial</span><span class="br0">(</span><span class="st0">"Materials/soldier2/soldier2.j3m"</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="kw1">final</span> Spatial soldier2 <span class="sy0">=</span> assetManager.<span class="me1">loadModel</span><span class="br0">(</span><span class="st0">"Models/soldier2/soldier2.j3o"</span><span class="br0">)</span><span class="sy0">;</span>
    TangentBinormalGenerator.<span class="me1">generate</span><span class="br0">(</span>soldier2<span class="br0">)</span><span class="sy0">;</span>
    soldier2.<span class="me1">setMaterial</span><span class="br0">(</span>soldier2Mat<span class="br0">)</span><span class="sy0">;</span>
 
    <span class="kw1">final</span> Node soldier2Node <span class="sy0">=</span> <span class="kw1">new</span> Node<span class="br0">(</span><span class="st0">"Soldier2 Node"</span><span class="br0">)</span><span class="sy0">;</span>
 
    soldier2Node.<span class="me1">attachChild</span><span class="br0">(</span>soldier2<span class="br0">)</span><span class="sy0">;</span>
    rootNode.<span class="me1">attachChild</span><span class="br0">(</span>soldier2Node<span class="br0">)</span><span class="sy0">;</span>
 
    <span class="kw1">final</span> AnimControl control <span class="sy0">=</span> soldier2.<span class="me1">getControl</span><span class="br0">(</span>AnimControl.<span class="kw1">class</span><span class="br0">)</span><span class="sy0">;</span>
    control.<span class="me1">addListener</span><span class="br0">(</span><span class="kw1">this</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="kw1">final</span> AnimChanel channel <span class="sy0">=</span> control.<span class="me1">createChannel</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
 
    <span class="kw1">final</span> SkeletonDebugger skeletonDebug <span class="sy0">=</span> <span class="kw1">new</span> SkeletonDebugger<span class="br0">(</span><span class="st0">"skeleton"</span>, control.<span class="me1">getSkeleton</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="kw1">final</span> Material mat <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>assetManager, <span class="st0">"Common/MatDefs/Misc/Unshaded.j3md"</span><span class="br0">)</span><span class="sy0">;</span>
    mat.<span class="me1">setColor</span><span class="br0">(</span><span class="st0">"Color"</span>, ColorRGBA.<span class="me1">Green</span><span class="br0">)</span><span class="sy0">;</span>
    mat.<span class="me1">getAdditionalRenderState</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">setDepthTest</span><span class="br0">(</span><span class="kw2">false</span><span class="br0">)</span><span class="sy0">;</span>
    skeletonDebug.<span class="me1">setMaterial</span><span class="br0">(</span>mat<span class="br0">)</span><span class="sy0">;</span>
    soldier2Node.<span class="me1">attachChild</span><span class="br0">(</span>skeletonDebug<span class="br0">)</span><span class="sy0">;</span></pre>
<ul>
<li class="level1"><div class="li"> <a href="/resources/jme3-external-blender_finished.png" class="media" title="jme3:external:blender_finished.png"><img src="/resources/jme3-external-blender_finished.png" class="media" alt="" width="500" /></a></div>
</li>
</ul>

<p>
Also check out these videos and resources:
</p>
<ul>
<li class="level1"><div class="li"> <a href="http://jmonkeyengine.org/groups/import-assets/forum/topic/blender-2-61-animation-issues/?topic_page=2&amp;num=15" class="urlextern" title="http://jmonkeyengine.org/groups/import-assets/forum/topic/blender-2-61-animation-issues/?topic_page=2&amp;num=15" rel="nofollow">Forum: How to import animated models from Blender 2.6 correctly</a> (<a href="https://www.youtube.com/watch?v=QiLCs4AKh28" class="urlextern" title="https://www.youtube.com/watch?v=QiLCs4AKh28" rel="nofollow">Video</a>)</div>
</li>
<li class="level1"><div class="li"> <a href="http://www.youtube.com/watch?v=NdjC9sCRV0s" class="urlextern" title="http://www.youtube.com/watch?v=NdjC9sCRV0s" rel="nofollow">Video tutorial for animated models from Blender 2.6</a></div>
</li>
<li class="level1"><div class="li"> <a href="https://docs.google.com/fileview?id=0B9hhZie2D-fENDBlZDU5MzgtNzlkYi00YmQzLTliNTQtNzZhYTJhYjEzNWNk&amp;hl=en" class="urlextern" title="https://docs.google.com/fileview?id=0B9hhZie2D-fENDBlZDU5MzgtNzlkYi00YmQzLTliNTQtNzZhYTJhYjEzNWNk&amp;hl=en" rel="nofollow">Exporting OgreXML scenes from Blender 2.49 to jME</a></div>
</li>
</ul>

</div>
<!-- EDIT6 SECTION "Model Checklist" [3752-7310] -->
<h2 class="sectionedit7" id="normalmap_baking">NormalMap baking</h2>
<div class="level2">

<p>
Models for live rendering should have a low polygon count. To increase the perceived detail of a model normal maps are commonly used in games. This tutorial will show how to create a normalmap from a highpoly version of your model that you can apply to a lowpoly version of the model in your game.
</p>

</div>
<!-- EDIT7 SECTION "NormalMap baking" [7311-7639] -->
<h3 class="sectionedit8" id="blender_modeling_lowpoly_highpoly">Blender modeling lowPoly &amp; highPoly</h3>
<div class="level3">
<ul>
<li class="level1"><div class="li"> If you use the multiresolution modifier you only need one object. Lets look at this example:</div>
<ul>
<li class="level2"><div class="li"> <a href="/resources/jme3-external-1.gif" class="media" title="jme3:external:1.gif"><img src="/resources/jme3-external-1.gif" class="media" alt="" width="150" /></a></div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Add a multiresolution modifier:</div>
<ul>
<li class="level2"><div class="li"> <a href="/resources/jme3-external-3.1.gif" class="media" title="jme3:external:3.1.gif"><img src="/resources/jme3-external-3.1.gif" class="media" alt="" width="300" /></a></div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> There are two types of modifiers: Catmull-Clark and Simple. </div>
<ul>
<li class="level2"><div class="li"> Simple is better for things like walls or floors.</div>
</li>
<li class="level2"><div class="li"> Catmull-Clark is better for objects like spheres.</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> When using Catmull-Clark with a higher “subdivide” value (more than 3) its good to have the “preview” value above 0 and less than the subdivide level. This is because Catmull-Clark smoothes the vertices, so the normalMap is not so precise.</div>
</li>
<li class="level1"><div class="li"> Here is an example of Prewiew 1, it's more smooth than the original mesh:</div>
<ul>
<li class="level2"><div class="li"> <a href="/resources/jme3-external-2.gif" class="media" title="jme3:external:2.gif"><img src="/resources/jme3-external-2.gif" class="media" alt="" width="150" /></a></div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Enable “Sculpt Mode” in blender and design the highPoly version of your model like here:</div>
<ul>
<li class="level2"><div class="li"> <a href="/resources/jme3-external-3.gif" class="media" title="jme3:external:3.gif"><img src="/resources/jme3-external-3.gif" class="media" alt="" width="150" /></a></div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Now go into Render Tab, and bake a normalMap using same configuration as here:</div>
<ul>
<li class="level2"><div class="li"> <a href="/resources/jme3-external-4.gif" class="media" title="jme3:external:4.gif"><img src="/resources/jme3-external-4.gif" class="media" alt="" width="300" /></a></div>
</li>
</ul>
</li>
</ul>

<p>
</p><p></p><div class="noteclassic">Remember! The actual preview affects the baking output and mesh export!
</div>


<p>
</p><p></p><div class="noteclassic">Be careful: The steps above lead to terrible normal maps - use this procedure instead:
</div>

<ul>
<li class="level1"><div class="li"> uncheck “[ ] Bake from Multires”</div>
</li>
<li class="level1"><div class="li"> switch to object mode</div>
</li>
<li class="level1"><div class="li"> make a copy of your mesh (SHIFT+D)</div>
</li>
<li class="level1"><div class="li"> remove the Multires modifier from the copied model</div>
</li>
<li class="level1"><div class="li"> remove any materials from the copied model</div>
</li>
<li class="level1"><div class="li"> remove the armature modifier from the copied model</div>
</li>
<li class="level1"><div class="li"> select the original (highres) model</div>
</li>
<li class="level1"><div class="li"> go into pose mode, clear any pose transformations</div>
</li>
<li class="level1"><div class="li"> the highres and lowres models should be on top of each other now</div>
</li>
<li class="level1"><div class="li"> select the original (highres) model</div>
</li>
<li class="level1"><div class="li"> hold SHIFT and select the copied (lowres) model</div>
</li>
<li class="level1"><div class="li"> in the properties menu go to render</div>
</li>
<li class="level1"><div class="li"> use Bake &gt; Normal</div>
</li>
<li class="level1"><div class="li"> check “[x] Selected to Active”</div>
</li>
<li class="level1"><div class="li"> use a reasonably high value for “Margin” (4+ pixels at least for 1024×1024 maps)</div>
</li>
<li class="level1"><div class="li"> don't forget to safe the normal map image</div>
</li>
</ul>

<p>
</p><p></p><div class="noteclassic">Be careful: in the Outliner the camera symbol (Restrict Render) must be on!
</div>


</div>
<!-- EDIT8 SECTION "Blender modeling lowPoly & highPoly" [7640-9694] -->
<h3 class="sectionedit9" id="fixing_the_normal_colors_in_blender">Fixing the normal colors in Blender</h3>
<div class="level3">

<p>
Blender has its own normal colors standard. We need to fix the colors to prepare the normalmap for using it with the JME Lighting Material.
</p>

<p>
To do this, go to the Blender Node Window
</p>
<ul>
<li class="level1"><div class="li"> Here is Blender Node example. It fixes the normal colors:</div>
<ul>
<li class="level2"><div class="li"> <a href="/resources/jme3-external-5.gif" class="media" title="jme3:external:5.gif"><img src="/resources/jme3-external-5.gif" class="media" alt="" width="500" /></a></div>
</li>
</ul>
</li>
</ul>
<ul>
<li class="level1"><div class="li"> Here is the colors configuration:</div>
<ul>
<li class="level2"><div class="li"> <a href="/resources/jme3-external-6.gif" class="media" title="jme3:external:6.gif"><img src="/resources/jme3-external-6.gif" class="media" alt="" width="180" /></a> <a href="/resources/jme3-external-7.gif" class="media" title="jme3:external:7.gif"><img src="/resources/jme3-external-7.gif" class="media" alt="" width="180" /></a> <a href="/resources/jme3-external-8.gif" class="media" title="jme3:external:8.gif"><img src="/resources/jme3-external-8.gif" class="media" alt="" width="180" /></a></div>
</li>
</ul>
</li>
</ul>
<ul>
<li class="level1"><div class="li"> Sometimes it will be needed to change R and G scale and add some blur for better effect. Do it like on image below</div>
<ul>
<li class="level2"><div class="li"> <a href="/resources/jme3-external-exception2.gif" class="media" title="jme3:external:exception2.gif"><img src="/resources/jme3-external-exception2.gif" class="media" alt="" /></a></div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> After rendering, save the file to a destination you want and use it with the JME Lighting Material and the lowpoly version of the model.</div>
<ul>
<li class="level2"><div class="li"> <a href="/resources/jme3-external-ready_normal.gif" class="media" title="jme3:external:ready_normal.gif"><img src="/resources/jme3-external-ready_normal.gif" class="media" alt="" /></a></div>
</li>
</ul>
</li>
</ul>

</div>
<!-- EDIT9 SECTION "Fixing the normal colors in Blender" [9695-10504] -->
<h2 class="sectionedit10" id="lightmap_baking">LightMap baking</h2>
<div class="level2">

<p>
The goal of this tutorial is to explain briefly how to bake light map in blender with a separate set of texture coordinates and then export a model using this map in jME3.
</p>

</div>
<!-- EDIT10 SECTION "LightMap baking" [10505-10706] -->
<h3 class="sectionedit11" id="blender_modeling_texturing">Blender modeling + texturing</h3>
<div class="level3">
<ul>
<li class="level1"><div class="li"> create a mesh in blender and unwrap it to create uvs</div>
<ul>
<li class="level2"><div class="li"> <a href="/resources/jme3-advanced-1.jpg" class="media" title="jme3:advanced:1.jpg"><img src="/resources/jme3-advanced-1.jpg" class="media" title="1.jpg" alt="1.jpg" width="600" /></a></div>
</li>
</ul>
</li>
</ul>
<ul>
<li class="level1"><div class="li"> In the mesh tab you can see the sets of Uvs, it will create the first one.</div>
<ul>
<li class="level2"><div class="li"> You can assign w/e texture on it, i used the built in checker of blender for the example.</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> In this list, create a new one and click on the camera icon so that baking is made with this set. Name it LightUvMap.</div>
</li>
<li class="level1"><div class="li"> In the 3D view in edit mode select all your mesh vertice and hit 'U'/LightMap pack then ok it will unfold the mesh for light map.</div>
</li>
<li class="level1"><div class="li"> Create a new image, go to the render tab an all at the end check the “Bake” section and select shadows. Then click bake.</div>
</li>
<li class="level1"><div class="li"> If all went ok it will create a light map like this.</div>
<ul>
<li class="level2"><div class="li"> <a href="/resources/jme3-advanced-2.jpg" class="media" title="jme3:advanced:2.jpg"><img src="/resources/jme3-advanced-2.jpg" class="media" title="2.jpg" alt="2.jpg" width="600" /></a></div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Go to the material tab, create a new one for your model and go to the Texture Tab.</div>
</li>
<li class="level1"><div class="li"> Create 2 textures one for the color map, and one for the light map.</div>
</li>
<li class="level1"><div class="li"> In the Mapping section be sure to select coordinates : UV and select the good set of coordinates.</div>
<ul>
<li class="level2"><div class="li"> <a href="/resources/jme3-advanced-3.jpg" class="media" title="jme3:advanced:3.jpg"><img src="/resources/jme3-advanced-3.jpg" class="media" title="3.jpg" alt="3.jpg" width="600" /></a></div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Then the light map</div>
<ul>
<li class="level2"><div class="li"> <a href="/resources/jme3-advanced-4.jpg" class="media" title="jme3:advanced:4.jpg"><img src="/resources/jme3-advanced-4.jpg" class="media" title="4.jpg" alt="4.jpg" width="600" /></a></div>
</li>
</ul>
</li>
</ul>

</div>
<!-- EDIT11 SECTION "Blender modeling + texturing" [10707-11841] -->
<h3 class="sectionedit12" id="importing_the_model_in_the_sdk_and_creating_the_appropriate_material">Importing the model in the SDK and creating the appropriate material</h3>
<div class="level3">

<p>
Once this is done, export your model with the ogre exporter (or import it directly via the blend importer), and turn it into J3o with the SDK.
</p>
<ul>
<li class="level1"><div class="li"> Create material for it using the lighting definition.</div>
</li>
<li class="level1"><div class="li"> Add the colorMap in the diffuse map slot and the lightMap in the light map slot.</div>
</li>
<li class="level1"><div class="li"> Make sure you check “SeparateTexCoords”</div>
<ul>
<li class="level2"><div class="li"> <a href="/resources/jme3-advanced-5.jpg" class="media" title="jme3:advanced:5.jpg"><img src="/resources/jme3-advanced-5.jpg" class="media" title="5.jpg" alt="5.jpg" width="600" /></a></div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> It should roughly result in something like that :</div>
<ul>
<li class="level2"><div class="li"> <a href="/resources/jme3-advanced-6.jpg" class="media" title="jme3:advanced:6.jpg"><img src="/resources/jme3-advanced-6.jpg" class="media" title="6.jpg" alt="6.jpg" width="600" /></a></div>
</li>
</ul>
</li>
</ul>

<p>
The blend file, the ogre xml files and the textures can be found in the download section of the google code repo
</p>

<p>
<a href="http://code.google.com/p/jmonkeyengine/downloads/detail?name=LightMap.zip&amp;can=2&amp;q=#makechanges" class="urlextern" title="http://code.google.com/p/jmonkeyengine/downloads/detail?name=LightMap.zip&amp;can=2&amp;q=#makechanges" rel="nofollow">http://code.google.com/p/jmonkeyengine/downloads/detail?name=LightMap.zip&amp;can=2&amp;q=#makechanges</a>
</p>

</div>
<!-- EDIT12 SECTION "Importing the model in the SDK and creating the appropriate material" [11842-12586] -->
<h2 class="sectionedit13" id="modelling_racing_tracks_and_cars">Modelling racing tracks and cars</h2>
<div class="level2">

<p>
Follow the link below to a pdf tutorial by rhymez where I guide you to modelling a car and importing it to the jMonkeyengine correctly and edit it in the vehicle editor.Plus how to model a simple racing track.
<a href="http://www.indiedb.com/games/street-rally-3d/downloads/modelling-in-blender-to-the-jmonkeyengine" class="urlextern" title="http://www.indiedb.com/games/street-rally-3d/downloads/modelling-in-blender-to-the-jmonkeyengine" rel="nofollow">http://www.indiedb.com/games/street-rally-3d/downloads/modelling-in-blender-to-the-jmonkeyengine</a>
</p>

</div>
<!-- EDIT13 SECTION "Modelling racing tracks and cars" [12587-12943] -->
<h2 class="sectionedit14" id="optimizing_models_for_3d_games">Optimizing Models for 3D games</h2>
<div class="level2">

<p>
Follow the link below to a pdf tutorial by rhymez where I guide you on how you can optimize your models for faster rendering.
<a href="http://www.indiedb.com/games/street-rally-3d/downloads/optimizing-3d-models-for-games" class="urlextern" title="http://www.indiedb.com/games/street-rally-3d/downloads/optimizing-3d-models-for-games" rel="nofollow">http://www.indiedb.com/games/street-rally-3d/downloads/optimizing-3d-models-for-games</a>
</p>

</div>
<!-- EDIT14 SECTION "Optimizing Models for 3D games" [12944-13203] -->
<h2 class="sectionedit15" id="skybox_baking">SkyBox baking</h2>
<div class="level2">

<p>
There are several ways to create static images to use for a sky in your game. This will describe the concepts used in blender and create an ugly sky <img src="/lib/images/smileys/icon_smile.gif" class="icon" alt=":-)" /> Check the links below for other ways and prettier skies.
</p>

<p>
A sky box is a texture mapped cube, it can also, loosely, be called en EnvMap or a CubeMap. The camera is inside the cube and the clever thing that jME does is to draw the sky so it is always behind whatever else is in your scene. Imagine the monkey is the camera in the picture.
</p>
<ul>
<li class="level1"><div class="li"> <a href="/resources/jme3-external-skybox-concept.png" class="media" title="jme3:external:skybox-concept.png"><img src="/resources/jme3-external-skybox-concept.png" class="media" alt="" /></a></div>
</li>
</ul>

<p>
But a real sky is not a box around our heads, it is more like a sphere. So if we put any old image in the sky it will look strange and might even look like a box. This is not what we want. The trick is to distort the image so that it will <em>look</em> like a sphere even if it in fact is a picture pasted on a box. Luckily blender can do that tricky distortion for us.
</p>

<p>
The screenshots are from Blender 2.63 but the equivalent operations have been in blender for years so with minor tweaks should work for almost any version.
</p>

<p>
So let's get started
</p>
<ul>
<li class="level1"><div class="li"> Fire up blender and you'll see something like this.</div>
<ul>
<li class="level2"><div class="li"> <a href="/resources/jme3-external-start-screen2.png" class="media" title="jme3:external:start-screen2.png"><img src="/resources/jme3-external-start-screen2.png" class="media" alt="" /></a></div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> The cube in the start scene is perfect for us. What we'll do is have Blender render the scene onto that cube. The resulting image is what we'll use for our sky box. So our jME sky will look like we stood inside the blender box and looked out on the scene in blender.</div>
</li>
<li class="level1"><div class="li"> Start by selecting the box and set its material to shadeless.</div>
<ul>
<li class="level2"><div class="li"> <a href="/resources/jme3-external-shadeless.png" class="media" title="jme3:external:shadeless.png"><img src="/resources/jme3-external-shadeless.png" class="media" alt="" /></a></div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Now we will create a texture for the box. Make sure the texture is an <code>Environment Map</code>, that the <code>Viewpoint Object</code> is set to the cube. The resolution is how large the resulting image will be. More pixels makes the sky look better but comes at the cost of texture memory. You'll have to trim the resolution to what works in your application.</div>
<ul>
<li class="level2"><div class="li"> <a href="/resources/jme3-external-texture.png" class="media" title="jme3:external:texture.png"><img src="/resources/jme3-external-texture.png" class="media" alt="" /></a></div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Next up is the fun part, create the sky scene in blender. You can do whatever fits your application, include models for a city landscape, set up a texture mapped sphere in blender with a nice photographed sky, whatever you can think will make a good sky. I am not so creative so I created this scene:</div>
<ul>
<li class="level2"><div class="li"> <a href="/resources/jme3-external-scene.png" class="media" title="jme3:external:scene.png"><img src="/resources/jme3-external-scene.png" class="media" alt="" /></a></div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Now render the scene (press F12). It doesn't actually matter where the camera is in blender but you might see something similar to this:</div>
<ul>
<li class="level2"><div class="li"> <a href="/resources/jme3-external-render.png" class="media" title="jme3:external:render.png"><img src="/resources/jme3-external-render.png" class="media" alt="" /></a></div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> You can see that Blender has actually drawn the scene onto the cube. This is exactly what we want. Now to save the image.</div>
</li>
<li class="level1"><div class="li"> Select the texture of the cube and select save environment map.</div>
<ul>
<li class="level2"><div class="li"> <a href="/resources/jme3-external-saveenvmap.png" class="media" title="jme3:external:saveenvmap.png"><img src="/resources/jme3-external-saveenvmap.png" class="media" alt="" /></a></div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> That is it for Blender. Open the saved image in some image editor (I use the Gimp from <a href="http://www.gimp.org" class="urlextern" title="http://www.gimp.org" rel="nofollow">http://www.gimp.org</a> here).</div>
</li>
</ul>

<p>
</p><p></p><div class="notetip">The SDK also contains an image editor, right-click the image and select “edit image” to open it.
</div>

<ul>
<li class="level1"><div class="li"> You will notice that Blender has taken the 6 sides of the cube and pasted together into one image (3×2). So now we need to cut it up again into 6 separate images. In gimp I usually set the guides to where I want to cut and then go into Filters→Web→Slice and let gimp cut it up for me.</div>
<ul>
<li class="level2"><div class="li"> <a href="/resources/jme3-external-post-slice.png" class="media" title="jme3:external:post-slice.png"><img src="/resources/jme3-external-post-slice.png" class="media" alt="" /></a></div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Next up is to move the image files into your assets directory and create the sky in jME. You can do that in the Scene Composer by right clicking the scene node, select <code>Add Spatial</code> and then select <code>Skybox</code>.</div>
</li>
</ul>

<p>
If you want to do it from code, here is an example:
</p>
<pre class="code java"><span class="kw1">public</span> <span class="kw4">void</span> simpleInitApp<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
 
    Texture westTex <span class="sy0">=</span> assetManager.<span class="me1">loadTexture</span><span class="br0">(</span><span class="st0">"Textures/west.png"</span><span class="br0">)</span><span class="sy0">;</span>
    Texture eastTex <span class="sy0">=</span> assetManager.<span class="me1">loadTexture</span><span class="br0">(</span><span class="st0">"Textures/east.png"</span><span class="br0">)</span><span class="sy0">;</span>
    Texture northTex <span class="sy0">=</span> assetManager.<span class="me1">loadTexture</span><span class="br0">(</span><span class="st0">"Textures/north.png"</span><span class="br0">)</span><span class="sy0">;</span>
    Texture southTex <span class="sy0">=</span> assetManager.<span class="me1">loadTexture</span><span class="br0">(</span><span class="st0">"Textures/south.png"</span><span class="br0">)</span><span class="sy0">;</span>
    Texture upTex <span class="sy0">=</span> assetManager.<span class="me1">loadTexture</span><span class="br0">(</span><span class="st0">"Textures/top.png"</span><span class="br0">)</span><span class="sy0">;</span>
    Texture downTex <span class="sy0">=</span> assetManager.<span class="me1">loadTexture</span><span class="br0">(</span><span class="st0">"Textures/bottom.png"</span><span class="br0">)</span><span class="sy0">;</span>
 
    <span class="kw1">final</span> Vector3f normalScale <span class="sy0">=</span> <span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="sy0">-</span><span class="nu0">1</span>, <span class="nu0">1</span>, <span class="nu0">1</span><span class="br0">)</span><span class="sy0">;</span>
    Spatial skySpatial <span class="sy0">=</span> SkyFactory.<span class="me1">createSky</span><span class="br0">(</span>
                        assetManager,
                        westTex,
                        eastTex,
                        northTex,
                        southTex,
                        upTex,
                        downTex,
                        normalScale<span class="br0">)</span><span class="sy0">;</span>
    rootNode.<span class="me1">attachChild</span><span class="br0">(</span>skySpatial<span class="br0">)</span><span class="sy0">;</span>
<span class="br0">}</span></pre>

<p>
</p><p></p><div class="notetip">This example uses a strange normalScale, this is to flip the image on the X-axis and might not be needed in your case. Hint: the texture is applied on the outside of the cube but we are inside so what do we see?
</div>


</div>
<!-- EDIT15 SECTION "SkyBox baking" [13204-17887] -->
<h3 class="sectionedit16" id="further_reading">Further reading</h3>
<div class="level3">
<ul>
<li class="level1"><div class="li"> <a href="/jme3/external/blender-example.html" class="wikilink1" title="jme3:external:blender-example">Warg - from cube to animated and textured game model Example</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/advanced/sky.html" class="wikilink1" title="jme3:advanced:sky">How to add a Sky to your Scene</a></div>
</li>
<li class="level1"><div class="li"> <a href="http://hub.jmonkeyengine.org/t/jmonkeyengine-tutorial-how-to-create-skymaps-using-blender/19313" class="urlextern" title="http://hub.jmonkeyengine.org/t/jmonkeyengine-tutorial-how-to-create-skymaps-using-blender/19313" rel="nofollow">http://hub.jmonkeyengine.org/t/jmonkeyengine-tutorial-how-to-create-skymaps-using-blender/19313</a></div>
</li>
</ul>

</div>
<!-- EDIT16 SECTION "Further reading" [17888-] -->
