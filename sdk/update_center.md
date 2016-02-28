---
title: Automatically Updating jMonkeyEngine SDK
---
<h2 class="sectionedit1" id="automatically_updating_jmonkeyengine_sdk">Automatically Updating jMonkeyEngine SDK</h2>
<div class="level2">

</div>
<!-- EDIT1 SECTION "Automatically Updating jMonkeyEngine SDK" [1-53] -->
<h3 class="sectionedit2" id="getting_stable_updates">Getting stable updates</h3>
<div class="level3">

<p>
The jMonkeyEngine SDK includes an automatic web update feature. To run an update, simply go to Help→Check for Updates and you will get the most current stable update of the SDK and the engine. By default the IDE will check every week for new updates and inform you about them with a symbol in the lower right.
</p>

</div>
<!-- EDIT2 SECTION "Getting stable updates" [54-397] -->
<h3 class="sectionedit3" id="testing_the_nightly_version">Testing the nightly version</h3>
<div class="level3">

<p>
You can test the nightly version with all the latest untested features to give feedback to the developers. Be warned however, the changes in the nightly versions might break your current game project if heavy changes have been committed. To make sure that you do not break your current development environment it is recommended to use a separate application and settings directory for the nightly version.
</p>
<ul>
<li class="level1"><div class="li"> Copy the whole application (folder) to a new name like jmonkeyplatform_nightly.</div>
</li>
<li class="level1"><div class="li"> Edit the file jmonkeyplatform.conf in the etc directory of the folder. Mac users have to right-click the application and select “Show package contents” and then navigate to Contents/Resources/jmonkeyplatform.</div>
</li>
<li class="level1"><div class="li"> Change the default_userdir or default_mac_userdir from “${HOME}/.${APPNAME}/version” to something like “${HOME}/.${APPNAME}/nightly”.</div>
</li>
</ul>

<p>
Then start the new application and have your SDK being updated to the most current nightly version:
</p>
<ul>
<li class="level1"><div class="li"> Go to Tools→Plugins</div>
</li>
<li class="level1"><div class="li"> Select the “Settings” tab</div>
</li>
<li class="level1"><div class="li"> Select the checkbox for “jMonkeyEngine SDK nightly svn”</div>
</li>
<li class="level1"><div class="li"> Make sure the “force install to shared directories” checkbox is selected</div>
</li>
<li class="level1"><div class="li"> Select the “Updates” tab</div>
</li>
<li class="level1"><div class="li"> Press “Reload Catalog”</div>
</li>
<li class="level1"><div class="li"> Press “Update”</div>
</li>
</ul>
<div class="tags"><span>
	<a href="/tag/documentation.html" class="wikilink1" title="tag:documentation" rel="tag">documentation</a>,
	<a href="/tag/sdk.html" class="wikilink1" title="tag:sdk" rel="tag">sdk</a>,
	<a href="/tag/builds.html" class="wikilink1" title="tag:builds" rel="tag">builds</a>,
	<a href="/tag/update.html" class="wikilink1" title="tag:update" rel="tag">update</a>
</span></div>

</div>
<!-- EDIT3 SECTION "Testing the nightly version" [398-] -->
