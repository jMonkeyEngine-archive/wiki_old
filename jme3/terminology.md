---
title: 3D Game Development Terminology
---
<h1 class="sectionedit1" id="d_game_development_terminology">3D Game Development Terminology</h1>
<div class="level1">

<p>
Before you start, make certain you are familiar with the following concepts and terminology. 
</p>

</div>
<!-- EDIT1 SECTION "3D Game Development Terminology" [1-142] -->
<h1 class="sectionedit2" id="d_graphics_and_audio">3D Graphics and Audio</h1>
<div class="level1">

<p>
<strong>OpenGL</strong> is the Open Graphics Library, a platform-independent specification for rendering 2D/3D computer graphics. For Java, there are two implementations of OpenGL-based renderers:
</p>
<ol>
<li class="level1"><div class="li"> Lightweight Java Game Library (LWJGL).</div>
</li>
<li class="level1"><div class="li"> Java OpenGL (JOGL)</div>
</li>
</ol>

<p>
<strong>OpenAL</strong> is the Open Audio Library, a platform-independent 3D audio <abbr title="Application Programming Interface">API</abbr>.
</p>

</div>
<!-- EDIT2 SECTION "3D Graphics and Audio" [143-505] -->
<h1 class="sectionedit3" id="context_display_renderer">Context, Display, Renderer</h1>
<div class="level1">

<p>
The <strong>jME Context</strong> makes settings, renderer, timer, input and event listeners, display system, accessible to a JME game.
</p>
<ul>
<li class="level1"><div class="li"> The <strong>jME Display System</strong> is what draws the custom JME window (instead of Java Swing).</div>
</li>
<li class="level1"><div class="li"> The <strong>Input System</strong> is the component that lets you respond to user input: Mouse clicks and movements, keyboard presses, and joystick motions.</div>
</li>
<li class="level1"><div class="li"> The <strong>Renderer</strong> is what does all the work of calculating how to draw the 3D scenegraph to the 2D screen.</div>
<ul>
<li class="level2"><div class="li"> The <strong>Shader</strong> is a programmable part of the rendering pipeline. The jME3 game engine uses it to offer advanced customizable materials.</div>
</li>
</ul>
</li>
</ul>

</div>
<!-- EDIT3 SECTION "Context, Display, Renderer" [506-1161] -->
<h1 class="sectionedit4" id="geometry">Geometry</h1>
<div class="level1">

</div>
<!-- EDIT4 SECTION "Geometry" [1162-1185] -->
<h2 class="sectionedit5" id="polygon_mesh_vertex">Polygon, Mesh, Vertex</h2>
<div class="level2">

<p>
<a href="/resources/jme3-dolphin-mesh.png" class="media" title="jme3:dolphin-mesh.png"><img src="/resources/jme3-dolphin-mesh.png" class="mediaright" title="Models (here a dolphin) are made up of polygon meshes" alt="Models (here a dolphin) are made up of polygon meshes" /></a>
</p>

<p>
Most visible objects in a 3D scene are made up of polygon meshes – characters, terrains, buildings, etc. A mesh is a grid-like structure that represents a complex shape. The advantage of a mesh is that it is mathematically simple enough to render in real time, and detailed enough to be recognizable.
</p>

<p>
Every shape is reduced to a number of connected polygons, usually triangles; even round surfaces such as spheres are reduced to a grid of triangles. The polygons' corner points are called vertices. Every vertex is positioned at a coordinate, all vertices together describe the outline of the shape.
</p>

<p>
You create 3D meshes in tools called mesh editors, e.g in Blender. The jMonkeyEngine can load finished meshes (=models) and arrange them to scenes, but it cannot edit the mesh itself.
</p>

</div>
<!-- EDIT5 SECTION "Polygon, Mesh, Vertex" [1186-2089] -->
<h1 class="sectionedit6" id="materialscolor_lighting_shading">Materials: Color, Lighting/Shading</h1>
<div class="level1">

<p>
What we call “color” is merely part of an object's light reflection. The onlooker's brain uses shading and reflecting properties to infer an object's shape and material. Factors like these make all the difference between chalk vs milk, skin vs paper, water vs plastic, etc! (<a href="http://www.shaders.org/ifw2_textures/whatsin10.htm" class="urlextern" title="http://www.shaders.org/ifw2_textures/whatsin10.htm" rel="nofollow">External examples</a>)
</p>

</div>
<!-- EDIT6 SECTION "Materials: Color, Lighting/Shading" [2090-2489] -->
<h2 class="sectionedit7" id="color">Color</h2>
<div class="level2">

</div>
<!-- EDIT7 SECTION "Color" [2490-2506] -->
<h3 class="sectionedit8" id="ambient_color">Ambient color</h3>
<div class="level3">
<ul>
<li class="level1"><div class="li">  The uniform base color of the mesh – what it looks like when not influenced by any light source.</div>
</li>
<li class="level1"><div class="li"> Usually similar to the Diffuse color.</div>
</li>
<li class="level1"><div class="li"> This is the minimum color you need for an object to be visible.</div>
</li>
</ul>

</div>
<!-- EDIT8 SECTION "Ambient color" [2507-2741] -->
<h3 class="sectionedit9" id="diffuse_color">Diffuse color</h3>
<div class="level3">
<ul>
<li class="level1"><div class="li"> The base color of the mesh plus shattered light and shadows that are caused by a light source.</div>
</li>
<li class="level1"><div class="li"> Usually similar to the Ambient color.</div>
</li>
</ul>

</div>
<!-- EDIT9 SECTION "Diffuse color" [2742-2906] -->
<h2 class="sectionedit10" id="light_sources">Light Sources</h2>
<div class="level2">

</div>
<!-- EDIT10 SECTION "Light Sources" [2907-2931] -->
<h3 class="sectionedit11" id="emissive_color">Emissive color</h3>
<div class="level3">
<ul>
<li class="level1"><div class="li"> The color of light emitted by a light source or glowing material.</div>
</li>
<li class="level1"><div class="li"> Only glowing materials such as lights have an emissive color, normal objects don't have this property.</div>
</li>
<li class="level1"><div class="li"> Often white (sun light).</div>
</li>
</ul>

</div>
<!-- EDIT11 SECTION "Emissive color" [2932-3162] -->
<h2 class="sectionedit12" id="reflections">Reflections</h2>
<div class="level2">

</div>
<!-- EDIT12 SECTION "Reflections" [3163-3186] -->
<h3 class="sectionedit13" id="shininess">Shininess</h3>
<div class="level3">
<ul>
<li class="level1"><div class="li"> Degree of shininess of a surface (1-128).</div>
</li>
<li class="level1"><div class="li"> Shiny objects have small, clearly outlined specular highlights. (E.g. glass, water, silver)</div>
</li>
<li class="level1"><div class="li"> Normal objects have wide, blurry specular highlights. (E.g. metal, plastic, stone, polished materials)</div>
</li>
<li class="level1"><div class="li"> Uneven objects are not shiny and have no specular highlights. (E.g. cloth, paper, wood, snow) <br />
Set the Specular color to ColorRGBA.Black to switch off shininess.</div>
</li>
</ul>

</div>
<!-- EDIT13 SECTION "Shininess" [3187-3621] -->
<h3 class="sectionedit14" id="specular_color">Specular Color</h3>
<div class="level3">
<ul>
<li class="level1"><div class="li"> If the material is shiny, then the Specular Color is the color of the reflected highlights.</div>
</li>
<li class="level1"><div class="li"> Usually the same as the emissive color of the light source (e.g. white).</div>
</li>
<li class="level1"><div class="li"> You can use colors to achieve special specular effects, such as metallic or iridescent reflections.</div>
</li>
<li class="level1"><div class="li"> Non-shiny objects have a black specular color.</div>
</li>
</ul>

<p>
<a href="/resources/fetch.php" class="media" title="http://wiki.jmonkeyengine.org/lib/exe/fetch.php/jme3:tanlglow2.png"><img src="/resources/fetch.php" class="mediacenter" alt="" width="400" height="234" /></a>
</p>

</div>
<!-- EDIT14 SECTION "Specular Color" [3622-4056] -->
<h1 class="sectionedit15" id="materialstextures">Materials: Textures</h1>
<div class="level1">

<p>
Textures are part of Materials. In the simplest case, an object could have just one texture, the Color Map, loaded from one image file. When you think back of old computer games you'll remember this looks quite plain.
</p>

<p>
The more information you (the game designer) provide additionally to the Color Map, the higher the degree of detail and realism. Whether you want photo-realistic rendering or “toon” rendering (Cel Shading), everything depends on the quality of your materials and textures. Modern 3D graphics use several layers of information to describe one material, each mapped layer is a texture.
</p>

<p>
</p><p></p><div class="notetip">Got no textures? <a href="http://opengameart.org" class="urlextern" title="http://opengameart.org" rel="nofollow">Download free textures from opengameart.org</a>. Remember to keep the copyright notice together with the textures!
</div>


</div>
<!-- EDIT15 SECTION "Materials: Textures" [4057-4868] -->
<h2 class="sectionedit16" id="texture_mapping">Texture Mapping</h2>
<div class="level2">

</div>
<!-- EDIT16 SECTION "Texture Mapping" [4869-4895] -->
<h3 class="sectionedit17" id="color_map_diffuse_map">Color Map / Diffuse Map</h3>
<div class="level3">

<p>
<a href="/resources/fetch.php" class="media" title="http://jmonkeyengine.googlecode.com/svn/trunk/engine/test-data/Models/HoverTank/tank_diffuse.jpg"><img src="/resources/fetch.php" class="mediaright" title="jmonkeyengine.googlecode.com_svn_trunk_engine_test-data_models_hovertank_tank_diffuse.jpg" alt="jmonkeyengine.googlecode.com_svn_trunk_engine_test-data_models_hovertank_tank_diffuse.jpg" width="128" height="128" /></a>
</p>
<ul>
<li class="level1"><div class="li"> A plain image file or a procedural texture that describes an object's visible surface.</div>
</li>
<li class="level1"><div class="li"> The image can have alpha channels for transparency.</div>
</li>
<li class="level1"><div class="li"> <strong>A Color Map is the minimum texture.</strong> You can map more textures as optional improvements. </div>
</li>
<li class="level1"><div class="li"> Color Maps are unshaded. The same is called Diffuse Map in a Phong-illuminated material, because this texture defines the basic colors of light that are <em>diffused</em> by this object.</div>
</li>
</ul>

</div>
<!-- EDIT17 SECTION "Color Map / Diffuse Map" [4896-5470] -->
<h3 class="sectionedit18" id="bump_map">Bump Map</h3>
<div class="level3">

<p>
Bump maps are used to describe detailed shapes that would be too hard or simply too inefficient to sculpt in a mesh editor. There are two types:
</p>
<ul>
<li class="level1"><div class="li"> You use Normal Maps to model tiny details such as cracks in walls, rust, skin texture, or a canvas weave ( (<a href="http://en.wikipedia.org/wiki/Bump_mapping" class="urlextern" title="http://en.wikipedia.org/wiki/Bump_mapping" rel="nofollow">More on BumpMaps</a>). </div>
</li>
<li class="level1"><div class="li"> You use Height Maps to model large terrains with valleys and mountains.</div>
</li>
</ul>

<p>
<a href="/resources/fetch.php" class="media" title="http://jmonkeyengine.googlecode.com/svn/trunk/engine/test-data/Textures/Terrain/splat/mountains512.png"><img src="/resources/fetch.php" class="mediaright" alt="" width="128" height="128" /></a>
</p>

</div>

<h4 id="height_map">Height Map</h4>
<div class="level4">
<ul>
<li class="level1"><div class="li"> A height map is a grayscale image looking similar to a terrain map used in topography. Brighter grays represent higher areas and darker grays lower areas.</div>
</li>
<li class="level1"><div class="li"> A heightmap can represent 256 height levels and is mostly used to roughly outline terrains.</div>
</li>
<li class="level1"><div class="li"> You can draw a heightmap by hand in any image editor.</div>
</li>
</ul>

</div>

<h4 id="normal_map">Normal Map</h4>
<div class="level4">

<p>
<a href="/resources/fetch.php" class="media" title="http://jmonkeyengine.googlecode.com/svn/trunk/engine/test-data/Models/HoverTank/tank_normals.png"><img src="/resources/fetch.php" class="mediaright" alt="" width="128" height="128" /></a>
</p>
<ul>
<li class="level1"><div class="li"> A well-done Normal Map makes a shape more detailed – without the need to add costly polygons to the mesh. It contains shading information that makes the object appear smoother and more fine-grained.</div>
</li>
<li class="level1"><div class="li"> When you open a Normal Map in an image editor, it looks like a false-color version of the Color Map. Normal maps however are never used for coloring, instead, each the color values encode displacement data of bumps and cracks on the surface. Displacement data is represented by the Surface Normals of the slopes, hence the name.</div>
</li>
<li class="level1"><div class="li"> You cannot draw or edit normal maps by hand, professional designers use software to calculate them off high-quality 3D models. You can either buy a professional texture set, or find free collections that include Normal Maps.</div>
</li>
</ul>

</div>
<!-- EDIT18 SECTION "Bump Map" [5471-7232] -->
<h3 class="sectionedit19" id="specular_map">Specular Map</h3>
<div class="level3">

<p>
<a href="/resources/fetch.php" class="media" title="http://jmonkeyengine.googlecode.com/svn/trunk/engine/test-data/Models/HoverTank/tank_specular.jpg"><img src="/resources/fetch.php" class="mediaright" title="jmonkeyengine.googlecode.com_svn_trunk_engine_test-data_models_hovertank_tank_specular.jpg" alt="jmonkeyengine.googlecode.com_svn_trunk_engine_test-data_models_hovertank_tank_specular.jpg" width="128" height="128" /></a>
</p>
<ul>
<li class="level1"><div class="li"> A Specular Map further improves the realism of an object's surface: It contains extra information about shininess and makes the shape appear more realistically illumated.</div>
</li>
<li class="level1"><div class="li"> Start out with a copy of the Diffuse Map in a medium gray that corresponds to the average shininess/dullness of this material. Then add ligher grays for smoother, shinier, more reflective areas; and darker grays for duller, rougher, worn-out areas. The resulting image file looks similar to a grayscale version of the Diffuse Map.</div>
</li>
<li class="level1"><div class="li"> You can use colors in a Specular map to create certain reflective effects (fake iridiscence, metallic effect).</div>
</li>
</ul>

</div>
<!-- EDIT19 SECTION "Specular Map" [7233-7991] -->
<h2 class="sectionedit20" id="seamless_tiled_textures">Seamless Tiled Textures</h2>
<div class="level2">

<p>
<a href="/resources/fetch.php" class="media" title="http://jmonkeyengine.googlecode.com/svn/trunk/engine/test-data/Textures/Terrain/BrickWall/BrickWall.jpg"><img src="/resources/fetch.php" class="mediaright" title="jmonkeyengine.googlecode.com_svn_trunk_engine_test-data_textures_terrain_brickwall_brickwall.jpg" alt="jmonkeyengine.googlecode.com_svn_trunk_engine_test-data_textures_terrain_brickwall_brickwall.jpg" width="128" height="128" /></a>
Tiles are a very simple, commonly used type of texture. When texturing a wide area (e.g. walls, floors), you don't create one huge texture – instead you tile a small texture repeatedly to fill the area.
</p>

<p>
A seamless texture is an image file that has been designed or modified so that it can be used as tiles: The right edge matches the left edge, and the top edge matches the bottom edge. The onlooker cannot easily tell where one starts and the next one ends, thus creating an illusion of a huge texture. The downside is that the tiling becomes painfully obvious when the area is viewed from a distance. Also you cannot use it on more complex models such as characters. 
</p>

<p>
See also this tutorial on <a href="http://www.photoshoptextures.com/texture-tutorials/seamless-textures.htm" class="urlextern" title="http://www.photoshoptextures.com/texture-tutorials/seamless-textures.htm" rel="nofollow">How to make seamless textures in Photoshop</a>.
</p>

</div>
<!-- EDIT20 SECTION "Seamless Tiled Textures" [7992-8964] -->
<h2 class="sectionedit21" id="uv_maps_texture_atlas">UV Maps / Texture Atlas</h2>
<div class="level2">

<p>
<a href="/resources/fetch.php" class="media" title="http://jmonkeyengine.googlecode.com/svn/trunk/engine/test-data/Models/Ferrari/Car.jpg"><img src="/resources/fetch.php" class="mediaright" title="jmonkeyengine.googlecode.com_svn_trunk_engine_test-data_models_ferrari_car.jpg" alt="jmonkeyengine.googlecode.com_svn_trunk_engine_test-data_models_ferrari_car.jpg" width="128" height="128" /></a>
</p>

<p>
Creating a texture for a cube is easy – but what about a character with a face and extremities? For more complex objects, you design the texture in the same ways as a flat sewing pattern: One image file contains the outline of the front, back, and side of the object, next to one another. Specific areas of the flat texture (UV coordinates) map onto certain areas of your 3D model (XYZ coordinates), hence the name UV map. Using UV Maps (also known as Texture Atlas), one model can have different textures on each side. You create one corresponding UV map for each texture.
</p>

<p>
Getting the seams and mappings right is crucial: You must use a graphic tool like Blender to create UV Maps (Texture Atlas) and store the coordinates correctly. It's worth the while to learn this, UV mapped models look a lot more professional.
</p>

</div>
<!-- EDIT21 SECTION "UV Maps / Texture Atlas" [8965-9920] -->
<h2 class="sectionedit22" id="environment_mapping">Environment Mapping</h2>
<div class="level2">

<p>
<a href="/resources/fetch.php" class="media" title="http://jmonkeyengine.org/wp-content/uploads/2010/10/glass-teapot1.png"><img src="/resources/fetch.php" class="mediaright" alt="" width="160" height="90" /></a>
</p>

<p>
Environment Mapping or Reflection Mapping is used to create the impression of reflections and refractions in real time. It's faster (but less accurate) than the raytracing methods used in offline rendering applications. 
</p>

<p>
You create a Cube Map to represent your environment; Sphere Maps are also possible, but often look distorted. Basically you give the environment map a set of images showing a “360° view” of the background scene – very similar to a skybox. The renderer maps the environment on the texture of the reflective surface, which results in an acceptable “glass/mirror/water” effect. Just like a skybox, the reflection map is static, so dynamic things (such as the player walking) are not part of the reflection. (!) 
</p>

<p>
See also: <a href="/jme3/advanced/water.html" class="wikilink1" title="jme3:advanced:water">Water</a>.
</p>

</div>
<!-- EDIT22 SECTION "Environment Mapping" [9921-10805] -->
<h2 class="sectionedit23" id="mip_map_texture">MIP Map Texture</h2>
<div class="level2">

<p>
MIP Map means that you provide one texture in two or three resolutions in one file (MIP = “multum in parvo” = “many in one”). Depending on how close (or far) the camera is, the engine automatically renders a more (or less) detailed texture for the object. Thus objects look detailed at close up, but also look good when viewed from far away. Good for everything, but requires more time to create and more space to store textures. If you don't provide custom ones, the jMonkeyEngine creates basic MIP maps automatically as an optimization.
</p>

</div>
<!-- EDIT23 SECTION "MIP Map Texture" [10806-11372] -->
<h2 class="sectionedit24" id="procedural_textures">Procedural Textures</h2>
<div class="level2">

<p>
A procedural texture is generated from repeating one small image, plus some pseudo-random, gradient variations (called Perlin noise). Procedural textures look more natural than static rectangular textures, and they look less distorted on spheres. On big meshes, their repetitiveness is much less noticable than with tiled seamless textures. Procedural textures are ideal for irregular large-area textures like grass, soil, rock, rust, and walls. Use the <a href="http://jmonkeyengine.org/wiki/doku.php/sdk:neotexture" class="urlextern" title="http://jmonkeyengine.org/wiki/doku.php/sdk:neotexture" rel="nofollow">jMonkeyEngine SDK NeoTexture plugin</a> to create them.
</p>

<p>
<a href="/resources/fetch.php" class="media" title="http://jmonkeyengine.org/wp-content/uploads/2010/10/neotexture-2.jpg"><img src="/resources/fetch.php" class="mediacenter" title="jmonkeyengine.org_wp-content_uploads_2010_10_neotexture-2.jpg" alt="jmonkeyengine.org_wp-content_uploads_2010_10_neotexture-2.jpg" width="380" height="189" /></a>
</p>

<p>
See also: <a href="http://www.blender.org/education-help/tutorials/materials/" class="urlextern" title="http://www.blender.org/education-help/tutorials/materials/" rel="nofollow">Creating Materials in Blender</a>, <a href="http://en.wikibooks.org/wiki/Blender_3D:_Noob_to_Pro/Every_Material_Known_to_Man" class="urlextern" title="http://en.wikibooks.org/wiki/Blender_3D:_Noob_to_Pro/Every_Material_Known_to_Man" rel="nofollow">Blender: Every Material Known to Man</a>
</p>

</div>
<!-- EDIT24 SECTION "Procedural Textures" [11373-12279] -->
<h1 class="sectionedit25" id="animation">Animation</h1>
<div class="level1">

<p>
In 3D games, Skeletal Animation is used for animated characters, but in principle the skeleton approach can be extended to any 3D mesh (for example, an opening crate's hinge can be considered a primitive joint).
</p>

<p>
Unless you animate a 3D cartoon, realism of animated characters is generally a problem: Movement can look alien-like mechanical or broken, the character appears hollow, or as if floating. Professional game designers invest a lot of effort to make characters animate in a natural way, including <a href="http://en.wikipedia.org/wiki/Motion_capture" class="urlextern" title="http://en.wikipedia.org/wiki/Motion_capture" rel="nofollow">motion capture</a>.
</p>

</div>
<!-- EDIT25 SECTION "Animation" [12280-12876] -->
<h2 class="sectionedit26" id="rigging_and_skinning">Rigging and Skinning</h2>
<div class="level2">

<p>
<a href="/resources/fetch.php" class="media" title="http://pub.admc.com/misc/jme/blenderjmetut/blenderswordsman.png"><img src="/resources/fetch.php" class="mediaright" alt="" width="195" height="151" /></a>
</p>

<p>
An animated character has an armature: An internal skeleton (Bones) and an external surface (Skin). The Skin is the visible outside of the character and it includes clothing. The Bones are not visible and are used to interpolate (calculate) the morphing steps of the skin.
</p>

<p>
JME3, the game engine, only loads and plays your recorded animations. You must use a tool (such as Blender) to set up (rig, skin, and animate) a character.
</p>
<ol>
<li class="level1"><div class="li"> <strong>Rigging:</strong> The Construction of a character's skeleton.</div>
<ul>
<li class="level2"><div class="li"> Create as few Bones as possible to decrease complexity.</div>
</li>
<li class="level2"><div class="li"> Bones are connected in a parent-child hierarchy: Moving one bone can pull another bone with it (e.g. arm pulls hand).</div>
</li>
<li class="level2"><div class="li"> Bones follow a certain naming scheme so the 3D engines know what's what.</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> <strong>Skinning:</strong> The association of individual bones with the corresponding skin sections.</div>
<ul>
<li class="level2"><div class="li"> Each Bone is connected to a part of the Skin. Animating the (invisible) Bone pulls the (visible) Skin with it. <br />
E.g. the thigh Bone is connected to the upper leg Skin.</div>
</li>
<li class="level2"><div class="li"> One part of the Skin can be affected by more than one bone (e.g. knee, elbow).</div>
</li>
<li class="level2"><div class="li"> The connection between bones and skin sections is gradual: You assign weights how much each skin polygon is affected by any bone's motion. <br />
E.g. when the thigh bone moves, the leg is fully affected, the hips joints less so, and the head not at all.</div>
</li>
<li class="level2"><div class="li"> jMonkeyEngine supports hardware skinning (on the GPU, not on the CPU).</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> <strong>Keyframe Animation:</strong> A keyframe is one recorded snapshot of a motion sequence.</div>
<ul>
<li class="level2"><div class="li"> A series of keyframes makes up one animation.</div>
</li>
<li class="level2"><div class="li"> Each model can have several animations. Each animation has a name to identify it (e.g. “walk”, “attack”, “jump”).</div>
</li>
<li class="level2"><div class="li"> You specify in your game code which keyframe animation to load, and when to play it.</div>
</li>
</ul>
</li>
</ol>

<p>
</p><p></p><div class="notetip">What is the difference between animation (rigging, skinning, keyframes) and transformation (rotation, scaling, moving, “slerp”)?

<ul>
<li class="level1"><div class="li"> Transformation is simpler than animation. Sometimes, transforming a geometry already makes it look like it is animated: For example, a spinning windmill, a pulsating alien ball of energy, moving rods of a machine. Transformations can be easily done with JME3 methods. </div>
</li>
<li class="level1"><div class="li"> Animations however are more complex and are encoded in a special format (keyframes). They distort the skin of the mesh, and complex series of motions be “recorded” (in external tools) and played (in JME3).</div>
</li>
</ul>

<p>

</p></div>


</div>
<!-- EDIT26 SECTION "Rigging and Skinning" [12877-15413] -->
<h2 class="sectionedit27" id="kinematics">Kinematics</h2>
<div class="level2">
<ul>
<li class="level1"><div class="li"> Forward kinematics: “Given the angles of all the character's joints, what is the position of the character's hand?”</div>
</li>
<li class="level1"><div class="li"> Inverse kinematics: “Given the position of the character's hand, what are the angles of all the character's joints?”</div>
</li>
</ul>

</div>
<!-- EDIT27 SECTION "Kinematics" [15414-15678] -->
<h2 class="sectionedit28" id="controller_and_channel">Controller and Channel</h2>
<div class="level2">

<p>
In the JME3 application, you register animated models to the Animation Controller. The controller object gives you access to the available animation sequences. The controller has several channels, each channel can run one animation sequence at a time. To run several sequences, you create several channels, and run them in parallel.
</p>

</div>
<!-- EDIT28 SECTION "Controller and Channel" [15679-16047] -->
<h1 class="sectionedit29" id="artificial_intelligence_ai">Artificial Intelligence (AI)</h1>
<div class="level1">

<p>
Non-player (computer-controlled) characters (NPCs) are only fun in a game if they do not stupidly bump into walls, or blindly run into the line of fire. You want to make NPCs “aware” of their surroundings and let them make decisions based on the game state – otherwise the player can just ignore them. The most common use case is that you want to make enemies interact in a way so they offer a more interesting challenge for the player.
</p>

<p>
“Smart” game elements are called artificially intelligent agents (AI agents). An AI agent can be used to implement enemy NPCs as well as trained pets; you also use them to create automatic alarm systems that lock doors and “call the guards” after the player triggers an intruder alert.
</p>

<p>
The domain of artificial intelligence deals, among other things, with:
</p>
<ul>
<li class="level1"><div class="li"> <strong>Knowledge</strong> – Knowledge is <em>the data</em> to which the AI agent has access, and on which the AI bases its decisions. Realistic agents only “know” what they “see and hear”. This implies that information can be hidden from the AI to keep the game fair. You can have an all-knowing AI, or you can let only some AI agents share information, or you let only AI agents who are close know the current state. <br />
Example: After the player trips the wire, only a few AI guards with two-way radios start moving towards the player's position, while many other guards don't suspect anything yet.</div>
</li>
<li class="level1"><div class="li"> <strong>Goal Planning</strong> – Planning is about how an AI agent <em>takes action</em>. Each agent has the priority to achieve a specific goal, to reach a future state. When programming, you split the agent's goal into several subgoals. The agent consults its knowledge about the current state, chooses from available tactics and strategies, and prioritizes them. The agent repeatedly tests whether the current state is closer to its goal. If unsuccessful, the agent must discard the current tactics/strategy and try another one. <br />
Example: An agent searches the best path to reach the player base in a changing environment, avoiding traps. An agent chases the player with the goal of eliminating him. An agent hides from the player with the goal of murdering a VIP. </div>
</li>
<li class="level1"><div class="li"> <strong>Problem Solving</strong> – Problem solving is about how the agent <em>reacts to interruptions</em>, obstacles that stand between it and its goal. The agent uses a given set of facts and rules to deduct what state it is in – triggered by perceptions similar to pain, agony, boredom, or being trapped. In each state, only a specific subset of reactions makes sense. The actual reaction also depends on the agent's, goal since the agent's reaction must not block its own goal! <br />
Examples: If player approaches, does the agent attack or conceal himself or raise alarm? While agent is idle, does he lay traps or heal self or recharge magic runes? If danger to own life, does the agent try to escape or kamikaze?</div>
</li>
</ul>

<p>
More advanced AIs can also learn, for example using neural networks.
</p>

<p>
There are lots of resources explaining interesting AI algorithms:
</p>
<ul>
<li class="level1"><div class="li"> <a href="http://www.policyalmanac.org/games/aStarTutorial.htm" class="urlextern" title="http://www.policyalmanac.org/games/aStarTutorial.htm" rel="nofollow">A* (A-Star) pathfinding for beginners</a></div>
</li>
<li class="level1"><div class="li"> <a href="http://theory.stanford.edu/~amitp/GameProgramming/" class="urlextern" title="http://theory.stanford.edu/~amitp/GameProgramming/" rel="nofollow">A* (A-star) pathfinding theory</a></div>
</li>
<li class="level1"><div class="li"> <a href="http://hem.fyristorg.com/dawnbringer/z-path.html" class="urlextern" title="http://hem.fyristorg.com/dawnbringer/z-path.html" rel="nofollow">"Z-Path" algorithm</a> (backwards pathfinding)</div>
</li>
<li class="level1"><div class="li"> <a href="http://web.media.mit.edu/~jorkin/goap.html" class="urlextern" title="http://web.media.mit.edu/~jorkin/goap.html" rel="nofollow">GOAP -- Goal-Oriented Action Planning</a></div>
</li>
<li class="level1"><div class="li"> <a href="http://neuroph.sourceforge.net/" class="urlextern" title="http://neuroph.sourceforge.net/" rel="nofollow">Neuroph -- Java Neural Networks</a></div>
</li>
<li class="level1"><div class="li"> …</div>
</li>
</ul>

</div>
<!-- EDIT29 SECTION "Artificial Intelligence (AI)" [16048-19533] -->
<h1 class="sectionedit30" id="math">Math</h1>
<div class="level1">

<p>
<a href="/resources/jme3-intermediate-coordinate-system.png" class="media" title="jme3:intermediate:coordinate-system.png"><img src="/resources/jme3-intermediate-coordinate-system.png" class="mediaright" alt="" width="235" height="210" /></a>
</p>

</div>
<!-- EDIT30 SECTION "Math" [19534-19607] -->
<h2 class="sectionedit31" id="coordinates">Coordinates</h2>
<div class="level2">

<p>
Coordinates represent a location in a coordinate system. Coordinates are relative to the origin at (0,0,0). In 3D space, you need to specify three coordinate values to locate a point: X (right), Y (up), Z (towards you). Similarly, -X (left), -Y (down), -Z (away from you).
In contrast to a vector (which looks similar), a coordinate is a location, not a direction.
</p>

</div>
<!-- EDIT31 SECTION "Coordinates" [19608-19997] -->
<h3 class="sectionedit32" id="the_origin">The Origin</h3>
<div class="level3">

<p>
The origin is the central point in the 3D world, where the three axes meet. It's always at the coordinates (0,0,0).
</p>

<p>
<strong>Example:</strong> <code>Vector3f origin = new Vector3f( Vector3f.ZERO );</code>
</p>

</div>
<!-- EDIT32 SECTION "The Origin" [19998-20202] -->
<h2 class="sectionedit33" id="vectors">Vectors</h2>
<div class="level2">

<p>
A vector has a length and a direction, like an arrow in 3D space. A vector starts at a coordinate (x1,y1,z1) or at the origin, and ends at the target coordinate (x2,y2,z2). Backwards directions are expressed with negative values.
</p>

<p>
<strong>Example:</strong> 
</p>
<pre class="code java">Vector3f v <span class="sy0">=</span> <span class="kw1">new</span> Vector3f<span class="br0">(</span> 17f , <span class="sy0">-</span>4f , 0f <span class="br0">)</span><span class="sy0">;</span> <span class="co1">// starts at (0/0/0)</span>
Vector3f v <span class="sy0">=</span> <span class="kw1">new</span> Vector3f<span class="br0">(</span> 8f , 0f , 33f <span class="br0">)</span>.<span class="me1">add</span><span class="br0">(</span><span class="kw1">new</span> Vector3f<span class="br0">(</span> 0f , <span class="sy0">-</span>2f , <span class="sy0">-</span>2f <span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// starts at (8,-2,31)</span></pre>

</div>
<!-- EDIT33 SECTION "Vectors" [20203-20653] -->
<h3 class="sectionedit34" id="unit_vectors">Unit Vectors</h3>
<div class="level3">

<p>
A <em>unit vector</em> is a basic vector with a length of 1 world unit. Since its length is fixed (and it thus can only point at one location anyway), the only interesting thing about this vector is its direction.
</p>
<ul>
<li class="level1"><div class="li"> <code>Vector3f.UNIT_X</code>  = ( 1, 0, 0) = right</div>
</li>
<li class="level1"><div class="li"> <code>Vector3f.UNIT_Y</code>  = ( 0, 1, 0) = up</div>
</li>
<li class="level1"><div class="li"> <code>Vector3f.UNIT_Z</code>  = ( 0, 0, 1) = forwards</div>
</li>
<li class="level1"><div class="li"> <code>Vector3f.UNIT_XYZ</code> = 1 wu diagonal right-up-forewards</div>
</li>
</ul>

<p>
Negate the components of the vector to turn its direction, e.g. negating right (1,0,0) results in left (-1,0,0).
</p>

</div>
<!-- EDIT34 SECTION "Unit Vectors" [20654-21197] -->
<h3 class="sectionedit35" id="normalized_vectors">Normalized Vectors</h3>
<div class="level3">

<p>
A <em>normalized vector</em> is a custom <em>unit vector</em>. A normalized vector is not the same as a <em>(surface) normal vector</em>.
When you normalize a vector, it still has the same direction, but you lose the information where the vector originally pointed.
</p>

<p>
<strong>Example:</strong> You normalize vectors before calculating angles. 
</p>

</div>
<!-- EDIT35 SECTION "Normalized Vectors" [21198-21541] -->
<h3 class="sectionedit36" id="surface_normal_vectors">Surface Normal Vectors</h3>
<div class="level3">

<p>
<a href="/resources/jme3-300px-surface_normal.png" class="media" title="jme3:300px-surface_normal.png"><img src="/resources/jme3-300px-surface_normal.png" class="mediaright" alt="" /></a>
A surface normal is a vector that is perpendicular (orthogonal) to a plane. 
You calculate the Surface Normal by calculating the cross product.
</p>

</div>
<!-- EDIT36 SECTION "Surface Normal Vectors" [21542-21754] -->
<h3 class="sectionedit37" id="cross_product">Cross Product</h3>
<div class="level3">

<p>
The cross product is a calculation that you use to find a perpendicular vector (an orthogonal, a “right angle” at 90°).
In 3D space, speaking of an orthogonal only makes sense with respect to a plane. You need two vectors to uniquely define a plane. The cross product of the two vectors, <code>v1 × v2</code>, is a new vector that is perpendicular to this plane. A vector perpendicular to a plane is a called <em>Surface Normal</em>.
</p>

<p>
<strong>Example:</strong> The x unit vector and the y unit vector together define the x/y plane. The vector perpendicular to them is the z axis. JME can calculate that this equation is true: <br />

<code>( Vector3f.UNIT_X.cross( Vector3f.UNIT_Y ) ).equals( Vector3f.UNIT_Z )</code> == true
</p>

</div>
<!-- EDIT37 SECTION "Cross Product" [21755-22465] -->
<h3 class="sectionedit38" id="transformation">Transformation</h3>
<div class="level3">

<p>
Transformation means rotating (turning), scaling (resizing), or translating (moving) objects in 3D scenes. 3D engines offer simple methods so you can write code that transforms nodes. 
</p>

<p>
Examples: Falling and rotating bricks in 3D Tetris.
</p>

</div>
<!-- EDIT38 SECTION "Transformation" [22466-22730] -->
<h3 class="sectionedit39" id="slerp">Slerp</h3>
<div class="level3">

<p>
Slerp is how we pronounce spherical linear interpolation when we are in a hurry. A slerp is an interpolated transformation that is used as a simple “animation” in 3D engines. You define a start and end state, and the slerp interpolates a constant-speed transition from one state to the other. You can play the motion, pause it at various percentages (values between 0.0 and 1.0), and play it backwards and forwards. <a href="http://jmonkeyengine.org/javadoc/com/jme3/math/Quaternion.html#slerp(com.jme3.math.Quaternion,%20com.jme3.math.Quaternion,%20float)" class="urlextern" title="http://jmonkeyengine.org/javadoc/com/jme3/math/Quaternion.html#slerp(com.jme3.math.Quaternion,%20com.jme3.math.Quaternion,%20float)" rel="nofollow">JavaDoc: slerp()</a>
</p>

<p>
Example: A burning meteorite Geometry slerps from “position p1, rotation r1, scale s1” in the sky down to “p2, r2, s2” into a crater.
</p>

<p>
<a href="/jme3/math.html" class="wikilink1" title="jme3:math">Learn more about 3D maths here.</a>
</p>

</div>
<!-- EDIT39 SECTION "Slerp" [22731-23500] -->
<h1 class="sectionedit40" id="game_developer_jargon">Game Developer Jargon</h1>
<div class="level1">
<ul>
<li class="level1"><div class="li"> <a href="http://www.gamasutra.com/view/feature/6504/a_game_studio_culture_dictionary.php?print=1" class="urlextern" title="http://www.gamasutra.com/view/feature/6504/a_game_studio_culture_dictionary.php?print=1" rel="nofollow">A Game Studio Culture Dictionary</a></div>
</li>
</ul>

</div>
<!-- EDIT40 SECTION "Game Developer Jargon" [23501-23664] -->
<h1 class="sectionedit41" id="d_graphics_terminology_wiki_book">3D graphics Terminology Wiki book</h1>
<div class="level1">
<ul>
<li class="level1"><div class="li"> <a href="http://en.wikipedia.org/wiki/User:Jreynaga/Books/3D_Graphics_Terms" class="urlextern" title="http://en.wikipedia.org/wiki/User:Jreynaga/Books/3D_Graphics_Terms" rel="nofollow">http://en.wikipedia.org/wiki/User:Jreynaga/Books/3D_Graphics_Terms</a></div>
</li>
</ul>

</div>
<!-- EDIT41 SECTION "3D graphics Terminology Wiki book" [23665-] -->
