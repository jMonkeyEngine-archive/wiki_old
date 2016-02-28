---
title: Space Lion on game assets
---
<h2 class="sectionedit1" id="space_lion_on_game_assets">Space Lion on game assets</h2>
<div class="level2">

<p>
<a href="/resources/space_lion_test.jpg" class="media" title="space_lion_test.jpg"><img src="/resources/space_lion_test.jpg" class="media" alt="" /></a>
</p>

<p>
Hello, I want to talk about several aspects of making game assets. Some of them will refer to the free open source software Blender, but some of them will be valid in a more general way.
</p>

<p>
If you're already an expert who makes 3d game assets for a living, this introduction might not be that much of a gain to you. There are other wiki pages describing how to get your Blender assets into a jME3 game or asset pack.
</p>

<p>
Well, that said, let's start…
</p>

</div>
<!-- EDIT1 SECTION "Space Lion on game assets" [1-515] -->
<h3 class="sectionedit2" id="different_3d_modeling_workflows">1. Different 3d modeling workflows</h3>
<div class="level3">

<p>
There are many ways to model a 3d asset:
</p>
<ul>
<li class="level1"><div class="li"> Low-Poly-First</div>
</li>
<li class="level1"><div class="li"> High-Poly-First</div>
</li>
<li class="level1"><div class="li"> 3D-Scan-First (a special kind of High-Poly-First)</div>
</li>
<li class="level1"><div class="li"> Topology-Sculpting</div>
</li>
</ul>

</div>

<h4 id="low-poly-first">1.1 Low-Poly-First</h4>
<div class="level4">

<p>
Based on reference images (drawn concept art or photographs or blueprints) you create a low-poly-mesh in a 3d modeling tool such as Blender. If you just want a quick test, you can stop here - just give your low-poly-mesh a material such as “wood” or “iron” or some procedural texture (NeoTexture plugin). 
</p>

<p>
But if you want higher quality game assets you will continue: Next, you would create an UV layout. This step is explained later in this tutorial. Basically the UV layout is needed for textures and normal maps.
</p>

<p>
In order to get a fancy normal map for your low-poly-mesh, you would now add a “Multiresolution” modifier, so you can sculpt details. There are two Multires modifiers available in Blender: “Catmull-Clark” and “Simple” (see image below)
</p>

<p>
<a href="/resources/multires_modifiers.png" class="media" title="multires_modifiers.png"><img src="/resources/multires_modifiers.png" class="media" alt="" /></a>
</p>

<p>
When should you use which? Here is a comparison table:
</p>
<div class="table sectionedit3"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0 leftalign"> Catmull-Clark     </th><th class="col1"> Simple </th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0"> + good for 'organic' models </td><td class="col1"> + good for 'technical' models </td>
	</tr>
	<tr class="row2">
		<td class="col0"> + auto-smoothes everything </td><td class="col1"> + keeps sharp features </td>
	</tr>
	<tr class="row3">
		<td class="col0"> - smoothes sharp features away </td><td class="col1"> - organic parts: smooth sculpting brush by hand </td>
	</tr>
</table></div>
<!-- EDIT3 TABLE [1589-1824] -->
<p>
Basically the teeth of a space monster need to be sharp, and I didn't find a good way - so I used “Simple” first and then later, I used the smooth brush in sculpt mode. Maybe someone has a good idea for me?
</p>

<p>
Another question is: Do I first give the model a texture or do I first sculpt the details? In my case, I did texture first, then sculpt the details - I was able to orient on the veins and other areas of the model. If you sculpt first, you will have to switch on the highest details of the Multires during texturing, which is slow. So, texture first is usually better.
</p>

</div>

<h4 id="high-poly-first">1.2 High-Poly-First</h4>
<div class="level4">

<p>
This workflow is best for technical stuff like “buildings” or “sci-fi-weapons”. It would not make sense, to sculpt on these objects like you would on an organic model. Instead, you create a very high-poly-mesh that has lots of little details like ridges, screws, gears, lamps, power cables, and so on.
</p>

<p>
When you've finished this stage, you will now create a copy of the high-poly-version. In the copy you would find some key vertices that you find good and which represent the overall shape in the best possible way. You will delete all the other vertices, and maybe create some more in a similar way, but all low-poly this time.
</p>

<p>
In the next stage you would create an UV layout for textures in the low-poly-version and project the high-poly-mesh of the original onto the low-poly-mesh via texture baking, using the “Bake &gt; Normals” section in the “Render” tab of the “Properties” view of Blender. You must first select the high-poly-mesh, then shift-select the low-poly-mesh and chose [x]“Selected to Active”.
</p>

<p>
For a detailed workflow description of the baking-normals-process, there will be a section later in this tutorial, that will cover this subject.
</p>

<p>
Another important note here: If you try to make “water tight models”, needed for certain 3D algorithms, then you would normally only do this for the low-poly-version of your model. The high-poly-version can be modelled faster, because you will only need it as a base for the normal map or maybe for some still-render cutscenes.
</p>

</div>

<h4 id="d-scan-first">1.3 3D-Scan-First</h4>
<div class="level4">

<p>
This workflow is similar to the “High-Poly-First” workflow. The original mesh is obtained via 3D scanning. If you don't know a lot about 3D scanning: You will be surprised how many good and cheap ways there are to get a 3D scan! Getting 3D scans can be as easy as using a free tool together with your webcam or mobile phone.
</p>

<p>
You would then polish the 3D scan with tools like “Meshlab”, to get a nice and complete version of your 3D Scan. Usually the scan will now consist of a vertex colored triangle mesh with a very high polygon count.
</p>

<p>
The rest is similar to the High-Poly-First way of doing things: Make a copy of the high-poly-version, select some vertices and delete the others. You now have a low-poly-version. All you have to do now, is finding a way to project the vertex colors of the high-poly-version onto the low-poly-version as a texture - you would use texture baking for this (detailed description will follow).
</p>

</div>

<h4 id="topology-sculpting">1.4 Topology-Sculpting</h4>
<div class="level4">

<p>
This workflow relies on a 'sculpting mode all from the start' approach: You sculpt the mesh from the beginning on and later you work similar to the 3D-Scan-First workflow (retopo the mesh and get a low poly version). In this video you can see somebody modeling a demon face with horns:
<a href="/lib/exe/fetch.php/youtube_opskpccfbr4" class="media mediafile mf_ wikilink2" title="youtube_opskpccfbr4">youtube_opskpccfbr4</a>
</p>

</div>
<!-- EDIT2 SECTION "1. Different 3d modeling workflows" [516-5225] -->
<h3 class="sectionedit4" id="several_hints_for_making_game_art">2. Several hints for making game art</h3>
<div class="level3">
<div class="table sectionedit5"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0"> You want to… </th><th class="col1"> What you need to do: </th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0"> Make humans </td><td class="col1"> Get “makehuman” <br />
use it <br />
export your humans to Blender <br />
polish them <br />
import them via the jME SDK. </td>
	</tr>
	<tr class="row2">
		<td class="col0"> Sculpt like a pro </td><td class="col1"> Blender's sculpting mode is enough for beginners like me. <br />
However, there are other tools like “Sculptris”, “Z Brush”, “Mudbox” and more </td>
	</tr>
	<tr class="row3">
		<td class="col0"> Make sci-fi assets </td><td class="col1"> Get yourself a collection of “greebles” (little surface details and gismos) <br />
combine them in numerous ways, <br />
to achieve the high-poly sci-fi model of your dream <br />
or just doom-style walls and machines <br />
look for “shipyard 0.7” on BlendSwap.com </td>
	</tr>
	<tr class="row4">
		<td class="col0"> Get free models </td><td class="col1"> Look at “OpenGameArt.org”, “BlendSwap.com”, “Turbosquid.com” or similar sites <br />
“OpenGameArt”: Lots of models, all of them for games, not all of them Blender, all free <br />
“BlendSwap”: Lots of models, not all of them for games, all of them Blender, all free <br />
“Turbosquid”: Lots of models, not all of them for games, not all of them Blender, not all free <br />
you will find a lot of models and textures on the internet. * </td>
	</tr>
</table></div>
<!-- EDIT5 TABLE [5274-6320] -->
<p>
(*) When they are licensed under CC0 or CC-BY, you can easily use them. CC-BY requires you to mention the original artist in a certain way in your games “credits roll”. Some very good models are under CC-BY-SA, which means that your program must be under open source license when you want to use these models. Other licenses are <abbr title="GNU Lesser General Public License">LGPL</abbr> (similar to CC-BY) and <abbr title="GNU General Public License">GPL</abbr> (similar to CC-BY-SA). There are other licenses, licensing can be a complex topic…
</p>

</div>

<h4 id="styleold_school_versus_new_school">2.1 Style: Old School versus New School</h4>
<div class="level4">

<p>
Here is what I mean by those two different styles:
</p>

<p>
<a href="/resources/old_school_vs_new_school_1_low.png" class="media" title="old_school_vs_new_school_1_low.png"><img src="/resources/old_school_vs_new_school_1_low.png" class="media" alt="" /></a>
<a href="/resources/old_school_vs_new_school_2_low.png" class="media" title="old_school_vs_new_school_2_low.png"><img src="/resources/old_school_vs_new_school_2_low.png" class="media" alt="" /></a>
<a href="/resources/old_school_vs_new_school_3_low.png" class="media" title="old_school_vs_new_school_3_low.png"><img src="/resources/old_school_vs_new_school_3_low.png" class="media" alt="" /></a>
</p>

<p>
This is a typical New School bow for a fantasy setting:
</p>

<p>
<a href="/resources/octavio_mendez_sanchez_durian_guardian_equipment.jpg" class="media" title="octavio_mendez_sanchez_durian_guardian_equipment.jpg"><img src="/resources/octavio_mendez_sanchez_durian_guardian_equipment.jpg" class="media" alt="" /></a>
</p>
<div class="table sectionedit6"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0 leftalign"> Old School    </th><th class="col1"> New School </th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0"> - looks simple </td><td class="col1"> + looks “cool” </td>
	</tr>
	<tr class="row2">
		<td class="col0"> + usually less work needed </td><td class="col1"> - usually more work needed </td>
	</tr>
	<tr class="row3">
		<td class="col0"> + less details render faster </td><td class="col1"> - fine details demand complex shape (slow) </td>
	</tr>
	<tr class="row4">
		<td class="col0"> + good enough for prototyping </td><td class="col1"> + more appealing to many modern gamers </td>
	</tr>
	<tr class="row5">
		<td class="col0"> + cheap items for lower-level game characters </td><td class="col1"> + helps visualize maxed-out game characters </td>
	</tr>
	<tr class="row6">
		<td class="col0"> + cultural style: humans, androids, … </td><td class="col1"> + cultural style: elves, telepathic aliens, … </td>
	</tr>
</table></div>
<!-- EDIT6 TABLE [7113-7582] -->
</div>

<h4 id="stylecomic-look_versus_realistic_look">2.2 Style: Comic-look versus Realistic look</h4>
<div class="level4">

<p>
There are great differences between a scene that was made to look realistic and a scene that has this certain “comic-look” (usually characters with crazy proportions: big heads, big eyes, extremely thin arms and legs).
</p>
<div class="table sectionedit7"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0 leftalign"> Comic-look    </th><th class="col1"> Realistic look </th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0"> + can be achieved very quickly <br />
(usually no normal maps etc.) </td><td class="col1"> - realistic models need a lot of work <br />
(several textures like normal, specular, gloss) </td>
	</tr>
	<tr class="row2">
		<td class="col0"> + more artistic freedom </td><td class="col1"> - artistic freedom is limited </td>
	</tr>
	<tr class="row3">
		<td class="col0"> - not suitable for some applications </td><td class="col1"> + suitable for simulations and AAA games </td>
	</tr>
	<tr class="row4">
		<td class="col0"> - usually animated by hand </td><td class="col1"> + can make use of motion capturing </td>
	</tr>
	<tr class="row5">
		<td class="col0"> + can be combined with hand-made textures </td><td class="col1"> - need high quality textures to look convincing </td>
	</tr>
	<tr class="row6">
		<td class="col0"> - hard to find free models all in the same style </td><td class="col1"> + easy to find models, because style always the same </td>
	</tr>
	<tr class="row7">
		<td class="col0"> + can make violence look sweet </td><td class="col1"> - violence might offend some people </td>
	</tr>
</table></div>
<!-- EDIT7 TABLE [7857-8539] -->
<p>
This comparison is not complete by far. I'm quite sure that there are more lenses that you could observe these two opponents and compare them, to find the best suitable for your project.
</p>

</div>

<h4 id="stylebe_consistent">2.3 Style: Be consistent!</h4>
<div class="level4">

<p>
Whatever your style/look for your 3D project is - you should be consistent when making the art assets. What this means? Stick to one way of doing things, so that all art assets fit together harmonically. Usually this means that you will have a hard time doing your comic-look world or your fantasy / sci-fi setting.
</p>

<p>
There are several parameters that must match:
</p>
<div class="table sectionedit8"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0"> What must I consider? </th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0"> high details <strong>vs</strong> low details </td>
	</tr>
	<tr class="row2">
		<td class="col0"> fantasy tech <strong>vs</strong> logically engineered tech </td>
	</tr>
	<tr class="row3">
		<td class="col0"> funny games <strong>vs</strong> serious games / simulations </td>
	</tr>
	<tr class="row4">
		<td class="col0"> toon shading <strong>vs</strong> simple shading <strong>vs</strong> photorealistic shading </td>
	</tr>
	<tr class="row5">
		<td class="col0"> colors and post processing filters should fit well </td>
	</tr>
	<tr class="row6">
		<td class="col0"> old school <strong>vs</strong> new school </td>
	</tr>
	<tr class="row7">
		<td class="col0"> comic look <strong>vs</strong> realistic look </td>
	</tr>
	<tr class="row8">
		<td class="col0"> … </td>
	</tr>
</table></div>
<!-- EDIT8 TABLE [9128-9492] -->
</div>

<h4 id="new_low_poly_modeling">2.4 New Low Poly modeling</h4>
<div class="level4">

<p>
There is an old way of doing Low-Poly and there is a new way of doing Low-Poly: In old games, you often saw assets with an ultra low poly count, mainly focussed on triangles. In newer game art you can often see lots of quads instead of triangles, which is mainly because this works best together with sculpting and animations.
</p>

</div>

<h4 id="lod_levels_of_detail">2.5 LOD (Levels Of Detail)</h4>
<div class="level4">

<p>
The jME engine supports LOD - the same model is represented in several ways: From high-detail to low-detail. The high-detail levels show the whole geometry (which is typically 10000 triangles for modern game characters), the lower levels reduce this geometry (you can actually control how many polygons, e.g. 5000, 2500, 1250, 625, …). The further away your model is, the fewer polygons are needed to represent its shape, because it will only be a few pixels large when this far away.
</p>

<p>
Both the Ogre-exporter and the jME SDK provide ways to configure the LOD steps of your model.
</p>

</div>

<h4 id="multiple_versions_for_different_purposes">2.6 Multiple versions for different purposes</h4>
<div class="level4">

<p>
In addition to LOD, you might be interested in providing several versions of your model, for different purposes. Here are some examples of what I mean:
</p>
<ul>
<li class="level1"><div class="li"> Shotgun model: a) equipped or laying around / b) during reloading, with open-barrel-animation</div>
</li>
<li class="level1"><div class="li"> Rocket launcher model: a) version with 4 rocket heads / b) version with 3, 2, 1, 0 rocket heads</div>
</li>
<li class="level1"><div class="li"> Rocket launcher model: a) version with closed hatch / b) version with open hatch and warhead</div>
</li>
<li class="level1"><div class="li"> Car model: a) without a scratch / b) somewhat damaged, heavily damaged, totally wrecked</div>
</li>
<li class="level1"><div class="li"> 3d Chat smiley: a) neutral face / b) workaround* for extreme shape change: laughing, surprised, angry…</div>
</li>
<li class="level1"><div class="li"> Evil samurai-demons: a) normal shape / b) sliced in two parts (several versions)</div>
</li>
</ul>

<p>
(*) This workaround will not be necessary anymore as soon as the engine allows for shape key deformation animations. You can also rig a face with bones, if you know how to do it well.
</p>

</div>
<!-- EDIT4 SECTION "2. Several hints for making game art" [5226-11449] -->
<h3 class="sectionedit9" id="uv_mapping">3. UV mapping</h3>
<div class="level3">

</div>

<h4 id="seams-unwrap_versus_auto-unwrap">3.1 Seams-Unwrap versus Auto-Unwrap</h4>
<div class="level4">

</div>

<h4 id="few_isles_versus_many_isles">3.2 Few Isles versus Many Isles</h4>
<div class="level4">

</div>

<h4 id="large_isles_versus_small_isles">3.3 Large Isles versus Small Isles</h4>
<div class="level4">

</div>

<h4 id="margins_-_the_answer_to_color_bleeding">3.4 Margins - the answer to color bleeding</h4>
<div class="level4">

</div>

<h4 id="details_by_mesh_versus_details_by_texture">3.5 Details by Mesh versus Details by Texture</h4>
<div class="level4">

</div>
<!-- EDIT9 SECTION "3. UV mapping" [11450-11706] -->
<h3 class="sectionedit10" id="rigging_basics">4. Rigging basics</h3>
<div class="level3">

</div>

<h4 id="different_types_of_rigs">4.1 Different types of rigs</h4>
<div class="level4">

</div>

<h4 id="skinning_with_vertex_group_editing">4.2 Skinning with vertex group editing</h4>
<div class="level4">

</div>

<h4 id="skinning_with_weight_painting">4.3 Skinning with weight painting</h4>
<div class="level4">

</div>

<h4 id="finding_unassigned_vertices">4.4 Finding unassigned vertices</h4>
<div class="level4">

</div>

<h4 id="posing_with_bone_constraints">4.5 Posing with bone constraints</h4>
<div class="level4">

</div>
<!-- EDIT10 SECTION "4. Rigging basics" [11707-11941] -->
<h3 class="sectionedit11" id="texturing">5. Texturing</h3>
<div class="level3">

</div>

<h4 id="painting_basic_texture_colors_in_2d">5.1 Painting basic texture colors in 2d</h4>
<div class="level4">

</div>

<h4 id="painting_texture_details_in_3d">5.2 Painting texture details in 3d</h4>
<div class="level4">

</div>

<h4 id="baking_texture_with_margin_around_isles">5.3 Baking texture with margin around isles</h4>
<div class="level4">

</div>

<h4 id="other_types_of_handmade_textures">5.4 Other types of handmade textures</h4>
<div class="level4">

</div>

<h4 id="baking_normal_maps">5.5 Baking normal maps</h4>
<div class="level4">

</div>

<h4 id="other_baking_techniques">5.6 Other baking techniques</h4>
<div class="level4">

</div>

<h4 id="texture_coordinate_recycling">5.7 Texture coordinate recycling</h4>
<div class="level4">

</div>

<h4 id="texture_atlas_sharing">5.8 Texture atlas sharing</h4>
<div class="level4">

</div>

<h4 id="human_faces_and_bodies">5.9 Human faces and bodies</h4>
<div class="level4">

</div>
<!-- EDIT11 SECTION "5. Texturing" [11942-12330] -->
<h3 class="sectionedit12" id="the_end">The End</h3>
<div class="level3">

<p>
Bye bye, polygon land, the Space Lion now rests to sleep. He will dream of digitally animated antilopes. He will dream of a glorious future for his favorite open source modeling tool. He will dream of the monkeys that live on their Java island. Another day, another project…
</p>

</div>
<!-- EDIT12 SECTION "The End" [12331-] -->
