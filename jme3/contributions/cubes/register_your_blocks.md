---
title: Register Block Types
---
<h1 class="sectionedit1" id="register_block_types">Register Block Types</h1>
<div class="level1">

<p>
To add blocks to the framework, you just have to add them to the BlockManager - This happens by specifying a block object (has to extend <strong>cubes.Block</strong>, by overriding methods you can specify own behaviours). Each block needs at least one “skin”, which you have to pass in the constructor of the <strong>cubes.Block</strong> class). A “skin” contains all information to display the block - Texture-Index in the Atlas, Transparency and so on.
</p>

<p>
After initialising your object, you have to register it in the BlockManager:
</p>
<pre class="code java">BlockManager.<span class="me1">register</span><span class="br0">(</span>myBlockObject<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
</p><p></p><div class="notetip">Using own blocks <em>should</em> work at the moment, if you encounter problems you can test your code using the default blocks (e.g. <strong>CubesTestAssets.BLOCK_GRASS</strong>).


<p>
You can register them by calling <code>CubesTestAssets.registerBlocks();</code>.
</p></div>


</div>
<!-- EDIT1 SECTION "Register Block Types" [1-854] -->
<h2 class="sectionedit2" id="single_texture_block">Single Texture Block</h2>
<div class="level2">

<p>
<a href="/resources/fetch.php" class="media" title="http://destroflyer.mania-community.de/other/imagehost/cubes/block_stone.png"><img src="/resources/fetch.php" class="mediaright" alt="" width="150" /></a>
Let's say, you want to add a simple block, which uses the same texture on every face. The framework recognizes, when only one texture is specified and therefore uses this for each face:
</p>
<pre class="code java"><span class="co1">//The stone texture is in the 10th column and 1st row in the texture atlas</span>
Block blockStone <span class="sy0">=</span> <span class="kw1">new</span> Block<span class="br0">(</span><span class="kw1">new</span> BlockSkin<span class="br0">(</span><span class="kw1">new</span> BlockSkin_TextureLocation<span class="br0">(</span><span class="nu0">9</span>, <span class="nu0">0</span><span class="br0">)</span>, <span class="kw2">false</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
BlockManager.<span class="me1">register</span><span class="br0">(</span>blockStone<span class="br0">)</span><span class="sy0">;</span></pre>

</div>
<!-- EDIT2 SECTION "Single Texture Block" [855-1386] -->
<h2 class="sectionedit3" id="face-dependant_textures_block">Face-Dependant Textures Block</h2>
<div class="level2">

<p>
<a href="/resources/fetch.php" class="media" title="http://destroflyer.mania-community.de/other/imagehost/cubes/block_wood.png"><img src="/resources/fetch.php" class="mediaright" alt="" width="150" /></a>
Now it's time to get prettier blocks - The wood block as known in Minecraft has two textures: Top/Bottom (cross-section) and Left/Right/Front/Back (bark). A simple way to set the texture for each face is to just give 6 textures to the skin (in the right order :P):
</p>
<pre class="code java">Block blockWood <span class="sy0">=</span> <span class="kw1">new</span> Block<span class="br0">(</span><span class="kw1">new</span> BlockSkin<span class="br0">[</span><span class="br0">]</span><span class="br0">{</span>
    <span class="kw1">new</span> BlockSkin<span class="br0">(</span><span class="kw1">new</span> BlockSkin_TextureLocation<span class="br0">(</span><span class="nu0">4</span>, <span class="nu0">0</span><span class="br0">)</span>, <span class="kw2">false</span><span class="br0">)</span>,
    <span class="kw1">new</span> BlockSkin<span class="br0">(</span><span class="kw1">new</span> BlockSkin_TextureLocation<span class="br0">(</span><span class="nu0">4</span>, <span class="nu0">0</span><span class="br0">)</span>, <span class="kw2">false</span><span class="br0">)</span>,
    <span class="kw1">new</span> BlockSkin<span class="br0">(</span><span class="kw1">new</span> BlockSkin_TextureLocation<span class="br0">(</span><span class="nu0">3</span>, <span class="nu0">0</span><span class="br0">)</span>, <span class="kw2">false</span><span class="br0">)</span>,
    <span class="kw1">new</span> BlockSkin<span class="br0">(</span><span class="kw1">new</span> BlockSkin_TextureLocation<span class="br0">(</span><span class="nu0">3</span>, <span class="nu0">0</span><span class="br0">)</span>, <span class="kw2">false</span><span class="br0">)</span>,
    <span class="kw1">new</span> BlockSkin<span class="br0">(</span><span class="kw1">new</span> BlockSkin_TextureLocation<span class="br0">(</span><span class="nu0">3</span>, <span class="nu0">0</span><span class="br0">)</span>, <span class="kw2">false</span><span class="br0">)</span>,
    <span class="kw1">new</span> BlockSkin<span class="br0">(</span><span class="kw1">new</span> BlockSkin_TextureLocation<span class="br0">(</span><span class="nu0">3</span>, <span class="nu0">0</span><span class="br0">)</span>, <span class="kw2">false</span><span class="br0">)</span>
<span class="br0">}</span><span class="br0">)</span><span class="sy0">;</span>
BlockManager.<span class="me1">register</span><span class="br0">(</span>blockWood<span class="br0">)</span><span class="sy0">;</span></pre>

</div>
<!-- EDIT3 SECTION "Face-Dependant Textures Block" [1387-2266] -->
<h2 class="sectionedit4" id="dynamic_textures_block">Dynamic Textures Block</h2>
<div class="level2">

<p>
Last but not least: What if a block wants to change its texture according to its environment?
</p>

<p>
<a href="/resources/fetch.php" class="media" title="http://destroflyer.mania-community.de/other/imagehost/cubes/block_grass.png"><img src="/resources/fetch.php" class="mediaright" alt="" width="150" /></a>
A nice example would be a grass block - If it's on the surface, it contains a nice grass texture at the top face and a little earth-grass-transition at the sides. Otherwise, all 6 sides should display an earth texture.
Special behaviours like this can be achieved by overwriting the <strong>getSkinIndex</strong> method:
</p>
<pre class="code java">Block blockGrass <span class="sy0">=</span> <span class="kw1">new</span> Block<span class="br0">(</span><span class="kw1">new</span> BlockSkin<span class="br0">[</span><span class="br0">]</span><span class="br0">{</span>
        <span class="co1">//We specify the 3 skins we need:</span>
        <span class="co1">//Grass, Earth-Grass-Transition and Earth</span>
        <span class="kw1">new</span> BlockSkin<span class="br0">(</span><span class="kw1">new</span> BlockSkin_TextureLocation<span class="br0">(</span><span class="nu0">0</span>, <span class="nu0">0</span><span class="br0">)</span>, <span class="kw2">false</span><span class="br0">)</span>,
        <span class="kw1">new</span> BlockSkin<span class="br0">(</span><span class="kw1">new</span> BlockSkin_TextureLocation<span class="br0">(</span><span class="nu0">1</span>, <span class="nu0">0</span><span class="br0">)</span>, <span class="kw2">false</span><span class="br0">)</span>,
        <span class="kw1">new</span> BlockSkin<span class="br0">(</span><span class="kw1">new</span> BlockSkin_TextureLocation<span class="br0">(</span><span class="nu0">2</span>, <span class="nu0">0</span><span class="br0">)</span>, <span class="kw2">false</span><span class="br0">)</span>
    <span class="br0">}</span><span class="br0">)</span><span class="br0">{</span>
 
    @Override
    <span class="co1">//The number that's being returned specified the index</span>
    <span class="co1">//of the skin in the previous declared BlockSkin array</span>
    <span class="kw1">protected</span> <span class="kw4">int</span> getSkinIndex<span class="br0">(</span>BlockChunkControl chunk, Vector3Int location, Block.<span class="me1">Face</span> face<span class="br0">)</span><span class="br0">{</span>
        <span class="kw1">if</span><span class="br0">(</span>chunk.<span class="me1">isBlockOnSurface</span><span class="br0">(</span>location<span class="br0">)</span><span class="br0">)</span><span class="br0">{</span>
            <span class="kw1">switch</span><span class="br0">(</span>face<span class="br0">)</span><span class="br0">{</span>
                <span class="kw1">case</span> Top<span class="sy0">:</span>
                    <span class="kw1">return</span> <span class="nu0">0</span><span class="sy0">;</span>
 
                <span class="kw1">case</span> Bottom<span class="sy0">:</span>
                    <span class="kw1">return</span> <span class="nu0">2</span><span class="sy0">;</span>
            <span class="br0">}</span>
            <span class="kw1">return</span> <span class="nu0">1</span><span class="sy0">;</span>
        <span class="br0">}</span>
        <span class="kw1">return</span> <span class="nu0">2</span><span class="sy0">;</span>
    <span class="br0">}</span>
<span class="br0">}</span><span class="sy0">;</span>
BlockManager.<span class="me1">register</span><span class="br0">(</span>blockGrass<span class="br0">)</span><span class="sy0">;</span></pre>

</div>
<!-- EDIT4 SECTION "Dynamic Textures Block" [2267-] -->
