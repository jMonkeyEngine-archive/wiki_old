---
title: Custom Mesh Shapes
---
<h1 class="sectionedit1" id="custom_mesh_shapes">Custom Mesh Shapes</h1>
<div class="level1">

<p>
<a href="/resources/fetch.php" class="media" title="http://wiki.jmonkeyengine.org/lib/exe/fetch.php/jme3:advanced:custom_mesh.png"><img src="/resources/fetch.php" class="medialeft" alt="" width="150" height="150" /></a>
Use the Mesh class to create custom shapes that go beyond Quad, Box, Cylinder, and Sphere, even procedural shapes are possible. Thank you to KayTrance for providing the sample code!
</p>

<p>
<strong>Note:</strong> In this tutorial, we (re)create a very simple rectangular mesh (a quad), and we have a look at different ways of coloring it. Coding a custom quad may not be very useful because it's exactly the same as the built-in <code>com.jme3.scene.shape.Quad</code>. We chose a simple quad to teach you how to build any shape out of triangles, without the distractions of more complex shapes.
</p>
<ul>
<li class="level1"><div class="li"> Full code sample: <a href="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-examples/src/main/java/jme3test/model/shape/TestCustomMesh.java" class="urlextern" title="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-examples/src/main/java/jme3test/model/shape/TestCustomMesh.java" rel="nofollow">TestCustomMesh.java</a></div>
</li>
</ul>

</div>
<!-- EDIT1 SECTION "Custom Mesh Shapes" [1-866] -->
<h2 class="sectionedit2" id="polygon_meshes">Polygon Meshes</h2>
<div class="level2">

<p>
Polygon <a href="/jme3/advanced/mesh.html" class="wikilink1" title="jme3:advanced:mesh">mesh</a>es are made up of triangles. The corners of the triangles are called vertices. When ever you create any new shape, you break it down into triangles.
</p>

<p>
<strong>Example:</strong> Let's look at a cube. A cube is made up of 6 rectangles. Each rectangle can be broken down into two triangles. This means you need 12 triangles to describe a cube mesh. Therefor you must provide the coordinates of the triangles' 8 corners (called vertices). 
</p>

<p>
The important thing is that you have to specify the vertices of each triangle in the right order: Each triangle separately, counter-clockwise. 
</p>

<p>
Sounds harder than it is – let's create a simple custom mesh, a quad.
</p>

</div>
<!-- EDIT2 SECTION "Polygon Meshes" [867-1550] -->
<h2 class="sectionedit3" id="creating_a_quad_mesh">Creating a Quad Mesh</h2>
<div class="level2">

<p>
In this tutorial we want to create a 3×3 Quad. The quad has four vertices, and is made up of two triangles. In our example, we decide that the bottom left corner is at 0/0/0 and the top right is at 3/3/0. 
</p>
<pre class="code">0,3,0--3,3,0
| \        |
|   \      |
|     \    |
|       \  |
|         \|
0,0,0--3,0,0</pre>

</div>
<!-- EDIT3 SECTION "Creating a Quad Mesh" [1551-1896] -->
<h3 class="sectionedit4" id="the_mesh_object">The Mesh Object</h3>
<div class="level3">

<p>
The base class for creating meshes is <code>com.jme3.scene.Mesh</code>.
</p>
<pre class="code java">Mesh mesh <span class="sy0">=</span> <span class="kw1">new</span> Mesh<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
Tip: If you create your own Mesh-based class (<code>public class MyMesh extends Mesh {  }</code>), replace the variable <code>mesh</code> by <code>this</code> in the following examples.
</p>

</div>
<!-- EDIT4 SECTION "The Mesh Object" [1897-2189] -->
<h3 class="sectionedit5" id="vertex_coordinates">Vertex Coordinates</h3>
<div class="level3">

<p>
To define your own shape, determine the shape's <strong>vertex coordinates</strong> in 3D space. Store the list of corner positions in an <code>com.jme3.math.Vector3f</code> array. For a Quad, we need four vertices: Bottom left, bottom right, top left, top right. We name the array <code>vertices[]</code>.
</p>
<pre class="code java">Vector3f <span class="br0">[</span><span class="br0">]</span> vertices <span class="sy0">=</span> <span class="kw1">new</span> Vector3f<span class="br0">[</span><span class="nu0">4</span><span class="br0">]</span><span class="sy0">;</span>
vertices<span class="br0">[</span><span class="nu0">0</span><span class="br0">]</span> <span class="sy0">=</span> <span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">0</span>,<span class="nu0">0</span>,<span class="nu0">0</span><span class="br0">)</span><span class="sy0">;</span>
vertices<span class="br0">[</span><span class="nu0">1</span><span class="br0">]</span> <span class="sy0">=</span> <span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">3</span>,<span class="nu0">0</span>,<span class="nu0">0</span><span class="br0">)</span><span class="sy0">;</span>
vertices<span class="br0">[</span><span class="nu0">2</span><span class="br0">]</span> <span class="sy0">=</span> <span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">0</span>,<span class="nu0">3</span>,<span class="nu0">0</span><span class="br0">)</span><span class="sy0">;</span>
vertices<span class="br0">[</span><span class="nu0">3</span><span class="br0">]</span> <span class="sy0">=</span> <span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">3</span>,<span class="nu0">3</span>,<span class="nu0">0</span><span class="br0">)</span><span class="sy0">;</span></pre>

</div>
<!-- EDIT5 SECTION "Vertex Coordinates" [2190-2696] -->
<h3 class="sectionedit6" id="texture_coordinates">Texture Coordinates</h3>
<div class="level3">

<p>
Next, we define the Quad's 2D <strong>texture coordinates</strong> for each vertex, in the same order as the vertices: Bottom left, bottom right, top left, top right. We name this Vector2f array <code>texCoord[]</code>
</p>
<pre class="code java">Vector2f<span class="br0">[</span><span class="br0">]</span> texCoord <span class="sy0">=</span> <span class="kw1">new</span> Vector2f<span class="br0">[</span><span class="nu0">4</span><span class="br0">]</span><span class="sy0">;</span>
texCoord<span class="br0">[</span><span class="nu0">0</span><span class="br0">]</span> <span class="sy0">=</span> <span class="kw1">new</span> Vector2f<span class="br0">(</span><span class="nu0">0</span>,<span class="nu0">0</span><span class="br0">)</span><span class="sy0">;</span>
texCoord<span class="br0">[</span><span class="nu0">1</span><span class="br0">]</span> <span class="sy0">=</span> <span class="kw1">new</span> Vector2f<span class="br0">(</span><span class="nu0">1</span>,<span class="nu0">0</span><span class="br0">)</span><span class="sy0">;</span>
texCoord<span class="br0">[</span><span class="nu0">2</span><span class="br0">]</span> <span class="sy0">=</span> <span class="kw1">new</span> Vector2f<span class="br0">(</span><span class="nu0">0</span>,<span class="nu0">1</span><span class="br0">)</span><span class="sy0">;</span>
texCoord<span class="br0">[</span><span class="nu0">3</span><span class="br0">]</span> <span class="sy0">=</span> <span class="kw1">new</span> Vector2f<span class="br0">(</span><span class="nu0">1</span>,<span class="nu0">1</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
This syntax means, when you apply a texture to this mesh, the texture will fill the quad from corner to corner at 100% percent size. Especially when you stitch together a larger mesh, you use this to tell the renderer whether, and how exactly, you want to cover the whole mesh. E.g. if you use .5f or 2f as texture coordinates instead of 1f, textures will be stretched or shrunk accordingly.
</p>

</div>
<!-- EDIT6 SECTION "Texture Coordinates" [2697-3507] -->
<h3 class="sectionedit7" id="connecting_the_dots">Connecting the Dots</h3>
<div class="level3">

<p>
Next we turn these unrelated coordinates into <strong>triangles</strong>: We define the order in which each triangle is constructed. Think of these indexes as coming in groups of three. Each group of indexes describes one triangle. If the corners are identical, you can (and should!) reuse an index for several triangles. 
</p>

<p>
Remember that you must specify the vertices counter-clockwise. 
</p>
<pre class="code java"><span class="kw4">int</span> <span class="br0">[</span><span class="br0">]</span> indexes <span class="sy0">=</span> <span class="br0">{</span> <span class="nu0">2</span>,<span class="nu0">0</span>,<span class="nu0">1</span>, <span class="nu0">1</span>,<span class="nu0">3</span>,<span class="nu0">2</span> <span class="br0">}</span><span class="sy0">;</span></pre>

<p>
This syntax means:
</p>
<ul>
<li class="level1"><div class="li"> The indices 0,1,2,3 stand for the four vertices that you specified for the quad in <code>vertices[]</code>.</div>
</li>
<li class="level1"><div class="li"> The 2,0,1 triangle starts at top left, continues bottom left, and ends at bottom right.</div>
</li>
<li class="level1"><div class="li"> The 1,3,2 triangle start at bottom right, continues top right, and ends at top left.</div>
</li>
</ul>
<pre class="code">2\2--3
| \  | Counter-clockwise
|  \ |
0--1\1</pre>

<p>
If the shape is more complex, it has more triangles, and therefor also more vertices/indices. Just continue expanding the list by adding groups of three indices for each triangle. (For example a three-triangle “house” shape has 5 vertices/indices and you'd specify three groups: <code>int [] indexes = { 2,0,1, 1,3,2, 2,3,4 };</code>.) 
</p>

<p>
</p><p></p><div class="notetip">If you get the order wrong (clockwise) for some of the triangles, then these triangles face backwards. If the <a href="/jme3/advanced/spatial.html" class="wikilink1" title="jme3:advanced:spatial">Spatial</a>'s material uses the default <code>FaceCullMode.Back</code> (see “face culling”), the broken triangles appear as holes in the rendered mesh. You need to identify and fix them in your code.
</div>


</div>
<!-- EDIT7 SECTION "Connecting the Dots" [3508-4979] -->
<h3 class="sectionedit8" id="setting_the_mesh_buffer">Setting the Mesh Buffer</h3>
<div class="level3">

<p>
You store the Mesh data in a buffer.
</p>
<ol>
<li class="level1"><div class="li"> Using <code>com.jme3.util.BufferUtils</code>, we create three buffers for the three types of information we have:</div>
<ul>
<li class="level2"><div class="li"> vertex coordinates,</div>
</li>
<li class="level2"><div class="li"> texture coordinates,</div>
</li>
<li class="level2"><div class="li"> indices.</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> We assign the data to the appropriate type of buffer inside the <code>Mesh</code> object. The three buffer types (<code>Position</code>, <code>TextCoord</code>, <code>Index</code>) are taken from an enum in <code>com.jme3.scene.VertexBuffer.Type</code>.</div>
</li>
<li class="level1"><div class="li"> The integer parameter describes the number of components of the values. Vertex postions are 3 float values, texture coordinates are 2 float values, and the indices are 3 ints representing 3 vertices in a triangle.</div>
</li>
<li class="level1"><div class="li"> To render the mesh in the scene, we need to pre-calculate the bounding volume of our new mesh: Call the <code>updateBound()</code> method on it.</div>
</li>
</ol>
<pre class="code java">mesh.<span class="me1">setBuffer</span><span class="br0">(</span>Type.<a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+position"><span class="kw3">Position</span></a>, <span class="nu0">3</span>, BufferUtils.<span class="me1">createFloatBuffer</span><span class="br0">(</span>vertices<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
mesh.<span class="me1">setBuffer</span><span class="br0">(</span>Type.<span class="me1">TexCoord</span>, <span class="nu0">2</span>, BufferUtils.<span class="me1">createFloatBuffer</span><span class="br0">(</span>texCoord<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
mesh.<span class="me1">setBuffer</span><span class="br0">(</span>Type.<span class="me1">Index</span>,    <span class="nu0">3</span>, BufferUtils.<span class="me1">createIntBuffer</span><span class="br0">(</span>indexes<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
mesh.<span class="me1">updateBound</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
Our Mesh is ready! Now we want to see it.
</p>

</div>
<!-- EDIT8 SECTION "Setting the Mesh Buffer" [4980-6105] -->
<h2 class="sectionedit9" id="using_the_mesh_in_a_scene">Using the Mesh in a Scene</h2>
<div class="level2">

<p>
We create a <code>com.jme3.scene.Geometry</code> and <code>com.jme3.material.Material</code>from our <code>mesh</code>, apply a simple color material to it, and attach it to the rootNode to make it appear in the scene.
</p>
<pre class="code java">Geometry geo <span class="sy0">=</span> <span class="kw1">new</span> Geometry<span class="br0">(</span><span class="st0">"OurMesh"</span>, mesh<span class="br0">)</span><span class="sy0">;</span> <span class="co1">// using our custom mesh object</span>
Material mat <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>assetManager, 
    <span class="st0">"Common/MatDefs/Misc/Unshaded.j3md"</span><span class="br0">)</span><span class="sy0">;</span>
mat.<span class="me1">setColor</span><span class="br0">(</span><span class="st0">"Color"</span>, ColorRGBA.<span class="me1">Blue</span><span class="br0">)</span><span class="sy0">;</span>
geo.<span class="me1">setMaterial</span><span class="br0">(</span>mat<span class="br0">)</span><span class="sy0">;</span>
rootNode.<span class="me1">attachChild</span><span class="br0">(</span>geo<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
Library for assetManager?
Ta-daa!
</p>

</div>
<!-- EDIT9 SECTION "Using the Mesh in a Scene" [6106-6642] -->
<h2 class="sectionedit10" id="using_a_quad_instead">Using a Quad instead</h2>
<div class="level2">

<p>
We created a quad Mesh it can be replace by a Quad such as :
</p>
<pre class="code java">Quad quad <span class="sy0">=</span> <span class="kw1">new</span> Quad<span class="br0">(</span><span class="nu0">1</span>,<span class="nu0">1</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// replace the definition of Vertex and Textures Coordinates plus indexes</span>
Geometry geo <span class="sy0">=</span> <span class="kw1">new</span> Geometry<span class="br0">(</span><span class="st0">"OurQuad"</span>, quad<span class="br0">)</span><span class="sy0">;</span> <span class="co1">// using Quad object</span>
Material mat <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>assetManager, 
    <span class="st0">"Common/MatDefs/Misc/Unshaded.j3md"</span><span class="br0">)</span><span class="sy0">;</span>
mat.<span class="me1">setColor</span><span class="br0">(</span><span class="st0">"Color"</span>, ColorRGBA.<span class="me1">Blue</span><span class="br0">)</span><span class="sy0">;</span>
geo.<span class="me1">setMaterial</span><span class="br0">(</span>mat<span class="br0">)</span><span class="sy0">;</span>
rootNode.<span class="me1">attachChild</span><span class="br0">(</span>geo<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
If you want to change the Textures Coordinates, in order to change the scale of the texture, use :
</p>
<pre class="code java">Quad quad <span class="sy0">=</span> <span class="kw1">new</span> Quad<span class="br0">(</span><span class="nu0">1</span>,<span class="nu0">1</span><span class="br0">)</span><span class="sy0">;</span>
quad.<span class="me1">scaleTextureCoordinates</span><span class="br0">(</span><span class="kw1">new</span> Vector2f<span class="br0">(</span>width , height<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span></pre>

</div>
<!-- EDIT10 SECTION "Using a Quad instead" [6643-7305] -->
<h2 class="sectionedit11" id="dynamic_meshes">Dynamic Meshes</h2>
<div class="level2">

<p>
If you are modifying a mesh dynamically in a way which changes the model's bounds, you need to update it:
</p>
<ol>
<li class="level1"><div class="li"> Call <code>updateBound()</code> on the mesh object, and then </div>
</li>
<li class="level1"><div class="li"> call <code>updateModelBound()</code> on the Geometry object containing the mesh. </div>
</li>
</ol>

<p>
The updateModelBound() method warns you about not usually needing to use it, but that can be ignored in this special case.
</p>

<p>
<em>N.B.: This does not work on TerrainQuad.  Please use the TerrainQuad.adjustHeight() function to edit the TerrainQuad mesh instead.  Additionally, if you want to use collisions on them afterwards, you need to call TerrainPatch.getMesh().createCollisionData(); to update the collision data, else it will collide with what seems to be the old mesh. </em>
</p>

</div>
<!-- EDIT11 SECTION "Dynamic Meshes" [7306-8050] -->
<h2 class="sectionedit12" id="optional_mesh_features">Optional Mesh Features</h2>
<div class="level2">

<p>
There are more vertex buffers in a Mesh than the three shown above. For an overview, see also <a href="/jme3/advanced/mesh.html" class="wikilink1" title="jme3:advanced:mesh">mesh</a>.
</p>

</div>
<!-- EDIT12 SECTION "Optional Mesh Features" [8051-8190] -->
<h3 class="sectionedit13" id="examplevertex_colors">Example: Vertex Colors</h3>
<div class="level3">

<p>
Vertex coloring is a simple way of coloring meshes. Instead of just assigning one solid color, each vertex (corner) has a color assigned. The faces between the vertices are then colored with a gradient. For this demo, you can use the same mesh <code>mesh</code> object that you defined above.
</p>
<pre class="code java">Geometry geo <span class="sy0">=</span> <span class="kw1">new</span> Geometry <span class="br0">(</span><span class="st0">"ColoredMesh"</span>, mesh<span class="br0">)</span><span class="sy0">;</span> <span class="co1">// using the custom mesh</span>
Material matVC <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>assetManager, <span class="st0">"Common/MatDefs/Misc/Unshaded.j3md"</span><span class="br0">)</span><span class="sy0">;</span>
matVC.<span class="me1">setBoolean</span><span class="br0">(</span><span class="st0">"VertexColor"</span>, <span class="kw2">true</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
You create a float array color buffer:
</p>
<ul>
<li class="level1"><div class="li"> Assign 4 color values, RGBA, to each vertex.</div>
<ul>
<li class="level2"><div class="li"> To loop over the 4 color values, use a color index <pre class="code java"><span class="kw4">int</span> colorIndex <span class="sy0">=</span> <span class="nu0">0</span><span class="sy0">;</span></pre>
</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> The color buffer contains four color values for each vertex.</div>
<ul>
<li class="level2"><div class="li"> The Quad in this example has 4 vertices. <pre class="code java"><span class="kw4">float</span><span class="br0">[</span><span class="br0">]</span> colorArray <span class="sy0">=</span> <span class="kw1">new</span> <span class="kw4">float</span><span class="br0">[</span><span class="nu0">4</span><span class="sy0">*</span><span class="nu0">4</span><span class="br0">]</span><span class="sy0">;</span></pre>
</div>
</li>
<li class="level2"><div class="li"> Tip: If your mesh has a different number of vertices, you would write: <pre class="code java"><span class="kw4">float</span><span class="br0">[</span><span class="br0">]</span> colorArray <span class="sy0">=</span> <span class="kw1">new</span> <span class="kw4">float</span><span class="br0">[</span>yourVertexCount <span class="sy0">*</span> <span class="nu0">4</span><span class="br0">]</span></pre>
</div>
</li>
</ul>
</li>
</ul>

<p>
Loop over the colorArray buffer to quickly set some RGBA value for each vertex. As usual, RGBA color values range from 0.0f to 1.0f. <strong>Note that the color values in this example are arbitrarily chosen.</strong> It's just a quick loop to give every vertex a different RGBA value (a purplish gray, purple, a greenish gray, green, see screenshot), without writing too much code. For your own mesh, you'd assign meaningful values for the color buffer depending on which color you want your mesh to have.
</p>
<pre class="code java"><span class="co1">// note: the red and green values are arbitray in this example</span>
<span class="kw1">for</span><span class="br0">(</span><span class="kw4">int</span> i <span class="sy0">=</span> <span class="nu0">0</span><span class="sy0">;</span> i <span class="sy0">&lt;</span> <span class="nu0">4</span><span class="sy0">;</span> i<span class="sy0">++</span><span class="br0">)</span><span class="br0">{</span>
   <span class="co1">// Red value (is increased by .2 on each next vertex here)</span>
   colorArray<span class="br0">[</span>colorIndex<span class="sy0">++</span><span class="br0">]</span><span class="sy0">=</span> 0.1f<span class="sy0">+</span><span class="br0">(</span>.2f<span class="sy0">*</span>i<span class="br0">)</span><span class="sy0">;</span>
   <span class="co1">// Green value (is reduced by .2 on each next vertex)</span>
   colorArray<span class="br0">[</span>colorIndex<span class="sy0">++</span><span class="br0">]</span><span class="sy0">=</span> 0.9f<span class="sy0">-</span><span class="br0">(</span>0.2f<span class="sy0">*</span>i<span class="br0">)</span><span class="sy0">;</span>
   <span class="co1">// Blue value (remains the same in our case)</span>
   colorArray<span class="br0">[</span>colorIndex<span class="sy0">++</span><span class="br0">]</span><span class="sy0">=</span> 0.5f<span class="sy0">;</span>
   <span class="co1">// Alpha value (no transparency set here)</span>
   colorArray<span class="br0">[</span>colorIndex<span class="sy0">++</span><span class="br0">]</span><span class="sy0">=</span> 1.0f<span class="sy0">;</span>
<span class="br0">}</span></pre>

<p>
Next, set the color buffer. An RGBA color value contains four float components, thus the parameter <code>4</code>.
</p>
<pre class="code java">mesh.<span class="me1">setBuffer</span><span class="br0">(</span>Type.<a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+color"><span class="kw3">Color</span></a>, <span class="nu0">4</span>, colorArray<span class="br0">)</span><span class="sy0">;</span>
geo.<span class="me1">setMaterial</span><span class="br0">(</span>matVC<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
When you run this code, you see a gradient color extending from each vertex.
</p>

</div>
<!-- EDIT13 SECTION "Example: Vertex Colors" [8191-10469] -->
<h3 class="sectionedit14" id="exampleusing_meshes_with_lightingj3md">Example: Using Meshes With Lighting.j3md</h3>
<div class="level3">

<p>
The previous examples used the mesh together with the <code>Unshaded.j3md</code> material. If you want to use the mesh with a Phong illuminated material (such as <code>Lighting.j3md</code>), the mesh must include information about its Normals. (Normal Vectors encode in which direction a mesh polygon is facing, which is important for calculating light and shadow!)
</p>
<pre class="code java"><span class="kw4">float</span><span class="br0">[</span><span class="br0">]</span> normals <span class="sy0">=</span> <span class="kw1">new</span> <span class="kw4">float</span><span class="br0">[</span><span class="nu0">12</span><span class="br0">]</span><span class="sy0">;</span>
normals <span class="sy0">=</span> <span class="kw1">new</span> <span class="kw4">float</span><span class="br0">[</span><span class="br0">]</span><span class="br0">{</span><span class="nu0">0</span>,<span class="nu0">0</span>,<span class="nu0">1</span>, <span class="nu0">0</span>,<span class="nu0">0</span>,<span class="nu0">1</span>, <span class="nu0">0</span>,<span class="nu0">0</span>,<span class="nu0">1</span>, <span class="nu0">0</span>,<span class="nu0">0</span>,<span class="nu0">1</span><span class="br0">}</span><span class="sy0">;</span>
mesh.<span class="me1">setBuffer</span><span class="br0">(</span>Type.<span class="me1">Normal</span>, <span class="nu0">3</span>, BufferUtils.<span class="me1">createFloatBuffer</span><span class="br0">(</span>normals<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
You need to specify as many normals as the polygon has vertices. For a flat quad, the four normals point in the same direction. In this case, the direction is the Z unit vector (0,0,1), this means our quad is facing the camera. 
</p>

<p>
If the mesh is more complex or rounded, calculate cross products of neighbouring vertices to identify normal vectors!
</p>

</div>
<!-- EDIT14 SECTION "Example: Using Meshes With Lighting.j3md" [10470-11396] -->
<h3 class="sectionedit15" id="examplepoint_mode">Example: Point Mode</h3>
<div class="level3">

<p>
Additionally to coloring the faces as just described, you can hide the faces and show only the vertices as colored corner points. 
</p>
<pre class="code java">Geometry coloredMesh <span class="sy0">=</span> <span class="kw1">new</span> Geometry <span class="br0">(</span><span class="st0">"ColoredMesh"</span>, cMesh<span class="br0">)</span><span class="sy0">;</span>
...
<span class="me1">mesh</span>.<span class="me1">setMode</span><span class="br0">(</span>Mesh.<span class="me1">Mode</span>.<span class="me1">Points</span><span class="br0">)</span><span class="sy0">;</span>
mesh.<span class="me1">setPointSize</span><span class="br0">(</span>10f<span class="br0">)</span><span class="sy0">;</span>
mesh.<span class="me1">updateBound</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
mesh.<span class="me1">setStatic</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
Geometry points <span class="sy0">=</span> <span class="kw1">new</span> Geometry<span class="br0">(</span><span class="st0">"Points"</span>, mesh<span class="br0">)</span><span class="sy0">;</span>
points.<span class="me1">setMaterial</span><span class="br0">(</span>mat<span class="br0">)</span><span class="sy0">;</span>
rootNode.<span class="me1">attachChild</span><span class="br0">(</span>points<span class="br0">)</span><span class="sy0">;</span>
rootNode.<span class="me1">attachChild</span><span class="br0">(</span>geo<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
This will result in a 10 px dot being rendered for each of the four vertices. The dot has the vertex color you specified above. The Quad's faces are not rendered at all in this mode. You can use this to visualize a special debugging or editing mode in your game.
</p>

</div>
<!-- EDIT15 SECTION "Example: Point Mode" [11397-12130] -->
<h2 class="sectionedit16" id="debugging_tipculling">Debugging Tip: Culling</h2>
<div class="level2">

<p>
By default, jME3 optimizes a mesh by “backface culling”, this means not drawing the inside. It determines the side of a triangle by the order of the vertices: The frontface is the face where the vertices are specified counter-clockwise.
</p>

<p>
This means for you that, by default, your custom mesh is invisible when seen from “behind” or from the inside. This may not be a problem, typically this is even intended, because it's faster. The player will not look at the inside of most things anyway. For example, if your custom mesh is a closed polyhedron, or a flat wallpaper-like object, then rendering the backfaces (the inside of the pillar, the back of the painting, etc) would indeed be a waste of resources.
</p>

<p>
In case however that your usecase requires the backfaces be visible, you have two options:
</p>
<ul>
<li class="level1"><div class="li"> If you have a very simple scene, you can simply deactivate backface culling for this one mesh's material. <pre class="code">mat.getAdditionalRenderState().setFaceCullMode(FaceCullMode.Off);</pre>
</div>
</li>
<li class="level1"><div class="li"> Another solution for truly double-sided meshes is to specify each triangle twice, the second time with the opposite order of vertices. The second (reversed) triangle is a second frontface that covers up the culled backface. <pre class="code">int[] indexes = { 2,0,1, 1,3,2, 2,3,1, 1,0,2 };</pre>
</div>
</li>
</ul>
<hr />

<p>
See also: 
</p>
<ul>
<li class="level1"><div class="li"> <a href="/jme3/advanced/spatial.html" class="wikilink1" title="jme3:advanced:spatial">Spatial</a> – contains more info about how to debug custom meshes (that do not render as expected) by changing the default culling behaviour.</div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/advanced/mesh.html" class="wikilink1" title="jme3:advanced:mesh">Mesh</a> – more details about advanced Mesh properties</div>
</li>
</ul>
<div class="tags"><span>
	<a href="/tag/spatial.html" class="wikilink1" title="tag:spatial" rel="tag">spatial</a>,
	<a href="/tag/node.html" class="wikilink1" title="tag:node" rel="tag">node</a>,
	<a href="/tag/mesh.html" class="wikilink1" title="tag:mesh" rel="tag">mesh</a>,
	<a href="/tag/geometry.html" class="wikilink1" title="tag:geometry" rel="tag">geometry</a>,
	<a href="/tag/scenegraph.html" class="wikilink1" title="tag:scenegraph" rel="tag">scenegraph</a>
</span></div>

</div>
<!-- EDIT16 SECTION "Debugging Tip: Culling" [12131-] -->
