---
title: The Forester
---
<h1 class="sectionedit1" id="the_forester">The Forester</h1>
<div class="level1">

<p>
This is the wiki page for the Forester grass/tree loading system. It contains information on how to add vegetation to a scene, and how to manage it. Grass and trees are treated differently, but the approaches are very similar.
</p>

<p>
Topics are flagged as (basic) or (advanced). Advanced topics can be skipped.
</p>

</div>
<!-- EDIT1 SECTION "The Forester" [1-334] -->
<h2 class="sectionedit2" id="the_forester_basic">The Forester (Basic)</h2>
<div class="level2">

<p>
The Forester class is the root class of this lib. You can use it to create grass/treeloaders, and a few other things. It also manages random number tables and a few other things. 
</p>

<p>
It is a singleton class, so it can be used anywhere for easy access to Forester data.
</p>

</div>
<!-- EDIT2 SECTION "The Forester (Basic)" [335-636] -->
<h2 class="sectionedit3" id="the_grass">The grass</h2>
<div class="level2">

<p>
Proceed to the grass section: <a href="http://jmonkeyengine.org/wiki/doku.php/jme3:contributions:vegetationsystem:grass" class="urlextern" title="http://jmonkeyengine.org/wiki/doku.php/jme3:contributions:vegetationsystem:grass" rel="nofollow">http://jmonkeyengine.org/wiki/doku.php/jme3:contributions:vegetationsystem:grass</a>
</p>

</div>
<!-- EDIT3 SECTION "The grass" [637-775] -->
<h2 class="sectionedit4" id="the_trees">The trees</h2>
<div class="level2">

<p>
Proceed to the tree section: <a href="http://jmonkeyengine.org/wiki/doku.php/jme3:contributions:vegetationsystem:trees" class="urlextern" title="http://jmonkeyengine.org/wiki/doku.php/jme3:contributions:vegetationsystem:trees" rel="nofollow">http://jmonkeyengine.org/wiki/doku.php/jme3:contributions:vegetationsystem:trees</a>
</p>

</div>
<!-- EDIT4 SECTION "The trees" [776-913] -->
<h2 class="sectionedit5" id="tuning_the_paging_engine_advanced">Tuning the paging engine (Advanced)</h2>
<div class="level2">

<p>
All tree/grassloaders use a paging engine to load/unload data. There are some things you can do that affects performance and memory usage for both trees and grass.
</p>

</div>
<!-- EDIT5 SECTION "Tuning the paging engine (Advanced)" [914-1127] -->
<h3 class="sectionedit6" id="manipulating_the_cache">Manipulating the cache</h3>
<div class="level3">

<p>
The cache saves expired tiles for some time before disposing of them. This makes it possible for the engine to re-use pages instead of having to load and prepare them again. 
</p>

<p>
An example: Lets say you walk across the border between two tiles. Passing the border between two tiles prompts the engine to load new tiles in the direction you are moving, and toss old ones away. Lets say you then walk back directly. Or keep walking back and forth across that border. Without the cache, you'd be loading and unloading tiles all the time. 
</p>

<p>
There is no point in turning it off, unless maybe if you use extremely small tiles. You can change the cache timer however. Default time is 2 seconds (2000 ms actually, the value is in ms). After 2 seconds the tiles are dropped from the cache.
</p>

<p>
To change the value, do this:
</p>
<pre class="code java">grassLoader.<span class="me1">getPagingManager</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">setCacheTime</span><span class="br0">(</span><span class="nu0">6000</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
That would increase the cache time to 6 seconds.
</p>

</div>
<!-- EDIT6 SECTION "Manipulating the cache" [1128-2094] -->
<h3 class="sectionedit7" id="changing_the_tile_size_resolution">Changing the tile size &amp; resolution</h3>
<div class="level3">

<p>
The tile size determines how much geometry is being loaded at the same time. The resolution determines how many sub-geometries are in a tile.
If you increase resolution from 2 to 4, it would change the amount of geometries in a tile from 4 to 16. You can think of resolution as being the height/width of an image. If you double it, the size of the image is squared.
</p>

<p>
Having few but large geometries is more efficient when rendering, however. That is how GPUs work; they rather take a few large blocks of data then many small ones. It also leads to less java objects, less overhead etc.
</p>

<p>
Having many geometries, on the other side, ensures more geometry is culled on average. If you use one mega-block of 512×512 square units, you'd have to render the entire block even if you can only see a tiny fraction of it. Also, when massive blocks are pushed in and out of the rendering queue you might get noticeable increases/drops in frame-rate.
</p>

<p>
It is very hard to say what is the correct resolution in an application, because it depends on very much, but it is possible to try a few different settings and see which is best. This may have an effect on performance; particularly if you're using massive amounts of grass. 
</p>

<p>
</p><p></p><div class="notetip"> It is generally not good to use gigantic geometries, or tiny ones - but larger is better than smaller.
</div>


<p>
More to come.
</p>

</div>
<!-- EDIT7 SECTION "Changing the tile size & resolution" [2095-] -->
