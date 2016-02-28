---
title: User Example: Third Person Camera
---
<h1 class="sectionedit1" id="user_examplethird_person_camera">User Example: Third Person Camera</h1>
<div class="level1">

<p>
<a href="/resources/jme3-user_examples-thirdpersoncamera-3p.png" class="media" title="jme3:user_examples:thirdpersoncamera:3p.png"><img src="/resources/jme3-user_examples-thirdpersoncamera-3p.png" class="media" alt="" /></a>
</p>

<p>
(by Berzee) (see a video demonstration here: <a href="https://www.youtube.com/watch?v=phu52hmIoYU" class="urlextern" title="https://www.youtube.com/watch?v=phu52hmIoYU" rel="nofollow">https://www.youtube.com/watch?v=phu52hmIoYU</a>)
</p>

<p>
Here is a small example of a self-contained Third Person Character (with camera). It uses the familiar Green Ninja model to demonstrate the following controls and animations:
</p>
<ul>
<li class="level1"><div class="li"> “WASD” movement</div>
</li>
<li class="level1"><div class="li"> “SPACE” to jump</div>
</li>
<li class="level1"><div class="li"> Horizontal mouse movement to turn left and right</div>
</li>
<li class="level1"><div class="li"> Vertical mouselook (camera pivots around character)</div>
</li>
<li class="level1"><div class="li"> Left Mouse Button to attack</div>
</li>
</ul>

<p>
To try this example for yourself, you can copy the classes from this page. Then you will be able to create a Third-Person Character in your apps like so:
</p>
<pre class="code java">player <span class="sy0">=</span> <span class="kw1">new</span> ThirdPersonPlayerNode<span class="br0">(</span>playerModel, inputManager, cam<span class="br0">)</span><span class="sy0">;</span>
rootNode.<span class="me1">attachChild</span><span class="br0">(</span>player<span class="br0">)</span><span class="sy0">;</span>
bulletAppState.<span class="me1">getPhysicsSpace</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">add</span><span class="br0">(</span>player<span class="br0">)</span><span class="sy0">;</span>
 
<span class="co1">//make sure to call "player.update()" in the app's update method, too</span></pre>

</div>
<!-- EDIT1 SECTION "User Example: Third Person Camera" [1-944] -->
<h2 class="sectionedit2" id="how_the_mouselook_works">How the mouselook works</h2>
<div class="level2">

<p>
Most of the code in the example files should be relatively self-explanatory, but mouselook deserves a lovely pictograph of its own. It's easy to make <a href="/jme3/advanced/making_the_camera_follow_a_character.html" class="wikilink1" title="jme3:advanced:making_the_camera_follow_a_character">a camera that follows an object and always looks at the back of it</a>, and thus it's easy to account for horizontal mouse movement by simple rotating the entire Player character left or right.
</p>

<p>
But what if we want to be able to move the camera angle up or down, while the Player stays firmly upright? We can accomplish this with minimal Horrible Maths by adding an invisible “pivot” node to the Player, and instructing the camera to follow that “pivot” instead. Then we can independently rotate the *pivot* instead of the Player, and do things like this:
</p>

<p>
<a href="/resources/jme3-user_examples-thirdpersoncamera-pivot2.png" class="media" title="jme3:user_examples:thirdpersoncamera:pivot2.png"><img src="/resources/jme3-user_examples-thirdpersoncamera-pivot2.png" class="media" alt="" /></a>
</p>

<p>
Now you know the mystical secrets, and are ready to see the code itself.
</p>

</div>
<!-- EDIT2 SECTION "How the mouselook works" [945-1868] -->
<h2 class="sectionedit3" id="source_code">Source Code</h2>
<div class="level2">

</div>
<!-- EDIT3 SECTION "Source Code" [1869-1893] -->
<h3 class="sectionedit4" id="thirdpersonplayernodejava">ThirdPersonPlayerNode.java</h3>
<div class="level3">

<p>
ThirdPersonPlayerNode.java contains the bulk of the logic for keyboard, mouse, physics, and animation. Most of this is lifted straight from the Tutorials for Beginners and can safely be ignored. However, pay particular attention to the “onAnalog()” method – that's where all of the mouse movement is processed to turn the player left and right, and the camera up and down.
</p>
<pre class="code java"><span class="kw1">package</span> <span class="co2">mygame</span><span class="sy0">;</span>
 
<span class="kw1">import</span> <span class="co2">com.jme3.animation.AnimChannel</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.animation.AnimControl</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.animation.AnimEventListener</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.animation.LoopMode</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.bullet.collision.shapes.CapsuleCollisionShape</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.bullet.control.CharacterControl</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.input.InputManager</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.input.KeyInput</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.input.MouseInput</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.input.controls.ActionListener</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.input.controls.AnalogListener</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.input.controls.KeyTrigger</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.input.controls.MouseAxisTrigger</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.input.controls.MouseButtonTrigger</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.math.FastMath</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.math.Quaternion</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.math.Vector3f</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.renderer.Camera</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.Node</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.Spatial</span><span class="sy0">;</span>
 
<span class="co3">/**
 *
 * @author Berzee
 */</span>
<span class="kw1">public</span> <span class="kw1">class</span> ThirdPersonPlayerNode <span class="kw1">extends</span> Node <span class="kw1">implements</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+actionlistener"><span class="kw3">ActionListener</span></a>, AnalogListener, AnimEventListener
<span class="br0">{</span>
    <span class="co1">//ThirdPersonCameraNode automatically sets itself up to follow a target</span>
    <span class="co1">//object. Check the "onAnalog" function here to see how we do mouselook.</span>
    <span class="kw1">private</span> ThirdPersonCamera camera<span class="sy0">;</span>
    <span class="kw1">private</span> Camera cam<span class="sy0">;</span>
 
    <span class="kw1">private</span> Spatial model<span class="sy0">;</span>
    <span class="kw1">private</span> CharacterControl characterControl<span class="sy0">;</span>
    <span class="kw1">private</span> AnimChannel animChannel<span class="sy0">;</span>
    <span class="kw1">private</span> AnimControl animControl<span class="sy0">;</span>
    <span class="kw1">private</span> InputManager inputManager<span class="sy0">;</span>
    <span class="kw1">private</span> Vector3f walkDirection <span class="sy0">=</span> <span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
 
    <span class="kw1">private</span> <span class="kw4">boolean</span> left <span class="sy0">=</span> <span class="kw2">false</span><span class="sy0">;</span>
    <span class="kw1">private</span> <span class="kw4">boolean</span> right <span class="sy0">=</span> <span class="kw2">false</span><span class="sy0">;</span>
    <span class="kw1">private</span> <span class="kw4">boolean</span> up <span class="sy0">=</span> <span class="kw2">false</span><span class="sy0">;</span>
    <span class="kw1">private</span> <span class="kw4">boolean</span> down <span class="sy0">=</span> <span class="kw2">false</span><span class="sy0">;</span>
    <span class="kw1">private</span> <span class="kw4">boolean</span> attack<span class="sy0">;</span>
    <span class="kw1">private</span> <span class="kw4">boolean</span> attacking<span class="sy0">;</span>
 
    <span class="co1">//These can all be changed according to your whims.</span>
    <span class="kw1">private</span> <span class="kw4">float</span> walkSpeed <span class="sy0">=</span> .15f<span class="sy0">;</span>
    <span class="kw1">private</span> <span class="kw4">float</span> mouselookSpeed <span class="sy0">=</span> FastMath.<span class="me1">PI</span><span class="sy0">;</span>
    <span class="kw1">private</span> <span class="kw4">float</span> jumpSpeed <span class="sy0">=</span> <span class="nu0">15</span><span class="sy0">;</span>
    <span class="kw1">private</span> <span class="kw4">float</span> fallSpeed <span class="sy0">=</span> <span class="nu0">20</span><span class="sy0">;</span>
    <span class="kw1">private</span> <span class="kw4">float</span> gravity <span class="sy0">=</span> <span class="nu0">25</span><span class="sy0">;</span>
    <span class="kw1">private</span> <span class="kw4">float</span> stepSize <span class="sy0">=</span> .05f<span class="sy0">;</span>
 
    <span class="co1">//Animation names. These are currently set up for the Ninja.mesh.xml from</span>
    <span class="co1">//jme3-test-data.jar (to add that jar to your project, right-click on</span>
    <span class="co1">//Libraries in the SDK project explorer, click "Add Library" and choose</span>
    <span class="co1">//jme3-test-data.jar from the menu).</span>
    <span class="co1">//</span>
    <span class="co1">//Alternatively, use any model you like and change these animation names</span>
    <span class="co1">//as needed.</span>
    <span class="kw1">private</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> idleAnim <span class="sy0">=</span> <span class="st0">"Idle1"</span><span class="sy0">;</span>
    <span class="kw1">private</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> walkAnim <span class="sy0">=</span> <span class="st0">"Walk"</span><span class="sy0">;</span>
    <span class="kw1">private</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> attackAnim <span class="sy0">=</span> <span class="st0">"Attack3"</span><span class="sy0">;</span>
    <span class="kw1">private</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> jumpAnim <span class="sy0">=</span> <span class="st0">"Climb"</span><span class="sy0">;</span> <span class="co1">//hilarious</span>
 
    <span class="kw1">public</span> ThirdPersonPlayerNode<span class="br0">(</span>Spatial model, InputManager inputManager, Camera cam<span class="br0">)</span>
    <span class="br0">{</span>
	<span class="kw1">super</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
	<span class="kw1">this</span>.<span class="me1">cam</span> <span class="sy0">=</span> cam<span class="sy0">;</span>
	camera <span class="sy0">=</span> <span class="kw1">new</span> ThirdPersonCamera<span class="br0">(</span><span class="st0">"CamNode"</span>, cam, <span class="kw1">this</span><span class="br0">)</span><span class="sy0">;</span>
 
        <span class="kw1">this</span>.<span class="me1">model</span> <span class="sy0">=</span> model<span class="sy0">;</span>
	<span class="kw1">this</span>.<span class="me1">model</span>.<span class="me1">scale</span><span class="br0">(</span>.01f<span class="br0">)</span><span class="sy0">;</span> <span class="co1">//Ninja.mesh.xml-specific scale stuff</span>
	<span class="kw1">this</span>.<span class="me1">model</span>.<span class="me1">setLocalTranslation</span><span class="br0">(</span>0f, <span class="sy0">-</span>1f, 0f<span class="br0">)</span><span class="sy0">;</span> <span class="co1">//Ninja-specific</span>
	<span class="kw1">this</span>.<span class="me1">attachChild</span><span class="br0">(</span><span class="kw1">this</span>.<span class="me1">model</span><span class="br0">)</span><span class="sy0">;</span>
 
	CapsuleCollisionShape playerShape <span class="sy0">=</span> <span class="kw1">new</span> CapsuleCollisionShape<span class="br0">(</span>.5f,1f<span class="br0">)</span><span class="sy0">;</span> <span class="co1">//Ninja-specific</span>
	characterControl <span class="sy0">=</span> <span class="kw1">new</span> CharacterControl<span class="br0">(</span>playerShape, stepSize<span class="br0">)</span><span class="sy0">;</span>
	characterControl.<span class="me1">setJumpSpeed</span><span class="br0">(</span>jumpSpeed<span class="br0">)</span><span class="sy0">;</span>
	characterControl.<span class="me1">setFallSpeed</span><span class="br0">(</span>fallSpeed<span class="br0">)</span><span class="sy0">;</span>
	characterControl.<span class="me1">setGravity</span><span class="br0">(</span>gravity<span class="br0">)</span><span class="sy0">;</span>
	<span class="kw1">this</span>.<span class="me1">addControl</span><span class="br0">(</span>characterControl<span class="br0">)</span><span class="sy0">;</span>
 
	animControl <span class="sy0">=</span> model.<span class="me1">getControl</span><span class="br0">(</span>AnimControl.<span class="kw1">class</span><span class="br0">)</span><span class="sy0">;</span>
	animControl.<span class="me1">addListener</span><span class="br0">(</span><span class="kw1">this</span><span class="br0">)</span><span class="sy0">;</span>
	animChannel <span class="sy0">=</span> animControl.<span class="me1">createChannel</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
	animChannel.<span class="me1">setAnim</span><span class="br0">(</span>idleAnim<span class="br0">)</span><span class="sy0">;</span>
 
	<span class="kw1">this</span>.<span class="me1">inputManager</span> <span class="sy0">=</span> inputManager<span class="sy0">;</span>
	setUpKeys<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    <span class="co1">//Make sure to call this from the main simpleUpdate() loop</span>
    <span class="kw1">public</span> <span class="kw4">void</span> update<span class="br0">(</span><span class="br0">)</span>
    <span class="br0">{</span>
	Vector3f camDir <span class="sy0">=</span> cam.<span class="me1">getDirection</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">clone</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
	camDir.<span class="me1">y</span> <span class="sy0">=</span> <span class="nu0">0</span><span class="sy0">;</span>
	Vector3f camLeft <span class="sy0">=</span> cam.<span class="me1">getLeft</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">clone</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
	camLeft.<span class="me1">y</span> <span class="sy0">=</span> <span class="nu0">0</span><span class="sy0">;</span>
	walkDirection.<span class="me1">set</span><span class="br0">(</span><span class="nu0">0</span>, <span class="nu0">0</span>, <span class="nu0">0</span><span class="br0">)</span><span class="sy0">;</span>
 
	<span class="kw1">if</span> <span class="br0">(</span>left<span class="br0">)</span>  <span class="br0">{</span> walkDirection.<span class="me1">addLocal</span><span class="br0">(</span>camLeft<span class="br0">)</span><span class="sy0">;</span> <span class="br0">}</span>
	<span class="kw1">if</span> <span class="br0">(</span>right<span class="br0">)</span> <span class="br0">{</span> walkDirection.<span class="me1">addLocal</span><span class="br0">(</span>camLeft.<span class="me1">negate</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span> <span class="br0">}</span>
	<span class="kw1">if</span> <span class="br0">(</span>up<span class="br0">)</span>    <span class="br0">{</span> walkDirection.<span class="me1">addLocal</span><span class="br0">(</span>camDir<span class="br0">)</span><span class="sy0">;</span> <span class="br0">}</span>
	<span class="kw1">if</span> <span class="br0">(</span>down<span class="br0">)</span>  <span class="br0">{</span> walkDirection.<span class="me1">addLocal</span><span class="br0">(</span>camDir.<span class="me1">negate</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span> <span class="br0">}</span>
 
	characterControl.<span class="me1">setWalkDirection</span><span class="br0">(</span>walkDirection.<span class="me1">normalize</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">multLocal</span><span class="br0">(</span>walkSpeed<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
 
	handleAnimations<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    <span class="kw1">private</span> <span class="kw4">void</span> handleAnimations<span class="br0">(</span><span class="br0">)</span>
    <span class="br0">{</span>
	<span class="kw1">if</span><span class="br0">(</span>attacking<span class="br0">)</span>
	<span class="br0">{</span>
	    <span class="co1">//waiting for attack animation to finish</span>
	<span class="br0">}</span>
	<span class="kw1">else</span> <span class="kw1">if</span><span class="br0">(</span>attack<span class="br0">)</span>
	<span class="br0">{</span>
 
	    animChannel.<span class="me1">setAnim</span><span class="br0">(</span>attackAnim,.3f<span class="br0">)</span><span class="sy0">;</span>
	    animChannel.<span class="me1">setLoopMode</span><span class="br0">(</span>LoopMode.<span class="me1">DontLoop</span><span class="br0">)</span><span class="sy0">;</span>
	    attack <span class="sy0">=</span> <span class="kw2">false</span><span class="sy0">;</span>
	    attacking <span class="sy0">=</span> <span class="kw2">true</span><span class="sy0">;</span>
	<span class="br0">}</span>
	<span class="kw1">else</span> <span class="kw1">if</span><span class="br0">(</span>characterControl.<span class="me1">onGround</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span>
	<span class="br0">{</span>
	    <span class="kw1">if</span><span class="br0">(</span>left <span class="sy0">||</span> right <span class="sy0">||</span> up <span class="sy0">||</span> down<span class="br0">)</span>
	    <span class="br0">{</span>
		<span class="kw1">if</span><span class="br0">(</span><span class="sy0">!</span>animChannel.<span class="me1">getAnimationName</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">equals</span><span class="br0">(</span>walkAnim<span class="br0">)</span><span class="br0">)</span>
		<span class="br0">{</span>
		    animChannel.<span class="me1">setAnim</span><span class="br0">(</span>walkAnim,.3f<span class="br0">)</span><span class="sy0">;</span>
		    animChannel.<span class="me1">setLoopMode</span><span class="br0">(</span>LoopMode.<span class="me1">Loop</span><span class="br0">)</span><span class="sy0">;</span>
		<span class="br0">}</span>
	    <span class="br0">}</span>
	    <span class="kw1">else</span>
	    <span class="br0">{</span>
		<span class="kw1">if</span><span class="br0">(</span><span class="sy0">!</span>animChannel.<span class="me1">getAnimationName</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">equals</span><span class="br0">(</span>idleAnim<span class="br0">)</span><span class="br0">)</span>
		<span class="br0">{</span>
		    animChannel.<span class="me1">setAnim</span><span class="br0">(</span>idleAnim,.3f<span class="br0">)</span><span class="sy0">;</span>
		    animChannel.<span class="me1">setLoopMode</span><span class="br0">(</span>LoopMode.<span class="me1">Cycle</span><span class="br0">)</span><span class="sy0">;</span>
		<span class="br0">}</span>
	    <span class="br0">}</span>
	<span class="br0">}</span>
    <span class="br0">}</span>
 
    <span class="kw1">private</span> <span class="kw4">void</span> setUpKeys<span class="br0">(</span><span class="br0">)</span>
    <span class="br0">{</span>
	inputManager.<span class="me1">addMapping</span><span class="br0">(</span><span class="st0">"Left"</span>, <span class="kw1">new</span> KeyTrigger<span class="br0">(</span>KeyInput.<span class="me1">KEY_A</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
	inputManager.<span class="me1">addMapping</span><span class="br0">(</span><span class="st0">"Right"</span>, <span class="kw1">new</span> KeyTrigger<span class="br0">(</span>KeyInput.<span class="me1">KEY_D</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
	inputManager.<span class="me1">addMapping</span><span class="br0">(</span><span class="st0">"Up"</span>, <span class="kw1">new</span> KeyTrigger<span class="br0">(</span>KeyInput.<span class="me1">KEY_W</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
	inputManager.<span class="me1">addMapping</span><span class="br0">(</span><span class="st0">"Down"</span>, <span class="kw1">new</span> KeyTrigger<span class="br0">(</span>KeyInput.<span class="me1">KEY_S</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
	inputManager.<span class="me1">addMapping</span><span class="br0">(</span><span class="st0">"Jump"</span>, <span class="kw1">new</span> KeyTrigger<span class="br0">(</span>KeyInput.<span class="me1">KEY_SPACE</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
	inputManager.<span class="me1">addMapping</span><span class="br0">(</span><span class="st0">"Attack"</span>, <span class="kw1">new</span> MouseButtonTrigger<span class="br0">(</span>MouseInput.<span class="me1">BUTTON_LEFT</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
	inputManager.<span class="me1">addMapping</span><span class="br0">(</span><span class="st0">"TurnLeft"</span>, <span class="kw1">new</span> MouseAxisTrigger<span class="br0">(</span>MouseInput.<span class="me1">AXIS_X</span>,<span class="kw2">true</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
	inputManager.<span class="me1">addMapping</span><span class="br0">(</span><span class="st0">"TurnRight"</span>, <span class="kw1">new</span> MouseAxisTrigger<span class="br0">(</span>MouseInput.<span class="me1">AXIS_X</span>,<span class="kw2">false</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
	inputManager.<span class="me1">addMapping</span><span class="br0">(</span><span class="st0">"MouselookDown"</span>, <span class="kw1">new</span> MouseAxisTrigger<span class="br0">(</span>MouseInput.<span class="me1">AXIS_Y</span>,<span class="kw2">true</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
	inputManager.<span class="me1">addMapping</span><span class="br0">(</span><span class="st0">"MouselookUp"</span>, <span class="kw1">new</span> MouseAxisTrigger<span class="br0">(</span>MouseInput.<span class="me1">AXIS_Y</span>,<span class="kw2">false</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
	inputManager.<span class="me1">addListener</span><span class="br0">(</span><span class="kw1">this</span>, <span class="st0">"Left"</span><span class="br0">)</span><span class="sy0">;</span>
	inputManager.<span class="me1">addListener</span><span class="br0">(</span><span class="kw1">this</span>, <span class="st0">"Right"</span><span class="br0">)</span><span class="sy0">;</span>
	inputManager.<span class="me1">addListener</span><span class="br0">(</span><span class="kw1">this</span>, <span class="st0">"Up"</span><span class="br0">)</span><span class="sy0">;</span>
	inputManager.<span class="me1">addListener</span><span class="br0">(</span><span class="kw1">this</span>, <span class="st0">"Down"</span><span class="br0">)</span><span class="sy0">;</span>
	inputManager.<span class="me1">addListener</span><span class="br0">(</span><span class="kw1">this</span>, <span class="st0">"Jump"</span><span class="br0">)</span><span class="sy0">;</span>
	inputManager.<span class="me1">addListener</span><span class="br0">(</span><span class="kw1">this</span>, <span class="st0">"Attack"</span><span class="br0">)</span><span class="sy0">;</span>
	inputManager.<span class="me1">addListener</span><span class="br0">(</span><span class="kw1">this</span>, <span class="st0">"TurnLeft"</span><span class="br0">)</span><span class="sy0">;</span>
	inputManager.<span class="me1">addListener</span><span class="br0">(</span><span class="kw1">this</span>, <span class="st0">"TurnRight"</span><span class="br0">)</span><span class="sy0">;</span>
	inputManager.<span class="me1">addListener</span><span class="br0">(</span><span class="kw1">this</span>, <span class="st0">"MouselookDown"</span><span class="br0">)</span><span class="sy0">;</span>
	inputManager.<span class="me1">addListener</span><span class="br0">(</span><span class="kw1">this</span>, <span class="st0">"MouselookUp"</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    <span class="kw1">public</span> <span class="kw4">void</span> onAction<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> binding, <span class="kw4">boolean</span> value, <span class="kw4">float</span> tpf<span class="br0">)</span> <span class="br0">{</span>
	<span class="kw1">if</span> <span class="br0">(</span>binding.<span class="me1">equals</span><span class="br0">(</span><span class="st0">"Left"</span><span class="br0">)</span><span class="br0">)</span>
	<span class="br0">{</span>
	    left <span class="sy0">=</span> value<span class="sy0">;</span>
	<span class="br0">}</span>
	<span class="kw1">else</span> <span class="kw1">if</span> <span class="br0">(</span>binding.<span class="me1">equals</span><span class="br0">(</span><span class="st0">"Right"</span><span class="br0">)</span><span class="br0">)</span>
	<span class="br0">{</span>
	    right <span class="sy0">=</span> value<span class="sy0">;</span>
	<span class="br0">}</span>
	<span class="kw1">else</span> <span class="kw1">if</span> <span class="br0">(</span>binding.<span class="me1">equals</span><span class="br0">(</span><span class="st0">"Up"</span><span class="br0">)</span><span class="br0">)</span>
	<span class="br0">{</span>
	    up <span class="sy0">=</span> value<span class="sy0">;</span>
	<span class="br0">}</span>
	<span class="kw1">else</span> <span class="kw1">if</span> <span class="br0">(</span>binding.<span class="me1">equals</span><span class="br0">(</span><span class="st0">"Down"</span><span class="br0">)</span><span class="br0">)</span>
	<span class="br0">{</span>
	    down <span class="sy0">=</span> value<span class="sy0">;</span>
	<span class="br0">}</span>
	<span class="kw1">else</span> <span class="kw1">if</span> <span class="br0">(</span>binding.<span class="me1">equals</span><span class="br0">(</span><span class="st0">"Jump"</span><span class="br0">)</span><span class="br0">)</span>
	<span class="br0">{</span>
	    <span class="kw1">if</span><span class="br0">(</span>characterControl.<span class="me1">onGround</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span>
	    <span class="br0">{</span>
		characterControl.<span class="me1">jump</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
		<span class="kw1">if</span><span class="br0">(</span><span class="sy0">!</span>attacking<span class="br0">)</span>
		<span class="br0">{</span>
		    animChannel.<span class="me1">setAnim</span><span class="br0">(</span>jumpAnim,.3f<span class="br0">)</span><span class="sy0">;</span>
		    animChannel.<span class="me1">setLoopMode</span><span class="br0">(</span>LoopMode.<span class="me1">Loop</span><span class="br0">)</span><span class="sy0">;</span>
		<span class="br0">}</span>
	    <span class="br0">}</span>
	<span class="br0">}</span>
	<span class="kw1">else</span> <span class="kw1">if</span> <span class="br0">(</span>binding.<span class="me1">equals</span><span class="br0">(</span><span class="st0">"Attack"</span><span class="br0">)</span><span class="br0">)</span>
	<span class="br0">{</span>
	    attack <span class="sy0">=</span> value<span class="sy0">;</span>
	<span class="br0">}</span>
    <span class="br0">}</span>
 
    <span class="co1">//Analog handler for mouse movement events.</span>
    <span class="co1">//It is assumed that we want horizontal movements to turn the character,</span>
    <span class="co1">//while vertical movements only make the camera rotate up or down.</span>
    <span class="kw1">public</span> <span class="kw4">void</span> onAnalog<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> binding, <span class="kw4">float</span> value, <span class="kw4">float</span> tpf<span class="br0">)</span>
    <span class="br0">{</span>
	<span class="kw1">if</span> <span class="br0">(</span>binding.<span class="me1">equals</span><span class="br0">(</span><span class="st0">"TurnLeft"</span><span class="br0">)</span><span class="br0">)</span>
	<span class="br0">{</span>
	    Quaternion turn <span class="sy0">=</span> <span class="kw1">new</span> Quaternion<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
	    turn.<span class="me1">fromAngleAxis</span><span class="br0">(</span>mouselookSpeed<span class="sy0">*</span>value, Vector3f.<span class="me1">UNIT_Y</span><span class="br0">)</span><span class="sy0">;</span>
	    characterControl.<span class="me1">setViewDirection</span><span class="br0">(</span>turn.<span class="me1">mult</span><span class="br0">(</span>characterControl.<span class="me1">getViewDirection</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
	<span class="br0">}</span>
	<span class="kw1">else</span> <span class="kw1">if</span> <span class="br0">(</span>binding.<span class="me1">equals</span><span class="br0">(</span><span class="st0">"TurnRight"</span><span class="br0">)</span><span class="br0">)</span>
	<span class="br0">{</span>
	    Quaternion turn <span class="sy0">=</span> <span class="kw1">new</span> Quaternion<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
	    turn.<span class="me1">fromAngleAxis</span><span class="br0">(</span><span class="sy0">-</span>mouselookSpeed<span class="sy0">*</span>value, Vector3f.<span class="me1">UNIT_Y</span><span class="br0">)</span><span class="sy0">;</span>
	    characterControl.<span class="me1">setViewDirection</span><span class="br0">(</span>turn.<span class="me1">mult</span><span class="br0">(</span>characterControl.<span class="me1">getViewDirection</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
	<span class="br0">}</span>
	<span class="kw1">else</span> <span class="kw1">if</span> <span class="br0">(</span>binding.<span class="me1">equals</span><span class="br0">(</span><span class="st0">"MouselookDown"</span><span class="br0">)</span><span class="br0">)</span>
	<span class="br0">{</span>
	    camera.<span class="me1">verticalRotate</span><span class="br0">(</span>mouselookSpeed<span class="sy0">*</span>value<span class="br0">)</span><span class="sy0">;</span>
	<span class="br0">}</span>
	<span class="kw1">else</span> <span class="kw1">if</span> <span class="br0">(</span>binding.<span class="me1">equals</span><span class="br0">(</span><span class="st0">"MouselookUp"</span><span class="br0">)</span><span class="br0">)</span>
	<span class="br0">{</span>
	    camera.<span class="me1">verticalRotate</span><span class="br0">(</span><span class="sy0">-</span>mouselookSpeed<span class="sy0">*</span>value<span class="br0">)</span><span class="sy0">;</span>
	<span class="br0">}</span>
    <span class="br0">}</span>
 
    <span class="kw1">public</span> <span class="kw4">void</span> onAnimCycleDone<span class="br0">(</span>AnimControl control, AnimChannel channel, <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> animName<span class="br0">)</span>
    <span class="br0">{</span>
	<span class="kw1">if</span><span class="br0">(</span>channel <span class="sy0">==</span> animChannel <span class="sy0">&amp;&amp;</span> attacking <span class="sy0">&amp;&amp;</span> animName.<span class="me1">equals</span><span class="br0">(</span>attackAnim<span class="br0">)</span><span class="br0">)</span>
	<span class="br0">{</span>
	    attacking <span class="sy0">=</span> <span class="kw2">false</span><span class="sy0">;</span>
	<span class="br0">}</span>
    <span class="br0">}</span>
 
    <span class="kw1">public</span> <span class="kw4">void</span> onAnimChange<span class="br0">(</span>AnimControl control, AnimChannel channel, <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> animName<span class="br0">)</span>
    <span class="br0">{</span>
    <span class="br0">}</span>
 
    <span class="kw1">public</span> CharacterControl getCharacterControl<span class="br0">(</span><span class="br0">)</span>
    <span class="br0">{</span>
	<span class="kw1">return</span> characterControl<span class="sy0">;</span>
    <span class="br0">}</span>
 
    <span class="kw1">public</span> ThirdPersonCamera getCameraNode<span class="br0">(</span><span class="br0">)</span>
    <span class="br0">{</span>
	<span class="kw1">return</span> camera<span class="sy0">;</span>
    <span class="br0">}</span>
<span class="br0">}</span></pre>

</div>
<!-- EDIT4 SECTION "ThirdPersonPlayerNode.java" [1894-10222] -->
<h3 class="sectionedit5" id="thirdpersoncamerajava">ThirdPersonCamera.java</h3>
<div class="level3">

<p>
ThirdPersonCamera.java sets up a CameraNode to follow behind the player. It uses the same “ControlDirection.SpatialToCamera” approach as <a href="/jme3/advanced/making_the_camera_follow_a_character.html" class="wikilink1" title="jme3:advanced:making_the_camera_follow_a_character">the advanced tutorial about 3rd-person cameras</a>, but also adds a pivot node for easy mouselook. (See the scientific diagram above, and the comments in the class, for more explanation).
</p>
<pre class="code java"><span class="kw1">package</span> <span class="co2">mygame</span><span class="sy0">;</span>
 
<span class="kw1">import</span> <span class="co2">com.jme3.math.FastMath</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.math.Vector3f</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.renderer.Camera</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.CameraNode</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.Node</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.control.CameraControl</span><span class="sy0">;</span>
 
<span class="co3">/**
 *
 * @author Berzee
 */</span>
<span class="kw1">public</span> <span class="kw1">class</span> ThirdPersonCamera
<span class="br0">{</span>
    <span class="co1">//The "pivot" Node allows for easy third-person mouselook! It's actually</span>
    <span class="co1">//just an empty Node that gets attached to the center of the Player.</span>
    <span class="co1">//</span>
    <span class="co1">//The CameraNode is set up to always position itself behind the *pivot*</span>
    <span class="co1">//instead of behind the Player. So when we want to mouselook around the</span>
    <span class="co1">//Player, we simply need to spin the pivot! The camera will orbit behind it</span>
    <span class="co1">//while the Player object remains still.</span>
    <span class="co1">//</span>
    <span class="co1">//NOTE: Currently only vertical mouselook (around the X axis) is working.</span>
    <span class="co1">//The other two axes could be added fairly easily, once you have an idea</span>
    <span class="co1">//for how they should actually behave (min and max angles, et cetera).</span>
    <span class="kw1">private</span> Node pivot<span class="sy0">;</span>
    <span class="kw1">private</span> CameraNode cameraNode<span class="sy0">;</span>
 
    <span class="co1">//Change these as you desire. Lower verticalAngle values will put the camera</span>
    <span class="co1">//closer to the ground.</span>
    <span class="kw1">public</span> <span class="kw4">float</span> followDistance <span class="sy0">=</span> <span class="nu0">7</span><span class="sy0">;</span>
    <span class="kw1">public</span> <span class="kw4">float</span> verticalAngle <span class="sy0">=</span> <span class="nu0">30</span> <span class="sy0">*</span> FastMath.<span class="me1">DEG_TO_RAD</span><span class="sy0">;</span>
 
    <span class="co1">//These bounds keep the camera from spinning too far and clipping through</span>
    <span class="co1">//the floor or turning upside-down. You can change them as needed but it is</span>
    <span class="co1">//recommended to keep the values in the (-90,90) range.</span>
    <span class="kw1">public</span> <span class="kw4">float</span> maxVerticalAngle <span class="sy0">=</span> <span class="nu0">85</span> <span class="sy0">*</span> FastMath.<span class="me1">DEG_TO_RAD</span><span class="sy0">;</span>
    <span class="kw1">public</span> <span class="kw4">float</span> minVerticalAngle <span class="sy0">=</span> <span class="nu0">5</span> <span class="sy0">*</span> FastMath.<span class="me1">DEG_TO_RAD</span><span class="sy0">;</span>
 
    <span class="kw1">public</span> ThirdPersonCamera<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> name, Camera cam, Node player<span class="br0">)</span>
    <span class="br0">{</span>
	pivot <span class="sy0">=</span> <span class="kw1">new</span> Node<span class="br0">(</span><span class="st0">"CamTrack"</span><span class="br0">)</span><span class="sy0">;</span>	
	player.<span class="me1">attachChild</span><span class="br0">(</span>pivot<span class="br0">)</span><span class="sy0">;</span>
 
	cameraNode <span class="sy0">=</span> <span class="kw1">new</span> CameraNode<span class="br0">(</span>name, cam<span class="br0">)</span><span class="sy0">;</span>
        cameraNode.<span class="me1">setControlDir</span><span class="br0">(</span>CameraControl.<span class="me1">ControlDirection</span>.<span class="me1">SpatialToCamera</span><span class="br0">)</span><span class="sy0">;</span>
	pivot.<span class="me1">attachChild</span><span class="br0">(</span>cameraNode<span class="br0">)</span><span class="sy0">;</span>
	cameraNode.<span class="me1">setLocalTranslation</span><span class="br0">(</span><span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">0</span>, <span class="nu0">0</span>, followDistance<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
	cameraNode.<span class="me1">lookAt</span><span class="br0">(</span>pivot.<span class="me1">getLocalTranslation</span><span class="br0">(</span><span class="br0">)</span>, Vector3f.<span class="me1">UNIT_Y</span><span class="br0">)</span><span class="sy0">;</span>
 
	pivot.<span class="me1">getLocalRotation</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">fromAngleAxis</span><span class="br0">(</span><span class="sy0">-</span>verticalAngle, Vector3f.<span class="me1">UNIT_X</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    <span class="kw1">public</span> <span class="kw4">void</span> verticalRotate<span class="br0">(</span><span class="kw4">float</span> angle<span class="br0">)</span>
    <span class="br0">{</span>
	verticalAngle <span class="sy0">+=</span> angle<span class="sy0">;</span>
 
	<span class="kw1">if</span><span class="br0">(</span>verticalAngle <span class="sy0">&gt;</span> maxVerticalAngle<span class="br0">)</span>
	<span class="br0">{</span>
	    verticalAngle <span class="sy0">=</span> maxVerticalAngle<span class="sy0">;</span>
	<span class="br0">}</span>
	<span class="kw1">else</span> <span class="kw1">if</span><span class="br0">(</span>verticalAngle <span class="sy0">&lt;</span> minVerticalAngle<span class="br0">)</span>
	<span class="br0">{</span>
	    verticalAngle <span class="sy0">=</span> minVerticalAngle<span class="sy0">;</span>
	<span class="br0">}</span>
 
	pivot.<span class="me1">getLocalRotation</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">fromAngleAxis</span><span class="br0">(</span><span class="sy0">-</span>verticalAngle, Vector3f.<span class="me1">UNIT_X</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    <span class="kw1">public</span> CameraNode getCameraNode<span class="br0">(</span><span class="br0">)</span>
    <span class="br0">{</span>
	<span class="kw1">return</span> cameraNode<span class="sy0">;</span>
    <span class="br0">}</span>
 
    <span class="kw1">public</span> Node getCameraTrack<span class="br0">(</span><span class="br0">)</span>
    <span class="br0">{</span>
	<span class="kw1">return</span> pivot<span class="sy0">;</span>
    <span class="br0">}</span>
<span class="br0">}</span></pre>

</div>
<!-- EDIT5 SECTION "ThirdPersonCamera.java" [10223-13211] -->
<h3 class="sectionedit6" id="mainjava">Main.java</h3>
<div class="level3">

<p>
Here is an example Main.java project that you can use to see the ThirdPersonPlayerNode in action. Just make sure to add the jme3-test-data.jar library to your project so it can access the Ninja model and ManyLights scene (In the SDK: Project Explorer → Right Click on “Libraries” → Add Library → jme3-test-data.jar).
</p>
<pre class="code java"><span class="kw1">package</span> <span class="co2">mygame</span><span class="sy0">;</span>
 
<span class="kw1">import</span> <span class="co2">com.jme3.app.SimpleApplication</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.bullet.BulletAppState</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.bullet.collision.shapes.CollisionShape</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.bullet.control.RigidBodyControl</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.bullet.util.CollisionShapeFactory</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.light.DirectionalLight</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.renderer.RenderManager</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.Spatial</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.math.Vector3f</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.Node</span><span class="sy0">;</span>
 
<span class="co3">/**
 * @author Berzee
 */</span>
<span class="kw1">public</span> <span class="kw1">class</span> Main <span class="kw1">extends</span> SimpleApplication
<span class="br0">{</span>    
    <span class="kw1">private</span> Spatial sceneModel<span class="sy0">;</span>
    <span class="kw1">private</span> RigidBodyControl scene<span class="sy0">;</span>
    <span class="kw1">private</span> BulletAppState bulletAppState<span class="sy0">;</span>
    <span class="kw1">private</span> ThirdPersonPlayerNode player<span class="sy0">;</span>
 
    <span class="kw1">public</span> <span class="kw1">static</span> <span class="kw4">void</span> main<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a><span class="br0">[</span><span class="br0">]</span> args<span class="br0">)</span> <span class="br0">{</span>
        Main app <span class="sy0">=</span> <span class="kw1">new</span> Main<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
        app.<span class="me1">start</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    @Override
    <span class="kw1">public</span> <span class="kw4">void</span> simpleInitApp<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>        
        mouseInput.<span class="me1">setCursorVisible</span><span class="br0">(</span><span class="kw2">false</span><span class="br0">)</span><span class="sy0">;</span>
	flyCam.<span class="me1">setEnabled</span><span class="br0">(</span><span class="kw2">false</span><span class="br0">)</span><span class="sy0">;</span>
 
	bulletAppState <span class="sy0">=</span> <span class="kw1">new</span> BulletAppState<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
	stateManager.<span class="me1">attach</span><span class="br0">(</span>bulletAppState<span class="br0">)</span><span class="sy0">;</span>
	<span class="co1">//bulletAppState.getPhysicsSpace().enableDebug(assetManager);</span>
 
        sceneModel <span class="sy0">=</span> assetManager.<span class="me1">loadModel</span><span class="br0">(</span><span class="st0">"Scenes/ManyLights/Main.scene"</span><span class="br0">)</span><span class="sy0">;</span>
	sceneModel.<span class="me1">scale</span><span class="br0">(</span>1f,.5f,1f<span class="br0">)</span><span class="sy0">;</span> <span class="co1">//Make scenery short enough to jump on. =P</span>
	CollisionShape sceneShape <span class="sy0">=</span> CollisionShapeFactory.<span class="me1">createMeshShape</span><span class="br0">(</span><span class="br0">(</span>Node<span class="br0">)</span> sceneModel<span class="br0">)</span><span class="sy0">;</span>
	scene <span class="sy0">=</span> <span class="kw1">new</span> RigidBodyControl<span class="br0">(</span>sceneShape, <span class="nu0">0</span><span class="br0">)</span><span class="sy0">;</span>
	sceneModel.<span class="me1">addControl</span><span class="br0">(</span>scene<span class="br0">)</span><span class="sy0">;</span>
        rootNode.<span class="me1">attachChild</span><span class="br0">(</span>sceneModel<span class="br0">)</span><span class="sy0">;</span>
	bulletAppState.<span class="me1">getPhysicsSpace</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">add</span><span class="br0">(</span>scene<span class="br0">)</span><span class="sy0">;</span>
 
	Spatial playerModel <span class="sy0">=</span> assetManager.<span class="me1">loadModel</span><span class="br0">(</span><span class="st0">"Models/Ninja/Ninja.mesh.xml"</span><span class="br0">)</span><span class="sy0">;</span>
	player <span class="sy0">=</span> <span class="kw1">new</span> ThirdPersonPlayerNode<span class="br0">(</span>playerModel, inputManager, cam<span class="br0">)</span><span class="sy0">;</span>
	player.<span class="me1">getCharacterControl</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">setPhysicsLocation</span><span class="br0">(</span><span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="sy0">-</span>5f,2f,5f<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
	rootNode.<span class="me1">attachChild</span><span class="br0">(</span>player<span class="br0">)</span><span class="sy0">;</span>
	bulletAppState.<span class="me1">getPhysicsSpace</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">add</span><span class="br0">(</span>player<span class="br0">)</span><span class="sy0">;</span>
 
        <span class="co1">// You must add a light to make the model visible</span>
        DirectionalLight sun <span class="sy0">=</span> <span class="kw1">new</span> DirectionalLight<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
        sun.<span class="me1">setDirection</span><span class="br0">(</span><span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="sy0">-</span>.1f, <span class="sy0">-</span>.7f, <span class="sy0">-</span>1f<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
        rootNode.<span class="me1">addLight</span><span class="br0">(</span>sun<span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    @Override
    <span class="kw1">public</span> <span class="kw4">void</span> simpleUpdate<span class="br0">(</span><span class="kw4">float</span> tpf<span class="br0">)</span>
    <span class="br0">{</span>
	player.<span class="me1">update</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    @Override
    <span class="kw1">public</span> <span class="kw4">void</span> simpleRender<span class="br0">(</span>RenderManager rm<span class="br0">)</span>
    <span class="br0">{</span>
        <span class="co1">//TODO: add render code</span>
    <span class="br0">}</span>
<span class="br0">}</span></pre>

</div>
<!-- EDIT6 SECTION "Main.java" [13212-] -->
