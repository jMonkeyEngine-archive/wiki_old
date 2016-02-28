---
title: Render Buckets
---
<h1 class="sectionedit1" id="render_buckets">Render Buckets</h1>
<div class="level1">

<p>
For each viewport the rendering happens as follows:
</p>
<ul>
<li class="level1"><div class="li"> For each processor call preFrame</div>
</li>
<li class="level1"><div class="li"> Dispatch each geometry in a corresponding renderQueue (one for each Bucket) and build shadow queues</div>
</li>
<li class="level1"><div class="li"> For each processor call postQueues</div>
</li>
<li class="level1"><div class="li"> Rendering OpaqueBucket with object sorted front to back. (In order to minimize overdraw)</div>
</li>
<li class="level1"><div class="li"> Rendering SkyBucket with depth forced to 1.0. this means every object of this bucket will be far away and behind everything</div>
</li>
<li class="level1"><div class="li"> Rendering TransparentBucket with object sorted back to front. (So transparent objects can be seen correctly through each other)</div>
</li>
<li class="level1"><div class="li"> For each processor call postFrame</div>
</li>
<li class="level1"><div class="li"> Rendering TranslucentBucket with objects sorted back to front</div>
</li>
</ul>

<p>
The translucent bucket is rendered at the end. That’s where you put transparent object that you don’t want to be affected by post processing ( shadows or what ever). Self-light-emitting particle emitters (such as a fire) are a good example.
</p>

<p>
Post processors are not applied to this bucket with one exception : the FilterPostProcessor.
</p>

<p>
The filter post processor hijacks the rendering process and renders a full screen quad with the texture of the scene applied on it.
</p>

<p>
Once it’s done the depth buffer is 0, so it’s impossible to render a queue over it with proper depth test so if you use a FilterPostProcessor you have to add at the end of your filter stack the TranslucentBucketFilter. It will handle the translucent bucket rendering instead of the RenderManager. (Of course the correct depth information is passed to the filter).
</p>

<p>
The nice side effect of this is that if you want to apply a post filter to your translucent bucket (like bloom for example) you can just push up the translucent bucket filter in the filter stack.
</p>

</div>
