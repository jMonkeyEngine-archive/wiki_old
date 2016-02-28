---
title: Anisotropic Filtering for Textures
---
<h2 class="sectionedit1" id="anisotropic_filtering_for_textures">Anisotropic Filtering for Textures</h2>
<div class="level2">

<p>
Anisotropic Filtering is very important for Desktop Games and their textures. Most games use AnisotropicFiltering = 4/8/16. It sharpens your textures under different Angle View. 
Anisotropy makes a performance draw back about 10-40 fps, but the result looks much better.
</p>

<p>
See Example: <a href="http://i.imgur.com/0yiv9.jpg" class="urlextern" title="http://i.imgur.com/0yiv9.jpg" rel="nofollow">http://i.imgur.com/0yiv9.jpg</a>
<a href="/resources/jme3-advanced-anisotropy_example_mifth_01.jpg" class="media" title="jme3:advanced:anisotropy_example_mifth_01.jpg"><img src="/resources/jme3-advanced-anisotropy_example_mifth_01.jpg" class="mediaright" title="anisotropy_example_mifth_01.jpg" alt="anisotropy_example_mifth_01.jpg" width="360" height="900" /></a>
</p>

<p>
JME has DEFAULT AnisotropicFiltering = 0. So, if you make a game for Windows/Linux/Mac.. you need to set the Anisotropic Filtering more than 0.
</p>

<p>
Example how to set AnisotropicFiltering = 4 for all textures:
</p>
<pre class="code java">        AssetEventListener asl <span class="sy0">=</span> <span class="kw1">new</span> AssetEventListener<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
            <span class="kw1">public</span> <span class="kw4">void</span> assetLoaded<span class="br0">(</span>AssetKey key<span class="br0">)</span> <span class="br0">{</span>
<span class="co1">//                throw new UnsupportedOperationException("Not supported yet.");</span>
            <span class="br0">}</span>
 
            <span class="kw1">public</span> <span class="kw4">void</span> assetRequested<span class="br0">(</span>AssetKey key<span class="br0">)</span> <span class="br0">{</span>
                <span class="kw1">if</span> <span class="br0">(</span>key.<span class="me1">getExtension</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">equals</span><span class="br0">(</span><span class="st0">"png"</span><span class="br0">)</span> <span class="sy0">||</span> key.<span class="me1">getExtension</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">equals</span><span class="br0">(</span><span class="st0">"jpg"</span><span class="br0">)</span> <span class="sy0">||</span> key.<span class="me1">getExtension</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">equals</span><span class="br0">(</span><span class="st0">"dds"</span><span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
                    <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+system"><span class="kw3">System</span></a>.<span class="me1">out</span>.<span class="me1">println</span><span class="br0">(</span>key.<span class="me1">getExtension</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
                    TextureKey tkey <span class="sy0">=</span> <span class="br0">(</span>TextureKey<span class="br0">)</span> key<span class="sy0">;</span>
                    tkey.<span class="me1">setAnisotropy</span><span class="br0">(</span><span class="nu0">8</span><span class="br0">)</span><span class="sy0">;</span>
                <span class="br0">}</span>
            <span class="br0">}</span>
 
            <span class="kw1">public</span> <span class="kw4">void</span> assetDependencyNotFound<span class="br0">(</span>AssetKey parentKey, AssetKey dependentAssetKey<span class="br0">)</span> <span class="br0">{</span>
<span class="co1">//                throw new UnsupportedOperationException("Not supported yet.");</span>
            <span class="br0">}</span>
        <span class="br0">}</span><span class="sy0">;</span>
 
        assetManager.<span class="me1">addAssetEventListener</span><span class="br0">(</span>asl<span class="br0">)</span><span class="sy0">;</span></pre>

</div>
