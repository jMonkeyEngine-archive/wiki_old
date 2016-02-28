---
title: Technical comparison between jME2 and jME3
---
<h1 class="sectionedit1" id="technical_comparison_between_jme2_and_jme3">Technical comparison between jME2 and jME3</h1>
<div class="level1">

</div>
<!-- EDIT1 SECTION "Technical comparison between jME2 and jME3" [1-57] -->
<h2 class="sectionedit2" id="shaders">Shaders?</h2>
<div class="level2">
<ul>
<li class="level1"><div class="li"> jME3: Shaders are integrated in the core and material system. JME3 supports shader libraries and permutations through defines. User-friendly post-processor filters, scene processors, and <a href="/jme3/advanced/jme3_shadernodes.html" class="wikilink1" title="jme3:advanced:jme3_shadernodes">shader node system</a> (you don't need to know shaders to be able to use them).</div>
</li>
<li class="level2"><div class="li"> jME2: Full access to shader support through a RenderState, requires user to know and understand shaders. No support for libraries or permutations.</div>
</li>
</ul>

</div>
<!-- EDIT2 SECTION "Shaders?" [58-536] -->
<h2 class="sectionedit3" id="resource_management">Resource management?</h2>
<div class="level2">
<ul>
<li class="level1"><div class="li"> jME3: Integrated in core. All data loaded from files is cached inside AssetManager. User customizable. Supports threaded loading. Can load from ZIP/JAR files on the local harddrive and on an HTTP server.</div>
</li>
<li class="level1"><div class="li"> jME2: Only textures are managed in TextureManager. ResourceLocatorTool is used for locating resources.</div>
</li>
</ul>

</div>
<!-- EDIT3 SECTION "Resource management?" [537-884] -->
<h2 class="sectionedit4" id="input_handling">Input handling?</h2>
<div class="level2">
<ul>
<li class="level1"><div class="li"> jME3: Designed for games. Abstracting keyboard, mouse and joystick into a single, binding based interface. Low level interface available for <abbr title="Graphical User Interface">GUI</abbr> access.</div>
</li>
<li class="level1"><div class="li"> jME2: Layer over keyboard, mouse and joystick. Main input interface (InputManager) can cause bloat in user code. Binding system available separately through darkfrog's input binding system.</div>
</li>
</ul>

</div>
<!-- EDIT4 SECTION "Input handling?" [885-1263] -->
<h2 class="sectionedit5" id="gl_object_handling">GL Object handling?</h2>
<div class="level2">
<ul>
<li class="level1"><div class="li"> jME3:  Unused GL objects are deleted when they are garbage collected by Java.</div>
</li>
<li class="level1"><div class="li"> jME2:  All objects are leaked unless manually cleaned up by the user.</div>
</li>
</ul>

</div>
<!-- EDIT5 SECTION "GL Object handling?" [1264-1451] -->
<h2 class="sectionedit6" id="collision_picking">Collision/Picking?</h2>
<div class="level2">
<ul>
<li class="level1"><div class="li"> jME3:  BIH (Bounding interleaved hierarchy) for static mesh picking and collision. Supports Volume vs. Tri collision.</div>
</li>
<li class="level1"><div class="li"> jME2:  Red-black tree over entire mesh data, less efficient collision than BIH but faster generation for animated objects. Supports Tri vs. Tri collision but not Volume vs. Tri which is more commonly used.</div>
</li>
</ul>

</div>
<!-- EDIT6 SECTION "Collision/Picking?" [1452-1814] -->
<h2 class="sectionedit7" id="native_library_handling">Native library handling?</h2>
<div class="level2">
<ul>
<li class="level1"><div class="li"> jME3:  Copies natives and loads them at runtime.</div>
</li>
<li class="level1"><div class="li"> jME2:  None, requires user to specify java.library.path property.</div>
</li>
</ul>

</div>
<!-- EDIT7 SECTION "Native library handling?" [1815-1974] -->
<h2 class="sectionedit8" id="post_processing">Post processing?</h2>
<div class="level2">
<ul>
<li class="level1"><div class="li"> jME3:  HDR/Tonemapping, SSAO, Bloom, Radial Blur, Light Scattering, CartoonEdge.</div>
</li>
<li class="level1"><div class="li"> jME2:  Bloom, Basic Motion Blur</div>
</li>
</ul>

</div>
<!-- EDIT8 SECTION "Post processing?" [1975-2124] -->
<h2 class="sectionedit9" id="shadow_effects">Shadow effects?</h2>
<div class="level2">
<ul>
<li class="level1"><div class="li"> jME3:  Built in the core. Customizable shadow map method, supports basic and PSSM methods.</div>
</li>
<li class="level1"><div class="li"> jME2:  ShadowedRenderPass for stencil shadows, issues if camera goes inside shadow volume. DirectionalShadowMapPass for basic shadow mapping.</div>
</li>
</ul>

</div>
<!-- EDIT9 SECTION "Shadow effects?" [2125-2393] -->
<h2 class="sectionedit10" id="geometry_handling">Geometry handling?</h2>
<div class="level2">
<ul>
<li class="level1"><div class="li"> jME3:  Geometry is a scene graph element, contains a Mesh object. Meshes contain VertexBuffers which specify # of components, type, float/int buffer. This allows a single mesh to be shared along many scene graph elements. Supports features like Level of Detail and animation internally.</div>
</li>
<li class="level1"><div class="li"> jME2:  Geometry/TriMesh a scene graph element contains float buffers and int buffers, VBO only supports static models, custom attributes are specified manually via GLSLShaderDataLogic and do not work if VBO is used.</div>
</li>
</ul>

</div>
<!-- EDIT10 SECTION "Geometry handling?" [2394-2935] -->
<h2 class="sectionedit11" id="scene_graph_updates">Scene graph updates?</h2>
<div class="level2">
<ul>
<li class="level1"><div class="li"> jME3:  Refresh flags prevent unneeded scene updates.</div>
</li>
<li class="level1"><div class="li"> jME2:  All data updated in updateGeometricState. Every call updates entire scene graph, locking mechanism is used to reduce unneeded updates but requires used intervention.</div>
</li>
</ul>

</div>
<!-- EDIT11 SECTION "Scene graph updates?" [2936-3202] -->
<h2 class="sectionedit12" id="renderstate_material">RenderState/Material</h2>
<div class="level2">
<ul>
<li class="level1"><div class="li"> jME3:  Only at leafs. Scriptable material system is used. materials contain techniques which contain shader &amp; render state. Shader is customized with defines specified in material instance (by user). This is a data-driven approach to materials.</div>
</li>
<li class="level1"><div class="li"> jME2:  Each scene graph element contains an array of RenderStates. They are combined and stored in the leafs. No data-driven solution.</div>
</li>
</ul>

</div>
<!-- EDIT12 SECTION "RenderState/Material" [3203-3623] -->
<h2 class="sectionedit13" id="support_for_fixed-function_old_gpus">Support for fixed-function/old gpus?</h2>
<div class="level2">
<ul>
<li class="level1"><div class="li"> jME3:  Supported via FixedFunc bindings in shader source.</div>
</li>
<li class="level1"><div class="li"> jME2:  Full support.</div>
</li>
</ul>

</div>
<!-- EDIT13 SECTION "Support for fixed-function/old gpus?" [3624-3759] -->
<h2 class="sectionedit14" id="renderer_capabilities">Renderer capabilities?</h2>
<div class="level2">
<ul>
<li class="level1"><div class="li"> jME3:  Queriable through cap system.</div>
</li>
<li class="level1"><div class="li"> jME2:  Queriable through the Renderer and the various renderstates.</div>
</li>
</ul>

</div>
<!-- EDIT14 SECTION "Renderer capabilities?" [3760-3907] -->
<h2 class="sectionedit15" id="math_object_pooling_vector_matrix_etc">Math object pooling (Vector, Matrix, etc)?</h2>
<div class="level2">
<ul>
<li class="level1"><div class="li"> jME3:  ThreadLocal-based system, defined as instance variables accessible by any class. Assertion-based “locking” is used to prevent data corruption.</div>
</li>
<li class="level1"><div class="li"> jME2:  static declarations (kills multithreading in these classes) or no pooling at all.</div>
</li>
</ul>

</div>
<!-- EDIT15 SECTION "Math object pooling (Vector, Matrix, etc)?" [3908-4209] -->
<h2 class="sectionedit16" id="text">Text?</h2>
<div class="level2">
<ul>
<li class="level1"><div class="li"> jME3:  AngelCode bitmap text</div>
</li>
<li class="level1"><div class="li"> jME2:  Fixed-length font, 3D text, AngelCode bitmap text</div>
</li>
</ul>

</div>
<!-- EDIT16 SECTION "Text?" [4210-4321] -->
<h2 class="sectionedit17" id="user_interface">User interface?</h2>
<div class="level2">
<ul>
<li class="level1"><div class="li"> jME3:  Simple text and ortho built-in, NiftyGui integration can be used for more advanced user interface.</div>
</li>
<li class="level1"><div class="li"> jME2:  Only simple text and ortho. jME-desktop (not working well under MacOS X), external libs available (FengGUI, GBUI, NiftyGui).</div>
</li>
</ul>

</div>
<!-- EDIT17 SECTION "User interface?" [4322-4595] -->
<h2 class="sectionedit18" id="animation">Animation?</h2>
<div class="level2">
<ul>
<li class="level1"><div class="li"> jME3:  OgreXML-based animation system with many features. Software skinning and hardware skinning are supported.</div>
</li>
<li class="level1"><div class="li"> jME2:  Too many systems, creating a big mess. jME-xml and collada use one system, md2/md3 use another, milkshape models use another, ogrexml uses another and md5 uses another.</div>
</li>
</ul>

</div>
<!-- EDIT18 SECTION "Animation?" [4596-4915] -->
<h2 class="sectionedit19" id="spatial_partitioning">Spatial partitioning?</h2>
<div class="level2">
<ul>
<li class="level1"><div class="li"> jME3:  None.</div>
</li>
<li class="level1"><div class="li"> jME2:  None.</div>
</li>
</ul>

</div>
<!-- EDIT19 SECTION "Spatial partitioning?" [4916-4983] -->
<h2 class="sectionedit20" id="model_formats">Model formats?</h2>
<div class="level2">
<ul>
<li class="level1"><div class="li"> jME3:  Ogre3D Mesh.XML and OBJ.</div>
</li>
<li class="level1"><div class="li"> jME2:  Static/VertexAnim: ase, obj, 3ds, md2, md3, ms3d, x3d. Skeleton: (broken) collada, ogre3d, jme-xml (md5 as a seperate lib)</div>
</li>
</ul>

</div>
<!-- EDIT20 SECTION "Model formats?" [4984-5180] -->
<h2 class="sectionedit21" id="import_export">Import/Export?</h2>
<div class="level2">
<ul>
<li class="level1"><div class="li"> jME3:  Same as jME2. Don't fix what's not broken.</div>
</li>
<li class="level1"><div class="li"> jME2:  Input/Output capsules and Savable. Binary and XML.</div>
</li>
</ul>

</div>
<!-- EDIT21 SECTION "Import/Export?" [5181-5323] -->
<h2 class="sectionedit22" id="physics">Physics?</h2>
<div class="level2">
<ul>
<li class="level1"><div class="li"> jME3:  Full JBullet integration.</div>
</li>
<li class="level1"><div class="li"> jME2:  External libs available: jME-physics, jbullet-jme, SimplePhysics.</div>
</li>
</ul>

</div>
<!-- EDIT22 SECTION "Physics?" [5324-5458] -->
<h2 class="sectionedit23" id="canvas_support">Canvas support?</h2>
<div class="level2">
<ul>
<li class="level1"><div class="li"> jME3:  Yes.</div>
</li>
<li class="level1"><div class="li"> jME2:  Yes, although the <abbr title="Application Programming Interface">API</abbr> could have been a little less convoluted.</div>
</li>
</ul>

</div>
<!-- EDIT23 SECTION "Canvas support?" [5459-5577] -->
<h2 class="sectionedit24" id="particles">Particles?</h2>
<div class="level2">
<ul>
<li class="level1"><div class="li"> jME3:  Yes.</div>
</li>
<li class="level1"><div class="li"> jME2:  Yes but <abbr title="Application Programming Interface">API</abbr> could be a little less convoluted.</div>
</li>
</ul>

</div>
<!-- EDIT24 SECTION "Particles?" [5578-5674] -->
<h2 class="sectionedit25" id="terrain">Terrain?</h2>
<div class="level2">
<ul>
<li class="level1"><div class="li"> jME3:  Image based heightmap, supports dynamic terrain loading, geomipmapping (LOD), and texture splatting. Can import Ogre3D dotScene files for non-heightmap terrain.</div>
</li>
<li class="level1"><div class="li"> jME2:  Image based or randomly generated heightmap. Quadtree support.</div>
</li>
</ul>

</div>
<!-- EDIT25 SECTION "Terrain?" [5675-] -->
