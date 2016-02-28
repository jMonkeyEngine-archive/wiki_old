---
title: Creating an extension library plugin
---
<h1 class="sectionedit1" id="creating_an_extension_library_plugin">Creating an extension library plugin</h1>
<div class="level1">

<p>
This page describes how you can wrap any jar library into a plugin that a jMonkeyEngine SDK user can download, install and then use the contained library in his own game projects.
</p>

<p>
Make sure you have your SDK set up for plugin development <a href="/sdk/development/setup.html" class="wikilink1" title="sdk:development:setup">as described here</a>.
</p>

<p>
Creating the plugin project (in jMonkeyEngine SDK):
</p>
<ul>
<li class="level1"><div class="li"> Create a new Module Suite (or use an existing one)</div>
</li>
<li class="level1"><div class="li"> Open the suite, right-click the “Modules” folder and select “Add new..”</div>
</li>
<li class="level1"><div class="li"> For “Project Name” enter an all-lowercase name without spaces like <code>my-library</code></div>
</li>
<li class="level1"><div class="li"> Make sure the “Project Location” is inside the module suite folder and press “Next”</div>
</li>
<li class="level1"><div class="li"> Enter the base java package for your plugin in “Code Name Base” like <code>com.mycompany.plugins.mylibrary</code></div>
</li>
<li class="level1"><div class="li"> Enter a “Module Display Name” for your plugin like “My Library”</div>
</li>
<li class="level1"><div class="li"> Press Finish</div>
</li>
</ul>

<p>
Adding the library:
</p>
<ul>
<li class="level1"><div class="li"> Right click the Module Project and select “New→Other”</div>
</li>
<li class="level1"><div class="li"> Under “Module Development” select the “Java SE Library Descriptor” template and press “Next”</div>
</li>
<li class="level1"><div class="li"> If you dont have the external library registered in the jMonkeyEngine SDK yet, click “Manage Libraries” and do the following:</div>
<ul>
<li class="level2"><div class="li"> Click “New Library”, enter a name for the library and press OK</div>
</li>
<li class="level2"><div class="li"> In the “Classpath” tab, press “Add JAR/Folder” and select the jar file(s) needed for the library</div>
</li>
<li class="level2"><div class="li"> In the “JavaDoc” tab, press “Add ZIP/Folder” and add the javadoc for the library (zipped or folder)</div>
</li>
<li class="level2"><div class="li"> In the “Sources” tab you can add a folder or jar file containing the source files of the library if available</div>
</li>
<li class="level2"><div class="li"> Press OK</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Select the external library from the list and press “Next”</div>
</li>
<li class="level1"><div class="li"> Enter a name for the Library (used as filename for the description file)</div>
</li>
<li class="level1"><div class="li"> Enter a display name for the Library (This is the name the user later sees in his library list)</div>
</li>
<li class="level1"><div class="li"> Press OK</div>
</li>
</ul>

<p>
You will notice a new file “MyLibrary.xml” is created in the plugins base package and linked to in the layer.xml file. Additionally the jar file and sources /javadoc are copied into a “release” folder in the project root. This is basically it, you can configure a version number, license file (should be placed in Module root folder) and more via the Module Properties.
</p>

<p>
Note that the files in the release folder are <strong>not</strong> automatically updated when the library changes, you have to pack and replace the jar and zip files manually. See the build script extension in the link below on how you can make your module build script do that automatically.
</p>

<p>
After you are done, you can <a href="/sdk/development/setup.html" class="wikilink1" title="sdk:development:setup">contribute the plugin in the jMonkeyEngine SDK contribution update center</a>.
</p>

</div>
