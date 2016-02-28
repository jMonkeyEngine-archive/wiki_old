---
title: Building jMonkeyEngine SDK Yourself
---
<h2 class="sectionedit1" id="building_jmonkeyengine_sdk_yourself">Building jMonkeyEngine SDK Yourself</h2>
<div class="level2">

</div>
<!-- EDIT1 SECTION "Building jMonkeyEngine SDK Yourself" [1-49] -->
<h3 class="sectionedit2" id="in_the_jmonkeyengine_sdk_or_netbeans">In the jMonkeyEngine SDK or NetBeans</h3>
<div class="level3">

</div>

<h4 id="plugins">Plugins</h4>
<div class="level4">

<p>
Make sure all necessary plugins are installed and active:
</p>
<ul>
<li class="level1"><div class="li"> From the menu bar, select <code>Tools</code> → <code>Plugins</code> to open a <code>Plugins</code> dialog.</div>
</li>
<li class="level1"><div class="li"> Select the <code>Available Plugins</code> tab.</div>
</li>
<li class="level1"><div class="li"> Sort the plugin list by category.</div>
</li>
<li class="level1"><div class="li"> Check the <code>Install</code> checkbox for any plugins in the <code>Developing NetBeans</code> category.</div>
</li>
<li class="level1"><div class="li"> Click on the <code>Install</code> button and complete the wizard.</div>
</li>
<li class="level1"><div class="li"> Select the <code>Installed</code> tab.</div>
</li>
<li class="level1"><div class="li"> Activate any inactive plugins in the <code>Developing NetBeans</code> category.</div>
</li>
<li class="level1"><div class="li"> Close the <code>Plugins</code> dialog.</div>
</li>
</ul>

</div>

<h4 id="checkout">Checkout</h4>
<div class="level4">
<ul>
<li class="level1"><div class="li"> From the menu bar, select <code>Team</code> → <code>Git</code> → <code>Clone</code> to open a <code>Clone Repository</code> dialog.</div>
</li>
<li class="level1"><div class="li"> In the <code>Repository <abbr title="Uniform Resource Locator">URL</abbr>:</code> textbox, type <code><a href="https://github.com/jMonkeyEngine/jmonkeyengine" class="urlextern" title="https://github.com/jMonkeyEngine/jmonkeyengine" rel="nofollow">https://github.com/jMonkeyEngine/jmonkeyengine</a></code>.</div>
</li>
<li class="level1"><div class="li"> Clear the <code>User:</code> and <code>Password:</code> textboxes.</div>
</li>
<li class="level1"><div class="li"> Click on the <code>Next</code> button.</div>
</li>
<li class="level1"><div class="li"> Choose the remote branch, typically “master”, and click the Next button.</div>
</li>
<li class="level1"><div class="li"> Click on the <code>Browse…</code> button to the right of the <code>Parent directory:</code> textbox to open a <code>Browse Local Folder</code> dialog.</div>
</li>
<li class="level1"><div class="li"> Select an empty or non-existent directory (folder) where you want to save the jMonkeyEngine sources on your hard drive.</div>
</li>
<li class="level1"><div class="li"> Click the <code>Finish</code> button.</div>
</li>
</ul>

<p>
Project checkout may take awhile.  Do not proceed before the task is complete.
</p>

</div>

<h4 id="build">Build</h4>
<div class="level4">

<p>
On the commandline:
</p>
<ol>
<li class="level1"><div class="li"> <code>cd jmonkeyengine</code></div>
</li>
<li class="level1"><div class="li"> <code>./gradlew build</code></div>
</li>
</ol>

<p>
From the SDK:
</p>
<ul>
<li class="level1"><div class="li"> From the menu bar, select <code>File</code> → <code>Open project…</code> to open an <code>Open Project</code> dialog.</div>
</li>
<li class="level1"><div class="li"> Highlight the free-form project folder you used for checkout and click on the <code>Open Project</code> button.</div>
<ul>
<li class="level2"><div class="li"> A new free-form project named <code>jME3-SDK</code> should appear in the SDK's <code>Projects</code> window.</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Build the free-form project by right-clicking on it and selecting <code>Build</code>.</div>
</li>
<li class="level1"><div class="li"> Wait until the <code>jME3-SDK (build)</code> task is complete.  At one point, a web browser window may open.</div>
</li>
<li class="level1"><div class="li"> From the menu bar, select <code>File</code> → <code>Open project…</code> to open an <code>Open Project</code> dialog.</div>
</li>
<li class="level1"><div class="li"> Browse into the free-form project folder, highlight the <code>sdk</code> node, and click on the <code>Open Project</code> button.</div>
<ul>
<li class="level2"><div class="li"> A number of new projects should appear in the SDK's <code>Projects</code> window.</div>
</li>
</ul>
</li>
</ul>

<p>
Building the main freeform project copies the jME3 libraries to the sdk, so you should run its build script each time jME3 changes.
</p>

</div>

<h4 id="run">Run</h4>
<div class="level4">
<ul>
<li class="level1"><div class="li"> In the SDK's <code>Projects</code> window, right-click on the <code>jMonkeyEngine SDK</code> project and select <code>Run</code>.</div>
<ul>
<li class="level2"><div class="li"> The SDK you just built will start executing in a new window.</div>
</li>
</ul>
</li>
</ul>
<div class="tags"><span>
	<a href="/tag/documentation.html" class="wikilink1" title="tag:documentation" rel="tag">documentation</a>,
	<a href="/tag/sdk.html" class="wikilink1" title="tag:sdk" rel="tag">sdk</a>,
	<a href="/tag/builds.html" class="wikilink1" title="tag:builds" rel="tag">builds</a>,
	<a href="/tag/project.html" class="wikilink1" title="tag:project" rel="tag">project</a>
</span></div>

</div>
<!-- EDIT2 SECTION "In the jMonkeyEngine SDK or NetBeans" [50-] -->
