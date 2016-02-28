---
title: Debugging
---
<h1 class="sectionedit1" id="debugging">Debugging</h1>
<div class="level1">

<p>
When you deal with complex game engine features like animations or physics it is handy to get feedback from the engine how it interpreted the current state. Is the physical object's collision shape really where you think it is? Is the skeleton of the animated character moving like you think it should? This document shows you how to activate visual debug aides.
</p>

<p>
What if you just want to quickly write code that loads models and brings them in their start position? You may not want to hunt for a sample model, convert it, add lights, and load materials. Instead you use “hasslefree” simple shapes, and a “hasslefree” unshaded material or wireframe: No model, no light source, no materials are needed to see them in your test scene. 
</p>

<p>
If you ever have problems with objects appearing in the wrong spot, with the wrong scale, or wrong orientation, simply attach debug shapes to your scene to have a point of reference in 3D space – just like a giant ruler. If your code positions the debug shapes correctly, but models remain invisible when you apply the same code to them, you know that the problem must be either the model (where is its origin coordinate?), or the light (too dark? too bright? missing?), or the model's material (missing?) – and not the positioning code.
</p>

<p>
Here are some different debug shapes: 
</p>

<p>
<a href="/resources/jme3-advanced-debug-shapes.png" class="media" title="jme3:advanced:debug-shapes.png"><img src="/resources/jme3-advanced-debug-shapes.png" class="mediacenter" alt="" width="600" height="220" /></a>
</p>

</div>
<!-- EDIT1 SECTION "Debugging" [1-1389] -->
<h2 class="sectionedit2" id="debug_shapes">Debug Shapes</h2>
<div class="level2">

</div>
<!-- EDIT2 SECTION "Debug Shapes" [1390-1415] -->
<h3 class="sectionedit3" id="coordinate_axes">Coordinate Axes</h3>
<div class="level3">

<p>
The coordinate axes (com.jme3.scene.debug.Arrow) help you see the cardinal directions (X,Y,Z) from their center point. Scale the arrows to use them as a “ruler” for a certain length. 
</p>
<pre class="code java"><span class="kw1">private</span> <span class="kw4">void</span> attachCoordinateAxes<span class="br0">(</span>Vector3f pos<span class="br0">)</span><span class="br0">{</span>
  Arrow arrow <span class="sy0">=</span> <span class="kw1">new</span> Arrow<span class="br0">(</span>Vector3f.<span class="me1">UNIT_X</span><span class="br0">)</span><span class="sy0">;</span>
  arrow.<span class="me1">setLineWidth</span><span class="br0">(</span><span class="nu0">4</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// make arrow thicker</span>
  putShape<span class="br0">(</span>arrow, ColorRGBA.<span class="me1">Red</span><span class="br0">)</span>.<span class="me1">setLocalTranslation</span><span class="br0">(</span>pos<span class="br0">)</span><span class="sy0">;</span>
 
  arrow <span class="sy0">=</span> <span class="kw1">new</span> Arrow<span class="br0">(</span>Vector3f.<span class="me1">UNIT_Y</span><span class="br0">)</span><span class="sy0">;</span>
  arrow.<span class="me1">setLineWidth</span><span class="br0">(</span><span class="nu0">4</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// make arrow thicker</span>
  putShape<span class="br0">(</span>arrow, ColorRGBA.<span class="me1">Green</span><span class="br0">)</span>.<span class="me1">setLocalTranslation</span><span class="br0">(</span>pos<span class="br0">)</span><span class="sy0">;</span>
 
  arrow <span class="sy0">=</span> <span class="kw1">new</span> Arrow<span class="br0">(</span>Vector3f.<span class="me1">UNIT_Z</span><span class="br0">)</span><span class="sy0">;</span>
  arrow.<span class="me1">setLineWidth</span><span class="br0">(</span><span class="nu0">4</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// make arrow thicker</span>
  putShape<span class="br0">(</span>arrow, ColorRGBA.<span class="me1">Blue</span><span class="br0">)</span>.<span class="me1">setLocalTranslation</span><span class="br0">(</span>pos<span class="br0">)</span><span class="sy0">;</span>
<span class="br0">}</span>
 
<span class="kw1">private</span> Geometry putShape<span class="br0">(</span>Mesh shape, ColorRGBA color<span class="br0">)</span><span class="br0">{</span>
  Geometry g <span class="sy0">=</span> <span class="kw1">new</span> Geometry<span class="br0">(</span><span class="st0">"coordinate axis"</span>, shape<span class="br0">)</span><span class="sy0">;</span>
  Material mat <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>assetManager, <span class="st0">"Common/MatDefs/Misc/Unshaded.j3md"</span><span class="br0">)</span><span class="sy0">;</span>
  mat.<span class="me1">getAdditionalRenderState</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">setWireframe</span><span class="br0">(</span><span class="kw2">true</span><span class="br0">)</span><span class="sy0">;</span>
  mat.<span class="me1">setColor</span><span class="br0">(</span><span class="st0">"Color"</span>, color<span class="br0">)</span><span class="sy0">;</span>
  g.<span class="me1">setMaterial</span><span class="br0">(</span>mat<span class="br0">)</span><span class="sy0">;</span>
  rootNode.<span class="me1">attachChild</span><span class="br0">(</span>g<span class="br0">)</span><span class="sy0">;</span>
  <span class="kw1">return</span> g<span class="sy0">;</span>
<span class="br0">}</span></pre>

</div>
<!-- EDIT3 SECTION "Coordinate Axes" [1416-2483] -->
<h3 class="sectionedit4" id="wireframe_grid">Wireframe Grid</h3>
<div class="level3">

<p>
Use a wireframe grid (com.jme3.scene.debug.Grid) as a ruler or simple floor.
</p>
<pre class="code java"><span class="kw1">private</span> Geometry attachGrid<span class="br0">(</span>Vector3f pos, <span class="kw4">float</span> size, ColorRGBA color<span class="br0">)</span><span class="br0">{</span>
  Geometry g <span class="sy0">=</span> <span class="kw1">new</span> Geometry<span class="br0">(</span><span class="st0">"wireframe grid"</span>, <span class="kw1">new</span> Grid<span class="br0">(</span>size, size, 0.2f<span class="br0">)</span> <span class="br0">)</span><span class="sy0">;</span>
  Material mat <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>assetManager, <span class="st0">"Common/MatDefs/Misc/Unshaded.j3md"</span><span class="br0">)</span><span class="sy0">;</span>
  mat.<span class="me1">getAdditionalRenderState</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">setWireframe</span><span class="br0">(</span><span class="kw2">true</span><span class="br0">)</span><span class="sy0">;</span>
  mat.<span class="me1">setColor</span><span class="br0">(</span><span class="st0">"Color"</span>, color<span class="br0">)</span><span class="sy0">;</span>
  g.<span class="me1">setMaterial</span><span class="br0">(</span>mat<span class="br0">)</span><span class="sy0">;</span>
  g.<span class="me1">center</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">move</span><span class="br0">(</span>pos<span class="br0">)</span><span class="sy0">;</span>
  rootNode.<span class="me1">attachChild</span><span class="br0">(</span>g<span class="br0">)</span><span class="sy0">;</span>
  <span class="kw1">return</span> g<span class="sy0">;</span>
<span class="br0">}</span></pre>

</div>
<!-- EDIT4 SECTION "Wireframe Grid" [2484-3009] -->
<h3 class="sectionedit5" id="wireframe_cube">Wireframe Cube</h3>
<div class="level3">

<p>
Use a wireframe cube (com.jme3.scene.debug.WireBox) as a stand-in object to see whether your code scales, positions, or orients, loaded models right.
</p>
<pre class="code java"><span class="kw1">public</span> Geometry attachWireBox<span class="br0">(</span>Vector3f pos, <span class="kw4">float</span> size, ColorRGBA color<span class="br0">)</span><span class="br0">{</span>
  Geometry g <span class="sy0">=</span> <span class="kw1">new</span> Geometry<span class="br0">(</span><span class="st0">"wireframe cube"</span>, <span class="kw1">new</span> WireBox<span class="br0">(</span>size, size, size<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
  Material mat <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>assetManager, <span class="st0">"Common/MatDefs/Misc/Unshaded.j3md"</span><span class="br0">)</span><span class="sy0">;</span>
  mat.<span class="me1">getAdditionalRenderState</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">setWireframe</span><span class="br0">(</span><span class="kw2">true</span><span class="br0">)</span><span class="sy0">;</span>
  mat.<span class="me1">setColor</span><span class="br0">(</span><span class="st0">"Color"</span>, color<span class="br0">)</span><span class="sy0">;</span>
  g.<span class="me1">setMaterial</span><span class="br0">(</span>mat<span class="br0">)</span><span class="sy0">;</span>
  g.<span class="me1">setLocalTranslation</span><span class="br0">(</span>pos<span class="br0">)</span><span class="sy0">;</span>
  rootNode.<span class="me1">attachChild</span><span class="br0">(</span>g<span class="br0">)</span><span class="sy0">;</span>
  <span class="kw1">return</span> g<span class="sy0">;</span>
<span class="br0">}</span></pre>

</div>
<!-- EDIT5 SECTION "Wireframe Cube" [3010-3619] -->
<h3 class="sectionedit6" id="wireframe_sphere">Wireframe Sphere</h3>
<div class="level3">

<p>
Use a wireframe sphere (com.jme3.scene.debug.WireSphere) as a stand-in object to see whether your code scales, positions, or orients, loaded models right.
</p>
<pre class="code java"><span class="kw1">private</span> Geometry attachWireSphere<span class="br0">(</span>Vector3f pos, <span class="kw4">float</span> size, ColorRGBA color<span class="br0">)</span><span class="br0">{</span>
  Geometry g <span class="sy0">=</span> <span class="kw1">new</span> Geometry<span class="br0">(</span><span class="st0">"wireframe sphere"</span>, <span class="kw1">new</span> WireSphere<span class="br0">(</span>size<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
  Material mat <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>assetManager, <span class="st0">"Common/MatDefs/Misc/Unshaded.j3md"</span><span class="br0">)</span><span class="sy0">;</span>
  mat.<span class="me1">getAdditionalRenderState</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">setWireframe</span><span class="br0">(</span><span class="kw2">true</span><span class="br0">)</span><span class="sy0">;</span>
  mat.<span class="me1">setColor</span><span class="br0">(</span><span class="st0">"Color"</span>, color<span class="br0">)</span><span class="sy0">;</span>
  g.<span class="me1">setMaterial</span><span class="br0">(</span>mat<span class="br0">)</span><span class="sy0">;</span>
  g.<span class="me1">setLocalTranslation</span><span class="br0">(</span>pos<span class="br0">)</span><span class="sy0">;</span>
  rootNode.<span class="me1">attachChild</span><span class="br0">(</span>g<span class="br0">)</span><span class="sy0">;</span>
  <span class="kw1">return</span> g<span class="sy0">;</span>
<span class="br0">}</span></pre>

</div>
<!-- EDIT6 SECTION "Wireframe Sphere" [3620-4232] -->
<h2 class="sectionedit7" id="wireframe_for_physics">Wireframe for Physics</h2>
<div class="level2">

<p>
You can display a wireframe of the (usually invisible) collision shape around all physical objects. Use this for debugging when analyzing unexpected behaviour. Does not work with DETACHED physics, please switch to PARALLEL or SEQUENTIAL for debugging.
</p>
<pre class="code java">physicsSpace.<span class="me1">enableDebug</span><span class="br0">(</span>assetManager<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
With debugging enabled, colors are used to indicate various types of physical objects:
</p>
<ul>
<li class="level1"><div class="li"> A magenta wire mesh indicates an active rigid body.</div>
</li>
<li class="level1"><div class="li"> A blue wire mesh indicates a rigid body which is either new or inactive.</div>
</li>
<li class="level1"><div class="li"> A yellow wire mesh indicates a ghost.</div>
</li>
<li class="level1"><div class="li"> Two green arrows indicate a joint.</div>
</li>
<li class="level1"><div class="li"> A pink wire mesh indicates a character.</div>
</li>
</ul>

</div>
<!-- EDIT7 SECTION "Wireframe for Physics" [4233-4925] -->
<h2 class="sectionedit8" id="wireframe_for_animations">Wireframe for Animations</h2>
<div class="level2">

<p>
Making the skeleton visible inside animated models can be handy for debugging animations. The <code>control</code> object is an AnimControl, <code>player</code> is the loaded model.
</p>
<pre class="code java">     SkeletonDebugger skeletonDebug <span class="sy0">=</span> 
         <span class="kw1">new</span> SkeletonDebugger<span class="br0">(</span><span class="st0">"skeleton"</span>, control.<span class="me1">getSkeleton</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
     Material mat <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>assetManager, <span class="st0">"Common/MatDefs/Misc/Unshaded.j3md"</span><span class="br0">)</span><span class="sy0">;</span>
     mat.<span class="me1">setColor</span><span class="br0">(</span><span class="st0">"Color"</span>, ColorRGBA.<span class="me1">Green</span><span class="br0">)</span><span class="sy0">;</span>
     mat.<span class="me1">getAdditionalRenderState</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">setDepthTest</span><span class="br0">(</span><span class="kw2">false</span><span class="br0">)</span><span class="sy0">;</span>
     skeletonDebug.<span class="me1">setMaterial</span><span class="br0">(</span>mat<span class="br0">)</span><span class="sy0">;</span>
     player.<span class="me1">attachChild</span><span class="br0">(</span>skeletonDebug<span class="br0">)</span><span class="sy0">;</span></pre>

</div>
<!-- EDIT8 SECTION "Wireframe for Animations" [4926-5517] -->
<h2 class="sectionedit9" id="exampletoggle_wireframe_on_model">Example: Toggle Wireframe on Model</h2>
<div class="level2">

<p>
We assume that you have loaded a model with a material <code>mat</code>.
</p>

<p>
Then you can add a switch to toggle the model's wireframe on and off, like this:
</p>
<ol>
<li class="level1"><div class="li"> Create a key input trigger that switches between the two materials: E.g. we toggle when the T key is pressed: <pre class="code java">    inputManager.<span class="me1">addMapping</span><span class="br0">(</span><span class="st0">"toggle wireframe"</span>, <span class="kw1">new</span> KeyTrigger<span class="br0">(</span>KeyInput.<span class="me1">KEY_T</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    inputManager.<span class="me1">addListener</span><span class="br0">(</span>actionListener, <span class="st0">"toggle wireframe"</span><span class="br0">)</span><span class="sy0">;</span></pre>
</div>
</li>
<li class="level1"><div class="li"> Now add the toggle action to the action listener <pre class="code java">  <span class="kw1">private</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+actionlistener"><span class="kw3">ActionListener</span></a> actionListener <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+actionlistener"><span class="kw3">ActionListener</span></a><span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
    @Override
    <span class="kw1">public</span> <span class="kw4">void</span> onAction<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> name, <span class="kw4">boolean</span> pressed, <span class="kw4">float</span> tpf<span class="br0">)</span> <span class="br0">{</span>
      <span class="co1">// toggle wireframe</span>
      <span class="kw1">if</span> <span class="br0">(</span>name.<span class="me1">equals</span><span class="br0">(</span><span class="st0">"toggle wireframe"</span><span class="br0">)</span> <span class="sy0">&amp;&amp;</span> <span class="sy0">!</span>pressed<span class="br0">)</span> <span class="br0">{</span>
        wireframe <span class="sy0">=</span> <span class="sy0">!</span>wireframe<span class="sy0">;</span> <span class="co1">// toggle boolean</span>
        mat.<span class="me1">getAdditionalRenderState</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">setWireframe</span><span class="br0">(</span>wireframe<span class="br0">)</span><span class="sy0">;</span> 
      <span class="br0">}</span>
      <span class="co1">// else ... other input tests.</span>
    <span class="br0">}</span>
  <span class="br0">}</span><span class="sy0">;</span></pre>
</div>
</li>
<li class="level1"><div class="li"> Alternatively you could traverse over the whole scene and toggle for all Geometry objects in there if you don't want to create a new SceneProcessor <pre class="code java">  <span class="kw1">private</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+actionlistener"><span class="kw3">ActionListener</span></a> actionListener <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+actionlistener"><span class="kw3">ActionListener</span></a><span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
    <span class="kw4">boolean</span> wireframe <span class="sy0">=</span> <span class="kw2">false</span><span class="sy0">;</span> 
 
    @Override
    <span class="kw1">public</span> <span class="kw4">void</span> onAction<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> name, <span class="kw4">boolean</span> pressed, <span class="kw4">float</span> tpf<span class="br0">)</span> <span class="br0">{</span>
      <span class="co1">// toggle wireframe</span>
      <span class="kw1">if</span> <span class="br0">(</span>name.<span class="me1">equals</span><span class="br0">(</span><span class="st0">"toggle wireframe"</span><span class="br0">)</span> <span class="sy0">&amp;&amp;</span> <span class="sy0">!</span>pressed<span class="br0">)</span> <span class="br0">{</span>
        wireframe <span class="sy0">=</span> <span class="sy0">!</span>wireframe<span class="sy0">;</span> <span class="co1">// toggle boolean</span>
        rootNode.<span class="me1">depthFirstTraversal</span><span class="br0">(</span><span class="kw1">new</span> SceneGraphVisitor<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
          <span class="kw1">public</span> <span class="kw4">void</span> visit<span class="br0">(</span>Spatial spatial<span class="br0">)</span> <span class="br0">{</span>
            <span class="kw1">if</span> <span class="br0">(</span>spatial <span class="kw1">instanceof</span> Geometry<span class="br0">)</span>
              <span class="br0">(</span><span class="br0">(</span>Geometry<span class="br0">)</span>spatial<span class="br0">)</span>.<span class="me1">getMaterial</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">getAdditionalRenderState</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">setWireframe</span><span class="br0">(</span>wireframe<span class="br0">)</span><span class="sy0">;</span>
          <span class="br0">}</span>
        <span class="br0">}</span><span class="br0">)</span><span class="sy0">;</span> 
      <span class="br0">}</span>
      <span class="co1">// else ... other input tests.</span>
    <span class="br0">}</span>
  <span class="br0">}</span><span class="sy0">;</span></pre>
</div>
</li>
</ol>

<p>
TIP :: To set the line width of wireframe display, use mesh.setLineWidth(lineWidth). Default line width is 1.
</p>

</div>
<!-- EDIT9 SECTION "Example: Toggle Wireframe on Model" [5518-7408] -->
<h2 class="sectionedit10" id="exampletoggle_wireframe_on_the_scene">Example: Toggle Wireframe on the scene</h2>
<div class="level2">

<p>
To display the wireframe of the entire scene instead on one material at a time, first create the following Scene Processor
</p>
<pre class="code java"><span class="kw1">public</span> <span class="kw1">class</span> WireProcessor <span class="kw1">implements</span> SceneProcessor <span class="br0">{</span>    
 
    RenderManager renderManager<span class="sy0">;</span>
    Material wireMaterial<span class="sy0">;</span>
 
    <span class="kw1">public</span> WireProcessor<span class="br0">(</span>AssetManager assetManager<span class="br0">)</span> <span class="br0">{</span>
        wireMaterial <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>assetManager, <span class="st0">"/Common/MatDefs/Misc/Unshaded.j3md"</span><span class="br0">)</span><span class="sy0">;</span>
        wireMaterial.<span class="me1">setColor</span><span class="br0">(</span><span class="st0">"Color"</span>, ColorRGBA.<span class="me1">Blue</span><span class="br0">)</span><span class="sy0">;</span>
        wireMaterial.<span class="me1">getAdditionalRenderState</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">setWireframe</span><span class="br0">(</span><span class="kw2">true</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    <span class="kw1">public</span> <span class="kw4">void</span> initialize<span class="br0">(</span>RenderManager rm, ViewPort vp<span class="br0">)</span> <span class="br0">{</span>
        renderManager <span class="sy0">=</span> rm<span class="sy0">;</span>
    <span class="br0">}</span>
 
    <span class="kw1">public</span> <span class="kw4">void</span> reshape<span class="br0">(</span>ViewPort vp, <span class="kw4">int</span> w, <span class="kw4">int</span> h<span class="br0">)</span> <span class="br0">{</span>
        <span class="kw1">throw</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+unsupportedoperationexception"><span class="kw3">UnsupportedOperationException</span></a><span class="br0">(</span><span class="st0">"Not supported yet."</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    <span class="kw1">public</span> <span class="kw4">boolean</span> isInitialized<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
        <span class="kw1">return</span> renderManager <span class="sy0">!=</span> <span class="kw2">null</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    <span class="kw1">public</span> <span class="kw4">void</span> preFrame<span class="br0">(</span><span class="kw4">float</span> tpf<span class="br0">)</span> <span class="br0">{</span>        
    <span class="br0">}</span>
 
    <span class="kw1">public</span> <span class="kw4">void</span> postQueue<span class="br0">(</span>RenderQueue rq<span class="br0">)</span> <span class="br0">{</span>
        renderManager.<span class="me1">setForcedMaterial</span><span class="br0">(</span>wireMaterial<span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    <span class="kw1">public</span> <span class="kw4">void</span> postFrame<span class="br0">(</span>FrameBuffer out<span class="br0">)</span> <span class="br0">{</span>
        renderManager.<span class="me1">setForcedMaterial</span><span class="br0">(</span><span class="kw2">null</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    <span class="kw1">public</span> <span class="kw4">void</span> cleanup<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
        renderManager.<span class="me1">setForcedMaterial</span><span class="br0">(</span><span class="kw2">null</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
<span class="br0">}</span></pre>

<p>
Then attach the scene processor to the <abbr title="Graphical User Interface">GUI</abbr> Viewport.
</p>
<pre class="code java">getViewPort<span class="br0">(</span><span class="br0">)</span>.<span class="me1">addProcessor</span><span class="br0">(</span><span class="kw1">new</span> WireProcessor<span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span></pre>

</div>
<!-- EDIT10 SECTION "Example: Toggle Wireframe on the scene" [7409-8782] -->
<h2 class="sectionedit11" id="see_also">See also</h2>
<div class="level2">
<ul>
<li class="level1"><div class="li"> <a href="/jme3/advanced/spatial.html" class="wikilink1" title="jme3:advanced:spatial">Spatial</a> – if you can't see certain spatials, you can modify the culling behaviour to identify problems (such as inside-out custom meshes)</div>
</li>
</ul>

</div>
<!-- EDIT11 SECTION "See also" [8783-] -->
