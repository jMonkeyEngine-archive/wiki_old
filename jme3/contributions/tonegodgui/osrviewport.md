---
title: OSRViewPort
---
<h3 class="sectionedit1" id="osrviewport">OSRViewPort</h3>
<div class="level3">

<p>
The OSRViewPort allows you to create a movable, resizable ViewPort with the ability to control the camera's rotation and zoom features via mouse input.<br />

<br />

To initialize the OSRViewPort you can call one of the 3 standard constructors as shown in the <a href="http://jmonkeyengine.org/wiki/doku.php/jme3:contributions:tonegodgui:quickstart" class="urlextern" title="http://jmonkeyengine.org/wiki/doku.php/jme3:contributions:tonegodgui:quickstart" rel="nofollow">Quick Start Guide</a>.
</p>

<p>
<strong>Constructor 1:</strong><br />

</p>
<pre class="code java"><span class="co3">/** Parameters:
  * Screen screen,
  * String UID,
  * Vector2f position
  */</span>
 
OSRViewPort vp <span class="sy0">=</span> <span class="kw1">new</span> OSRViewPort<span class="br0">(</span>screen, “vp”, <span class="kw1">new</span> Vector2f<span class="br0">(</span><span class="nu0">15</span>, <span class="nu0">15</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
<strong>Constructor 2:</strong><br />

</p>
<pre class="code java"><span class="co3">/** Additional Parameter:
  * Vector2f dimensions  */</span>
 
OSRViewPort vp <span class="sy0">=</span> <span class="kw1">new</span> OSRViewPort<span class="br0">(</span>screen, “vp”, <span class="kw1">new</span> Vector2f<span class="br0">(</span><span class="nu0">15</span>, <span class="nu0">15</span><span class="br0">)</span>,
    <span class="kw1">new</span> Vector2f<span class="br0">(</span><span class="nu0">150</span>, <span class="nu0">150</span><span class="br0">)</span>
<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
<strong>Constructor 3:</strong><br />

</p>
<pre class="code java"><span class="co3">/** Additional Parameters:
  * Vector4f resizeBorders,
  * String defaultImg
  */</span>
 
OSRViewPort vp <span class="sy0">=</span> <span class="kw1">new</span> OSRViewPort<span class="br0">(</span>screen, “vp”, <span class="kw1">new</span> Vector2f<span class="br0">(</span><span class="nu0">15</span>, <span class="nu0">15</span><span class="br0">)</span>, <span class="kw1">new</span> Vector2f<span class="br0">(</span><span class="nu0">150</span>, <span class="nu0">150</span><span class="br0">)</span>,
    <span class="kw1">new</span> Vector4f<span class="br0">(</span><span class="nu0">0</span>,<span class="nu0">0</span>,<span class="nu0">0</span>,<span class="nu0">0</span><span class="br0">)</span>,
    <span class="st0">"imagePathToOverlayImage"</span>
<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
Once initialized, you will want to active the OSRBridge for off-screen rendering of your new scene:
</p>
<pre class="code java">vp.<span class="me1">setOSRBridge</span><span class="br0">(</span>Node newScene, <span class="kw4">int</span> renderWidth, <span class="kw4">int</span> renderHeight<span class="br0">)</span><span class="sy0">;</span></pre>

</div>

<h4 id="the_viewport_s_camera_control_methods">The ViewPort’s Camera control methods:</h4>
<div class="level4">
<pre class="code java">vp.<span class="me1">setUseCameraControlRotate</span><span class="br0">(</span><span class="kw4">boolean</span> rotateEnabled<span class="br0">)</span><span class="sy0">;</span> <span class="co1">// enable/disable rotation control</span>
vp.<span class="me1">setUseCameraControlZoom</span><span class="br0">(</span><span class="kw4">boolean</span> zoomEnabled<span class="br0">)</span><span class="sy0">;</span> <span class="co1">// enable/disable zoom control</span>
 
vp.<span class="me1">setCameraDistance</span><span class="br0">(</span><span class="kw4">float</span> distance<span class="br0">)</span><span class="sy0">;</span>
vp.<span class="me1">setCameraHorizonalRotation</span><span class="br0">(</span><span class="kw4">float</span> angleInRads<span class="br0">)</span><span class="sy0">;</span>
vp.<span class="me1">setCameraVerticalRotation</span><span class="br0">(</span><span class="kw4">float</span> angleInRads<span class="br0">)</span><span class="sy0">;</span>
vp.<span class="me1">setCameraMinDistance</span><span class="br0">(</span><span class="kw4">float</span> distance<span class="br0">)</span><span class="sy0">;</span>
vp.<span class="me1">setCameraMaxDistance</span><span class="br0">(</span><span class="kw4">float</span> distance<span class="br0">)</span><span class="sy0">;</span>
vp.<span class="me1">setCameraMinVerticalRotation</span><span class="br0">(</span><span class="kw4">float</span> angleInRads<span class="br0">)</span><span class="sy0">;</span>
vp.<span class="me1">setCameraMaxVerticalRotation</span><span class="br0">(</span><span class="kw4">float</span> angleInRads<span class="br0">)</span><span class="sy0">;</span></pre>

</div>

<h4 id="other_methods">Other methods:</h4>
<div class="level4">
<pre class="code java">vp.<span class="me1">setBackgroundColor</span><span class="br0">(</span>ColorRGBA color<span class="br0">)</span><span class="sy0">;</span> <span class="co1">// ViewPort is transparent by default</span></pre>

</div>
