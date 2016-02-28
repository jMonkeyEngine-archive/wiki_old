---
title: 
---
<p>
<a href="http://www.youtube.com/watch?v=dXGfecvI1Sk" class="urlextern" title="http://www.youtube.com/watch?v=dXGfecvI1Sk" rel="nofollow">Youtube video</a>
</p>

<p>
<a href="/resources/jme3-beginner-chasecamera.png" class="media" title="jme3:beginner:chasecamera.png"><img src="/resources/jme3-beginner-chasecamera.png" class="media" alt="" /></a>
</p>
<ul>
<li class="level1"><div class="li"> <a href="https://code.google.com/p/jmonkeyengine/source/browse/#svn%2Ftrunk%2Fengine%2Ftest-data%2FModels%2FNinja" class="urlextern" title="https://code.google.com/p/jmonkeyengine/source/browse/#svn%2Ftrunk%2Fengine%2Ftest-data%2FModels%2FNinja" rel="nofollow">Ninja Mesh</a></div>
</li>
<li class="level1"><div class="li"> <a href="http://jmonkeyengine.googlecode.com/svn/trunk/engine/town.zip" class="urlextern" title="http://jmonkeyengine.googlecode.com/svn/trunk/engine/town.zip" rel="nofollow">Town Scene</a></div>
</li>
</ul>
<ul>
<li class="level1"><div class="li"> Walk Bugs <img src="/lib/images/smileys/fixme.gif" class="icon" alt="FIXME" /></div>
</li>
<li class="level1"><div class="li"> Jump Bugs <img src="/lib/images/smileys/fixme.gif" class="icon" alt="FIXME" /></div>
</li>
</ul>

<p>
Memo:
</p>
<ol>
<li class="level1"><div class="li"> jMonkeyEngine calls the update() methods of all AppState objects in the order in which you attached them.</div>
</li>
<li class="level1"><div class="li"> jMonkeyEngine calls the controlUpdate() methods of all controls in the order in which you added them.</div>
</li>
<li class="level1"><div class="li"> jMonkeyEngine calls the simpleUpdate() method of the main SimpleApplication class.</div>
</li>
</ol>

<p>
—AbstractPhysicBodyContext
</p>
<pre class="code java"><span class="kw1">package</span> <span class="co2">org.jmonkey3.chasecam</span><span class="sy0">;</span>
 
<span class="kw1">import</span> <span class="co2">com.jme3.app.state.AbstractAppState</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.app.state.AppStateManager</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.bullet.BulletAppState</span><span class="sy0">;</span>
 
<span class="coMULTI">/*
 Chase camera (aka 3rd person camera) example
 Based on official TestQ3.java
 
 @author Alex Cham aka Jcrypto
 */</span>
<span class="kw1">public</span> <span class="kw1">abstract</span> <span class="kw1">class</span> AbstractPhysicBodyContext <span class="kw1">extends</span> AbstractAppState
<span class="br0">{</span>
 
    <span class="kw1">private</span> AppStateManager stateManager <span class="sy0">=</span> <span class="kw2">null</span><span class="sy0">;</span>
    <span class="co1">//</span>
    <span class="kw1">private</span> <span class="kw1">static</span> <span class="kw1">final</span> BulletAppState bulletAppState<span class="sy0">;</span>
 
    <span class="kw1">static</span>
    <span class="br0">{</span>
        bulletAppState <span class="sy0">=</span> <span class="kw1">new</span> BulletAppState<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    <span class="kw1">public</span> AbstractPhysicBodyContext<span class="br0">(</span><span class="br0">)</span>
    <span class="br0">{</span>
    <span class="br0">}</span>
 
    <span class="co3">/**
     @return the bulletAppState
     */</span>
    <span class="kw1">public</span> BulletAppState getBulletAppState<span class="br0">(</span><span class="br0">)</span>
    <span class="br0">{</span>
        <span class="kw1">return</span> bulletAppState<span class="sy0">;</span>
    <span class="br0">}</span>
 
    <span class="co3">/**
     @param stateManager the stateManager to set
     Attaching BulletAppstate to Initialize PhysicsSpace
     */</span>
    <span class="kw1">public</span> <span class="kw4">void</span> attachBulletAppstate<span class="br0">(</span>AppStateManager stateManager<span class="br0">)</span>
    <span class="br0">{</span>
        <span class="kw1">this</span>.<span class="me1">stateManager</span> <span class="sy0">=</span> stateManager<span class="sy0">;</span>
        stateManager.<span class="me1">attach</span><span class="br0">(</span>bulletAppState<span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
<span class="br0">}</span></pre>

<p>
—AbstractSpatialBodyContext.java
</p>
<pre class="code java"><span class="kw1">package</span> <span class="co2">org.jmonkey3.chasecam</span><span class="sy0">;</span>
 
<span class="kw1">import</span> <span class="co2">com.jme3.app.state.AbstractAppState</span><span class="sy0">;</span>
 
<span class="coMULTI">/*
 Chase camera (aka 3rd person camera) example
 Based on official TestQ3.java
 
 @author Alex Cham aka Jcrypto
 */</span>
<span class="kw1">public</span> <span class="kw1">abstract</span> <span class="kw1">class</span> AbstractSpatialBodyContext <span class="kw1">extends</span> AbstractAppState
<span class="br0">{</span>
 
    <span class="kw1">public</span> AbstractSpatialBodyContext<span class="br0">(</span><span class="br0">)</span>
    <span class="br0">{</span>
    <span class="br0">}</span>
 
<span class="br0">}</span></pre>

<p>
—ApplicationContext.java
</p>
<pre class="code java"><span class="kw1">package</span> <span class="co2">org.jmonkey3.chasecam</span><span class="sy0">;</span>
 
<span class="kw1">import</span> <span class="co2">com.jme3.app.Application</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.app.state.AbstractAppState</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.app.state.AppStateManager</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.asset.AssetManager</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.input.FlyByCamera</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.input.InputManager</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.math.ColorRGBA</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.math.Vector3f</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.renderer.Camera</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.Node</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.system.AppSettings</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">org.jmonkey.utils.Debug</span><span class="sy0">;</span>
 
<span class="coMULTI">/*
 Chase camera (aka 3rd person camera) example
 Based on official TestQ3.java
 
 @author Alex Cham aka Jcrypto
 */</span>
<span class="kw1">public</span> <span class="kw1">class</span> ApplicationContext <span class="kw1">extends</span> AbstractAppState
<span class="br0">{</span>
 
    <span class="kw1">private</span> <span class="kw1">final</span> Node rootNode<span class="sy0">;</span>
<span class="co1">//</span>
    <span class="kw1">private</span> <span class="kw1">final</span> CameraContext sceneCameraContext<span class="sy0">;</span>
    <span class="kw1">private</span> <span class="kw1">final</span> AvatarBodyManager avatarBodyManager<span class="sy0">;</span>
    <span class="kw1">private</span> <span class="kw1">final</span> SceneBodyManager sceneBodyManager<span class="sy0">;</span>
 
<span class="co3">/**
 
    @param stateManager
    @param am
    @param settings
    @param inputManager
    @param rootNode
    @param cam
    @param flyByCam 
    */</span>
    <span class="kw1">public</span> ApplicationContext<span class="br0">(</span>AppStateManager stateManager, AssetManager am, AppSettings settings, InputManager inputManager, Node rootNode, Camera cam, FlyByCamera flyByCam<span class="br0">)</span>
    <span class="br0">{</span>
 
        <span class="kw1">this</span>.<span class="me1">rootNode</span> <span class="sy0">=</span> rootNode<span class="sy0">;</span>
        <span class="kw1">this</span>.<span class="me1">sceneCameraContext</span> <span class="sy0">=</span> <span class="kw1">new</span> CameraContext<span class="br0">(</span>settings, inputManager, cam, flyByCam<span class="br0">)</span><span class="sy0">;</span>
        <span class="kw1">this</span>.<span class="me1">sceneBodyManager</span> <span class="sy0">=</span> <span class="kw1">new</span> SceneBodyManager<span class="br0">(</span>stateManager, am, rootNode<span class="br0">)</span><span class="sy0">;</span>
        <span class="kw1">this</span>.<span class="me1">avatarBodyManager</span> <span class="sy0">=</span> <span class="kw1">new</span> AvatarBodyManager<span class="br0">(</span>am, rootNode, sceneCameraContext<span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    @Override
    <span class="kw1">public</span> <span class="kw4">void</span> initialize<span class="br0">(</span>AppStateManager stateManager, Application app<span class="br0">)</span>
    <span class="br0">{</span>
        <span class="co1">//super.initialize(stateManager, app);</span>
        <span class="co1">//TODO: initialize your AppState, e.g. attach spatials to rootNode</span>
        <span class="co1">//this is called on the OpenGL thread after the AppState has been attached</span>
 
<span class="co1">//</span>
        stateManager.<span class="me1">attach</span><span class="br0">(</span><span class="kw1">this</span>.<span class="me1">sceneCameraContext</span><span class="br0">)</span><span class="sy0">;</span>
        stateManager.<span class="me1">attach</span><span class="br0">(</span><span class="kw1">this</span>.<span class="me1">sceneBodyManager</span><span class="br0">)</span><span class="sy0">;</span><span class="co1">//initialize physic spacein constructor</span>
        stateManager.<span class="me1">attach</span><span class="br0">(</span><span class="kw1">this</span>.<span class="me1">avatarBodyManager</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="co1">//</span>
        Debug.<span class="me1">showNodeAxes</span><span class="br0">(</span>app.<span class="me1">getAssetManager</span><span class="br0">(</span><span class="br0">)</span>, <span class="kw1">this</span>.<span class="me1">rootNode</span>, 1024.0f<span class="br0">)</span><span class="sy0">;</span>
        Debug.<span class="me1">attachWireFrameDebugGrid</span><span class="br0">(</span>app.<span class="me1">getAssetManager</span><span class="br0">(</span><span class="br0">)</span>, rootNode, Vector3f.<span class="me1">ZERO</span>, <span class="nu0">2048</span>, ColorRGBA.<span class="me1">DarkGray</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    @Override
    <span class="kw1">public</span> <span class="kw4">void</span> update<span class="br0">(</span><span class="kw4">float</span> tpf<span class="br0">)</span>
    <span class="br0">{</span>
 
    <span class="br0">}</span>
<span class="br0">}</span></pre>

<p>
—AvatarAnimationEventListener.java
</p>
<pre class="code java"><span class="kw1">package</span> <span class="co2">org.jmonkey3.chasecam</span><span class="sy0">;</span>
 
<span class="kw1">import</span> <span class="co2">com.jme3.animation.AnimChannel</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.animation.AnimControl</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.animation.AnimEventListener</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.app.Application</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.app.state.AbstractAppState</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.app.state.AppStateManager</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.bullet.objects.PhysicsCharacter</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.Spatial</span><span class="sy0">;</span>
 
<span class="coMULTI">/*
 Chase camera (aka 3rd person camera) example
 Based on official TestQ3.java
 
 @author Alex Cham aka Jcrypto
 */</span>
<span class="kw1">public</span> <span class="kw1">class</span> AvatarAnimationEventListener <span class="kw1">extends</span> AbstractAppState <span class="kw1">implements</span> AnimEventListener
<span class="br0">{</span>
 
    <span class="kw1">private</span> <span class="kw1">final</span> AnimChannel channel<span class="sy0">;</span>
    <span class="kw1">private</span> <span class="kw1">final</span> AnimControl control<span class="sy0">;</span>
    <span class="kw1">private</span> <span class="kw1">final</span> PlayerInputActionListener pial<span class="sy0">;</span>
    <span class="kw1">private</span> <span class="kw1">final</span> AvatarAnimationHelper animHelper<span class="sy0">;</span>
    <span class="kw1">private</span> <span class="kw1">final</span> PhysicsCharacter physicBody<span class="sy0">;</span>
<span class="co3">/**
 
    @param pial
    @param pc
    @param avatarMesh 
    */</span>
    <span class="kw1">public</span> AvatarAnimationEventListener<span class="br0">(</span>PlayerInputActionListener pial, PhysicsCharacter pc, Spatial avatarMesh<span class="br0">)</span>
    <span class="br0">{</span>
        <span class="kw1">this</span>.<span class="me1">pial</span> <span class="sy0">=</span> pial<span class="sy0">;</span>
        <span class="kw1">this</span>.<span class="me1">control</span> <span class="sy0">=</span> avatarMesh.<span class="me1">getControl</span><span class="br0">(</span>AnimControl.<span class="kw1">class</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="kw1">assert</span> <span class="br0">(</span><span class="kw1">this</span>.<span class="me1">control</span> <span class="sy0">!=</span> <span class="kw2">null</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="kw1">this</span>.<span class="me1">channel</span> <span class="sy0">=</span> <span class="kw1">this</span>.<span class="me1">control</span>.<span class="me1">createChannel</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="kw1">this</span>.<span class="me1">physicBody</span> <span class="sy0">=</span> pc<span class="sy0">;</span>
        <span class="kw1">this</span>.<span class="me1">animHelper</span> <span class="sy0">=</span> <span class="kw1">new</span> AvatarAnimationHelper<span class="br0">(</span><span class="kw1">this</span>.<span class="me1">physicBody</span>, <span class="kw1">this</span>.<span class="me1">channel</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    @Override
    <span class="kw1">public</span> <span class="kw4">void</span> initialize<span class="br0">(</span>AppStateManager stateManager, Application app<span class="br0">)</span>
    <span class="br0">{</span>
        <span class="kw1">this</span>.<span class="me1">control</span>.<span class="me1">addListener</span><span class="br0">(</span><span class="kw1">this</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="kw1">this</span>.<span class="me1">channel</span>.<span class="me1">setAnim</span><span class="br0">(</span><span class="st0">"Idle1"</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="kw1">this</span>.<span class="me1">channel</span>.<span class="me1">setSpeed</span><span class="br0">(</span>0.5f<span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    <span class="kw1">public</span> <span class="kw4">void</span> onAnimCycleDone<span class="br0">(</span>AnimControl control, AnimChannel channel, <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> animName<span class="br0">)</span>
    <span class="br0">{</span>
        <span class="co1">//throw new UnsupportedOperationException("Not supported yet."); //To change body of generated methods, choose Tools | Templates.</span>
    <span class="br0">}</span>
 
    <span class="kw1">public</span> <span class="kw4">void</span> onAnimChange<span class="br0">(</span>AnimControl control, AnimChannel channel, <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> animName<span class="br0">)</span>
    <span class="br0">{</span>
        <span class="co1">//throw new UnsupportedOperationException("Not supported yet."); //To change body of generated methods, choose Tools | Templates.</span>
 
    <span class="br0">}</span>
 
    <span class="co3">/**
     @return the channel
     */</span>
    <span class="kw1">protected</span> AnimChannel getChannel<span class="br0">(</span><span class="br0">)</span>
    <span class="br0">{</span>
        <span class="kw1">return</span> channel<span class="sy0">;</span>
    <span class="br0">}</span>
 
    <span class="co3">/**
     @return the control
     */</span>
    <span class="kw1">protected</span> AnimControl getControl<span class="br0">(</span><span class="br0">)</span>
    <span class="br0">{</span>
        <span class="kw1">return</span> control<span class="sy0">;</span>
    <span class="br0">}</span>
 
    <span class="co3">/**
     * @return the animHelper
     */</span>
    <span class="kw1">protected</span> AvatarAnimationHelper getAnimHelper<span class="br0">(</span><span class="br0">)</span>
    <span class="br0">{</span>
        <span class="kw1">return</span> animHelper<span class="sy0">;</span>
    <span class="br0">}</span>
<span class="br0">}</span></pre>

<p>
—AvatarAnimationHelper.java
</p>
<pre class="code java"><span class="kw1">package</span> <span class="co2">org.jmonkey3.chasecam</span><span class="sy0">;</span>
 
<span class="kw1">import</span> <span class="co2">com.jme3.animation.AnimChannel</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.animation.LoopMode</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.bullet.objects.PhysicsCharacter</span><span class="sy0">;</span>
 
<span class="coMULTI">/*
 Chase camera (aka 3rd person camera) example
 Based on official TestQ3.java
 
 @author Alex Cham aka Jcrypto
 */</span>
<span class="kw1">public</span> <span class="kw1">class</span> AvatarAnimationHelper
<span class="br0">{</span>
 
    <span class="kw1">private</span> <span class="kw1">final</span> AnimChannel animChannel<span class="sy0">;</span>
    <span class="kw1">private</span> <span class="kw1">final</span> PhysicsCharacter physicBody<span class="sy0">;</span>
<span class="co3">/**
 
    @param pc
    @param ac 
    */</span>
    <span class="kw1">public</span> AvatarAnimationHelper<span class="br0">(</span>PhysicsCharacter pc, AnimChannel ac<span class="br0">)</span>
    <span class="br0">{</span>
        <span class="kw1">this</span>.<span class="me1">animChannel</span> <span class="sy0">=</span> ac<span class="sy0">;</span>
        <span class="kw1">this</span>.<span class="me1">physicBody</span> <span class="sy0">=</span> pc<span class="sy0">;</span>
    <span class="br0">}</span>
 
    <span class="kw1">protected</span> <span class="kw4">void</span> idle<span class="br0">(</span><span class="br0">)</span>
    <span class="br0">{</span>
        animChannel.<span class="me1">setAnim</span><span class="br0">(</span><span class="st0">"Idle1"</span><span class="br0">)</span><span class="sy0">;</span>
        animChannel.<span class="me1">setSpeed</span><span class="br0">(</span>0.5f<span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    <span class="kw1">protected</span> <span class="kw4">boolean</span> forward<span class="br0">(</span><span class="kw4">boolean</span> pressed<span class="br0">)</span>
    <span class="br0">{</span>
        <span class="kw1">if</span> <span class="br0">(</span>pressed<span class="br0">)</span>
        <span class="br0">{</span>
            <span class="kw1">if</span> <span class="br0">(</span><span class="kw1">this</span>.<span class="me1">physicBody</span>.<span class="me1">onGround</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span>
            <span class="br0">{</span>
                animChannel.<span class="me1">setAnim</span><span class="br0">(</span><span class="st0">"Walk"</span><span class="br0">)</span><span class="sy0">;</span>
                animChannel.<span class="me1">setSpeed</span><span class="br0">(</span>AvatarConstants.<span class="me1">FORWARD_MOVE_SPEED</span> <span class="sy0">*</span> 2f<span class="br0">)</span><span class="sy0">;</span>
                animChannel.<span class="me1">setLoopMode</span><span class="br0">(</span>LoopMode.<span class="me1">Loop</span><span class="br0">)</span><span class="sy0">;</span>
            <span class="br0">}</span>
            <span class="kw1">return</span> <span class="kw2">true</span><span class="sy0">;</span>
        <span class="br0">}</span> <span class="kw1">else</span>
        <span class="br0">{</span>
            idle<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
            <span class="kw1">return</span> <span class="kw2">false</span><span class="sy0">;</span>
        <span class="br0">}</span>
        <span class="co1">//throw new UnsupportedOperationException("Not supported yet."); //To change body of generated methods, choose Tools | Templates.</span>
    <span class="br0">}</span>
 
    <span class="kw1">protected</span> <span class="kw4">boolean</span> backward<span class="br0">(</span><span class="kw4">boolean</span> pressed<span class="br0">)</span>
    <span class="br0">{</span>
        <span class="kw1">if</span> <span class="br0">(</span>pressed<span class="br0">)</span>
        <span class="br0">{</span>
            <span class="kw1">return</span> <span class="kw2">true</span><span class="sy0">;</span>
        <span class="br0">}</span> <span class="kw1">else</span>
        <span class="br0">{</span>
            <span class="kw1">return</span> <span class="kw2">false</span><span class="sy0">;</span>
        <span class="br0">}</span>
    <span class="br0">}</span>
 
    <span class="kw1">protected</span> <span class="kw4">boolean</span> rightward<span class="br0">(</span><span class="kw4">boolean</span> pressed<span class="br0">)</span>
    <span class="br0">{</span>
        <span class="kw1">if</span> <span class="br0">(</span>pressed<span class="br0">)</span>
        <span class="br0">{</span>
            <span class="kw1">return</span> <span class="kw2">true</span><span class="sy0">;</span>
        <span class="br0">}</span> <span class="kw1">else</span>
        <span class="br0">{</span>
            <span class="kw1">return</span> <span class="kw2">false</span><span class="sy0">;</span>
        <span class="br0">}</span>
    <span class="br0">}</span>
 
    <span class="kw1">protected</span> <span class="kw4">boolean</span> leftward<span class="br0">(</span><span class="kw4">boolean</span> pressed<span class="br0">)</span>
    <span class="br0">{</span>
        <span class="kw1">if</span> <span class="br0">(</span>pressed<span class="br0">)</span>
        <span class="br0">{</span>
            <span class="kw1">return</span> <span class="kw2">true</span><span class="sy0">;</span>
        <span class="br0">}</span> <span class="kw1">else</span>
        <span class="br0">{</span>
            <span class="kw1">return</span> <span class="kw2">false</span><span class="sy0">;</span>
        <span class="br0">}</span>
    <span class="br0">}</span>
 
    <span class="kw1">protected</span> <span class="kw4">boolean</span> jump<span class="br0">(</span><span class="kw4">boolean</span> pressed<span class="br0">)</span>
    <span class="br0">{</span>
            <span class="kw1">if</span> <span class="br0">(</span>pressed<span class="br0">)</span>
            <span class="br0">{</span>
                <span class="kw1">if</span> <span class="br0">(</span><span class="kw1">this</span>.<span class="me1">physicBody</span>.<span class="me1">onGround</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span>
                <span class="br0">{</span>
                    animChannel.<span class="me1">setAnim</span><span class="br0">(</span><span class="st0">"HighJump"</span><span class="br0">)</span><span class="sy0">;</span>
                    animChannel.<span class="me1">setSpeed</span><span class="br0">(</span>AvatarConstants.<span class="me1">FORWARD_MOVE_SPEED</span> <span class="sy0">/</span> 1.8f<span class="br0">)</span><span class="sy0">;</span>
                    animChannel.<span class="me1">setLoopMode</span><span class="br0">(</span>LoopMode.<span class="me1">DontLoop</span><span class="br0">)</span><span class="sy0">;</span>
                    <span class="co1">//</span>
                    <span class="kw1">this</span>.<span class="me1">physicBody</span>.<span class="me1">jump</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
                <span class="br0">}</span>
                <span class="kw1">return</span> <span class="kw2">true</span><span class="sy0">;</span>
            <span class="br0">}</span> <span class="kw1">else</span>
            <span class="br0">{</span>
                <span class="kw1">return</span> <span class="kw2">false</span><span class="sy0">;</span>
            <span class="br0">}</span>
    <span class="br0">}</span>
<span class="br0">}</span></pre>

<p>
—AvatarBodyManager.java
</p>
<pre class="code java"><span class="kw1">package</span> <span class="co2">org.jmonkey3.chasecam</span><span class="sy0">;</span>
 
<span class="kw1">import</span> <span class="co2">com.jme3.app.Application</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.app.state.AppStateManager</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.asset.AssetManager</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.bullet.control.BetterCharacterControl</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.bullet.objects.PhysicsCharacter</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.input.ChaseCamera</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.input.InputManager</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.renderer.Camera</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.Node</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">org.jmonkey.utils.Debug</span><span class="sy0">;</span>
 
<span class="coMULTI">/*
 Chase camera (aka 3rd person camera) example
 Based on official TestQ3.java
 
 @author Alex Cham aka Jcrypto
 */</span>
<span class="kw1">public</span> <span class="kw1">class</span> AvatarBodyManager <span class="kw1">extends</span> AbstractPhysicBodyContext
<span class="br0">{</span>
 
    <span class="kw1">private</span> InputManager inputManager<span class="sy0">;</span>
    <span class="kw1">private</span> <span class="kw1">final</span> Node rootNode<span class="sy0">;</span>
    <span class="co1">//</span>
    <span class="kw1">private</span> <span class="kw1">final</span> CameraContext cc<span class="sy0">;</span>
    <span class="kw1">private</span> <span class="kw1">final</span> Camera cam<span class="sy0">;</span>
    <span class="kw1">private</span> <span class="kw1">final</span> ChaseCamera chaseCam<span class="sy0">;</span>
    <span class="co1">//</span>
    <span class="kw1">private</span> <span class="kw1">final</span> AvatarPhysicBodyContext apbc<span class="sy0">;</span>
    <span class="kw1">private</span> <span class="kw1">final</span> AvatarSpatialBodyContext asbc<span class="sy0">;</span>
    <span class="co1">//</span>
    <span class="kw1">private</span> <span class="kw1">final</span> PhysicsCharacter physicBody<span class="sy0">;</span>
    <span class="kw1">private</span> <span class="kw1">final</span> Node avatar<span class="sy0">;</span>
    <span class="kw1">private</span> <span class="kw1">final</span> BetterCharacterControl bcc<span class="sy0">;</span>
    <span class="co1">//</span>
 
    <span class="kw1">private</span> <span class="kw1">final</span> PlayerInputActionListener playerInputListener<span class="sy0">;</span>
 
<span class="co3">/**
 
    @param am
    @param rootNode
    @param cc 
    */</span>
    <span class="kw1">public</span> AvatarBodyManager<span class="br0">(</span>AssetManager am, Node rootNode, CameraContext cc<span class="br0">)</span>
    <span class="br0">{</span>
 
        <span class="co1">//</span>
        <span class="kw1">this</span>.<span class="me1">rootNode</span> <span class="sy0">=</span> rootNode<span class="sy0">;</span>
        <span class="co1">//</span>
        <span class="kw1">this</span>.<span class="me1">asbc</span> <span class="sy0">=</span> <span class="kw1">new</span> AvatarSpatialBodyContext<span class="br0">(</span>am, rootNode<span class="br0">)</span><span class="sy0">;</span>
        <span class="kw1">this</span>.<span class="me1">apbc</span> <span class="sy0">=</span> <span class="kw1">new</span> AvatarPhysicBodyContext<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="co1">//</span>
        <span class="kw1">this</span>.<span class="me1">physicBody</span> <span class="sy0">=</span> apbc.<span class="me1">getPhysicBody</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
 
        <span class="kw1">this</span>.<span class="me1">avatar</span> <span class="sy0">=</span> asbc.<span class="me1">getAvatar</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="kw1">this</span>.<span class="me1">bcc</span> <span class="sy0">=</span> <span class="kw1">new</span> BetterCharacterControl<span class="br0">(</span>AvatarConstants.<span class="me1">COLLISION_SHAPE_RADIUS</span>, AvatarConstants.<span class="me1">COLLISION_SHAPE_RADIUS</span> <span class="sy0">*</span> <span class="nu0">2</span>, AvatarConstants.<span class="me1">PHYSIC_BODY_MASS</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="co1">//</span>
        <span class="kw1">this</span>.<span class="me1">playerInputListener</span> <span class="sy0">=</span> <span class="kw1">new</span> PlayerInputActionListener<span class="br0">(</span><span class="kw1">this</span>.<span class="me1">physicBody</span>, <span class="kw1">this</span>.<span class="me1">asbc</span>.<span class="me1">getAvatarMesh</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="co1">//</span>
        <span class="kw1">this</span>.<span class="me1">cc</span> <span class="sy0">=</span> cc<span class="sy0">;</span>
        <span class="kw1">this</span>.<span class="me1">cam</span> <span class="sy0">=</span> cc.<span class="me1">getCam</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="kw1">this</span>.<span class="me1">chaseCam</span> <span class="sy0">=</span> cc.<span class="me1">getChaseCam</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    @Override
    <span class="kw1">public</span> <span class="kw4">void</span> initialize<span class="br0">(</span>AppStateManager stateManager, Application app<span class="br0">)</span>
    <span class="br0">{</span>
        <span class="co1">//TODO: initialize your AppState, e.g. attach spatials to rootNode</span>
        <span class="co1">//this is called on the OpenGL thread after the AppState has been attached</span>
 
        stateManager.<span class="me1">attach</span><span class="br0">(</span><span class="kw1">this</span>.<span class="me1">asbc</span><span class="br0">)</span><span class="sy0">;</span>
        stateManager.<span class="me1">attach</span><span class="br0">(</span><span class="kw1">this</span>.<span class="me1">apbc</span><span class="br0">)</span><span class="sy0">;</span>
        stateManager.<span class="me1">attach</span><span class="br0">(</span><span class="kw1">this</span>.<span class="me1">playerInputListener</span><span class="br0">)</span><span class="sy0">;</span>
 
 
<span class="co1">//</span>
        <span class="kw1">this</span>.<span class="me1">avatar</span>.<span class="me1">addControl</span><span class="br0">(</span><span class="kw1">new</span> AvatarBodyMoveControl<span class="br0">(</span>playerInputListener, physicBody, cam<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="kw1">this</span>.<span class="me1">avatar</span>.<span class="me1">addControl</span><span class="br0">(</span>chaseCam<span class="br0">)</span><span class="sy0">;</span>
        <span class="kw1">this</span>.<span class="me1">avatar</span>.<span class="me1">addControl</span><span class="br0">(</span>bcc<span class="br0">)</span><span class="sy0">;</span>
 
        <span class="co1">//DEBUG</span>
        Debug.<span class="me1">showNodeAxes</span><span class="br0">(</span>app.<span class="me1">getAssetManager</span><span class="br0">(</span><span class="br0">)</span>, avatar, <span class="nu0">4</span><span class="br0">)</span><span class="sy0">;</span>
        getBulletAppState<span class="br0">(</span><span class="br0">)</span>.<span class="me1">getPhysicsSpace</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">enableDebug</span><span class="br0">(</span>app.<span class="me1">getAssetManager</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
 
 
    @Override
    <span class="kw1">public</span> <span class="kw4">void</span> update<span class="br0">(</span><span class="kw4">float</span> tpf<span class="br0">)</span>
    <span class="br0">{</span>
        <span class="co1">//assert (sceneCameraContext != null);</span>
 
        <span class="co1">//correctDirectionVectors(cam.getDirection(), cam.getLeft());</span>
 
    <span class="br0">}</span>
<span class="br0">}</span></pre>

<p>
—AvatarBodyMoveControl.java
</p>
<pre class="code java"><span class="kw1">package</span> <span class="co2">org.jmonkey3.chasecam</span><span class="sy0">;</span>
 
<span class="kw1">import</span> <span class="co2">com.jme3.bullet.control.BetterCharacterControl</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.bullet.objects.PhysicsCharacter</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.math.Vector3f</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.renderer.Camera</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.renderer.RenderManager</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.renderer.ViewPort</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.control.AbstractControl</span><span class="sy0">;</span>
 
<span class="coMULTI">/*
 Chase camera (aka 3rd person camera) example
 Based on official TestQ3.java
 
 @author Alex Cham aka Jcrypto
 */</span>
<span class="kw1">public</span> <span class="kw1">class</span> AvatarBodyMoveControl <span class="kw1">extends</span> AbstractControl
<span class="br0">{</span>
    <span class="kw1">private</span> <span class="kw1">final</span> Camera cam<span class="sy0">;</span>
    <span class="kw1">private</span> <span class="kw1">final</span> PhysicsCharacter physicBody<span class="sy0">;</span>
    <span class="kw1">private</span> <span class="kw1">final</span> PlayerInputActionListener pial<span class="sy0">;</span>
<span class="co3">/**
 
    @param pial
    @param physicBody
    @param cam 
    */</span>
    <span class="kw1">public</span> AvatarBodyMoveControl<span class="br0">(</span>PlayerInputActionListener pial, PhysicsCharacter physicBody, Camera cam<span class="br0">)</span>
    <span class="br0">{</span>
        <span class="kw1">this</span>.<span class="me1">pial</span> <span class="sy0">=</span> pial<span class="sy0">;</span>
        <span class="kw1">this</span>.<span class="me1">physicBody</span> <span class="sy0">=</span> physicBody<span class="sy0">;</span>
        <span class="kw1">this</span>.<span class="me1">cam</span> <span class="sy0">=</span> cam<span class="sy0">;</span>
    <span class="br0">}</span>
    <span class="kw1">private</span> <span class="kw1">final</span> Vector3f walkDirection <span class="sy0">=</span> <span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
 
    @Override
    <span class="kw1">protected</span> <span class="kw4">void</span> controlUpdate<span class="br0">(</span><span class="kw4">float</span> tpf<span class="br0">)</span>
    <span class="br0">{</span>
        <span class="co1">//throw new UnsupportedOperationException("Not supported yet."); //To change body of generated methods, choose Tools | Templates.</span>
        correctDirectionVectors<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    @Override
    <span class="kw1">protected</span> <span class="kw4">void</span> controlRender<span class="br0">(</span>RenderManager rm, ViewPort vp<span class="br0">)</span>
    <span class="br0">{</span>
        <span class="co1">//throw new UnsupportedOperationException("Not supported yet."); //To change body of generated methods, choose Tools | Templates.</span>
    <span class="br0">}</span>
 
 
        <span class="co3">/**
 
     @param camDir
     @param camLeft
     */</span>
    <span class="kw1">public</span> <span class="kw4">void</span> correctDirectionVectors<span class="br0">(</span><span class="br0">)</span>
    <span class="br0">{</span>
<span class="co1">//        assert (camDir != null);</span>
<span class="co1">//        assert (camLeft != null);</span>
<span class="co1">//        assert (walkDirection != null);</span>
        <span class="co1">//Affect forward, backward move speed 0.6f lower - 1.0f faster</span>
        Vector3f camDirVector <span class="sy0">=</span> cam.<span class="me1">getDirection</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">clone</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">multLocal</span><span class="br0">(</span>AvatarConstants.<span class="me1">FORWARD_MOVE_SPEED</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="co1">//Affect left, right move speed 0.6f lower - 1.0f faster</span>
        Vector3f camLeftVector <span class="sy0">=</span> cam.<span class="me1">getLeft</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">clone</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">multLocal</span><span class="br0">(</span>AvatarConstants.<span class="me1">SIDEWARD_MOVE_SPEED</span><span class="br0">)</span><span class="sy0">;</span>
 
        walkDirection.<span class="me1">set</span><span class="br0">(</span><span class="nu0">0</span>, <span class="nu0">0</span>, <span class="nu0">0</span><span class="br0">)</span><span class="sy0">;</span><span class="co1">//critical</span>
        <span class="kw1">if</span> <span class="br0">(</span>pial.<span class="me1">isLeftward</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span>
        <span class="br0">{</span>
            walkDirection.<span class="me1">addLocal</span><span class="br0">(</span>camLeftVector<span class="br0">)</span><span class="sy0">;</span>
        <span class="br0">}</span>
        <span class="kw1">if</span> <span class="br0">(</span>pial.<span class="me1">isRightward</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span>
        <span class="br0">{</span>
            walkDirection.<span class="me1">addLocal</span><span class="br0">(</span>camLeftVector.<span class="me1">negate</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="br0">}</span>
        <span class="kw1">if</span> <span class="br0">(</span>pial.<span class="me1">isForward</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span>
        <span class="br0">{</span>
            walkDirection.<span class="me1">addLocal</span><span class="br0">(</span>camDirVector<span class="br0">)</span><span class="sy0">;</span>
        <span class="br0">}</span>
        <span class="kw1">if</span> <span class="br0">(</span>pial.<span class="me1">isBackward</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span>
        <span class="br0">{</span>
            <span class="co1">//@TODO Bug if cam direction (0, -n, 0) - character fly upwards ;)</span>
            walkDirection.<span class="me1">addLocal</span><span class="br0">(</span>camDirVector.<span class="me1">negate</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="br0">}</span>
        physicBody.<span class="me1">setWalkDirection</span><span class="br0">(</span>walkDirection<span class="br0">)</span><span class="sy0">;</span><span class="co1">//Critical</span>
 
 
 
        <span class="co1">//Avoid vibration</span>
        spatial.<span class="me1">setLocalTranslation</span><span class="br0">(</span>physicBody.<span class="me1">getPhysicsLocation</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="co1">//Translate Node accordingly</span>
        spatial.<span class="me1">getControl</span><span class="br0">(</span>BetterCharacterControl.<span class="kw1">class</span><span class="br0">)</span>.<span class="me1">warp</span><span class="br0">(</span>physicBody.<span class="me1">getPhysicsLocation</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="co1">//Rotate Node accordingly to camera</span>
        spatial.<span class="me1">getControl</span><span class="br0">(</span>
                BetterCharacterControl.<span class="kw1">class</span><span class="br0">)</span>.<span class="me1">setViewDirection</span><span class="br0">(</span>
                cam.<span class="me1">getDirection</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">negate</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
 
    <span class="br0">}</span>
<span class="br0">}</span></pre>

<p>
—AvatarConstants.java
</p>
<pre class="code java"><span class="kw1">package</span> <span class="co2">org.jmonkey3.chasecam</span><span class="sy0">;</span>
 
<span class="coMULTI">/*
 Chase camera (aka 3rd person camera) example
 Based on official TestQ3.java
 
 @author Alex Cham aka Jcrypto
 */</span>
<span class="kw1">public</span> <span class="kw1">class</span> AvatarConstants
<span class="br0">{</span>
    <span class="kw1">public</span> <span class="kw1">static</span> <span class="kw1">final</span> <span class="kw4">float</span> COLLISION_SHAPE_CENTERAL_POINT <span class="sy0">=</span> 0.0f<span class="sy0">;</span>
    <span class="kw1">public</span> <span class="kw1">static</span> <span class="kw1">final</span> <span class="kw4">float</span> COLLISION_SHAPE_RADIUS <span class="sy0">=</span> 4.0f<span class="sy0">;</span>
    <span class="co1">//</span>
    <span class="kw1">public</span> <span class="kw1">static</span> <span class="kw1">final</span> <span class="kw4">float</span> PHYSIC_BODY_MASS <span class="sy0">=</span> 1.0f<span class="sy0">;</span>
    <span class="kw1">public</span> <span class="kw1">static</span> <span class="kw4">float</span> FORWARD_MOVE_SPEED <span class="sy0">=</span> 0.8f<span class="sy0">;</span>
    <span class="kw1">public</span> <span class="kw1">static</span> <span class="kw4">float</span> SIDEWARD_MOVE_SPEED <span class="sy0">=</span> 0.6f<span class="sy0">;</span>
<span class="br0">}</span></pre>

<p>
—AvatarPhysicBodyContext.java
</p>
<pre class="code java"><span class="kw1">package</span> <span class="co2">org.jmonkey3.chasecam</span><span class="sy0">;</span>
 
<span class="kw1">import</span> <span class="co2">com.jme3.app.Application</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.app.state.AppStateManager</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.bullet.collision.shapes.SphereCollisionShape</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.bullet.objects.PhysicsCharacter</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.math.Vector3f</span><span class="sy0">;</span>
 
<span class="coMULTI">/*
 Chase camera (aka 3rd person camera) example
 Based on official TestQ3.java
 
 @author Alex Cham aka Jcrypto
 */</span>
<span class="kw1">public</span> <span class="kw1">class</span> AvatarPhysicBodyContext <span class="kw1">extends</span> AbstractPhysicBodyContext
<span class="br0">{</span>
 
 
 
    <span class="kw1">private</span> <span class="kw1">final</span> PhysicsCharacter physicBody<span class="sy0">;</span>
 
 
    <span class="kw1">public</span> AvatarPhysicBodyContext<span class="br0">(</span><span class="br0">)</span>
    <span class="br0">{</span>
 
        <span class="kw1">this</span>.<span class="me1">physicBody</span> <span class="sy0">=</span> <span class="kw1">new</span> PhysicsCharacter<span class="br0">(</span><span class="kw1">new</span> SphereCollisionShape<span class="br0">(</span>AvatarConstants.<span class="me1">COLLISION_SHAPE_RADIUS</span><span class="br0">)</span>, .01f<span class="br0">)</span><span class="sy0">;</span>
 
    <span class="br0">}</span>
 
 
 
    @Override
    <span class="kw1">public</span> <span class="kw4">void</span> initialize<span class="br0">(</span>AppStateManager stateManager, Application app<span class="br0">)</span>
    <span class="br0">{</span>
<span class="co1">//</span>
        <span class="kw1">assert</span> <span class="br0">(</span>getBulletAppState<span class="br0">(</span><span class="br0">)</span> <span class="sy0">!=</span> <span class="kw2">null</span><span class="br0">)</span><span class="sy0">;</span>
        <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+system"><span class="kw3">System</span></a>.<span class="me1">out</span>.<span class="me1">println</span><span class="br0">(</span><span class="kw1">this</span>.<span class="me1">getClass</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">getName</span><span class="br0">(</span><span class="br0">)</span> <span class="sy0">+</span> <span class="st0">".getBulletAppState().hashCode() = "</span> <span class="sy0">+</span> getBulletAppState<span class="br0">(</span><span class="br0">)</span>.<span class="me1">hashCode</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
 
<span class="co1">//</span>
        <span class="kw1">this</span>.<span class="me1">physicBody</span>.<span class="me1">setJumpSpeed</span><span class="br0">(</span><span class="nu0">32</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="kw1">this</span>.<span class="me1">physicBody</span>.<span class="me1">setFallSpeed</span><span class="br0">(</span><span class="nu0">32</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="kw1">this</span>.<span class="me1">physicBody</span>.<span class="me1">setGravity</span><span class="br0">(</span><span class="nu0">32</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="kw1">this</span>.<span class="me1">physicBody</span>.<span class="me1">setPhysicsLocation</span><span class="br0">(</span><span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">0</span>, <span class="nu0">10</span>, <span class="nu0">0</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="co1">//</span>
        getBulletAppState<span class="br0">(</span><span class="br0">)</span>.<span class="me1">getPhysicsSpace</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">add</span><span class="br0">(</span><span class="kw1">this</span>.<span class="me1">physicBody</span><span class="br0">)</span><span class="sy0">;</span>
 
    <span class="br0">}</span>
 
    @Override
    <span class="kw1">public</span> <span class="kw4">void</span> update<span class="br0">(</span><span class="kw4">float</span> tpf<span class="br0">)</span>
    <span class="br0">{</span>
    <span class="br0">}</span>
 
    @Override
    <span class="kw1">public</span> <span class="kw4">void</span> cleanup<span class="br0">(</span><span class="br0">)</span>
    <span class="br0">{</span>
        <span class="kw1">super</span>.<span class="me1">cleanup</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    <span class="co3">/**
     @return the physicBody
     */</span>
    <span class="kw1">public</span> PhysicsCharacter getPhysicBody<span class="br0">(</span><span class="br0">)</span>
    <span class="br0">{</span>
        <span class="kw1">return</span> <span class="kw1">this</span>.<span class="me1">physicBody</span><span class="sy0">;</span>
    <span class="br0">}</span>
<span class="br0">}</span></pre>

<p>
—AvatarSpatialBodyContext.java
</p>
<pre class="code java"><span class="kw1">package</span> <span class="co2">org.jmonkey3.chasecam</span><span class="sy0">;</span>
 
<span class="kw1">import</span> <span class="co2">com.jme3.app.Application</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.app.state.AppStateManager</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.asset.AssetManager</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.math.Vector3f</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.Node</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.Spatial</span><span class="sy0">;</span>
 
<span class="coMULTI">/*
 Chase camera (aka 3rd person camera) example
 Based on official TestQ3.java
 
 @author Alex Cham aka Jcrypto
 */</span>
<span class="kw1">public</span> <span class="kw1">class</span> AvatarSpatialBodyContext <span class="kw1">extends</span> AbstractSpatialBodyContext
<span class="br0">{</span>
 
    <span class="co1">//</span>
    <span class="kw1">private</span> <span class="kw1">final</span> Node rootNode<span class="sy0">;</span>
    <span class="co1">//</span>
    <span class="kw1">private</span> <span class="kw1">final</span> Node avatar<span class="sy0">;</span>
    <span class="kw1">private</span> <span class="kw1">final</span> Spatial avatarMesh<span class="sy0">;</span>
    <span class="kw1">private</span> <span class="kw1">final</span> Vector3f correction<span class="sy0">;</span>
<span class="co3">/**
 
    @param am
    @param rootNode 
    */</span>    
    <span class="kw1">public</span> AvatarSpatialBodyContext<span class="br0">(</span>AssetManager am, Node rootNode<span class="br0">)</span>
    <span class="br0">{</span>
        <span class="kw1">this</span>.<span class="me1">rootNode</span> <span class="sy0">=</span> rootNode<span class="sy0">;</span>
        <span class="co1">//</span>
        <span class="kw1">this</span>.<span class="me1">avatar</span> <span class="sy0">=</span> <span class="kw1">new</span> Node<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="kw1">this</span>.<span class="me1">avatarMesh</span> <span class="sy0">=</span> am.<span class="me1">loadModel</span><span class="br0">(</span><span class="st0">"Models/Ninja/Ninja.mesh.xml"</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="kw1">this</span>.<span class="me1">correction</span> <span class="sy0">=</span> <span class="kw1">new</span> Vector3f<span class="br0">(</span>
                <span class="nu0">0</span>,
                AvatarConstants.<span class="me1">COLLISION_SHAPE_CENTERAL_POINT</span> <span class="sy0">-</span> AvatarConstants.<span class="me1">COLLISION_SHAPE_RADIUS</span>,
                <span class="nu0">0</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    @Override
    <span class="kw1">public</span> <span class="kw4">void</span> initialize<span class="br0">(</span>AppStateManager stateManager, Application app<span class="br0">)</span>
    <span class="br0">{</span>
 
 
        <span class="kw1">this</span>.<span class="me1">avatarMesh</span>.<span class="me1">setLocalScale</span><span class="br0">(</span><span class="kw1">new</span> Vector3f<span class="br0">(</span>0.05f, 0.05f, 0.05f<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span><span class="co1">//Trouble with scales?</span>
        <span class="kw1">this</span>.<span class="me1">avatarMesh</span>.<span class="me1">setLocalTranslation</span><span class="br0">(</span><span class="kw1">this</span>.<span class="me1">correction</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="kw1">this</span>.<span class="me1">avatar</span>.<span class="me1">attachChild</span><span class="br0">(</span><span class="kw1">this</span>.<span class="me1">avatarMesh</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="kw1">this</span>.<span class="me1">rootNode</span>.<span class="me1">attachChild</span><span class="br0">(</span><span class="kw1">this</span>.<span class="me1">avatar</span><span class="br0">)</span><span class="sy0">;</span>
 
        <span class="co1">//super.initialize(stateManager, app); //To change body of generated methods, choose Tools | Templates.</span>
    <span class="br0">}</span>
 
    <span class="co3">/**
     @return the avatar
     */</span>
    <span class="kw1">public</span> Node getAvatar<span class="br0">(</span><span class="br0">)</span>
    <span class="br0">{</span>
        <span class="kw1">return</span> avatar<span class="sy0">;</span>
    <span class="br0">}</span>
 
    <span class="co3">/**
     * @return the avatarMesh
     */</span>
    <span class="kw1">public</span> Spatial getAvatarMesh<span class="br0">(</span><span class="br0">)</span>
    <span class="br0">{</span>
        <span class="kw1">return</span> avatarMesh<span class="sy0">;</span>
    <span class="br0">}</span>
<span class="br0">}</span></pre>

<p>
—CameraContext.java
</p>
<pre class="code java"><span class="kw1">package</span> <span class="co2">org.jmonkey3.chasecam</span><span class="sy0">;</span>
 
<span class="kw1">import</span> <span class="co2">com.jme3.app.Application</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.app.state.AbstractAppState</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.app.state.AppStateManager</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.input.ChaseCamera</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.input.FlyByCamera</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.input.InputManager</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.renderer.Camera</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.system.AppSettings</span><span class="sy0">;</span>
 
<span class="coMULTI">/*
 Chase camera (aka 3rd person camera) example
 Based on official TestQ3.java
 
 @author Alex Cham aka Jcrypto
 */</span>
<span class="kw1">public</span> <span class="kw1">class</span> CameraContext <span class="kw1">extends</span> AbstractAppState
<span class="br0">{</span>
 
    <span class="kw1">private</span> <span class="kw1">final</span> AppSettings settings<span class="sy0">;</span>
    <span class="kw1">private</span> <span class="kw1">final</span> InputManager inputManager<span class="sy0">;</span>
    <span class="coMULTI">/*
     http://hub.jmonkeyengine.org/javadoc/com/jme3/renderer/Camera.html
     public class Camera
     extends java.lang.Object
     implements Savable, java.lang.Cloneable
 
     Width and height are set to the current Application's settings.getWidth() and settings.getHeight() values.
     Frustum Perspective:
     Frame of view angle of 45Â° along the Y axis
     Aspect ratio of width divided by height
     Near view plane of 1 wu
     Far view plane of 1000 wu
     Start location at (0f, 0f, 10f).
     Start direction is looking at the origin.
     */</span>
    <span class="kw1">private</span> <span class="kw1">final</span> Camera cam<span class="sy0">;</span>
    <span class="coMULTI">/*
     http://hub.jmonkeyengine.org/javadoc/com/jme3/input/ChaseCamera.html
     public class ChaseCamera
     extends java.lang.Object
     implements ActionListener, AnalogListener, Control
 
     A camera that follows a spatial and can turn around it by dragging the mouse
     Constructs the chase camera, and registers inputs if you use this 
     constructor you have to attach the cam later to a spatial doing 
     spatial.addControl(chaseCamera);
     */</span>
    <span class="kw1">private</span> <span class="kw1">final</span> ChaseCamera chaseCam<span class="sy0">;</span>
    <span class="kw1">private</span> <span class="kw1">final</span> FlyByCamera flyByCam<span class="sy0">;</span>
 
<span class="co3">/**
 
    @param settings
    @param inputManager
    @param cam
    @param flyByCam 
    */</span>
    <span class="kw1">public</span> CameraContext<span class="br0">(</span>AppSettings settings, InputManager inputManager, Camera cam, FlyByCamera flyByCam<span class="br0">)</span>
    <span class="br0">{</span>
 
        <span class="kw1">assert</span> <span class="br0">(</span>settings <span class="sy0">!=</span> <span class="kw2">null</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="kw1">this</span>.<span class="me1">settings</span> <span class="sy0">=</span> settings<span class="sy0">;</span>
        <span class="kw1">assert</span> <span class="br0">(</span>inputManager <span class="sy0">!=</span> <span class="kw2">null</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="kw1">this</span>.<span class="me1">inputManager</span> <span class="sy0">=</span> inputManager<span class="sy0">;</span>
        <span class="kw1">assert</span> <span class="br0">(</span>cam <span class="sy0">!=</span> <span class="kw2">null</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="kw1">this</span>.<span class="me1">cam</span> <span class="sy0">=</span> cam<span class="sy0">;</span>
        <span class="kw1">assert</span> <span class="br0">(</span>flyByCam <span class="sy0">!=</span> <span class="kw2">null</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="kw1">this</span>.<span class="me1">flyByCam</span> <span class="sy0">=</span> flyByCam<span class="sy0">;</span>
        <span class="kw1">this</span>.<span class="me1">chaseCam</span> <span class="sy0">=</span> <span class="kw1">new</span> ChaseCamera<span class="br0">(</span><span class="kw1">this</span>.<span class="me1">cam</span>, <span class="kw1">this</span>.<span class="me1">inputManager</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    @Override
    <span class="kw1">public</span> <span class="kw4">void</span> initialize<span class="br0">(</span>AppStateManager stateManager, Application app<span class="br0">)</span>
    <span class="br0">{</span>
        <span class="kw1">super</span>.<span class="me1">initialize</span><span class="br0">(</span>stateManager, app<span class="br0">)</span><span class="sy0">;</span>
        <span class="co1">//TODO: initialize your AppState, e.g. attach spatials to rootNode</span>
        <span class="co1">//this is called on the OpenGL thread after the AppState has been attached</span>
 
        <span class="kw1">this</span>.<span class="me1">cam</span>.<span class="me1">setFrustumPerspective</span><span class="br0">(</span>116.0f, <span class="br0">(</span>settings.<span class="me1">getWidth</span><span class="br0">(</span><span class="br0">)</span> <span class="sy0">/</span> settings.<span class="me1">getHeight</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span>, 1.0f, 2000.0f<span class="br0">)</span><span class="sy0">;</span>
        <span class="co1">//this.flyByCam.setMoveSpeed(100);</span>
        <span class="kw1">this</span>.<span class="me1">flyByCam</span>.<span class="me1">setEnabled</span><span class="br0">(</span><span class="kw2">false</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    <span class="co3">/**
     @return the cam
     */</span>
    <span class="kw1">public</span> Camera getCam<span class="br0">(</span><span class="br0">)</span>
    <span class="br0">{</span>
        <span class="kw1">return</span> cam<span class="sy0">;</span>
    <span class="br0">}</span>
 
    <span class="co3">/**
     @return the chaseCam
     */</span>
    <span class="kw1">public</span> ChaseCamera getChaseCam<span class="br0">(</span><span class="br0">)</span>
    <span class="br0">{</span>
        <span class="kw1">return</span> chaseCam<span class="sy0">;</span>
    <span class="br0">}</span>
<span class="br0">}</span></pre>

<p>
—PlayerInputActionListener.java
</p>
<pre class="code java"><span class="kw1">package</span> <span class="co2">org.jmonkey3.chasecam</span><span class="sy0">;</span>
 
<span class="kw1">import</span> <span class="co2">com.jme3.app.Application</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.app.state.AbstractAppState</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.app.state.AppStateManager</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.bullet.objects.PhysicsCharacter</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.input.KeyInput</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.input.controls.ActionListener</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.input.controls.KeyTrigger</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.Spatial</span><span class="sy0">;</span>
 
<span class="coMULTI">/*
 Chase camera (aka 3rd person camera) example
 Based on official TestQ3.java
 
 @author Alex Cham aka Jcrypto
 */</span>
<span class="kw1">public</span> <span class="kw1">class</span> PlayerInputActionListener <span class="kw1">extends</span> AbstractAppState <span class="kw1">implements</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+actionlistener"><span class="kw3">ActionListener</span></a>
<span class="br0">{</span>
 
    <span class="kw1">private</span> <span class="kw1">final</span> PhysicsCharacter physicBody<span class="sy0">;</span>
<span class="co1">//</span>
    <span class="kw1">private</span> <span class="kw4">boolean</span> leftward <span class="sy0">=</span> <span class="kw2">false</span><span class="sy0">;</span>
    <span class="kw1">private</span> <span class="kw4">boolean</span> rightward <span class="sy0">=</span> <span class="kw2">false</span><span class="sy0">;</span>
    <span class="kw1">private</span> <span class="kw4">boolean</span> forward <span class="sy0">=</span> <span class="kw2">false</span><span class="sy0">;</span>
    <span class="kw1">private</span> <span class="kw4">boolean</span> backward <span class="sy0">=</span> <span class="kw2">false</span><span class="sy0">;</span>
    <span class="kw1">private</span> <span class="kw4">boolean</span> jump <span class="sy0">=</span> <span class="kw2">false</span><span class="sy0">;</span>
    <span class="kw1">private</span> <span class="kw1">final</span> AvatarAnimationEventListener aael<span class="sy0">;</span>
<span class="co3">/**
 
    @param pc
    @param avatar 
    */</span>
    <span class="kw1">public</span> PlayerInputActionListener<span class="br0">(</span>PhysicsCharacter pc, Spatial avatar<span class="br0">)</span>
    <span class="br0">{</span>
        <span class="kw1">this</span>.<span class="me1">physicBody</span> <span class="sy0">=</span> pc<span class="sy0">;</span>
        <span class="kw1">this</span>.<span class="me1">aael</span> <span class="sy0">=</span> <span class="kw1">new</span> AvatarAnimationEventListener<span class="br0">(</span><span class="kw1">this</span>, <span class="kw1">this</span>.<span class="me1">physicBody</span>, avatar<span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    @Override
    <span class="kw1">public</span> <span class="kw4">void</span> initialize<span class="br0">(</span>AppStateManager stateManager, Application app<span class="br0">)</span>
    <span class="br0">{</span>
        stateManager.<span class="me1">attach</span><span class="br0">(</span><span class="kw1">this</span>.<span class="me1">aael</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="co1">//</span>
        app.<span class="me1">getInputManager</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">addMapping</span><span class="br0">(</span><span class="st0">"LEFTWARD"</span>, <span class="kw1">new</span> KeyTrigger<span class="br0">(</span>KeyInput.<span class="me1">KEY_A</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
        app.<span class="me1">getInputManager</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">addMapping</span><span class="br0">(</span><span class="st0">"RIGHTWARD"</span>, <span class="kw1">new</span> KeyTrigger<span class="br0">(</span>KeyInput.<span class="me1">KEY_D</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
        app.<span class="me1">getInputManager</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">addMapping</span><span class="br0">(</span><span class="st0">"FORWARD"</span>, <span class="kw1">new</span> KeyTrigger<span class="br0">(</span>KeyInput.<span class="me1">KEY_W</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
        app.<span class="me1">getInputManager</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">addMapping</span><span class="br0">(</span><span class="st0">"BACKWARD"</span>, <span class="kw1">new</span> KeyTrigger<span class="br0">(</span>KeyInput.<span class="me1">KEY_S</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
        app.<span class="me1">getInputManager</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">addMapping</span><span class="br0">(</span><span class="st0">"JUMP"</span>, <span class="kw1">new</span> KeyTrigger<span class="br0">(</span>KeyInput.<span class="me1">KEY_SPACE</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
        app.<span class="me1">getInputManager</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">addListener</span><span class="br0">(</span><span class="kw1">this</span>, <span class="st0">"LEFTWARD"</span><span class="br0">)</span><span class="sy0">;</span>
        app.<span class="me1">getInputManager</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">addListener</span><span class="br0">(</span><span class="kw1">this</span>, <span class="st0">"RIGHTWARD"</span><span class="br0">)</span><span class="sy0">;</span>
        app.<span class="me1">getInputManager</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">addListener</span><span class="br0">(</span><span class="kw1">this</span>, <span class="st0">"FORWARD"</span><span class="br0">)</span><span class="sy0">;</span>
        app.<span class="me1">getInputManager</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">addListener</span><span class="br0">(</span><span class="kw1">this</span>, <span class="st0">"BACKWARD"</span><span class="br0">)</span><span class="sy0">;</span>
        app.<span class="me1">getInputManager</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">addListener</span><span class="br0">(</span><span class="kw1">this</span>, <span class="st0">"JUMP"</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="co1">//</span>
    <span class="br0">}</span>
 
    <span class="co3">/**
     @param binding
     @param keyPressed
     @param tpf
     */</span>
    <span class="kw1">public</span> <span class="kw4">void</span> onAction<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> binding, <span class="kw4">boolean</span> keyPressed, <span class="kw4">float</span> tpf<span class="br0">)</span>
    <span class="br0">{</span>
 
        <span class="kw1">if</span> <span class="br0">(</span>binding.<span class="me1">equals</span><span class="br0">(</span><span class="st0">"LEFTWARD"</span><span class="br0">)</span><span class="br0">)</span>
        <span class="br0">{</span>
 
            <span class="kw1">this</span>.<span class="me1">leftward</span> <span class="sy0">=</span> <span class="kw1">this</span>.<span class="me1">aael</span>.<span class="me1">getAnimHelper</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">leftward</span><span class="br0">(</span>keyPressed<span class="br0">)</span><span class="sy0">;</span>
 
        <span class="br0">}</span> <span class="kw1">else</span> <span class="kw1">if</span> <span class="br0">(</span>binding.<span class="me1">equals</span><span class="br0">(</span><span class="st0">"RIGHTWARD"</span><span class="br0">)</span><span class="br0">)</span>
        <span class="br0">{</span>
 
            <span class="kw1">this</span>.<span class="me1">rightward</span> <span class="sy0">=</span> <span class="kw1">this</span>.<span class="me1">aael</span>.<span class="me1">getAnimHelper</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">rightward</span><span class="br0">(</span>keyPressed<span class="br0">)</span><span class="sy0">;</span>
 
        <span class="br0">}</span> <span class="kw1">else</span> <span class="kw1">if</span> <span class="br0">(</span>binding.<span class="me1">equals</span><span class="br0">(</span><span class="st0">"FORWARD"</span><span class="br0">)</span><span class="br0">)</span>
        <span class="br0">{</span>
 
            <span class="kw1">this</span>.<span class="me1">forward</span> <span class="sy0">=</span> <span class="kw1">this</span>.<span class="me1">aael</span>.<span class="me1">getAnimHelper</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">forward</span><span class="br0">(</span>keyPressed<span class="br0">)</span><span class="sy0">;</span>
 
        <span class="br0">}</span> <span class="kw1">else</span> <span class="kw1">if</span> <span class="br0">(</span>binding.<span class="me1">equals</span><span class="br0">(</span><span class="st0">"BACKWARD"</span><span class="br0">)</span><span class="br0">)</span>
        <span class="br0">{</span>
 
                <span class="kw1">this</span>.<span class="me1">backward</span> <span class="sy0">=</span> <span class="kw1">this</span>.<span class="me1">aael</span>.<span class="me1">getAnimHelper</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">backward</span><span class="br0">(</span>keyPressed<span class="br0">)</span><span class="sy0">;</span>
 
        <span class="br0">}</span> <span class="kw1">else</span> <span class="kw1">if</span> <span class="br0">(</span>binding.<span class="me1">equals</span><span class="br0">(</span><span class="st0">"JUMP"</span><span class="br0">)</span><span class="br0">)</span>
        <span class="br0">{</span>
 
            <span class="kw1">this</span>.<span class="me1">jump</span> <span class="sy0">=</span> <span class="kw1">this</span>.<span class="me1">aael</span>.<span class="me1">getAnimHelper</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">jump</span><span class="br0">(</span>keyPressed<span class="br0">)</span><span class="sy0">;</span>
 
        <span class="br0">}</span>
    <span class="br0">}</span>
 
    <span class="co3">/**
     @return the leftward
     */</span>
    <span class="kw1">public</span> <span class="kw4">boolean</span> isLeftward<span class="br0">(</span><span class="br0">)</span>
    <span class="br0">{</span>
        <span class="kw1">return</span> <span class="kw1">this</span>.<span class="me1">leftward</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    <span class="co3">/**
     @return the rightward
     */</span>
    <span class="kw1">public</span> <span class="kw4">boolean</span> isRightward<span class="br0">(</span><span class="br0">)</span>
    <span class="br0">{</span>
        <span class="kw1">return</span> <span class="kw1">this</span>.<span class="me1">rightward</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    <span class="co3">/**
     @return the forward
     */</span>
    <span class="kw1">public</span> <span class="kw4">boolean</span> isForward<span class="br0">(</span><span class="br0">)</span>
    <span class="br0">{</span>
        <span class="kw1">return</span> <span class="kw1">this</span>.<span class="me1">forward</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    <span class="co3">/**
     @return the backward
     */</span>
    <span class="kw1">public</span> <span class="kw4">boolean</span> isBackward<span class="br0">(</span><span class="br0">)</span>
    <span class="br0">{</span>
        <span class="kw1">return</span> <span class="kw1">this</span>.<span class="me1">backward</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    <span class="co3">/**
     @return the jump
     */</span>
    <span class="kw1">public</span> <span class="kw4">boolean</span> isJump<span class="br0">(</span><span class="br0">)</span>
    <span class="br0">{</span>
        <span class="kw1">return</span> <span class="kw1">this</span>.<span class="me1">jump</span><span class="sy0">;</span>
    <span class="br0">}</span>
<span class="br0">}</span></pre>

<p>
—SceneBodyManager.java
</p>
<pre class="code java"><span class="kw1">package</span> <span class="co2">org.jmonkey3.chasecam</span><span class="sy0">;</span>
 
<span class="kw1">import</span> <span class="co2">com.jme3.app.Application</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.app.state.AppStateManager</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.asset.AssetManager</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.Node</span><span class="sy0">;</span>
 
<span class="coMULTI">/*
 Chase camera (aka 3rd person camera) example
 Based on official TestQ3.java
 
 @author Alex Cham aka Jcrypto
 */</span>
<span class="kw1">public</span> <span class="kw1">class</span> SceneBodyManager <span class="kw1">extends</span> AbstractPhysicBodyContext
<span class="br0">{</span>
 
    <span class="kw1">private</span> <span class="kw1">final</span> ScenePhysicBodyContext spbc<span class="sy0">;</span>
    <span class="kw1">private</span> <span class="kw1">final</span> SceneSpatialBodyContext ssbc<span class="sy0">;</span>
 
<span class="co3">/**
 
    @param stateManager
    @param am
    @param rootNode 
    */</span>
    <span class="kw1">public</span> SceneBodyManager<span class="br0">(</span>AppStateManager stateManager, AssetManager am, Node rootNode<span class="br0">)</span>
    <span class="br0">{</span>
 
 
        <span class="kw1">this</span>.<span class="me1">ssbc</span> <span class="sy0">=</span> <span class="kw1">new</span> SceneSpatialBodyContext<span class="br0">(</span>am, rootNode<span class="br0">)</span><span class="sy0">;</span>
        <span class="kw1">this</span>.<span class="me1">spbc</span> <span class="sy0">=</span> <span class="kw1">new</span> ScenePhysicBodyContext<span class="br0">(</span>ssbc.<span class="me1">getScene</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    @Override
    <span class="kw1">public</span> <span class="kw4">void</span> initialize<span class="br0">(</span>AppStateManager stateManager, Application app<span class="br0">)</span>
    <span class="br0">{</span>
 
        <span class="co1">//PhysicsSpace Initialization</span>
        attachBulletAppstate<span class="br0">(</span>stateManager<span class="br0">)</span><span class="sy0">;</span>
<span class="co1">//</span>
        stateManager.<span class="me1">attach</span><span class="br0">(</span><span class="kw1">this</span>.<span class="me1">ssbc</span><span class="br0">)</span><span class="sy0">;</span>
        stateManager.<span class="me1">attach</span><span class="br0">(</span><span class="kw1">this</span>.<span class="me1">spbc</span><span class="br0">)</span><span class="sy0">;</span>
 
    <span class="br0">}</span>
<span class="br0">}</span></pre>

<p>
—ScenePhysicBodyContext.java
</p>
<pre class="code java"><span class="kw1">package</span> <span class="co2">org.jmonkey3.chasecam</span><span class="sy0">;</span>
 
<span class="kw1">import</span> <span class="co2">com.jme3.app.Application</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.app.state.AppStateManager</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.bullet.control.RigidBodyControl</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.Node</span><span class="sy0">;</span>
 
<span class="coMULTI">/*
 Chase camera (aka 3rd person camera) example
 Based on official TestQ3.java
 
 @author Alex Cham aka Jcrypto
 */</span>
<span class="kw1">public</span> <span class="kw1">class</span> ScenePhysicBodyContext <span class="kw1">extends</span> AbstractPhysicBodyContext
<span class="br0">{</span>
    <span class="kw1">private</span> <span class="kw1">final</span> RigidBodyControl rigidBodyControl<span class="sy0">;</span>
    <span class="kw1">private</span> <span class="kw1">final</span> Node scene<span class="sy0">;</span>
 
<span class="co3">/**
 
    @param scene 
    */</span>
    <span class="kw1">public</span> ScenePhysicBodyContext<span class="br0">(</span>Node scene<span class="br0">)</span>
    <span class="br0">{</span>
        <span class="kw1">this</span>.<span class="me1">scene</span> <span class="sy0">=</span> scene<span class="sy0">;</span>
        <span class="kw1">this</span>.<span class="me1">rigidBodyControl</span> <span class="sy0">=</span> <span class="kw1">new</span> RigidBodyControl<span class="br0">(</span>.0f<span class="br0">)</span><span class="sy0">;</span>       
    <span class="br0">}</span>
 
 
    @Override
    <span class="kw1">public</span> <span class="kw4">void</span> initialize<span class="br0">(</span>AppStateManager stateManager, Application app<span class="br0">)</span>
    <span class="br0">{</span>
        <span class="co1">//</span>
        <span class="co1">//Add scene to PhysicsSpace</span>
        <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+system"><span class="kw3">System</span></a>.<span class="me1">out</span>.<span class="me1">println</span><span class="br0">(</span><span class="kw1">this</span>.<span class="me1">getClass</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">getName</span><span class="br0">(</span><span class="br0">)</span> <span class="sy0">+</span> <span class="st0">".getBulletAppState().hashCode() = "</span> <span class="sy0">+</span> getBulletAppState<span class="br0">(</span><span class="br0">)</span>.<span class="me1">hashCode</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
        scene.<span class="me1">addControl</span><span class="br0">(</span>rigidBodyControl<span class="br0">)</span><span class="sy0">;</span>
        getBulletAppState<span class="br0">(</span><span class="br0">)</span>.<span class="me1">getPhysicsSpace</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">addAll</span><span class="br0">(</span>scene<span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
<span class="br0">}</span></pre>

<p>
—SceneSpatialBodyContext.java
</p>
<pre class="code java"><span class="kw1">package</span> <span class="co2">org.jmonkey3.chasecam</span><span class="sy0">;</span>
 
<span class="kw1">import</span> <span class="co2">com.jme3.app.Application</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.app.state.AppStateManager</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.asset.AssetManager</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.asset.plugins.ZipLocator</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.light.AmbientLight</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.light.DirectionalLight</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.math.Vector3f</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.Node</span><span class="sy0">;</span>
 
<span class="coMULTI">/*
 Chase camera (aka 3rd person camera) example
 Based on official TestQ3.java
 
 @author Alex Cham aka Jcrypto
 */</span>
<span class="kw1">public</span> <span class="kw1">class</span> SceneSpatialBodyContext <span class="kw1">extends</span> AbstractSpatialBodyContext
<span class="br0">{</span>
 
    <span class="kw1">private</span> <span class="kw1">final</span> Node rootNode<span class="sy0">;</span>
    <span class="co1">//</span>
    <span class="kw1">private</span> <span class="kw1">final</span> Node scene<span class="sy0">;</span>
    <span class="kw1">private</span> AmbientLight ambient<span class="sy0">;</span>
    <span class="kw1">private</span> DirectionalLight sun<span class="sy0">;</span>
<span class="co3">/**
 
    @param am
    @param rootNode 
    */</span>
    <span class="kw1">public</span> SceneSpatialBodyContext<span class="br0">(</span>AssetManager am, Node rootNode<span class="br0">)</span>
    <span class="br0">{</span>
        <span class="kw1">this</span>.<span class="me1">rootNode</span> <span class="sy0">=</span> rootNode<span class="sy0">;</span>
        <span class="co1">//</span>
        am.<span class="me1">registerLocator</span><span class="br0">(</span><span class="st0">"town.zip"</span>, ZipLocator.<span class="kw1">class</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="kw1">this</span>.<span class="me1">scene</span> <span class="sy0">=</span> <span class="br0">(</span>Node<span class="br0">)</span> am.<span class="me1">loadModel</span><span class="br0">(</span><span class="st0">"main.scene"</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="kw1">this</span>.<span class="me1">ambient</span> <span class="sy0">=</span> <span class="kw1">new</span> AmbientLight<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="kw1">this</span>.<span class="me1">sun</span> <span class="sy0">=</span> <span class="kw1">new</span> DirectionalLight<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    @Override
    <span class="kw1">public</span> <span class="kw4">void</span> initialize<span class="br0">(</span>AppStateManager stateManager, Application app<span class="br0">)</span>
    <span class="br0">{</span>
        <span class="co1">//Main Scene loading</span>
 
        <span class="kw1">this</span>.<span class="me1">scene</span>.<span class="me1">setLocalScale</span><span class="br0">(</span>0.1f<span class="br0">)</span><span class="sy0">;</span>
        <span class="kw1">this</span>.<span class="me1">scene</span>.<span class="me1">scale</span><span class="br0">(</span>32.0f<span class="br0">)</span><span class="sy0">;</span>
        <span class="co1">//</span>
        <span class="kw1">this</span>.<span class="me1">sun</span>.<span class="me1">setDirection</span><span class="br0">(</span><span class="kw1">new</span> Vector3f<span class="br0">(</span>1.4f, <span class="sy0">-</span>1.4f, <span class="sy0">-</span>1.4f<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="kw1">this</span>.<span class="me1">scene</span>.<span class="me1">setLocalTranslation</span><span class="br0">(</span>Vector3f.<span class="me1">ZERO</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="co1">//</span>
 
        rootNode.<span class="me1">attachChild</span><span class="br0">(</span><span class="kw1">this</span>.<span class="me1">scene</span><span class="br0">)</span><span class="sy0">;</span>
        rootNode.<span class="me1">addLight</span><span class="br0">(</span><span class="kw1">this</span>.<span class="me1">ambient</span><span class="br0">)</span><span class="sy0">;</span>
        rootNode.<span class="me1">addLight</span><span class="br0">(</span><span class="kw1">this</span>.<span class="me1">sun</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    <span class="co3">/**
     @return the scene
     */</span>
    <span class="kw1">public</span> Node getScene<span class="br0">(</span><span class="br0">)</span>
    <span class="br0">{</span>
        <span class="kw1">return</span> scene<span class="sy0">;</span>
    <span class="br0">}</span>
<span class="br0">}</span></pre>

<p>
—TheGame.java
</p>
<pre class="code java"><span class="kw1">package</span> <span class="co2">org.jmonkey3.chasecam</span><span class="sy0">;</span>
 
<span class="kw1">import</span> <span class="co2">com.jme3.app.SimpleApplication</span><span class="sy0">;</span>
 
<span class="coMULTI">/*
 Chase camera (aka 3rd person camera) example
 Based on official TestQ3.java
 
 @author Alex Cham aka Jcrypto
 */</span>
<span class="kw1">public</span> <span class="kw1">class</span> TheGame <span class="kw1">extends</span> SimpleApplication
<span class="br0">{</span>
 
    <span class="kw1">private</span> ApplicationContext applicationContext<span class="sy0">;</span>
 
    <span class="kw1">public</span> TheGame<span class="br0">(</span><span class="br0">)</span>
    <span class="br0">{</span>
    <span class="br0">}</span>
 
    <span class="co1">//</span>
    <span class="kw1">public</span> <span class="kw1">static</span> <span class="kw4">void</span> main<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a><span class="br0">[</span><span class="br0">]</span> args<span class="br0">)</span>
    <span class="br0">{</span>
        TheGame game <span class="sy0">=</span> <span class="kw1">new</span> TheGame<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
        game.<span class="me1">setShowSettings</span><span class="br0">(</span><span class="kw2">false</span><span class="br0">)</span><span class="sy0">;</span>
        game.<span class="me1">start</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    @Override
    <span class="kw1">public</span> <span class="kw4">void</span> simpleInitApp<span class="br0">(</span><span class="br0">)</span>
    <span class="br0">{</span>
        <span class="kw1">this</span>.<span class="me1">applicationContext</span> <span class="sy0">=</span> <span class="kw1">new</span> ApplicationContext<span class="br0">(</span>stateManager, assetManager, settings, inputManager, rootNode, cam, flyCam<span class="br0">)</span><span class="sy0">;</span>
        <span class="co1">//</span>
        stateManager.<span class="me1">attach</span><span class="br0">(</span>applicationContext<span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
<span class="br0">}</span></pre>

<p>
—Debug.java
</p>
<pre class="code java"><span class="kw1">package</span> <span class="co2">org.jmonkey.utils</span><span class="sy0">;</span>
 
<span class="kw1">import</span> <span class="co2">com.jme3.animation.AnimControl</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.asset.AssetManager</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.material.Material</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.math.ColorRGBA</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.math.Vector3f</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.Geometry</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.Node</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.debug.Arrow</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.debug.Grid</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.debug.SkeletonDebugger</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.shape.Line</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">static</span> org.<span class="me1">jmonkey</span>.<span class="me1">utils</span>.<span class="me1">SpatialUtils</span>.<span class="me1">makeGeometry</span><span class="sy0">;</span>
 
<span class="coMULTI">/*
 Chase camera (aka 3rd person camera) example
 Based on official TestQ3.java
 
 @author Alex Cham aka Jcrypto
 */</span>
<span class="kw1">public</span> <span class="kw1">class</span> Debug
<span class="br0">{</span>
 
    <span class="kw1">public</span> <span class="kw1">static</span> <span class="kw4">void</span> showNodeAxes<span class="br0">(</span>AssetManager am, Node n, <span class="kw4">float</span> axisLen<span class="br0">)</span>
    <span class="br0">{</span>
        Vector3f v <span class="sy0">=</span> <span class="kw1">new</span> Vector3f<span class="br0">(</span>axisLen, <span class="nu0">0</span>, <span class="nu0">0</span><span class="br0">)</span><span class="sy0">;</span>
        Arrow a <span class="sy0">=</span> <span class="kw1">new</span> Arrow<span class="br0">(</span>v<span class="br0">)</span><span class="sy0">;</span>
        Material mat <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>am, <span class="st0">"Common/MatDefs/Misc/Unshaded.j3md"</span><span class="br0">)</span><span class="sy0">;</span>
        mat.<span class="me1">setColor</span><span class="br0">(</span><span class="st0">"Color"</span>, ColorRGBA.<span class="me1">Red</span><span class="br0">)</span><span class="sy0">;</span>
        Geometry geom <span class="sy0">=</span> <span class="kw1">new</span> Geometry<span class="br0">(</span>n.<span class="me1">getName</span><span class="br0">(</span><span class="br0">)</span> <span class="sy0">+</span> <span class="st0">"XAxis"</span>, a<span class="br0">)</span><span class="sy0">;</span>
        geom.<span class="me1">setMaterial</span><span class="br0">(</span>mat<span class="br0">)</span><span class="sy0">;</span>
        n.<span class="me1">attachChild</span><span class="br0">(</span>geom<span class="br0">)</span><span class="sy0">;</span>
 
 
        <span class="co1">//</span>
        v <span class="sy0">=</span> <span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">0</span>, axisLen, <span class="nu0">0</span><span class="br0">)</span><span class="sy0">;</span>
        a <span class="sy0">=</span> <span class="kw1">new</span> Arrow<span class="br0">(</span>v<span class="br0">)</span><span class="sy0">;</span>
        mat <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>am, <span class="st0">"Common/MatDefs/Misc/Unshaded.j3md"</span><span class="br0">)</span><span class="sy0">;</span>
        mat.<span class="me1">setColor</span><span class="br0">(</span><span class="st0">"Color"</span>, ColorRGBA.<span class="me1">Green</span><span class="br0">)</span><span class="sy0">;</span>
        geom <span class="sy0">=</span> <span class="kw1">new</span> Geometry<span class="br0">(</span>n.<span class="me1">getName</span><span class="br0">(</span><span class="br0">)</span> <span class="sy0">+</span> <span class="st0">"YAxis"</span>, a<span class="br0">)</span><span class="sy0">;</span>
        geom.<span class="me1">setMaterial</span><span class="br0">(</span>mat<span class="br0">)</span><span class="sy0">;</span>
        n.<span class="me1">attachChild</span><span class="br0">(</span>geom<span class="br0">)</span><span class="sy0">;</span>
 
 
        <span class="co1">//</span>
        v <span class="sy0">=</span> <span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">0</span>, <span class="nu0">0</span>, axisLen<span class="br0">)</span><span class="sy0">;</span>
        a <span class="sy0">=</span> <span class="kw1">new</span> Arrow<span class="br0">(</span>v<span class="br0">)</span><span class="sy0">;</span>
        mat <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>am, <span class="st0">"Common/MatDefs/Misc/Unshaded.j3md"</span><span class="br0">)</span><span class="sy0">;</span>
        mat.<span class="me1">setColor</span><span class="br0">(</span><span class="st0">"Color"</span>, ColorRGBA.<span class="me1">Blue</span><span class="br0">)</span><span class="sy0">;</span>
        geom <span class="sy0">=</span> <span class="kw1">new</span> Geometry<span class="br0">(</span>n.<span class="me1">getName</span><span class="br0">(</span><span class="br0">)</span> <span class="sy0">+</span> <span class="st0">"ZAxis"</span>, a<span class="br0">)</span><span class="sy0">;</span>
        geom.<span class="me1">setMaterial</span><span class="br0">(</span>mat<span class="br0">)</span><span class="sy0">;</span>
        n.<span class="me1">attachChild</span><span class="br0">(</span>geom<span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    <span class="co1">//</span>
    <span class="kw1">public</span> <span class="kw1">static</span> <span class="kw4">void</span> showVector3fArrow<span class="br0">(</span>AssetManager am, Node n, Vector3f v, ColorRGBA color, <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> name<span class="br0">)</span>
    <span class="br0">{</span>
        Arrow a <span class="sy0">=</span> <span class="kw1">new</span> Arrow<span class="br0">(</span>v<span class="br0">)</span><span class="sy0">;</span>
        Material mat <span class="sy0">=</span> MaterialUtils.<span class="me1">makeMaterial</span><span class="br0">(</span>am, <span class="st0">"Common/MatDefs/Misc/Unshaded.j3md"</span>, color<span class="br0">)</span><span class="sy0">;</span>
        Geometry geom <span class="sy0">=</span> makeGeometry<span class="br0">(</span>a, mat, name<span class="br0">)</span><span class="sy0">;</span>
        n.<span class="me1">attachChild</span><span class="br0">(</span>geom<span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    <span class="kw1">public</span> <span class="kw1">static</span> <span class="kw4">void</span> showVector3fLine<span class="br0">(</span>AssetManager am, Node n, Vector3f v, ColorRGBA color, <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> name<span class="br0">)</span>
    <span class="br0">{</span>
        <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+line"><span class="kw3">Line</span></a> l <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+line"><span class="kw3">Line</span></a><span class="br0">(</span>v.<span class="me1">subtract</span><span class="br0">(</span>v<span class="br0">)</span>, v<span class="br0">)</span><span class="sy0">;</span>
        Material mat <span class="sy0">=</span> MaterialUtils.<span class="me1">makeMaterial</span><span class="br0">(</span>am, <span class="st0">"Common/MatDefs/Misc/Unshaded.j3md"</span>, color<span class="br0">)</span><span class="sy0">;</span>
        Geometry geom <span class="sy0">=</span> makeGeometry<span class="br0">(</span>l, mat, name<span class="br0">)</span><span class="sy0">;</span>
        n.<span class="me1">attachChild</span><span class="br0">(</span>geom<span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
<span class="co1">//Skeleton Debugger</span>
    <span class="kw1">public</span> <span class="kw1">static</span> <span class="kw4">void</span> attachSkeleton<span class="br0">(</span>AssetManager am, Node player, AnimControl control<span class="br0">)</span>
    <span class="br0">{</span>
        SkeletonDebugger skeletonDebug <span class="sy0">=</span> <span class="kw1">new</span> SkeletonDebugger<span class="br0">(</span><span class="st0">"skeleton"</span>, control.<span class="me1">getSkeleton</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
        Material mat2 <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>am, <span class="st0">"Common/MatDefs/Misc/Unshaded.j3md"</span><span class="br0">)</span><span class="sy0">;</span>
        mat2.<span class="me1">setColor</span><span class="br0">(</span><span class="st0">"Color"</span>, ColorRGBA.<span class="me1">Yellow</span><span class="br0">)</span><span class="sy0">;</span>
        mat2.<span class="me1">getAdditionalRenderState</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">setDepthTest</span><span class="br0">(</span><span class="kw2">false</span><span class="br0">)</span><span class="sy0">;</span>
        skeletonDebug.<span class="me1">setMaterial</span><span class="br0">(</span>mat2<span class="br0">)</span><span class="sy0">;</span>
        player.<span class="me1">attachChild</span><span class="br0">(</span>skeletonDebug<span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    <span class="co1">///</span>
    <span class="kw1">public</span> <span class="kw1">static</span> <span class="kw4">void</span> attachWireFrameDebugGrid<span class="br0">(</span>AssetManager assetManager, Node n, Vector3f pos, <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+integer"><span class="kw3">Integer</span></a> size, ColorRGBA color<span class="br0">)</span>
    <span class="br0">{</span>
        Geometry g <span class="sy0">=</span> <span class="kw1">new</span> Geometry<span class="br0">(</span><span class="st0">"wireFrameDebugGrid"</span>, <span class="kw1">new</span> Grid<span class="br0">(</span>size, size, 1.0f<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span><span class="co1">//1WU</span>
        Material mat <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>assetManager, <span class="st0">"Common/MatDefs/Misc/Unshaded.j3md"</span><span class="br0">)</span><span class="sy0">;</span>
        mat.<span class="me1">getAdditionalRenderState</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">setWireframe</span><span class="br0">(</span><span class="kw2">true</span><span class="br0">)</span><span class="sy0">;</span>
        mat.<span class="me1">setColor</span><span class="br0">(</span><span class="st0">"Color"</span>, color<span class="br0">)</span><span class="sy0">;</span>
        g.<span class="me1">setMaterial</span><span class="br0">(</span>mat<span class="br0">)</span><span class="sy0">;</span>
        g.<span class="me1">center</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">move</span><span class="br0">(</span>pos<span class="br0">)</span><span class="sy0">;</span>
        n.<span class="me1">attachChild</span><span class="br0">(</span>g<span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
<span class="br0">}</span></pre>

<p>
—MaterialUtils.java
</p>
<pre class="code java"><span class="kw1">package</span> <span class="co2">org.jmonkey.utils</span><span class="sy0">;</span>
 
<span class="kw1">import</span> <span class="co2">com.jme3.asset.AssetManager</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.material.Material</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.math.ColorRGBA</span><span class="sy0">;</span>
 
<span class="coMULTI">/*
 Chase camera (aka 3rd person camera) example
 Based on official TestQ3.java
 
 @author Alex Cham aka Jcrypto
 */</span>
<span class="kw1">public</span> <span class="kw1">class</span> MaterialUtils
<span class="br0">{</span>
 
    <span class="kw1">public</span> MaterialUtils<span class="br0">(</span><span class="br0">)</span>
    <span class="br0">{</span>
    <span class="br0">}</span>
 
 
    <span class="co1">//"Common/MatDefs/Misc/Unshaded.j3md"</span>
    <span class="kw1">public</span> <span class="kw1">static</span> Material makeMaterial<span class="br0">(</span>AssetManager am, <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> name, ColorRGBA color<span class="br0">)</span>
    <span class="br0">{</span>
        Material mat <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>am, name<span class="br0">)</span><span class="sy0">;</span>
        mat.<span class="me1">setColor</span><span class="br0">(</span><span class="st0">"Color"</span>, color<span class="br0">)</span><span class="sy0">;</span>
        <span class="kw1">return</span> mat<span class="sy0">;</span>
    <span class="br0">}</span>
<span class="br0">}</span></pre>

<p>
—SpatialUtils.java
</p>
<pre class="code java"><span class="kw1">package</span> <span class="co2">org.jmonkey.utils</span><span class="sy0">;</span>
 
<span class="kw1">import</span> <span class="co2">com.jme3.material.Material</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.math.Vector3f</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.Geometry</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.Mesh</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.Node</span><span class="sy0">;</span>
 
<span class="co3">/**
 
 @author java
 */</span>
<span class="kw1">public</span> <span class="kw1">class</span> SpatialUtils
<span class="br0">{</span>
    <span class="co1">//</span>
    <span class="kw1">public</span> <span class="kw1">static</span> Node makeNode<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> name<span class="br0">)</span>
    <span class="br0">{</span>
        Node n <span class="sy0">=</span> <span class="kw1">new</span> Node<span class="br0">(</span>name<span class="br0">)</span><span class="sy0">;</span>
        <span class="kw1">return</span> n<span class="sy0">;</span>
    <span class="br0">}</span>
 
<span class="co1">//</span>
    <span class="kw1">public</span> <span class="kw1">static</span> Geometry makeGeometry<span class="br0">(</span>Mesh mesh, Material mat, <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> name<span class="br0">)</span>
    <span class="br0">{</span>
        Geometry geom <span class="sy0">=</span> <span class="kw1">new</span> Geometry<span class="br0">(</span>name, mesh<span class="br0">)</span><span class="sy0">;</span>
        geom.<span class="me1">setMaterial</span><span class="br0">(</span>mat<span class="br0">)</span><span class="sy0">;</span>
        <span class="kw1">return</span> geom<span class="sy0">;</span>
    <span class="br0">}</span>
 
    <span class="co1">//</span>
    <span class="kw1">public</span> <span class="kw1">static</span> Geometry makeGeometry<span class="br0">(</span>Vector3f loc, Vector3f scl, Mesh mesh, Material mat, <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> name<span class="br0">)</span>
    <span class="br0">{</span>
        Geometry geom <span class="sy0">=</span> <span class="kw1">new</span> Geometry<span class="br0">(</span>name, mesh<span class="br0">)</span><span class="sy0">;</span>
        geom.<span class="me1">setMaterial</span><span class="br0">(</span>mat<span class="br0">)</span><span class="sy0">;</span>
        geom.<span class="me1">setLocalTranslation</span><span class="br0">(</span>loc<span class="br0">)</span><span class="sy0">;</span>
        geom.<span class="me1">setLocalScale</span><span class="br0">(</span>scl<span class="br0">)</span><span class="sy0">;</span>
        <span class="kw1">return</span> geom<span class="sy0">;</span>
    <span class="br0">}</span>
<span class="br0">}</span></pre>
