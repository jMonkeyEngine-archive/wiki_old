---
title: Multiple Camera Views
---
<h1 class="sectionedit1" id="multiple_camera_views">Multiple Camera Views</h1>
<div class="level1">

<p>
You can split the screen and look into the 3D scene from different camera angles at the same time. E.g. you can have two rootnodes with different scene graphs, and two viewPorts, each of which can only see its own subset of the scene with its own subset of port-processing filters, so you get two very different views of the scene.
</p>

<p>
The packages used in this example are <code>com.jme3.renderer.Camera</code> and <code>com.jme3.renderer.ViewPort</code>. You can get the full sample code here: <a href="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/renderer/TestMultiViews.java" class="urlextern" title="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/renderer/TestMultiViews.java" rel="nofollow">TestMultiViews.java</a>
</p>

</div>
<!-- EDIT1 SECTION "Multiple Camera Views" [1-650] -->
<h2 class="sectionedit2" id="how_to_resize_and_position_viewports">How to resize and Position ViewPorts</h2>
<div class="level2">

<p>
The default viewPort is as big as the window. If you have several, they must be of different sizes, either overlapping or adjacent to one another. How do you tell jME which of the ViewPorts should appear where on the screen, and how big they should be?
</p>

<p>
Imagine the window as a 1.0f x 1.0f rectangle. The default cam's viewPort is set to 
</p>
<pre class="code java">cam.<span class="me1">setViewPort</span><span class="br0">(</span>0f, 1f, 0f, 1f<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
This setting makes the ViewPort take up the whole rectangle. 
</p>

<p>
The four values are read in the following order: 
</p>
<pre class="code java">cam.<span class="me1">setViewPort</span><span class="br0">(</span>x1,x2 , y1,y2<span class="br0">)</span><span class="sy0">;</span></pre>
<ul>
<li class="level1"><div class="li"> <strong>X-axis</strong> from left to right</div>
</li>
<li class="level1"><div class="li"> <strong>Y-axis</strong> upwards from bottom to top</div>
</li>
</ul>

<p>
Here are a few examples:
</p>
<pre class="code java">cam1.<span class="me1">setViewPort</span><span class="br0">(</span> 0.0f , 1.0f   ,   0.0f , 1.0f <span class="br0">)</span><span class="sy0">;</span>
cam2.<span class="me1">setViewPort</span><span class="br0">(</span> 0.5f , 1.0f   ,   0.0f , 0.5f <span class="br0">)</span><span class="sy0">;</span></pre>

<p>
These viewport parameters are, (in this order) the left-right extend, and the bottom-top extend of a views's rectangle on the screen. 
</p>
<pre class="code">0.0 , 1.0       1.0 , 1.0
       +-----+-----+
       |cam1       |
       |           |
       |     +-----+
       |     |     |
       |     |cam2 |
       +-----+-----+
0.0 , 0.0       1.0 , 0.0</pre>

<p>
Example: Cam2's rectangle is in the bottom right: It extends from mid (x1=0.5f) bottom (y1=0.0f), to right (x2=1.0f) mid (y2=0.5f)
</p>

<p>
</p><p></p><div class="noteimportant">If you scale the views in a way so that the aspect ratio of a ViewPort is different than the window's aspect ratio, then the ViewPort appears distorted. In these cases, you must recreate (not clone) the ViewPort's cam object with the right aspect ratio. For example: <code>Camera cam5 = new Camera(100,100);</code> 
</div>


</div>
<!-- EDIT2 SECTION "How to resize and Position ViewPorts" [651-2294] -->
<h2 class="sectionedit3" id="four-time_split_screen">Four-Time Split Screen</h2>
<div class="level2">

<p>
In this example, you create four views (2×2) with the same aspect ratio as the window, but each is only half the width and height. 
</p>

</div>
<!-- EDIT3 SECTION "Four-Time Split Screen" [2295-2463] -->
<h3 class="sectionedit4" id="set_up_the_first_view">Set up the First View</h3>
<div class="level3">

<p>
You use the preconfigured Camera <code>cam</code> and <code>viewPort</code> from <code>SimpleApplication</code> for the first view. It's in the bottom right.
</p>
<pre class="code java">cam.<span class="me1">setViewPort</span><span class="br0">(</span>.5f, 1f, 0f, 0.5f<span class="br0">)</span><span class="sy0">;</span> <span class="co1">// Resize the viewPort to half its size, bottom right.</span></pre>

<p>
Optionally, place the main camera in the scene and rotate it in its start position. 
</p>
<pre class="code java">cam.<span class="me1">setLocation</span><span class="br0">(</span><span class="kw1">new</span> Vector3f<span class="br0">(</span>3.32f, 4.48f, 4.28f<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
cam.<span class="me1">setRotation</span><span class="br0">(</span><span class="kw1">new</span> Quaternion <span class="br0">(</span><span class="sy0">-</span>0.07f, 0.92f, <span class="sy0">-</span>0.25f, <span class="sy0">-</span>0.27f<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span></pre>

</div>
<!-- EDIT4 SECTION "Set up the First View" [2464-2960] -->
<h3 class="sectionedit5" id="set_up_three_more_views">Set Up Three More Views</h3>
<div class="level3">

<p>
Here is the outline for how you create the three other cams and viewPorts (<a href="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/renderer/TestMultiViews.java" class="urlextern" title="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/renderer/TestMultiViews.java" rel="nofollow">Full code sample is here</a>.) In the code snippet, <code>cam_n</code> stand for <code>cam_2</code> - <code>cam_4</code>, respectively, same for <code>view_n</code>.
</p>
<ol>
<li class="level1"><div class="li"> Clone the first cam to reuse its settings</div>
</li>
<li class="level1"><div class="li"> Resize and position the cam's viewPort with setViewPort().</div>
</li>
<li class="level1"><div class="li"> (Optionally) Move the cameras in the scene and rotate them so they face what you want to see.</div>
</li>
<li class="level1"><div class="li"> Create a ViewPort for each camera</div>
</li>
<li class="level1"><div class="li"> Reset the camera's enabled statuses</div>
</li>
<li class="level1"><div class="li"> Attach the Node to be displayed to this ViewPort. <br />
The camera doesn't have to look at the rootNode, but that is the most common use case.</div>
</li>
</ol>

<p>
Here is the abstract code sample for camera <code>n</code>:
</p>
<pre class="code java">Camera cam_n    <span class="sy0">=</span> cam.<span class="me1">clone</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
cam_n.<span class="me1">setViewPort</span><span class="br0">(</span>...<span class="br0">)</span><span class="sy0">;</span> <span class="co1">// resize the viewPort</span>
cam_n.<span class="me1">setLocation</span><span class="br0">(</span><span class="kw1">new</span> Vector3f<span class="br0">(</span>...<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
cam_n.<span class="me1">setRotation</span><span class="br0">(</span><span class="kw1">new</span> Quaternion<span class="br0">(</span>...<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
 
ViewPort view_n <span class="sy0">=</span> renderManager.<span class="me1">createMainView</span><span class="br0">(</span><span class="st0">"View of camera #n"</span>, cam_n<span class="br0">)</span><span class="sy0">;</span>
view_n.<span class="me1">setClearEnabled</span><span class="br0">(</span><span class="kw2">true</span><span class="br0">)</span><span class="sy0">;</span>
view_n.<span class="me1">attachScene</span><span class="br0">(</span>rootNode<span class="br0">)</span><span class="sy0">;</span>
view_n.<span class="me1">setBackgroundColor</span><span class="br0">(</span>ColorRGBA.<span class="me1">Black</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
To visualize what you do, use the following drawing of the viewport positions:
</p>
<pre class="code">0.0 , 1.0       1.0 , 1.0
       +-----+-----+
       |     |     |
       |cam3 |cam4 |
       +-----------+
       |     |     |
       |cam2 |cam1 |
       +-----+-----+
0.0 , 0.0       1.0 , 0.0</pre>

<p>
This are the lines of code that set the four cameras to create a four-times split screen.
</p>
<pre class="code java">cam1.<span class="me1">setViewPort</span><span class="br0">(</span> 0.5f , 1.0f  ,  0.0f , 0.5f<span class="br0">)</span><span class="sy0">;</span>
...
<span class="me1">cam2</span>.<span class="me1">setViewPort</span><span class="br0">(</span> 0.0f , 0.5f  ,  0.0f , 0.5f<span class="br0">)</span><span class="sy0">;</span>
...
<span class="me1">cam3</span>.<span class="me1">setViewPort</span><span class="br0">(</span> 0.0f , 0.5f  ,  0.5f , 1.0f<span class="br0">)</span><span class="sy0">;</span>
...
<span class="me1">cam4</span>.<span class="me1">setViewPort</span><span class="br0">(</span> 0.5f , 1.0f  ,  0.5f , 1.0f<span class="br0">)</span><span class="sy0">;</span></pre>

</div>
<!-- EDIT5 SECTION "Set Up Three More Views" [2961-4771] -->
<h2 class="sectionedit6" id="picture_in_picture">Picture in Picture</h2>
<div class="level2">

<p>
The following code snippet sets up two views, one covers the whole screen, and the second is a small view in the top center.
</p>
<pre class="code">       +-----+-----+
       |   |cam|   |
       |   | 2 |   |
       +   +---+   +
       |           |
       |    cam    |
       +-----+-----+</pre>
<pre class="code java"><span class="co1">// Setup first full-window view</span>
cam.<span class="me1">setViewPort</span><span class="br0">(</span>0f, 1f, 0f, 1f<span class="br0">)</span><span class="sy0">;</span>
cam.<span class="me1">setLocation</span><span class="br0">(</span><span class="kw1">new</span> Vector3f<span class="br0">(</span>3.32f, 4.48f, 4.28f<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
cam.<span class="me1">setRotation</span><span class="br0">(</span><span class="kw1">new</span> Quaternion<span class="br0">(</span><span class="sy0">-</span>0.07f, 0.92f, <span class="sy0">-</span>0.25f, <span class="sy0">-</span>0.27f<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
 
<span class="co1">// Setup second, smaller PiP view</span>
Camera cam2 <span class="sy0">=</span> cam.<span class="me1">clone</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
cam2.<span class="me1">setViewPort</span><span class="br0">(</span>.4f, .6f, 0.8f, 1f<span class="br0">)</span><span class="sy0">;</span>
cam2.<span class="me1">setLocation</span><span class="br0">(</span><span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="sy0">-</span>0.10f, 1.57f, 4.81f<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
cam2.<span class="me1">setRotation</span><span class="br0">(</span><span class="kw1">new</span> Quaternion<span class="br0">(</span>0.00f, 0.99f, <span class="sy0">-</span>0.04f, 0.02f<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
ViewPort viewPort2 <span class="sy0">=</span> renderManager.<span class="me1">createMainView</span><span class="br0">(</span><span class="st0">"PiP"</span>, cam2<span class="br0">)</span><span class="sy0">;</span>
viewPort2.<span class="me1">setClearFlags</span><span class="br0">(</span><span class="kw2">true</span>, <span class="kw2">true</span>, <span class="kw2">true</span><span class="br0">)</span><span class="sy0">;</span>
viewPort2.<span class="me1">attachScene</span><span class="br0">(</span>rootNode<span class="br0">)</span><span class="sy0">;</span></pre>

</div>
<!-- EDIT6 SECTION "Picture in Picture" [4772-5652] -->
<h2 class="sectionedit7" id="viewport_settings">ViewPort Settings</h2>
<div class="level2">

<p>
You can customize the camera and the viewPort of each view individually. For example, each view can have a different background color:
</p>
<pre class="code java">viewPort.<span class="me1">setBackgroundColor</span><span class="br0">(</span>ColorRGBA.<span class="me1">Blue</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
You have full control to determine which Nodes the camera can see! It can see the full rootNode…
</p>
<pre class="code java">viewPort1.<span class="me1">attachScene</span><span class="br0">(</span>rootNode<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
… or you can give each camera a special node whose content it can see:
</p>
<pre class="code java">viewPort2.<span class="me1">attachScene</span><span class="br0">(</span>spookyGhostDetectorNode<span class="br0">)</span><span class="sy0">;</span></pre>
<div class="tags"><span>
	<a href="/tag/camera.html" class="wikilink1" title="tag:camera" rel="tag">camera</a>,
	<a href="/tag/documentation.html" class="wikilink1" title="tag:documentation" rel="tag">documentation</a>
</span></div>

</div>
<!-- EDIT7 SECTION "ViewPort Settings" [5653-] -->
