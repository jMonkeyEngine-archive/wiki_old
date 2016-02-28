---
title: MakeHuman Blender OgreXML toolchain for creating and importing animated human characters
---
<h1 class="sectionedit1" id="makehuman_blender_ogrexml_toolchain_for_creating_and_importing_animated_human_characters">MakeHuman Blender OgreXML toolchain for creating and importing animated human characters</h1>
<div class="level1">

<p>
This guide describes how to use MakeHuman Blender OgreXML toolchain.
</p>

</div>
<!-- EDIT1 SECTION "MakeHuman Blender OgreXML toolchain for creating and importing animated human characters" [1-174] -->
<h3 class="sectionedit2" id="tools">Tools</h3>
<div class="level3">

<p>
The latest versions at time of writing are:
</p>
<ul>
<li class="level1"><div class="li"> MakeHuman: 1.0.2</div>
</li>
<li class="level1"><div class="li"> Blender: 2.72</div>
</li>
<li class="level1"><div class="li"> OgreXML exporter for Blender: 0.6.0</div>
</li>
</ul>

<p>
The tools can be downloaded from the following URLs:
</p>
<ul>
<li class="level1"><div class="li"> MakeHuman: [<a href="http://www.makehuman.org/]" class="urlextern" title="http://www.makehuman.org/]" rel="nofollow">http://www.makehuman.org/]</a></div>
</li>
<li class="level1"><div class="li"> Blender: [<a href="http://www.blender.org/]" class="urlextern" title="http://www.blender.org/]" rel="nofollow">http://www.blender.org/]</a></div>
</li>
<li class="level1"><div class="li"> OgreXML exporter for Blender: [<a href="https://code.google.com/p/blender2ogre/downloads/list]" class="urlextern" title="https://code.google.com/p/blender2ogre/downloads/list]" rel="nofollow">https://code.google.com/p/blender2ogre/downloads/list]</a></div>
</li>
</ul>

</div>
<!-- EDIT2 SECTION "Tools" [175-543] -->
<h3 class="sectionedit3" id="seed_project">Seed Project</h3>
<div class="level3">

<p>
Public domain seed project with some preset characters and animations:
</p>
<ul>
<li class="level1"><div class="li"> JME3 Open Asset Pack: [<a href="https://github.com/bubblecloud/jme3-open-asset-pack]" class="urlextern" title="https://github.com/bubblecloud/jme3-open-asset-pack]" rel="nofollow">https://github.com/bubblecloud/jme3-open-asset-pack]</a></div>
</li>
</ul>

</div>
<!-- EDIT3 SECTION "Seed Project" [544-720] -->
<h3 class="sectionedit4" id="preparation">Preparation</h3>
<div class="level3">
<ol>
<li class="level1"><div class="li"> Install MakeHuman and Blender.</div>
</li>
<li class="level1"><div class="li"> Install MakeHuman Blender importer from MakeHuman installation to Blender scripts folder and enable the script from Blender File → User Preferences → Addons.</div>
</li>
<li class="level1"><div class="li"> Install OgreXML exporter to Blender scripts folder and enable the script from Blender File → User Preferences → Addons.</div>
</li>
<li class="level1"><div class="li"> Clone the seed project or create your own project.</div>
</li>
<li class="level1"><div class="li"> Locate or create character model folder (src/main/resources/character/human/female)</div>
</li>
</ol>

</div>
<!-- EDIT4 SECTION "Preparation" [721-1212] -->
<h3 class="sectionedit5" id="creating_character_model_with_makehuman">Creating Character Model with MakeHuman</h3>
<div class="level3">
<ol>
<li class="level1"><div class="li"> Create character model with MakeHuman. ([<a href="http://www.makehuman.org/documentation]" class="urlextern" title="http://www.makehuman.org/documentation]" rel="nofollow">http://www.makehuman.org/documentation]</a>)</div>
<ul>
<li class="level2"><div class="li"> NOTE: If you want to use JME3 Open Asset Pack animations without tweaking then use either male.mhm or female.mhm as preset and do not change the body proportions.</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Choose basic skeleton from Pose/Animate tab if you are not already using either of the presets.</div>
</li>
<li class="level1"><div class="li"> Export to blender exchange format from Files → Export tab.</div>
<ul>
<li class="level2"><div class="li"> Choose Mesh Format → Blender exchange.</div>
</li>
<li class="level2"><div class="li"> Tick only Options → Feet on Ground and Scale Units → Meter </div>
</li>
</ul>
</li>
</ol>

</div>
<!-- EDIT5 SECTION "Creating Character Model with MakeHuman" [1213-1797] -->
<h3 class="sectionedit6" id="animating_character_model_with_blender">Animating Character Model with Blender</h3>
<div class="level3">
<ol>
<li class="level1"><div class="li"> Import the character model in blender exchange format (MHX) to Blender or open preset blender file female.blend.</div>
</li>
<li class="level1"><div class="li"> If you use your own character you can append animations from male.blend or female.blend preset files with Blender File → Append  function. Animations are in the animation folder.</div>
</li>
<li class="level1"><div class="li"> Tune the character model / materials and animate the character. ([<a href="http://www.blender.org/support/tutorials/]" class="urlextern" title="http://www.blender.org/support/tutorials/]" rel="nofollow">http://www.blender.org/support/tutorials/]</a>)</div>
</li>
</ol>

</div>
<!-- EDIT6 SECTION "Animating Character Model with Blender" [1798-2262] -->
<h3 class="sectionedit7" id="exporting_character_model_from_blender_to_ogre_xml">Exporting Character Model from Blender to Ogre XML</h3>
<div class="level3">
<ol>
<li class="level1"><div class="li"> Make sure that your scene objects in Blender do not have any spaces or special characters in their names. Rename them if they do.</div>
</li>
<li class="level1"><div class="li"> Arrange all your animations in single NLA track after each other without overlaps or touching in the timeline.</div>
</li>
<li class="level1"><div class="li"> Unlink any animations linked directly to your character armature or mesh.</div>
</li>
<li class="level1"><div class="li"> Export using Blender → File → Export Ogre3D (scene and mesh) and tick the following options:</div>
<ul>
<li class="level2"><div class="li"> copy shader programs</div>
</li>
<li class="level2"><div class="li"> Export Scen</div>
</li>
<li class="level2"><div class="li"> Export Meshes</div>
</li>
<li class="level2"><div class="li"> Export Meshes (overwrite)</div>
</li>
<li class="level2"><div class="li"> Armature Animation</div>
</li>
<li class="level2"><div class="li"> Optimize Arrays</div>
</li>
<li class="level2"><div class="li"> Export Materials</div>
</li>
<li class="level2"><div class="li"> Tangents</div>
</li>
<li class="level2"><div class="li"> Reorganize Buffers</div>
</li>
<li class="level2"><div class="li"> Optimize Animations</div>
</li>
</ul>
</li>
</ol>

</div>
<!-- EDIT7 SECTION "Exporting Character Model from Blender to Ogre XML" [2263-2983] -->
<h3 class="sectionedit8" id="importing_ogre_xml_to_jme3">Importing Ogre XML to JME3</h3>
<div class="level3">

<p>
You can load the ogre XML with asset manager or import them to SDK and hence convert them to JME3 asset format.
</p>

<p>
You can test the animations by making your own version of AnimationPreviewer:
</p>

<p>
<a href="https://github.com/bubblecloud/jme3-open-asset-pack/blob/master/src/main/java/com/jme3/asset/AnimationPreview.java" class="urlextern" title="https://github.com/bubblecloud/jme3-open-asset-pack/blob/master/src/main/java/com/jme3/asset/AnimationPreview.java" rel="nofollow">https://github.com/bubblecloud/jme3-open-asset-pack/blob/master/src/main/java/com/jme3/asset/AnimationPreview.java</a>
</p>

</div>
<!-- EDIT8 SECTION "Importing Ogre XML to JME3" [2984-] -->
