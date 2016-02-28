---
title: Warg - from cube to animated and textured game model Example
---
<h1 class="sectionedit1" id="warg_-_from_cube_to_animated_and_textured_game_model_example">Warg - from cube to animated and textured game model Example</h1>
<div class="level1">

<p>
</p><p></p><div class="noteimportant">to make this example you need to know basic of modeling like extending faces / merge vertexes / (move vertex / edge / face) / etc. 
</div>


</div>
<!-- EDIT1 SECTION "Warg - from cube to animated and textured game model Example" [2-233] -->
<h2 class="sectionedit2" id="preview">Preview</h2>
<div class="level2">

<p>
<a href="/resources/jme3-external-preview.jpg" class="media" title="jme3:external:preview.jpg"><img src="/resources/jme3-external-preview.jpg" class="media" alt="" /></a>
</p>

</div>
<!-- EDIT2 SECTION "Preview" [234-287] -->
<h2 class="sectionedit3" id="step_1_-_prepare">Step 1 - Prepare</h2>
<div class="level2">

<p>
- Open Blender with new Scene
- Add a simple Cube. To make it press shift-a and select Cube
</p>

<p>
<a href="/resources/jme3-external-2.jpg" class="media" title="jme3:external:2.jpg"><img src="/resources/jme3-external-2.jpg" class="media" alt="" /></a>
</p>

<p>
- “t” key open tool window. let’s open it and set x-mirror ON
</p>

<p>
<a href="/resources/jme3-external-4.jpg" class="media" title="jme3:external:4.jpg"><img src="/resources/jme3-external-4.jpg" class="media" alt="" /></a>
</p>

<p>
- Subdivide this cube to get more faces
* this can be also done via modifiers → subdivision surface (it will be later)
</p>

<p>
<a href="/resources/jme3-external-5.jpg" class="media" title="jme3:external:5.jpg"><img src="/resources/jme3-external-5.jpg" class="media" alt="" /></a>
</p>

<p>
- “n” key open second toolbar with useable options. let's load an example image to help us build Warg.
I found a nice warg image on devian art.
</p>

<p>
<a href="/resources/jme3-external-example.jpg" class="media" title="jme3:external:example.jpg"><img src="/resources/jme3-external-example.jpg" class="media" alt="" /></a>
</p>

<p>
- make simple Warg Shape like on images
</p>

<p>
<a href="/resources/jme3-external-6.jpg" class="media" title="jme3:external:6.jpg"><img src="/resources/jme3-external-6.jpg" class="media" alt="" /></a>
<a href="/resources/jme3-external-7.jpg" class="media" title="jme3:external:7.jpg"><img src="/resources/jme3-external-7.jpg" class="media" alt="" /></a>
<a href="/resources/jme3-external-9.jpg" class="media" title="jme3:external:9.jpg"><img src="/resources/jme3-external-9.jpg" class="media" alt="" /></a>
</p>

</div>
<!-- EDIT3 SECTION "Step 1 - Prepare" [288-982] -->
<h2 class="sectionedit4" id="step_2_-_modeling">Step 2 - Modeling</h2>
<div class="level2">

<p>
- in tool window(“t”) is a smooth tool that can help model the warg.
</p>

<p>
<a href="/resources/jme3-external-10.jpg" class="media" title="jme3:external:10.jpg"><img src="/resources/jme3-external-10.jpg" class="media" alt="" /></a>
</p>

<p>
- to easly add edge loop use “loop cut and slide” tool that work that way:
</p>

<p>
<a href="/resources/jme3-external-12.jpg" class="media" title="jme3:external:12.jpg"><img src="/resources/jme3-external-12.jpg" class="media" alt="" /></a>
<a href="/resources/jme3-external-13.jpg" class="media" title="jme3:external:13.jpg"><img src="/resources/jme3-external-13.jpg" class="media" alt="" /></a>
</p>

<p>
- Go to modifiers and add Mirror surface
</p>

<p>
<a href="/resources/jme3-external-14.jpg" class="media" title="jme3:external:14.jpg"><img src="/resources/jme3-external-14.jpg" class="media" alt="" /></a>
</p>

<p>
- add some details like eyes / etc.
</p>

<p>
</p><p></p><div class="noteimportant">need to know how to use extend faces(key “e”) and merge extended face.
</div>


<p>
<a href="/resources/jme3-external-15.jpg" class="media" title="jme3:external:15.jpg"><img src="/resources/jme3-external-15.jpg" class="media" alt="" /></a>
<a href="/resources/jme3-external-16.jpg" class="media" title="jme3:external:16.jpg"><img src="/resources/jme3-external-16.jpg" class="media" alt="" /></a>
</p>

<p>
- to use smooth shading just set it in tool window.
</p>

<p>
<a href="/resources/jme3-external-17.jpg" class="media" title="jme3:external:17.jpg"><img src="/resources/jme3-external-17.jpg" class="media" alt="" /></a>
</p>

<p>
- Apply modifier. just press “Apply” button in Mirror modifier.
- Remove doubles (it removes vertexes that are too close each other).
</p>

<p>
<a href="/resources/jme3-external-18.jpg" class="media" title="jme3:external:18.jpg"><img src="/resources/jme3-external-18.jpg" class="media" alt="" /></a>
</p>

</div>
<!-- EDIT4 SECTION "Step 2 - Modeling" [983-1754] -->
<h2 class="sectionedit5" id="step_2_-_armature">Step 2 - Armature</h2>
<div class="level2">

<p>
- Shift-a and add armature in Object Mode.
</p>

<p>
</p><p></p><div class="noteclassic">shift-a to add a bone in Edit Mode
</div>
<a href="/resources/jme3-external-19.jpg" class="media" title="jme3:external:19.jpg"><img src="/resources/jme3-external-19.jpg" class="media" alt="" /></a>
<p></p><div class="noteclassic">tail should be done in other way. Start to build skeleton from start of the tail (not end)
</div>
<a href="/resources/jme3-external-21.jpg" class="media" title="jme3:external:21.jpg"><img src="/resources/jme3-external-21.jpg" class="media" alt="" /></a>


<p>
- Show names and change armature view (if you like)
</p>

<p>
<a href="/resources/jme3-external-22.jpg" class="media" title="jme3:external:22.jpg"><img src="/resources/jme3-external-22.jpg" class="media" alt="" /></a>
</p>

<p>
- set Names for bones (via properties window or “n” option window)
</p>

<p>
<a href="/resources/jme3-external-23.jpg" class="media" title="jme3:external:23.jpg"><img src="/resources/jme3-external-23.jpg" class="media" alt="" /></a>
</p>

<p>
- Select left side bones only, press shift-d to copy them, and make mirror.
Remember to have cursor in 0,0,0 and have settings like on image (if not then you will need just to move copied bones manually)
</p>

<p>
<a href="/resources/jme3-external-25.jpg" class="media" title="jme3:external:25.jpg"><img src="/resources/jme3-external-25.jpg" class="media" alt="" /></a>
</p>

<p>
- Press “w” and select “flip names”
</p>

<p>
<a href="/resources/jme3-external-26.jpg" class="media" title="jme3:external:26.jpg"><img src="/resources/jme3-external-26.jpg" class="media" alt="" /></a>
<a href="/resources/jme3-external-27.jpg" class="media" title="jme3:external:27.jpg"><img src="/resources/jme3-external-27.jpg" class="media" alt="" /></a>
</p>

<p>
- In Object Mode:
* Select Model
* With SHIFT select armature
* Press “p” and select “with automatic weights”
</p>

<p>
<a href="/resources/jme3-external-28.jpg" class="media" title="jme3:external:28.jpg"><img src="/resources/jme3-external-28.jpg" class="media" alt="" /></a>
</p>

<p>
- Try move a leg in Pose Mode
</p><p></p><div class="noteclassic">Pose Mode work like Edit mode, use “r” to rotate a bone. using “x”/“y”/“z” after “g”/“r”/“s” will also work here like everything else.
</div>
<a href="/resources/jme3-external-29.jpg" class="media" title="jme3:external:29.jpg"><img src="/resources/jme3-external-29.jpg" class="media" alt="" /></a>


<p>
- Go to Animation View
</p>

<p>
<a href="/resources/jme3-external-30.jpg" class="media" title="jme3:external:30.jpg"><img src="/resources/jme3-external-30.jpg" class="media" alt="" /></a>
</p>

<p>
- Add a new action
</p>

<p>
<a href="/resources/jme3-external-31.jpg" class="media" title="jme3:external:31.jpg"><img src="/resources/jme3-external-31.jpg" class="media" alt="" /></a>
</p>

<p>
- Select all bones in Pose Mode and apply location / rottion / scale.
To do it press “i” and select it like on image:
</p>

<p>
<a href="/resources/jme3-external-32.jpg" class="media" title="jme3:external:32.jpg"><img src="/resources/jme3-external-32.jpg" class="media" alt="" /></a>
</p>

<p>
</p><p></p><div class="notetip">alt-r / alt-g / alt-s – clear rotation / location / scale
</div>
- there is possibility to copy poses


<p>
<a href="/resources/jme3-external-33.jpg" class="media" title="jme3:external:33.jpg"><img src="/resources/jme3-external-33.jpg" class="media" alt="" /></a>
</p>

<p>
- and also to copy them in mirrored pose
</p>

<p>
<a href="/resources/jme3-external-35.jpg" class="media" title="jme3:external:35.jpg"><img src="/resources/jme3-external-35.jpg" class="media" alt="" /></a>
</p>

<p>
- in action editor you can easly remove / move / scale frames
</p>

<p>
<a href="/resources/jme3-external-34.jpg" class="media" title="jme3:external:34.jpg"><img src="/resources/jme3-external-34.jpg" class="media" alt="" /></a>
</p>

<p>
- If animation work not linear (and you don't like it), then you can change it in Curve editor window
</p>

<p>
<a href="/resources/jme3-external-36.jpg" class="media" title="jme3:external:36.jpg"><img src="/resources/jme3-external-36.jpg" class="media" alt="" /></a>
</p>

<p>
- Thats all for Animations, for more just Read JME wiki / documentation.
</p>

</div>
<!-- EDIT5 SECTION "Step 2 - Armature" [1755-3661] -->
<h2 class="sectionedit6" id="step_2_-_texturing">Step 2 - Texturing</h2>
<div class="level2">

<p>
- Move armature to second layer.
press “m” to make it.
</p>

<p>
<a href="/resources/jme3-external-37.jpg" class="media" title="jme3:external:37.jpg"><img src="/resources/jme3-external-37.jpg" class="media" alt="" /></a>
</p>

<p>
- In edit mode, need to mark seam on Edges to prepare model for texturing.
press ctrl-e to make it.
</p>

<p>
<a href="/resources/jme3-external-38.jpg" class="media" title="jme3:external:38.jpg"><img src="/resources/jme3-external-38.jpg" class="media" alt="" /></a>
</p>

<p>
- do it similar to this (or you can make it better):
</p>

<p>
<a href="/resources/jme3-external-40.jpg" class="media" title="jme3:external:40.jpg"><img src="/resources/jme3-external-40.jpg" class="media" alt="" /></a>
<a href="/resources/jme3-external-41.jpg" class="media" title="jme3:external:41.jpg"><img src="/resources/jme3-external-41.jpg" class="media" alt="" /></a>
<a href="/resources/jme3-external-43.jpg" class="media" title="jme3:external:43.jpg"><img src="/resources/jme3-external-43.jpg" class="media" alt="" /></a>
</p>

<p>
- Press “u” and select first option “unwrap”
- In UV window you can minimize stretch
(minimize stretch change with mouse wheele).
</p>

<p>
<a href="/resources/jme3-external-44.jpg" class="media" title="jme3:external:44.jpg"><img src="/resources/jme3-external-44.jpg" class="media" alt="" /></a>
</p>

<p>
- make a 2 geometries for model:
* body (contains faces for body)
* eyes (containes faces for eyes)
</p>

<p>
<a href="/resources/jme3-external-45.jpg" class="media" title="jme3:external:45.jpg"><img src="/resources/jme3-external-45.jpg" class="media" alt="" /></a>
</p>

<p>
<a href="/resources/jme3-external-48.jpg" class="media" title="jme3:external:48.jpg"><img src="/resources/jme3-external-48.jpg" class="media" alt="" /></a>
</p>

<p>
- for eyes you can use “Sphere projection for unwrap”
</p>

<p>
<a href="/resources/jme3-external-49.jpg" class="media" title="jme3:external:49.jpg"><img src="/resources/jme3-external-49.jpg" class="media" alt="" /></a>
</p>

<p>
- Select texture image
</p>

<p>
<a href="/resources/jme3-external-50.jpg" class="media" title="jme3:external:50.jpg"><img src="/resources/jme3-external-50.jpg" class="media" alt="" /></a>
</p>

<p>
- under “n” option window, set like on image to see texture.
(ViewPort need to be set as solid, ViewPort is near Object/Edit select)
</p>

<p>
<a href="/resources/jme3-external-52.jpg" class="media" title="jme3:external:52.jpg"><img src="/resources/jme3-external-52.jpg" class="media" alt="" /></a>
</p>

<p>
- Just make texture of model (using Texture Mode – where Object / edit mode is)
</p>

<p>
</p><p></p><div class="noteclassic">under “t” tools you can change color / size / etc of brush
</div>


<p>
<a href="/resources/jme3-external-55.jpg" class="media" title="jme3:external:55.jpg"><img src="/resources/jme3-external-55.jpg" class="media" alt="" /></a>
</p>

<p>
- Using 2d tool like Gimp / Photoshop, use filter/modifier to get nice looking skin
</p>

<p>
<a href="/resources/jme3-external-56.jpg" class="media" title="jme3:external:56.jpg"><img src="/resources/jme3-external-56.jpg" class="media" alt="" /></a>
</p>

<p>
- Now only need to export via Ogre Mesh or just via Blend file (using SDK).
</p>

<p>
- For eyes and body, use separated j3m files, then set them in SceneComposer.
</p>

<p>
</p><p></p><div class="noteimportant">also don’t forget about NLA editor and set off envelopes to make animations work!
</div>


<p>
here are docs:
</p>

<p>
<a href="http://jmonkeyengine.org/wiki/doku.php/jme3:external:blender" class="urlextern" title="http://jmonkeyengine.org/wiki/doku.php/jme3:external:blender" rel="nofollow">http://jmonkeyengine.org/wiki/doku.php/jme3:external:blender</a>
</p>

<p>
- Done!
</p>

</div>
<!-- EDIT6 SECTION "Step 2 - Texturing" [3662-] -->
