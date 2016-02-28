---
title: Models and Scenes
---
<h1 class="sectionedit1" id="models_and_scenes">Models and Scenes</h1>
<div class="level1">

<p>
Like <a href="/jme3/advanced/shape.html" class="wikilink1" title="jme3:advanced:shape">Shape</a>s, 3D models are also made up of <a href="/jme3/advanced/mesh.html" class="wikilink1" title="jme3:advanced:mesh">Mesh</a>es, but models are more complex than Shapes. While Shapes are built into jME3, you typically create models in external 3D Mesh Editors. 
</p>

</div>
<!-- EDIT1 SECTION "Models and Scenes" [1-226] -->
<h2 class="sectionedit2" id="using_models_and_scenes_with_jme3">Using Models and Scenes with jME3</h2>
<div class="level2">

<p>
To use 3D models in a jME3 application:
</p>
<ol>
<li class="level1"><div class="li"> Export the 3D model in Ogre XML or Wavefront OBJ format. Export Scenes as Ogre DotScene format.</div>
</li>
<li class="level1"><div class="li"> Save the files into a subdirectory of your jME3 project's <code>assets</code> directory.</div>
</li>
<li class="level1"><div class="li"> In your code, you use the <a href="/jme3/advanced/asset_manager.html" class="wikilink1" title="jme3:advanced:asset_manager">Asset Manager</a> to load models as <a href="/jme3/advanced/spatial.html" class="wikilink1" title="jme3:advanced:spatial">Spatial</a>s into a jME application. <pre class="code java">Spatial model <span class="sy0">=</span> assetManager.<span class="me1">loadModel</span><span class="br0">(</span>
    <span class="st0">"Models/MonkeyHead/MonkeyHead.mesh.xml"</span> <span class="br0">)</span><span class="sy0">;</span></pre>
</div>
</li>
<li class="level1"><div class="li"> (For the release build:) Use the jMonkeyEngine SDK to convert models to .j3o format. You don't need this step as long you still develop and test the aplication within the jMonkeyEngine SDK.</div>
</li>
</ol>

</div>
<!-- EDIT2 SECTION "Using Models and Scenes with jME3" [227-901] -->
<h2 class="sectionedit3" id="creating_models_and_scenes">Creating Models and Scenes</h2>
<div class="level2">

<p>
To create 3D models and scenes, you need a 3D Mesh Editor such as <a href="http://www.blender.org/" class="urlextern" title="http://www.blender.org/" rel="nofollow">Blender</a>, with an OgreXML Exporter plugin. 
</p>

<p>
<strong>Tip:</strong> Learn how to create <a href="http://en.wikibooks.org/wiki/Blender_3D:_Noob_to_Pro/UV_Map_Basics" class="urlextern" title="http://en.wikibooks.org/wiki/Blender_3D:_Noob_to_Pro/UV_Map_Basics" rel="nofollow">UV textures</a> for more complex models, it looks more professional. 
</p>

<p>
3D model editors are third-party products, so please consult their documentation for instructions how to use them. Here is an example workflow for Blender users:
</p>
<ul>
<li class="level1"><div class="li"> <a href="/jme3/external/blender.html" class="wikilink1" title="jme3:external:blender">Creating jME3 compatible 3D models in Blender</a></div>
</li>
</ul>

<p>
To export your models as Ogre XML meshes with materials:
</p>
<ol>
<li class="level1"><div class="li"> Open the menu File &gt; Export &gt; OgreXML Exporter to open the exporter dialog.</div>
</li>
<li class="level1"><div class="li"> In the Export Materials field: Give the material the same name as the model. For example, the model <code>something.mesh.xml</code> goes with <code>something.material</code>, plus (optionally) <code>something.skeleton.xml</code>, and some JPG files.</div>
</li>
<li class="level1"><div class="li"> In the Export Meshes field: Select a target subdirectory of your <code>assets/Models/</code> directory. E.g. <code>assets/Models/something/</code>.</div>
</li>
<li class="level1"><div class="li"> Activate the following exporter settings: </div>
<ul>
<li class="level2"><div class="li"> Copy Textures: YES</div>
</li>
<li class="level2"><div class="li"> Rendering Materials: YES</div>
</li>
<li class="level2"><div class="li"> Flip Axis: YES</div>
</li>
<li class="level2"><div class="li"> Require Materials: YES</div>
</li>
<li class="level2"><div class="li"> Skeleton name follows mesh: YES</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Click export.</div>
</li>
</ol>

<p>
You can now use the <a href="/sdk.html" class="wikilink1" title="sdk">jMonkeyEngine SDK</a> to <a href="/sdk/model_loader_and_viewer.html" class="wikilink1" title="sdk:model_loader_and_viewer">load and view models</a>. You can <a href="/sdk/scene_composer.html" class="wikilink1" title="sdk:scene_composer">create scenes</a> from them and write code that loads them into your application. 
</p>

</div>
<!-- EDIT3 SECTION "Creating Models and Scenes" [902-] -->
