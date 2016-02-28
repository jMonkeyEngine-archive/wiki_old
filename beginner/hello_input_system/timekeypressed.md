---
title: jMonkeyEngine 3 Tutorial (5) - Hello Input System - Variation over time key is pressed
---
<h1 class="sectionedit1" id="jmonkeyengine_3_tutorial_5_-_hello_input_system_-_variation_over_time_key_is_pressed">jMonkeyEngine 3 Tutorial (5) - Hello Input System - Variation over time key is pressed</h1>
<div class="level1">

<p>
Parent: <a href="/jme3/beginner/hello_input_system.html" class="wikilink1" title="jme3:beginner:hello_input_system">jMonkeyEngine 3 Tutorial (5) - Hello Input System</a>
</p>

<p>
Here is a sample of a program where the camera accelerates if the key is kept pressed.
</p>
<pre class="code java"><span class="kw1">import</span> <span class="co2">com.jme3.app.SimpleApplication</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.bounding.BoundingBox</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.font.BitmapText</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.input.KeyInput</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.input.controls.ActionListener</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.input.controls.KeyTrigger</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.light.DirectionalLight</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.light.PointLight</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.material.Material</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.math.ColorRGBA</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.math.Vector3f</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.Geometry</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.terrain.geomipmap.TerrainLodControl</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.terrain.geomipmap.TerrainQuad</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.terrain.geomipmap.lodcalc.DistanceLodCalculator</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.terrain.heightmap.AbstractHeightMap</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.terrain.heightmap.ImageBasedHeightMap</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.texture.Texture</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.texture.Texture.WrapMode</span><span class="sy0">;</span>
 
<span class="kw1">public</span> <span class="kw1">class</span> Accelerate <span class="kw1">extends</span> SimpleApplication <span class="kw1">implements</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+actionlistener"><span class="kw3">ActionListener</span></a> <span class="br0">{</span>
 
    <span class="kw1">private</span> TerrainQuad terrain<span class="sy0">;</span>
    Material matTerrain<span class="sy0">;</span>
    Material matWire<span class="sy0">;</span>
    <span class="kw4">boolean</span> wireframe <span class="sy0">=</span> <span class="kw2">false</span><span class="sy0">;</span>
    <span class="kw4">boolean</span> triPlanar <span class="sy0">=</span> <span class="kw2">false</span><span class="sy0">;</span>
    <span class="kw4">boolean</span> wardiso <span class="sy0">=</span> <span class="kw2">false</span><span class="sy0">;</span>
    <span class="kw4">boolean</span> minnaert <span class="sy0">=</span> <span class="kw2">false</span><span class="sy0">;</span>
    <span class="kw1">protected</span> BitmapText hintText<span class="sy0">;</span>
    PointLight pl<span class="sy0">;</span>
    Geometry lightMdl<span class="sy0">;</span>
    <span class="kw1">private</span> <span class="kw4">float</span> dirtScale <span class="sy0">=</span> <span class="nu0">16</span><span class="sy0">;</span>
 
    <span class="kw1">private</span> <span class="kw1">enum</span> Actions <span class="br0">{</span>
 
        LEFT, RIGHT, UP, DOWN<span class="sy0">;</span>
    <span class="br0">}</span>
    <span class="kw1">private</span> <span class="kw1">final</span> <span class="kw4">int</span> CAMERA_HEIGHT <span class="sy0">=</span> <span class="nu0">250</span><span class="sy0">;</span>
    <span class="kw1">private</span> <span class="kw1">final</span> <span class="kw4">int</span> STARTING_CAM_SPEED <span class="sy0">=</span> <span class="nu0">1</span><span class="sy0">;</span>
    <span class="kw1">private</span> <span class="kw1">final</span> Vector3f CAM_DIRECTION <span class="sy0">=</span> <span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">0</span>, <span class="sy0">-</span>0.3f, 1f<span class="br0">)</span><span class="sy0">;</span>
    <span class="kw1">private</span> <span class="kw1">final</span> Vector3f CAM_LOCATION <span class="sy0">=</span> <span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="sy0">-</span><span class="nu0">1</span>, <span class="nu0">0</span>, <span class="sy0">-</span>CAMERA_HEIGHT<span class="br0">)</span><span class="sy0">;</span>
    <span class="kw1">private</span> <span class="kw1">final</span> Vector3f walkDirection <span class="sy0">=</span> <span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="kw1">private</span> <span class="kw4">boolean</span> left <span class="sy0">=</span> <span class="kw2">false</span><span class="sy0">;</span>
    <span class="kw1">private</span> <span class="kw4">boolean</span> right <span class="sy0">=</span> <span class="kw2">false</span><span class="sy0">;</span>
    <span class="kw1">private</span> <span class="kw4">boolean</span> up <span class="sy0">=</span> <span class="kw2">false</span><span class="sy0">;</span>
    <span class="kw1">private</span> <span class="kw4">boolean</span> down <span class="sy0">=</span> <span class="kw2">false</span><span class="sy0">;</span>
    <span class="kw1">private</span> <span class="kw4">float</span> camSpeed <span class="sy0">=</span> STARTING_CAM_SPEED<span class="sy0">;</span>
 
    <span class="kw1">private</span> <span class="kw4">void</span> initCamera<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
        cam.<span class="me1">setLocation</span><span class="br0">(</span>CAM_LOCATION<span class="br0">)</span><span class="sy0">;</span>
        cam.<span class="me1">lookAtDirection</span><span class="br0">(</span>CAM_DIRECTION.<span class="me1">normalizeLocal</span><span class="br0">(</span><span class="br0">)</span>, Vector3f.<span class="me1">UNIT_Y</span>.<span class="me1">clone</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">addLocal</span><span class="br0">(</span><span class="nu0">0</span>, <span class="nu0">2</span>, <span class="nu0">0</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    <span class="kw1">public</span> <span class="kw1">static</span> <span class="kw4">void</span> main<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a><span class="br0">[</span><span class="br0">]</span> args<span class="br0">)</span> <span class="br0">{</span>
        Accelerate app <span class="sy0">=</span> <span class="kw1">new</span> Accelerate<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
        app.<span class="me1">start</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    @Override
    <span class="kw1">public</span> <span class="kw4">void</span> simpleInitApp<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
        setupKeys<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
        initTerrain<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
        initCamera<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    @Override
    <span class="kw1">public</span> <span class="kw4">void</span> simpleUpdate<span class="br0">(</span><span class="kw4">float</span> tpf<span class="br0">)</span> <span class="br0">{</span>
        updateMovement<span class="br0">(</span>tpf<span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    <span class="kw1">private</span> <span class="kw4">void</span> updateMovement<span class="br0">(</span><span class="kw4">float</span> tpf<span class="br0">)</span> <span class="br0">{</span>
        <span class="kw1">if</span> <span class="br0">(</span>left <span class="sy0">||</span> right <span class="sy0">||</span> up <span class="sy0">||</span> down<span class="br0">)</span> <span class="br0">{</span>
            <span class="co1">// here we increment the speed using the tpf</span>
            camSpeed <span class="sy0">+=</span> tpf <span class="sy0">*</span> <span class="nu0">2</span><span class="sy0">;</span>
            <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+system"><span class="kw3">System</span></a>.<span class="me1">out</span>.<span class="me1">print</span><span class="br0">(</span><span class="st0">"Camera speed "</span> <span class="sy0">+</span> camSpeed <span class="sy0">+</span> <span class="st0">";  Location:"</span> <span class="sy0">+</span> cam.<span class="me1">getLocation</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">toString</span><span class="br0">(</span><span class="br0">)</span> 
                    <span class="sy0">+</span> <span class="st0">";  direction:"</span><span class="sy0">+</span>cam.<span class="me1">getDirection</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">+</span><span class="st0">"walkDirection:"</span> <span class="sy0">+</span> walkDirection.<span class="me1">toString</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="br0">}</span>
        Vector3f camDir <span class="sy0">=</span> cam.<span class="me1">getDirection</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">clone</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">multLocal</span><span class="br0">(</span>camSpeed<span class="br0">)</span><span class="sy0">;</span>
        Vector3f camLeft <span class="sy0">=</span> cam.<span class="me1">getLeft</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">clone</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">multLocal</span><span class="br0">(</span>camSpeed<span class="br0">)</span><span class="sy0">;</span>
        <span class="co1">// adjust position of rigid body for collisions</span>
        walkDirection.<span class="me1">set</span><span class="br0">(</span>cam.<span class="me1">getLocation</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">clone</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="kw1">if</span> <span class="br0">(</span>left<span class="br0">)</span> <span class="br0">{</span>
            walkDirection.<span class="me1">addLocal</span><span class="br0">(</span>camLeft<span class="br0">)</span><span class="sy0">;</span>
        <span class="br0">}</span>
        <span class="kw1">if</span> <span class="br0">(</span>right<span class="br0">)</span> <span class="br0">{</span>
            walkDirection.<span class="me1">addLocal</span><span class="br0">(</span>camLeft.<span class="me1">negate</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="br0">}</span>
        <span class="kw1">if</span> <span class="br0">(</span>up<span class="br0">)</span> <span class="br0">{</span>
            walkDirection.<span class="me1">addLocal</span><span class="br0">(</span>camDir<span class="br0">)</span><span class="sy0">;</span>
        <span class="br0">}</span>
        <span class="kw1">if</span> <span class="br0">(</span>down<span class="br0">)</span> <span class="br0">{</span>
            walkDirection.<span class="me1">addLocal</span><span class="br0">(</span>camDir.<span class="me1">negate</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="br0">}</span>
<span class="co1">//        player.setWalkDirection(walkDirection);</span>
        cam.<span class="me1">setLocation</span><span class="br0">(</span>walkDirection<span class="br0">)</span><span class="sy0">;</span>
        <span class="kw1">if</span> <span class="br0">(</span>left <span class="sy0">||</span> right <span class="sy0">||</span> up <span class="sy0">||</span> down<span class="br0">)</span> <span class="br0">{</span>
            <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+system"><span class="kw3">System</span></a>.<span class="me1">out</span>.<span class="me1">println</span><span class="br0">(</span><span class="st0">"; new walkDirection:"</span> <span class="sy0">+</span> walkDirection<span class="br0">)</span><span class="sy0">;</span>
        <span class="br0">}</span>
    <span class="br0">}</span>
 
    <span class="kw1">private</span> <span class="kw4">void</span> initTerrain<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
        <span class="co1">// First, we load up our textures and the heightmap texture for the terrain</span>
 
        <span class="co1">// TERRAIN TEXTURE material</span>
        matTerrain <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>assetManager, <span class="st0">"Common/MatDefs/Terrain/TerrainLighting.j3md"</span><span class="br0">)</span><span class="sy0">;</span>
        matTerrain.<span class="me1">setBoolean</span><span class="br0">(</span><span class="st0">"useTriPlanarMapping"</span>, <span class="kw2">false</span><span class="br0">)</span><span class="sy0">;</span>
        matTerrain.<span class="me1">setFloat</span><span class="br0">(</span><span class="st0">"Shininess"</span>, 0.0f<span class="br0">)</span><span class="sy0">;</span>
 
        <span class="co1">// ALPHA map (for splat textures)</span>
        matTerrain.<span class="me1">setTexture</span><span class="br0">(</span><span class="st0">"AlphaMap"</span>, assetManager.<span class="me1">loadTexture</span><span class="br0">(</span><span class="st0">"Textures/Terrain/splat/alpha1.png"</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
        matTerrain.<span class="me1">setTexture</span><span class="br0">(</span><span class="st0">"AlphaMap_1"</span>, assetManager.<span class="me1">loadTexture</span><span class="br0">(</span><span class="st0">"Textures/Terrain/splat/alpha2.png"</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
 
        <span class="co1">// HEIGHTMAP image (for the terrain heightmap)</span>
        Texture heightMapImage <span class="sy0">=</span> assetManager.<span class="me1">loadTexture</span><span class="br0">(</span><span class="st0">"Textures/Terrain/splat/mountains512.png"</span><span class="br0">)</span><span class="sy0">;</span>
 
        <span class="co1">// GRASS texture</span>
        Texture grass <span class="sy0">=</span> assetManager.<span class="me1">loadTexture</span><span class="br0">(</span><span class="st0">"Textures/Terrain/splat/grass.jpg"</span><span class="br0">)</span><span class="sy0">;</span>
        grass.<span class="me1">setWrap</span><span class="br0">(</span>WrapMode.<span class="me1">Repeat</span><span class="br0">)</span><span class="sy0">;</span>
 
        <span class="co1">// DIRT texture</span>
        Texture dirt <span class="sy0">=</span> assetManager.<span class="me1">loadTexture</span><span class="br0">(</span><span class="st0">"Textures/Terrain/splat/dirt.jpg"</span><span class="br0">)</span><span class="sy0">;</span>
        dirt.<span class="me1">setWrap</span><span class="br0">(</span>WrapMode.<span class="me1">Repeat</span><span class="br0">)</span><span class="sy0">;</span>
        matTerrain.<span class="me1">setTexture</span><span class="br0">(</span><span class="st0">"DiffuseMap"</span>, dirt<span class="br0">)</span><span class="sy0">;</span>
        matTerrain.<span class="me1">setFloat</span><span class="br0">(</span><span class="st0">"DiffuseMap_0_scale"</span>, dirtScale<span class="br0">)</span><span class="sy0">;</span>
 
        <span class="co1">// ROCK texture</span>
        Texture rock <span class="sy0">=</span> assetManager.<span class="me1">loadTexture</span><span class="br0">(</span><span class="st0">"Textures/Terrain/splat/road.jpg"</span><span class="br0">)</span><span class="sy0">;</span>
        rock.<span class="me1">setWrap</span><span class="br0">(</span>WrapMode.<span class="me1">Repeat</span><span class="br0">)</span><span class="sy0">;</span>
 
        <span class="co1">// BRICK texture</span>
        Texture brick <span class="sy0">=</span> assetManager.<span class="me1">loadTexture</span><span class="br0">(</span><span class="st0">"Textures/Terrain/BrickWall/BrickWall.jpg"</span><span class="br0">)</span><span class="sy0">;</span>
        brick.<span class="me1">setWrap</span><span class="br0">(</span>WrapMode.<span class="me1">Repeat</span><span class="br0">)</span><span class="sy0">;</span>
 
        <span class="co1">// RIVER ROCK texture</span>
        Texture riverRock <span class="sy0">=</span> assetManager.<span class="me1">loadTexture</span><span class="br0">(</span><span class="st0">"Textures/Terrain/Pond/Pond.jpg"</span><span class="br0">)</span><span class="sy0">;</span>
        riverRock.<span class="me1">setWrap</span><span class="br0">(</span>WrapMode.<span class="me1">Repeat</span><span class="br0">)</span><span class="sy0">;</span>
 
        <span class="co1">// WIREFRAME material</span>
        matWire <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>assetManager, <span class="st0">"Common/MatDefs/Misc/Unshaded.j3md"</span><span class="br0">)</span><span class="sy0">;</span>
        matWire.<span class="me1">getAdditionalRenderState</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">setWireframe</span><span class="br0">(</span><span class="kw2">true</span><span class="br0">)</span><span class="sy0">;</span>
        matWire.<span class="me1">setColor</span><span class="br0">(</span><span class="st0">"Color"</span>, ColorRGBA.<span class="me1">Green</span><span class="br0">)</span><span class="sy0">;</span>
 
 
        <span class="co1">// CREATE HEIGHTMAP</span>
        AbstractHeightMap heightmap <span class="sy0">=</span> <span class="kw2">null</span><span class="sy0">;</span>
        <span class="kw1">try</span> <span class="br0">{</span>
            heightmap <span class="sy0">=</span> <span class="kw1">new</span> ImageBasedHeightMap<span class="br0">(</span>heightMapImage.<span class="me1">getImage</span><span class="br0">(</span><span class="br0">)</span>, 0.5f<span class="br0">)</span><span class="sy0">;</span>
            heightmap.<span class="me1">load</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
            heightmap.<span class="me1">smooth</span><span class="br0">(</span>0.9f, <span class="nu0">1</span><span class="br0">)</span><span class="sy0">;</span>
 
        <span class="br0">}</span> <span class="kw1">catch</span> <span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+exception"><span class="kw3">Exception</span></a> e<span class="br0">)</span> <span class="br0">{</span>
            e.<span class="me1">printStackTrace</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="br0">}</span>
 
        <span class="coMULTI">/*
         * Here we create the actual terrain. The tiles will be 65x65, and the total size of the
         * terrain will be 513x513. It uses the heightmap we created to generate the height values.
         */</span>
        <span class="co3">/**
         * Optimal terrain patch size is 65 (64x64).
         * The total size is up to you. At 1025 it ran fine for me (200+FPS), however at
         * size=2049, it got really slow. But that is a jump from 2 million to 8 million triangles...
         */</span>
        terrain <span class="sy0">=</span> <span class="kw1">new</span> TerrainQuad<span class="br0">(</span><span class="st0">"terrain"</span>, <span class="nu0">65</span>, <span class="nu0">513</span>, heightmap.<span class="me1">getHeightMap</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span><span class="co1">//, new LodPerspectiveCalculatorFactory(getCamera(), 4)); // add this in to see it use entropy for LOD calculations</span>
        TerrainLodControl control <span class="sy0">=</span> <span class="kw1">new</span> TerrainLodControl<span class="br0">(</span>terrain, getCamera<span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
        control.<span class="me1">setLodCalculator</span><span class="br0">(</span><span class="kw1">new</span> DistanceLodCalculator<span class="br0">(</span><span class="nu0">65</span>, 2.7f<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// patch size, and a multiplier</span>
        terrain.<span class="me1">addControl</span><span class="br0">(</span>control<span class="br0">)</span><span class="sy0">;</span>
        terrain.<span class="me1">setMaterial</span><span class="br0">(</span>matTerrain<span class="br0">)</span><span class="sy0">;</span>
        terrain.<span class="me1">setModelBound</span><span class="br0">(</span><span class="kw1">new</span> BoundingBox<span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
        terrain.<span class="me1">updateModelBound</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
        terrain.<span class="me1">setLocalTranslation</span><span class="br0">(</span><span class="nu0">0</span>, <span class="sy0">-</span><span class="nu0">100</span>, <span class="nu0">0</span><span class="br0">)</span><span class="sy0">;</span>
        terrain.<span class="me1">setLocalScale</span><span class="br0">(</span>1f, 1f, 1f<span class="br0">)</span><span class="sy0">;</span>
        rootNode.<span class="me1">attachChild</span><span class="br0">(</span>terrain<span class="br0">)</span><span class="sy0">;</span>
 
 
        DirectionalLight light <span class="sy0">=</span> <span class="kw1">new</span> DirectionalLight<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
        light.<span class="me1">setDirection</span><span class="br0">(</span><span class="br0">(</span><span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="sy0">-</span>0.5f, <span class="sy0">-</span>0.5f, <span class="sy0">-</span>0.5f<span class="br0">)</span><span class="br0">)</span>.<span class="me1">normalize</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
        rootNode.<span class="me1">addLight</span><span class="br0">(</span>light<span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    <span class="kw1">private</span> <span class="kw4">void</span> setupKeys<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
        inputManager.<span class="me1">addMapping</span><span class="br0">(</span>Actions.<span class="me1">LEFT</span>.<span class="me1">name</span><span class="br0">(</span><span class="br0">)</span>, <span class="kw1">new</span> KeyTrigger<span class="br0">(</span>KeyInput.<span class="me1">KEY_A</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
        inputManager.<span class="me1">addMapping</span><span class="br0">(</span>Actions.<span class="me1">RIGHT</span>.<span class="me1">name</span><span class="br0">(</span><span class="br0">)</span>, <span class="kw1">new</span> KeyTrigger<span class="br0">(</span>KeyInput.<span class="me1">KEY_D</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
        inputManager.<span class="me1">addMapping</span><span class="br0">(</span>Actions.<span class="me1">UP</span>.<span class="me1">name</span><span class="br0">(</span><span class="br0">)</span>, <span class="kw1">new</span> KeyTrigger<span class="br0">(</span>KeyInput.<span class="me1">KEY_W</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
        inputManager.<span class="me1">addMapping</span><span class="br0">(</span>Actions.<span class="me1">DOWN</span>.<span class="me1">name</span><span class="br0">(</span><span class="br0">)</span>, <span class="kw1">new</span> KeyTrigger<span class="br0">(</span>KeyInput.<span class="me1">KEY_S</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
        inputManager.<span class="me1">addListener</span><span class="br0">(</span><span class="kw1">this</span>, Actions.<span class="me1">LEFT</span>.<span class="me1">name</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
        inputManager.<span class="me1">addListener</span><span class="br0">(</span><span class="kw1">this</span>, Actions.<span class="me1">RIGHT</span>.<span class="me1">name</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
        inputManager.<span class="me1">addListener</span><span class="br0">(</span><span class="kw1">this</span>, Actions.<span class="me1">UP</span>.<span class="me1">name</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
        inputManager.<span class="me1">addListener</span><span class="br0">(</span><span class="kw1">this</span>, Actions.<span class="me1">DOWN</span>.<span class="me1">name</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    <span class="co3">/**
     * These are our custom actions triggered by key presses. We do not walk yet, we just keep track of the direction
     * the user pressed.
     */</span>
    @Override
    <span class="kw1">public</span> <span class="kw4">void</span> onAction<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> name, <span class="kw4">boolean</span> keyPressed, <span class="kw4">float</span> tpf<span class="br0">)</span> <span class="br0">{</span>
        <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+system"><span class="kw3">System</span></a>.<span class="me1">out</span>.<span class="me1">println</span><span class="br0">(</span><span class="st0">"name:"</span> <span class="sy0">+</span> name <span class="sy0">+</span> <span class="st0">"; keyPressed:"</span> <span class="sy0">+</span> keyPressed<span class="br0">)</span><span class="sy0">;</span>
        <span class="kw1">if</span> <span class="br0">(</span>name.<span class="me1">equals</span><span class="br0">(</span>Actions.<span class="me1">LEFT</span>.<span class="me1">name</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
            left <span class="sy0">=</span> keyPressed<span class="sy0">;</span>
            <span class="kw1">if</span> <span class="br0">(</span><span class="sy0">!</span>keyPressed<span class="br0">)</span> <span class="br0">{</span> <span class="co1">// if the key isn't pressed anymore reset the speed to the initial value</span>
                camSpeed <span class="sy0">=</span> STARTING_CAM_SPEED<span class="sy0">;</span>
            <span class="br0">}</span>
        <span class="br0">}</span> <span class="kw1">else</span> <span class="kw1">if</span> <span class="br0">(</span>name.<span class="me1">equals</span><span class="br0">(</span>Actions.<span class="me1">RIGHT</span>.<span class="me1">name</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
            right <span class="sy0">=</span> keyPressed<span class="sy0">;</span>
            <span class="kw1">if</span> <span class="br0">(</span><span class="sy0">!</span>keyPressed<span class="br0">)</span> <span class="br0">{</span>
                camSpeed <span class="sy0">=</span> STARTING_CAM_SPEED<span class="sy0">;</span>
            <span class="br0">}</span>
        <span class="br0">}</span> <span class="kw1">else</span> <span class="kw1">if</span> <span class="br0">(</span>name.<span class="me1">equals</span><span class="br0">(</span>Actions.<span class="me1">UP</span>.<span class="me1">name</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
            up <span class="sy0">=</span> keyPressed<span class="sy0">;</span>
            <span class="kw1">if</span> <span class="br0">(</span><span class="sy0">!</span>keyPressed<span class="br0">)</span> <span class="br0">{</span>
                camSpeed <span class="sy0">=</span> STARTING_CAM_SPEED<span class="sy0">;</span>
            <span class="br0">}</span>
        <span class="br0">}</span> <span class="kw1">else</span> <span class="kw1">if</span> <span class="br0">(</span>name.<span class="me1">equals</span><span class="br0">(</span>Actions.<span class="me1">DOWN</span>.<span class="me1">name</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
            down <span class="sy0">=</span> keyPressed<span class="sy0">;</span>
            <span class="kw1">if</span> <span class="br0">(</span><span class="sy0">!</span>keyPressed<span class="br0">)</span> <span class="br0">{</span>
                camSpeed <span class="sy0">=</span> STARTING_CAM_SPEED<span class="sy0">;</span>
            <span class="br0">}</span>
        <span class="br0">}</span>
    <span class="br0">}</span>
<span class="br0">}</span></pre>

</div>
