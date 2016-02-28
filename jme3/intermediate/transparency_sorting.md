---
title: Transparency Sorting
---
<h1 class="sectionedit1" id="transparency_sorting">Transparency Sorting</h1>
<div class="level1">

<p>
There is often a lot of confusion with how pixels get processed in relation to the z-buffer and why sorting is important.  Most importantly it can be mind-warping trying to wrap one's head around how to 'fix' the cases where proper sorting isn't possible.
</p>

<p>
Hopefully these diagrams help show the futility of it all… I mean the trade offs one has to make to get transparency looking its best in the general case.
</p>

<p>
The first image I'll show is the 'best case' where all objects are drawn back to front.  I'll then discuss briefly the steps JME goes through to try to make that happen.
</p>

<p>
<a href="/resources/jme3-intermediate-transparency_sorting1.png" class="media" title="jme3:intermediate:transparency_sorting1.png"><img src="/resources/jme3-intermediate-transparency_sorting1.png" class="mediacenter" alt="" width="600" /></a>
</p>

<p>
In JME, the opaque layer would generally be placed in the opaque bucket.  All opaque layers are drawn first and within the ability to sort them, they are sorted front to back to prevent overdraw.
</p>

<p>
After the opaque bucket is drawn, the transparent bucket is drawn and it is sorted back to front.  So in the ideal case it would appear exactly as in this picture.
</p>

<p>
</p><p></p><div class="noteclassic">Sorting is done at the object level and it can never be perfect.  It is impossible to properly sort objects by distance in the general case even if they were just triangles.  Simply imagine intersecting triangles and it's clear there is no proper order.  JME tries its best.
</div>


<p>
Next I'll show an image of the worst case scenario to show why sorting is important and how your 'best friend' the z-buffer is really transparency's worst enemy.
</p>

<p>
<a href="/resources/jme3-intermediate-transparency_sorting2.png" class="media" title="jme3:intermediate:transparency_sorting2.png"><img src="/resources/jme3-intermediate-transparency_sorting2.png" class="mediacenter" alt="" width="600" /></a>
</p>

<p>
This is what will happen if you put all of your objects in the opaque buffer.  JME will sort them front to back and you will get these strange 'windows' into your background.
</p>

<p>
</p><p></p><div class="noteclassic">ecause sorting is done at the object level, you may have triangle to triangle overlap even within the same mesh if it is non-convex.  Think of a glass donut where the near surface triangles are drawn before the hole's triangles.  There will be this same issue where they occlude the farther triangles.  A different angle on the donut might produce the correct results depending on the order of the triangles in the mesh.
</div>


<p>
Finally, I'll augment the worst case sorting with something like <code>alphaDiscardThreshold</code> (or the old alphaTest/alphaFalloff values).  In this example, let's pretend we only discard pixels with alpha = 0.
</p>

<p>
<a href="/resources/jme3-intermediate-transparency_sorting3.png" class="media" title="jme3:intermediate:transparency_sorting3.png"><img src="/resources/jme3-intermediate-transparency_sorting3.png" class="mediacenter" alt="" width="600" /></a>
</p>

<p>
It's better but not perfect.  Any partially transparent pixels will still show the issue.  Partial transparency will drive you crazy if you let it.
</p>

<p>
Bottom line:
</p>
<ul>
<li class="level1"><div class="li"> back to front sorting would fix all issues</div>
</li>
<li class="level1"><div class="li"> accurate back to front sorting in the general case is impossible</div>
</li>
<li class="level1"><div class="li"> for purely on/off a = 1 or a = 0 transparency then a discard threshold is the best bet to mitigate sorting problems.</div>
</li>
<li class="level1"><div class="li"> Where 0 &lt; alpha &lt; 1, improper sorting of triangles/pixels will always cause artifacts.</div>
</li>
</ul>
<div class="tags"><span>
	<a href="/tag/transparent.html" class="wikilink1" title="tag:transparent" rel="tag">transparent</a>,
	<a href="/tag/sorting.html" class="wikilink1" title="tag:sorting" rel="tag">sorting</a>,
	<a href="/tag/bucket.html" class="wikilink1" title="tag:bucket" rel="tag">bucket</a>,
	<a href="/tag/z-buffer.html" class="wikilink1" title="tag:z-buffer" rel="tag">z-buffer</a>,
	<a href="/tag/alpha.html" class="wikilink1" title="tag:alpha" rel="tag">alpha</a>
</span></div>

</div>
