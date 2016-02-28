---
title: 3ds Max Bone Animation to JME3 using OgreMax plugin
---
<h1 class="sectionedit1" id="ds_max_bone_animation_to_jme3_using_ogremax_plugin">3ds Max Bone Animation to JME3 using OgreMax plugin</h1>
<div class="level1">

</div>
<!-- EDIT1 SECTION "3ds Max Bone Animation to JME3 using OgreMax plugin" [1-67] -->
<h2 class="sectionedit2" id="asset_management">Asset Management</h2>
<div class="level2">

<p>
For the managing of assets in general, be sure to read the <a href="/jme3/intermediate/multi-media_asset_pipeline.html" class="wikilink1" title="jme3:intermediate:multi-media_asset_pipeline">Asset Pipeline Documentation</a>. It contains vital information on how to manage your asset files.
</p>

</div>
<!-- EDIT2 SECTION "Asset Management" [68-300] -->
<h2 class="sectionedit3" id="creating_models_in_3dsmax">Creating models in 3dsMax</h2>
<div class="level2">

<p>
For this tutorial I used 3D Studio Max 2012 and OgreMax 2.4.3 free edition
</p>

</div>
<!-- EDIT3 SECTION "Creating models in 3dsMax" [301-414] -->
<h3 class="sectionedit4" id="create_model_and_bones">Create Model and Bones</h3>
<div class="level3">
<ul>
<li class="level1"><div class="li"> Create a new file</div>
</li>
<li class="level1"><div class="li"> Select the “Create” tab &gt; “Geometry” &gt; “Cylinder”</div>
</li>
</ul>

<p>
<a href="/resources/jme3-external-3dsmax-0.png" class="media" title="jme3:external:3dsmax-0.png"><img src="/resources/jme3-external-3dsmax-0.png" class="media" alt="" /></a>
</p>
<ul>
<li class="level1"><div class="li"> Draw a cylinder, lets say with 8 height segments (must be enough for a smooth deformation)</div>
</li>
<li class="level1"><div class="li"> Also check “Generate Mapping Coords.”</div>
</li>
</ul>

<p>
<a href="/resources/jme3-external-3dsmax-1.png" class="media" title="jme3:external:3dsmax-1.png"><img src="/resources/jme3-external-3dsmax-1.png" class="media" alt="" /></a>
</p>
<ul>
<li class="level1"><div class="li"> Click “Create” tab &gt; “Systems” &gt; “Bones”</div>
</li>
</ul>

<p>
<a href="/resources/jme3-external-3dsmax-2.png" class="media" title="jme3:external:3dsmax-2.png"><img src="/resources/jme3-external-3dsmax-2.png" class="media" alt="" /></a>
</p>
<ul>
<li class="level1"><div class="li"> Add some bones in the center of the cylinder</div>
</li>
</ul>

<p>
<a href="/resources/jme3-external-3dsmax-3.png" class="media" title="jme3:external:3dsmax-3.png"><img src="/resources/jme3-external-3dsmax-3.png" class="media" alt="" /></a>
</p>
<ul>
<li class="level1"><div class="li"> Select the cylinder, right click it and click “Convert To:” &gt; “Convert to Editable Mesh” to prevent issues with OgreMax</div>
</li>
<li class="level1"><div class="li"> Click the “Modify” tab &gt; “Modifier List” and add the “Skin” modifier</div>
</li>
</ul>

<p>
<a href="/resources/jme3-external-3dsmax-4.png" class="media" title="jme3:external:3dsmax-4.png"><img src="/resources/jme3-external-3dsmax-4.png" class="media" alt="" /></a>
</p>
<ul>
<li class="level1"><div class="li"> Beneath “Bones:” click “Add” and select all of your bones</div>
</li>
</ul>

<p>
<a href="/resources/jme3-external-3dsmax-5.png" class="media" title="jme3:external:3dsmax-5.png"><img src="/resources/jme3-external-3dsmax-5.png" class="media" alt="" /></a>
</p>
<ul>
<li class="level1"><div class="li"> You may also edit the envelopes, but for a small test the default settings are ok</div>
</li>
</ul>

</div>
<!-- EDIT4 SECTION "Create Model and Bones" [415-1354] -->
<h3 class="sectionedit5" id="create_the_animation">Create the animation</h3>
<div class="level3">
<ul>
<li class="level1"><div class="li"> Select the cylinder, and click “Display” tab &gt; “Freeze Selected” so it is easier to select the bones during animation</div>
</li>
<li class="level1"><div class="li"> Select the two top bones and enable the “Auto Key” mode</div>
</li>
</ul>

<p>
<a href="/resources/jme3-external-3dsmax-6.png" class="media" title="jme3:external:3dsmax-6.png"><img src="/resources/jme3-external-3dsmax-6.png" class="media" alt="" /></a>
</p>
<ul>
<li class="level1"><div class="li"> The first key frame will be created automatically. Move the animation track slider to frame 5</div>
</li>
<li class="level1"><div class="li"> Move the selected bones a bit. The cylinder mesh will be deformed. Because you are in the “Auto Key” mode, a key frame will be created</div>
</li>
</ul>

<p>
<a href="/resources/jme3-external-3dsmax-7.png" class="media" title="jme3:external:3dsmax-7.png"><img src="/resources/jme3-external-3dsmax-7.png" class="media" alt="" /></a>
</p>
<ul>
<li class="level1"><div class="li"> Create some additional key frames. You may also select more bones and move or rotate them. I’ve created 25 frames and the last key frame equals the first, so the animation is loopable</div>
</li>
<li class="level1"><div class="li"> After creating the animation, disable the “Auto Key” mode</div>
</li>
</ul>

</div>
<!-- EDIT5 SECTION "Create the animation" [1355-2141] -->
<h3 class="sectionedit6" id="ogremax_settings">OgreMax settings</h3>
<div class="level3">
<ul>
<li class="level1"><div class="li"> Open the “OgreMax Scene Settings” dialog from the menu</div>
</li>
<li class="level1"><div class="li"> In the “Meshes” tab, enable “Export XML Files” and disable “Export Binary Files” as well as “Export Vertex Colors”</div>
</li>
</ul>

<p>
<a href="/resources/jme3-external-3dsmax-8.png" class="media" title="jme3:external:3dsmax-8.png"><img src="/resources/jme3-external-3dsmax-8.png" class="media" alt="" /></a>
</p>
<ul>
<li class="level1"><div class="li"> Click the “Environment” tab and uncheck “Export Environment Settings”. Otherwise the JME importer will throw a NullPointerException</div>
</li>
</ul>

<p>
<a href="/resources/jme3-external-3dsmax-9.png" class="media" title="jme3:external:3dsmax-9.png"><img src="/resources/jme3-external-3dsmax-9.png" class="media" alt="" /></a>
</p>
<ul>
<li class="level1"><div class="li"> If you have textured your model, you may also check “Copy Bitmaps to Export Directory” in the “Bitmaps” tab</div>
</li>
<li class="level1"><div class="li"> Unfreeze the cylinder by clicking “Display” tab &gt; “Unfreeze All” and select it</div>
</li>
<li class="level1"><div class="li"> While having the cylinder selected, open the “OgreMax Object Settings” dialog from the menu</div>
</li>
<li class="level1"><div class="li"> Open the “Mesh Animations” tab and select type “Skeleton”, “Export Skeleton” : “Yes”</div>
</li>
<li class="level1"><div class="li"> Below “Mesh Animations” hit the “Add…” button</div>
</li>
<li class="level1"><div class="li"> Assign a name to the track, maybe “wobble”. The track type must be “Skin. Set the right “Start/End Frames” for your animation</div>
</li>
</ul>

<p>
<a href="/resources/jme3-external-3dsmax-10.png" class="media" title="jme3:external:3dsmax-10.png"><img src="/resources/jme3-external-3dsmax-10.png" class="media" alt="" /></a>
</p>
<ul>
<li class="level1"><div class="li"> Hit ok and you will see the animation in the table. You may add additional animations by selecting other frame ranges, if desired</div>
</li>
</ul>

<p>
<a href="/resources/jme3-external-3dsmax-11.png" class="media" title="jme3:external:3dsmax-11.png"><img src="/resources/jme3-external-3dsmax-11.png" class="media" alt="" /></a>
</p>

</div>
<!-- EDIT6 SECTION "OgreMax settings" [2142-3395] -->
<h3 class="sectionedit7" id="export_and_import">Export and Import</h3>
<div class="level3">
<ul>
<li class="level1"><div class="li"> When all animations are in the list, select “OgreMax” &gt; “Export” &gt; “Export Scene” and name the file “worm.scene”</div>
</li>
<li class="level1"><div class="li"> Create a JME test class that imports the file, get the animation controller and start the “wobble” animation</div>
</li>
</ul>
<pre class="code java"><span class="kw1">import</span> <span class="co2">com.jme3.animation.AnimChannel</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.animation.AnimControl</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.animation.Skeleton</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.app.SimpleApplication</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.asset.plugins.FileLocator</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.light.AmbientLight</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.light.PointLight</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.material.Material</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.math.ColorRGBA</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.Geometry</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.Node</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.Spatial</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.control.LodControl</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.debug.SkeletonDebugger</span><span class="sy0">;</span>
 
<span class="co3">/**
 * This is a test class for loading a Ogre XML scene exported by OgreMax.
 * 
 * @author Stephan Dreyer
 * 
 */</span>
<span class="kw1">public</span> <span class="kw1">class</span> TestOgreMaxImport <span class="co2">extends</span> SimpleApplication <span class="br0">{</span>
 
  @Override
  <span class="kw1">public</span> <span class="kw4">void</span> simpleInitApp<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
    assetManager.<span class="me1">registerLocator</span><span class="br0">(</span><span class="st0">"Assets/model/ogre/test/"</span>, FileLocator.<span class="kw1">class</span><span class="br0">)</span><span class="sy0">;</span>
 
    <span class="co1">// create the geometry and attach it</span>
    <span class="kw1">final</span> Node model <span class="sy0">=</span> <span class="br0">(</span>Node<span class="br0">)</span> assetManager.<span class="me1">loadModel</span><span class="br0">(</span><span class="st0">"worm.scene"</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="co1">// resize it, because of the large 3dsmax scales</span>
    model.<span class="me1">setLocalScale</span><span class="br0">(</span>.001f<span class="br0">)</span><span class="sy0">;</span>
 
    <span class="co1">// attach to root node</span>
    rootNode.<span class="me1">attachChild</span><span class="br0">(</span>model<span class="br0">)</span><span class="sy0">;</span>
    addLodControl<span class="br0">(</span>model<span class="br0">)</span><span class="sy0">;</span>
 
    <span class="kw1">final</span> AnimControl ac <span class="sy0">=</span> findAnimControl<span class="br0">(</span>model<span class="br0">)</span><span class="sy0">;</span>
 
    <span class="kw1">try</span> <span class="br0">{</span>
      <span class="co1">// add a skeleton debugger to make bones visible</span>
      <span class="kw1">final</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+skeleton"><span class="kw3">Skeleton</span></a> skel <span class="sy0">=</span> ac.<span class="me1">getSkeleton</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
      <span class="kw1">final</span> SkeletonDebugger skeletonDebug <span class="sy0">=</span> <span class="kw1">new</span> SkeletonDebugger<span class="br0">(</span><span class="st0">"skeleton"</span>,
          skel<span class="br0">)</span><span class="sy0">;</span>
      <span class="kw1">final</span> Material mat <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>assetManager,
          <span class="st0">"Common/MatDefs/Misc/Unshaded.j3md"</span><span class="br0">)</span><span class="sy0">;</span>
      mat.<span class="me1">setColor</span><span class="br0">(</span><span class="st0">"Color"</span>, ColorRGBA.<span class="me1">Green</span><span class="br0">)</span><span class="sy0">;</span>
      mat.<span class="me1">getAdditionalRenderState</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">setDepthTest</span><span class="br0">(</span><span class="kw2">false</span><span class="br0">)</span><span class="sy0">;</span>
      skeletonDebug.<span class="me1">setMaterial</span><span class="br0">(</span>mat<span class="br0">)</span><span class="sy0">;</span>
      <span class="br0">(</span><span class="br0">(</span>Node<span class="br0">)</span> ac.<span class="me1">getSpatial</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span>.<span class="me1">attachChild</span><span class="br0">(</span>skeletonDebug<span class="br0">)</span><span class="sy0">;</span>
 
      <span class="co1">// create a channel and start the wobble animation</span>
      <span class="kw1">final</span> AnimChannel channel <span class="sy0">=</span> ac.<span class="me1">createChannel</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
      channel.<span class="me1">setAnim</span><span class="br0">(</span><span class="st0">"wobble"</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span> <span class="kw1">catch</span> <span class="br0">(</span><span class="kw1">final</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+exception"><span class="kw3">Exception</span></a> e<span class="br0">)</span> <span class="br0">{</span>
      e.<span class="me1">printStackTrace</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    <span class="co1">// add some lights</span>
    rootNode.<span class="me1">addLight</span><span class="br0">(</span><span class="kw1">new</span> AmbientLight<span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    rootNode.<span class="me1">addLight</span><span class="br0">(</span><span class="kw1">new</span> PointLight<span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
  <span class="br0">}</span>
 
  <span class="kw1">public</span> <span class="kw4">void</span> addLodControl<span class="br0">(</span><span class="kw1">final</span> Spatial parent<span class="br0">)</span> <span class="br0">{</span>
    <span class="kw1">if</span> <span class="br0">(</span>parent <span class="kw1">instanceof</span> Node<span class="br0">)</span> <span class="br0">{</span>
      <span class="kw1">for</span> <span class="br0">(</span><span class="kw1">final</span> Spatial s <span class="sy0">:</span> <span class="br0">(</span><span class="br0">(</span>Node<span class="br0">)</span> parent<span class="br0">)</span>.<span class="me1">getChildren</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
        addLodControl<span class="br0">(</span>s<span class="br0">)</span><span class="sy0">;</span>
      <span class="br0">}</span>
    <span class="br0">}</span> <span class="kw1">else</span> <span class="kw1">if</span> <span class="br0">(</span>parent <span class="kw1">instanceof</span> Geometry<span class="br0">)</span> <span class="br0">{</span>
      <span class="kw1">final</span> LodControl lc <span class="sy0">=</span> <span class="kw1">new</span> LodControl<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
      lc.<span class="me1">setDistTolerance</span><span class="br0">(</span>1f<span class="br0">)</span><span class="sy0">;</span>
      parent.<span class="me1">addControl</span><span class="br0">(</span>lc<span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
  <span class="br0">}</span>
 
  <span class="co3">/**
   * Method to find the animation control, because it is not on the models root
   * node.
   * 
   * @param parent
   *          The spatial to search.
   * @return The {@link AnimControl} or null if it does not exist.
   */</span>
  <span class="kw1">public</span> AnimControl findAnimControl<span class="br0">(</span><span class="kw1">final</span> Spatial parent<span class="br0">)</span> <span class="br0">{</span>
    <span class="kw1">final</span> AnimControl animControl <span class="sy0">=</span> parent.<span class="me1">getControl</span><span class="br0">(</span>AnimControl.<span class="kw1">class</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="kw1">if</span> <span class="br0">(</span>animControl <span class="sy0">!=</span> <span class="kw2">null</span><span class="br0">)</span> <span class="br0">{</span>
      <span class="kw1">return</span> animControl<span class="sy0">;</span>
    <span class="br0">}</span>
 
    <span class="kw1">if</span> <span class="br0">(</span>parent <span class="kw1">instanceof</span> Node<span class="br0">)</span> <span class="br0">{</span>
      <span class="kw1">for</span> <span class="br0">(</span><span class="kw1">final</span> Spatial s <span class="sy0">:</span> <span class="br0">(</span><span class="br0">(</span>Node<span class="br0">)</span> parent<span class="br0">)</span>.<span class="me1">getChildren</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
        <span class="kw1">final</span> AnimControl animControl2 <span class="sy0">=</span> findAnimControl<span class="br0">(</span>s<span class="br0">)</span><span class="sy0">;</span>
        <span class="kw1">if</span> <span class="br0">(</span>animControl2 <span class="sy0">!=</span> <span class="kw2">null</span><span class="br0">)</span> <span class="br0">{</span>
          <span class="kw1">return</span> animControl2<span class="sy0">;</span>
        <span class="br0">}</span>
      <span class="br0">}</span>
    <span class="br0">}</span>
 
    <span class="kw1">return</span> <span class="kw2">null</span><span class="sy0">;</span>
  <span class="br0">}</span>
 
  <span class="kw1">public</span> <span class="kw1">static</span> <span class="kw4">void</span> main<span class="br0">(</span><span class="kw1">final</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a><span class="br0">[</span><span class="br0">]</span> args<span class="br0">)</span> <span class="br0">{</span>
    <span class="kw1">new</span> TestOgreMaxImport<span class="br0">(</span><span class="br0">)</span>.<span class="me1">start</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
  <span class="br0">}</span>
<span class="br0">}</span></pre>

<p>
You will see your worms strange movements. Have fun!
</p>

<p>
<a href="/resources/jme3-external-3dsmax-12.png" class="media" title="jme3:external:3dsmax-12.png"><img src="/resources/jme3-external-3dsmax-12.png" class="media" alt="" /></a>
</p>

</div>
<!-- EDIT7 SECTION "Export and Import" [3396-6903] -->
<h1 class="sectionedit8" id="ds_max_biped_animation_to_jme3">3ds Max Biped Animation to JME3</h1>
<div class="level1">

<p>
You can also use the biped operator to animate models, but you have to consider a lot of things.
</p>

</div>
<!-- EDIT8 SECTION "3ds Max Biped Animation to JME3" [6904-7048] -->
<h3 class="sectionedit9" id="creating_a_character_in_3dsmax">Creating a character in 3dsMax</h3>
<div class="level3">

<p>
I will not tell you in detail how to model a character. There I many good tutorials on the web, I used <a href="http://majoh.deviantart.com/art/Mandi-s-3dsmax-Biped-Tutorial-26515784" class="urlextern" title="http://majoh.deviantart.com/art/Mandi-s-3dsmax-Biped-Tutorial-26515784" rel="nofollow">that one</a>.
</p>
<ul>
<li class="level1"><div class="li"> You may create a biped before you start modeling, so it is quite easier to fit the proportions of the biped.</div>
</li>
<li class="level1"><div class="li"> After creating a model and a biped I got something like that:</div>
</li>
</ul>

<p>
<a href="/resources/jme3-external-1.png" class="media" title="jme3:external:1.png"><img src="/resources/jme3-external-1.png" class="media" alt="" /></a>
</p>
<ul>
<li class="level1"><div class="li"> I added the “Meshmooth” modifier with 2 iterations and got this result:</div>
</li>
</ul>

<p>
<a href="/resources/jme3-external-3dsmax_biped_2.png" class="media" title="jme3:external:3dsmax_biped_2.png"><img src="/resources/jme3-external-3dsmax_biped_2.png" class="media" alt="" /></a>
</p>
<ul>
<li class="level1"><div class="li"> After smoothing your mesh you could correct vertices with the “Edit Mesh” modifier. Finally you add the “Physique” modifier.</div>
</li>
<li class="level1"><div class="li"> Now you can edit your envelopes to fit your model.</div>
</li>
</ul>

</div>
<!-- EDIT9 SECTION "Creating a character in 3dsMax" [7049-7788] -->
<h3 class="sectionedit10" id="creating_a_simple_walk_animation">Creating a simple walk animation</h3>
<div class="level3">
<ul>
<li class="level1"><div class="li"> Select the chest of your biped, choose “Motion” (1) tab &gt; “Foot Step Mode” (2) &gt; “Create Multiple Footsteps” (3)</div>
</li>
<li class="level1"><div class="li"> You need to select the “In Place Mode” (4), so the character moves in place without changing its location.</div>
</li>
</ul>

<p>
<a href="/resources/jme3-external-3dsmax_biped_3_1.png" class="media" title="jme3:external:3dsmax_biped_3_1.png"><img src="/resources/jme3-external-3dsmax_biped_3_1.png" class="media" alt="" /></a>
</p>
<ul>
<li class="level1"><div class="li"> You can now play a bit with the settings, I adjusted “Actual Stride Length” and “Actual Stride Height”. </div>
</li>
<li class="level1"><div class="li"> For the “Number of Footsteps” 6 will be sufficient because the animation is cycled later.</div>
</li>
<li class="level1"><div class="li"> <strong>Note:</strong> You can also create or edit footsteps by hand and move or rotate them.</div>
</li>
<li class="level1"><div class="li"> After all footsteps are created, hit the “Create Keys for Inactive Footsteps” button in the “Footstep Operations” panel</div>
</li>
<li class="level1"><div class="li"> You can now check your animation by pressing the “Play” button in the timeline.</div>
</li>
</ul>

</div>
<!-- EDIT10 SECTION "Creating a simple walk animation" [7789-8600] -->
<h3 class="sectionedit11" id="preparing_the_export_and_setting_up_ogremax">Preparing the export and setting up OgreMax</h3>
<div class="level3">
<ul>
<li class="level1"><div class="li"> The “OgreMax Scene Settings” should be the same as shown above.</div>
</li>
<li class="level1"><div class="li"> Because you want your animation to be looped, you've got to find two key frames where the legs are nearly in the same position. For my settings I've chosen the frames 48-78 for the walk animation.</div>
</li>
<li class="level1"><div class="li"> Select the character mesh and open the “OgreMax Scene Settings” dialog. </div>
</li>
<li class="level1"><div class="li"> Open the “Mesh Animations” tab and select type “Skeleton”, “Export Skeleton” : “Yes”</div>
</li>
<li class="level1"><div class="li"> Below “Mesh Animations” hit the “Add…” button</div>
</li>
</ul>

<p>
<a href="/resources/jme3-external-3dsmax_biped_4.png" class="media" title="jme3:external:3dsmax_biped_4.png"><img src="/resources/jme3-external-3dsmax_biped_4.png" class="media" alt="" /></a>
</p>
<ul>
<li class="level1"><div class="li"> Enter a name for the track, e.g. “walk”.</div>
</li>
<li class="level1"><div class="li"> Assure the track type is set to “Physique”.</div>
</li>
<li class="level1"><div class="li"> Set the start and end frames, for me it is 48-78.</div>
</li>
<li class="level1"><div class="li"> Close the dialog by pushing “Ok”.</div>
</li>
<li class="level1"><div class="li"> <strong>Note:</strong> It could be useful to create also a track “start_run”, that blends between the stand and walk animation. I would use frame 0-47 for that.</div>
</li>
<li class="level1"><div class="li"> Because you have a smooth model with a lot of polygons, it may be useful to create <a href="/jme3/advanced/mesh.html" class="wikilink1" title="jme3:advanced:mesh">levels of detail (LOD)</a>. When the camera is farther away, a low-poly mesh of your character will be rendered.</div>
</li>
</ul>

<p>
<a href="/resources/jme3-external-3dsmax_biped_5.png" class="media" title="jme3:external:3dsmax_biped_5.png"><img src="/resources/jme3-external-3dsmax_biped_5.png" class="media" alt="" /></a>
</p>
<ul>
<li class="level1"><div class="li"> Open the “Mesh LOD” tab in object settings.</div>
</li>
<li class="level1"><div class="li"> It will suffice to select the “Automatic” setting, but if your animation starts to look weird, you can create them by hand.</div>
</li>
<li class="level1"><div class="li"> I used 4 levels of LOD with a distance of 1. Don't worry about the distance setting, you can change it later in JME.</div>
</li>
<li class="level1"><div class="li"> For the level reduction, I used 20 percent, which produce good results. You may adjust all the settings depending on your needs.</div>
</li>
<li class="level1"><div class="li"> Close the dialoque by clicking “Ok”.</div>
</li>
</ul>

</div>
<!-- EDIT11 SECTION "Preparing the export and setting up OgreMax" [8601-10275] -->
<h3 class="sectionedit12" id="fixing_the_location">Fixing the location</h3>
<div class="level3">
<ul>
<li class="level1"><div class="li"> Before you export you need to do a little fix, because your model is not really located where you see it. JME will get into a lot of trouble, if you don't change that.</div>
</li>
<li class="level1"><div class="li"> Assure to save the max file. Sometimes OgreMax crashes the whole application during export. If you want to change the animation after export, you should reload this file because fixing the location changes something I can't really figure out.</div>
</li>
</ul>

<p>
<a href="/resources/jme3-external-3dsmax_biped_6.png" class="media" title="jme3:external:3dsmax_biped_6.png"><img src="/resources/jme3-external-3dsmax_biped_6.png" class="media" alt="" /></a>
</p>
<ul>
<li class="level1"><div class="li"> Right click the “Select and Move” tool in the upper toolbar. A dialog will pop up.</div>
</li>
<li class="level1"><div class="li"> Set the X and Y location to 0 and close the dialog.</div>
</li>
<li class="level1"><div class="li"> There is another way to achieve this. If you have scaled, moved or rotated your model, just open the “Hierarchy” tab and click “Transform” and “Scale” on the “Reset” panel.</div>
</li>
</ul>

</div>
<!-- EDIT12 SECTION "Fixing the location" [10276-11085] -->
<h3 class="sectionedit13" id="export_and_import1">Export and Import</h3>
<div class="level3">
<ul>
<li class="level1"><div class="li"> Now you can export your scene. Select only the mesh and use “Export selected objects”. You will not need the whole scene including the biped object, but the bones are created automatically during export.</div>
</li>
<li class="level1"><div class="li"> Create a JME test class for the scene import.</div>
</li>
</ul>

<p>
For that, I extended the first class:
</p>
<pre class="code java"><span class="kw1">import</span> <span class="co2">com.jme3.animation.AnimChannel</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.animation.AnimControl</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.animation.Skeleton</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.app.SimpleApplication</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.asset.plugins.FileLocator</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.light.AmbientLight</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.light.PointLight</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.material.Material</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.math.ColorRGBA</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.math.Vector3f</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.Geometry</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.Node</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.Spatial</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.control.LodControl</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.debug.SkeletonDebugger</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.shape.Box</span><span class="sy0">;</span>
 
<span class="co3">/**
 * This is a test class for loading a Ogre XML scene exported by OgreMax.
 * 
 * @author Stephan Dreyer
 * 
 */</span>
<span class="kw1">public</span> <span class="kw1">class</span> TestOgreMaxImport <span class="co2">extends</span> SimpleApplication <span class="br0">{</span>
 
  @Override
  <span class="kw1">public</span> <span class="kw4">void</span> simpleInitApp<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
    assetManager.<span class="me1">registerLocator</span><span class="br0">(</span><span class="st0">"Assets/model/ogre/test/"</span>, FileLocator.<span class="kw1">class</span><span class="br0">)</span><span class="sy0">;</span>
 
    <span class="co1">// create the geometry and attach it</span>
    <span class="kw1">final</span> Node model <span class="sy0">=</span> <span class="br0">(</span>Node<span class="br0">)</span> assetManager.<span class="me1">loadModel</span><span class="br0">(</span><span class="st0">"guy.scene"</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="co1">// resize it, because of the large 3dsmax scales</span>
    model.<span class="me1">setLocalScale</span><span class="br0">(</span>.02f<span class="br0">)</span><span class="sy0">;</span>
 
    <span class="co1">// attach to root node</span>
    rootNode.<span class="me1">attachChild</span><span class="br0">(</span>model<span class="br0">)</span><span class="sy0">;</span>
    addLodControl<span class="br0">(</span>model<span class="br0">)</span><span class="sy0">;</span>
 
    <span class="kw1">final</span> AnimControl ac <span class="sy0">=</span> findAnimControl<span class="br0">(</span>model<span class="br0">)</span><span class="sy0">;</span>
 
    <span class="kw1">try</span> <span class="br0">{</span>
      <span class="co1">// add a skeleton debugger to make bones visible</span>
      <span class="kw1">final</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+skeleton"><span class="kw3">Skeleton</span></a> skel <span class="sy0">=</span> ac.<span class="me1">getSkeleton</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
      <span class="kw1">final</span> SkeletonDebugger skeletonDebug <span class="sy0">=</span> <span class="kw1">new</span> SkeletonDebugger<span class="br0">(</span><span class="st0">"skeleton"</span>,
          skel<span class="br0">)</span><span class="sy0">;</span>
      <span class="kw1">final</span> Material mat <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>assetManager,
          <span class="st0">"Common/MatDefs/Misc/Unshaded.j3md"</span><span class="br0">)</span><span class="sy0">;</span>
      mat.<span class="me1">setColor</span><span class="br0">(</span><span class="st0">"Color"</span>, ColorRGBA.<span class="me1">Green</span><span class="br0">)</span><span class="sy0">;</span>
      mat.<span class="me1">getAdditionalRenderState</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">setDepthTest</span><span class="br0">(</span><span class="kw2">false</span><span class="br0">)</span><span class="sy0">;</span>
      skeletonDebug.<span class="me1">setMaterial</span><span class="br0">(</span>mat<span class="br0">)</span><span class="sy0">;</span>
      <span class="br0">(</span><span class="br0">(</span>Node<span class="br0">)</span> ac.<span class="me1">getSpatial</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span>.<span class="me1">attachChild</span><span class="br0">(</span>skeletonDebug<span class="br0">)</span><span class="sy0">;</span>
 
      <span class="co1">// create a channel and start the walk animation</span>
      <span class="kw1">final</span> AnimChannel channel <span class="sy0">=</span> ac.<span class="me1">createChannel</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
      channel.<span class="me1">setAnim</span><span class="br0">(</span><span class="st0">"walk"</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span> <span class="kw1">catch</span> <span class="br0">(</span><span class="kw1">final</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+exception"><span class="kw3">Exception</span></a> e<span class="br0">)</span> <span class="br0">{</span>
      e.<span class="me1">printStackTrace</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    flyCam.<span class="me1">setMoveSpeed</span><span class="br0">(</span>40f<span class="br0">)</span><span class="sy0">;</span>
    cam.<span class="me1">setLocation</span><span class="br0">(</span><span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">15</span>, <span class="nu0">10</span>, <span class="nu0">15</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    cam.<span class="me1">lookAt</span><span class="br0">(</span>Vector3f.<span class="me1">ZERO</span>, Vector3f.<span class="me1">UNIT_Y</span><span class="br0">)</span><span class="sy0">;</span>
    cam.<span class="me1">setFrustumNear</span><span class="br0">(</span>1f<span class="br0">)</span><span class="sy0">;</span>
 
    <span class="co1">// add some lights</span>
    rootNode.<span class="me1">addLight</span><span class="br0">(</span><span class="kw1">new</span> AmbientLight<span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
 
    <span class="kw1">final</span> PointLight pl <span class="sy0">=</span> <span class="kw1">new</span> PointLight<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    pl.<span class="me1">setPosition</span><span class="br0">(</span><span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="sy0">-</span>3f, 3f, 1f<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    rootNode.<span class="me1">addLight</span><span class="br0">(</span>pl<span class="br0">)</span><span class="sy0">;</span>
 
    <span class="co1">// add a box as floor</span>
    <span class="kw1">final</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a> b <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a><span class="br0">(</span>100f, 0.1f, 100f<span class="br0">)</span><span class="sy0">;</span>
    <span class="kw1">final</span> Geometry geo <span class="sy0">=</span> <span class="kw1">new</span> Geometry<span class="br0">(</span><span class="st0">"floor"</span>, b<span class="br0">)</span><span class="sy0">;</span>
 
    <span class="kw1">final</span> Material mat <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>assetManager,
        <span class="st0">"Common/MatDefs/Misc/Unshaded.j3md"</span><span class="br0">)</span><span class="sy0">;</span>
    mat.<span class="me1">setColor</span><span class="br0">(</span><span class="st0">"Color"</span>, ColorRGBA.<span class="me1">LightGray</span><span class="br0">)</span><span class="sy0">;</span>
    geo.<span class="me1">setMaterial</span><span class="br0">(</span>mat<span class="br0">)</span><span class="sy0">;</span>
 
    rootNode.<span class="me1">attachChild</span><span class="br0">(</span>geo<span class="br0">)</span><span class="sy0">;</span>
  <span class="br0">}</span>
 
  <span class="co3">/**
   * Method to traverse through the scene graph and add a {@link LodControl} to
   * the mesh.
   * 
   * @param parent
   *          The Node to add the control to.
   */</span>
  <span class="kw1">public</span> <span class="kw4">void</span> addLodControl<span class="br0">(</span><span class="kw1">final</span> Spatial parent<span class="br0">)</span> <span class="br0">{</span>
    <span class="kw1">if</span> <span class="br0">(</span>parent <span class="kw1">instanceof</span> Node<span class="br0">)</span> <span class="br0">{</span>
      <span class="kw1">for</span> <span class="br0">(</span><span class="kw1">final</span> Spatial s <span class="sy0">:</span> <span class="br0">(</span><span class="br0">(</span>Node<span class="br0">)</span> parent<span class="br0">)</span>.<span class="me1">getChildren</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
        addLodControl<span class="br0">(</span>s<span class="br0">)</span><span class="sy0">;</span>
      <span class="br0">}</span>
    <span class="br0">}</span> <span class="kw1">else</span> <span class="kw1">if</span> <span class="br0">(</span>parent <span class="kw1">instanceof</span> Geometry<span class="br0">)</span> <span class="br0">{</span>
      <span class="kw1">final</span> LodControl lc <span class="sy0">=</span> <span class="kw1">new</span> LodControl<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
 
      <span class="co1">// the distance for LOD changes is set here, you may adjust this</span>
      lc.<span class="me1">setDistTolerance</span><span class="br0">(</span>1f<span class="br0">)</span><span class="sy0">;</span>
      parent.<span class="me1">addControl</span><span class="br0">(</span>lc<span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
  <span class="br0">}</span>
 
  <span class="co3">/**
   * Method to find the animation control, because it is not on the models root
   * node.
   * 
   * @param parent
   *          The spatial to search.
   * @return The {@link AnimControl} or null if it does not exist.
   */</span>
  <span class="kw1">public</span> AnimControl findAnimControl<span class="br0">(</span><span class="kw1">final</span> Spatial parent<span class="br0">)</span> <span class="br0">{</span>
    <span class="kw1">final</span> AnimControl animControl <span class="sy0">=</span> parent.<span class="me1">getControl</span><span class="br0">(</span>AnimControl.<span class="kw1">class</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="kw1">if</span> <span class="br0">(</span>animControl <span class="sy0">!=</span> <span class="kw2">null</span><span class="br0">)</span> <span class="br0">{</span>
      <span class="kw1">return</span> animControl<span class="sy0">;</span>
    <span class="br0">}</span>
 
    <span class="kw1">if</span> <span class="br0">(</span>parent <span class="kw1">instanceof</span> Node<span class="br0">)</span> <span class="br0">{</span>
      <span class="kw1">for</span> <span class="br0">(</span><span class="kw1">final</span> Spatial s <span class="sy0">:</span> <span class="br0">(</span><span class="br0">(</span>Node<span class="br0">)</span> parent<span class="br0">)</span>.<span class="me1">getChildren</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
        <span class="kw1">final</span> AnimControl animControl2 <span class="sy0">=</span> findAnimControl<span class="br0">(</span>s<span class="br0">)</span><span class="sy0">;</span>
        <span class="kw1">if</span> <span class="br0">(</span>animControl2 <span class="sy0">!=</span> <span class="kw2">null</span><span class="br0">)</span> <span class="br0">{</span>
          <span class="kw1">return</span> animControl2<span class="sy0">;</span>
        <span class="br0">}</span>
      <span class="br0">}</span>
    <span class="br0">}</span>
 
    <span class="kw1">return</span> <span class="kw2">null</span><span class="sy0">;</span>
  <span class="br0">}</span>
 
  <span class="kw1">public</span> <span class="kw1">static</span> <span class="kw4">void</span> main<span class="br0">(</span><span class="kw1">final</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a><span class="br0">[</span><span class="br0">]</span> args<span class="br0">)</span> <span class="br0">{</span>
    <span class="kw1">new</span> TestOgreMaxImport<span class="br0">(</span><span class="br0">)</span>.<span class="me1">start</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
  <span class="br0">}</span>
<span class="br0">}</span></pre>

<p>
After starting the class, you can see a nice smooth walk animation (if it's not smooth, you need to adjust your track frames):
</p>

<p>
<a href="/resources/jme3-external-3dsmax_biped_7.png" class="media" title="jme3:external:3dsmax_biped_7.png"><img src="/resources/jme3-external-3dsmax_biped_7.png" class="media" alt="" /></a>
</p>

<p>
As you can see, the LOD is working:
</p>

<p>
<a href="/resources/jme3-external-3dsmax_biped_8.png" class="media" title="jme3:external:3dsmax_biped_8.png"><img src="/resources/jme3-external-3dsmax_biped_8.png" class="media" alt="" /></a>
</p>

</div>
<!-- EDIT13 SECTION "Export and Import" [11086-] -->
