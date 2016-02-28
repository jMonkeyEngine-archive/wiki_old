---
title: Submitting Your Plugin
---
<p>
</p><p></p><div class="noteimportant"><strong>IMPORTANT - (6th May 2014):</strong>
This page is for information purposes only. This system is still being developed.
</div>


<p>
If you wish to share your code with the jMonkey community, you can do so easily by <a href="http://hub.jmonkeyengine.org/plugins/submit.php" class="urlextern" title="http://hub.jmonkeyengine.org/plugins/submit.php" rel="nofollow">submitting your project to us</a>! Once your submission has been approved, your plugin will be listed on <a href="http://hub.jmonkeyengine.org/plugins/submissions.php" class="urlextern" title="http://hub.jmonkeyengine.org/plugins/submissions.php" rel="nofollow">the submissions page</a> and will be added to the plugin list within the next 24 hours (plugins are compiled once a day on our build server). Your submission may be refused if it is of bad taste, is empty, or is unrelated to jMonkey.
</p>

<h1 class="sectionedit1" id="submitting_your_plugin">Submitting Your Plugin</h1>
<div class="level1">
<ul>
<li class="level1"><div class="li"> Create a <code>jmeplugin.properties</code> file in your project. The contents of this file is outlined below and <strong>must</strong> be present. </div>
</li>
</ul>
<ul>
<li class="level1"><div class="li"> Upload your project to <a href="http://github.com" class="urlextern" title="http://github.com" rel="nofollow">GitHub</a> (See <a href="https://guides.github.com/activities/hello-world/" class="urlextern" title="https://guides.github.com/activities/hello-world/" rel="nofollow">GitHub's Hello World guide</a> if you need a quick introduction)</div>
</li>
</ul>
<ul>
<li class="level1"><div class="li"> Submit your project to us at <a href="http://hub.jmonkeyengine.org/plugins/submit.php" class="urlextern" title="http://hub.jmonkeyengine.org/plugins/submit.php" rel="nofollow">http://hub.jmonkeyengine.org/plugins/submit.php</a>.</div>
</li>
</ul>

</div>
<!-- EDIT1 SECTION "Submitting Your Plugin" [664-1097] -->
<h1 class="sectionedit2" id="configuring_the_plugin_properties_file">Configuring The Plugin Properties File</h1>
<div class="level1">

<p>
The plugin properties file <code>jmeplugin.properties</code> can be located anywhere in your project, and contains the descriptive data that will be displayed in the plugin list. You can modify the contents and location of this file at any point in the future should you wish to do so. The changes will be reflected the next time the plugin is compiled. Below is an example of the contents of the <code>jmeplugin.properties</code> file. The <code>DisplayName</code> and <code>Category</code> fields cannot be blank.
</p>
<pre class="code">DisplayName: TerrainPager
Category: jme-plugin
ShortDescription: A TerrainQuad based world generator and pager.
LongDescription: A really awesome TerrainQuad based world generator.</pre>

</div>
<!-- EDIT2 SECTION "Configuring The Plugin Properties File" [1098-1829] -->
<h1 class="sectionedit3" id="version_control">Version Control</h1>
<div class="level1">

<p>
When you submit your github repository to us you also have the opportunity to choose a branch. This allows you to have multiple versions of your code, which can be of great use. You can for example have “experimental, nightly, testing” and “stable” branches. You can then submit one of these branches to us. Our server will then only pull changes from the given branch. This allows you to modify and push your code to git, and only push changes to the branch you submitted when you want that code to go live.
</p>

</div>
<!-- EDIT3 SECTION "Version Control" [1830-] -->
