---
title: jMonkeyEngine SDK: Creating a model importer
---
<h1 class="sectionedit1" id="jmonkeyengine_sdkcreating_a_model_importer">jMonkeyEngine SDK: Creating a model importer</h1>
<div class="level1">

<p>
You can create custom model importers for the jMonkeyEngine SDK. The SDK supports NBM plugins.
</p>
<ol>
<li class="level1"><div class="li"> <a href="http://platform.netbeans.org/tutorials/nbm-filetype.html" class="urlextern" title="http://platform.netbeans.org/tutorials/nbm-filetype.html" rel="nofollow">Create an NBM plugin</a></div>
</li>
<li class="level1"><div class="li"> Add importer jar file (wrap jar file)</div>
</li>
<li class="level1"><div class="li"> Add filetype (Template)</div>
</li>
<li class="level1"><div class="li"> Change DataObject to extend SpatialAssetDataObject</div>
</li>
<li class="level1"><div class="li"> Implement getAssetKey(): if(!assetKey instanceof MyKeyType){assetKey = new MyKeyType(oldKey);} return key;</div>
</li>
<li class="level1"><div class="li"> Maybe implement loadAsset method in DataObject (if necessary, most model formats should load normally via the loader)</div>
</li>
<li class="level1"><div class="li"> Create AssetManagerConfigurator </div>
</li>
</ol>

<p>
See also:
</p>
<ul>
<li class="level1"><div class="li"> <a href="/sdk/development/projects_assets.html" class="wikilink1" title="sdk:development:projects_assets">Projects and Assets</a></div>
</li>
<li class="level1"><div class="li"> <a href="http://platform.netbeans.org/tutorials/nbm-filetype.html" class="urlextern" title="http://platform.netbeans.org/tutorials/nbm-filetype.html" rel="nofollow">http://platform.netbeans.org/tutorials/nbm-filetype.html</a></div>
</li>
</ul>
<div class="tags"><span>
	<a href="/tag/documentation.html" class="wikilink1" title="tag:documentation" rel="tag">documentation</a>,
	<a href="/tag/sdk.html" class="wikilink1" title="tag:sdk" rel="tag">sdk</a>,
	<a href="/tag/tool.html" class="wikilink1" title="tag:tool" rel="tag">tool</a>
</span></div>

</div>
