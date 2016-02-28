---
title: Creating a Character using MakeHuman
---
<h1 class="sectionedit1" id="creating_a_character_using_makehuman">Creating a Character using MakeHuman</h1>
<div class="level1">

<p>
Here's the procedure:
</p>
<ol>
<li class="level1"><div class="li"> If you haven't already, install the jMonkeyEngine3 SDK, launch the IDE, and create a JME3 project.</div>
</li>
<li class="level1"><div class="li"> Install the MakeHuman application, the Blender application, and the MakeHuman Blender tools.</div>
<ul>
<li class="level2"><div class="li"> Download the latest stable version of the MakeHuman application from <a href="http://www.makehuman.org/" class="urlextern" title="http://www.makehuman.org/" rel="nofollow">http://www.makehuman.org/</a></div>
</li>
<li class="level2"><div class="li"> Download the latest stable MakeHuman Blender tools from <a href="http://www.makehuman.org/" class="urlextern" title="http://www.makehuman.org/" rel="nofollow">http://www.makehuman.org/</a></div>
</li>
<li class="level2"><div class="li"> Download the corresponding (not necessarily the latest) version of the Blender application from <a href="http://www.blender.org/" class="urlextern" title="http://www.blender.org/" rel="nofollow">http://www.blender.org/</a></div>
</li>
<li class="level2"><div class="li"> Install the MakeHuman application as directed by <a href="http://www.makehuman.org/doc/node/install_makehuman.html" class="urlextern" title="http://www.makehuman.org/doc/node/install_makehuman.html" rel="nofollow">http://www.makehuman.org/doc/node/install_makehuman.html</a></div>
</li>
<li class="level2"><div class="li"> Install the Blender application.</div>
</li>
<li class="level2"><div class="li"> Install the MakeHuman tool scripts to Blender's scripts directory.  On Windows 7 machines, this involves unzipping the archive to <code>C:\Users\&lt;username&gt;\AppData\Roaming\Blender Foundation\Blender\&lt;version&gt;\scripts\addons</code></div>
</li>
<li class="level2"><div class="li"> Launch the Blender application, open a <code>User Preferences</code> editor, activate the <code>Addons</code> tab, and check the box labelled <code>Import-Export:Import:MakeHuman(.mhx)</code>.</div>
</li>
<li class="level2"><div class="li"> Click the <code>Save User Preferences</code> button.</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Generate an .mhx file containing a human figure.</div>
<ul>
<li class="level2"><div class="li"> Launch the MakeHuman application.</div>
</li>
<li class="level2"><div class="li"> Configure a human figure using the <code>Modelling</code>, <code>Geometries</code>, and <code>Materials</code> tabs.</div>
</li>
<li class="level2"><div class="li"> On the <code>Pose/Animate</code> tab, select a rig for animation if desired.</div>
</li>
<li class="level2"><div class="li"> Under the <code>Files</code> tab, select the <code>Save</code> sub-tab.</div>
</li>
<li class="level2"><div class="li"> Save to a file (in case you need to make changes later).  Note that there are two <code>Save</code> buttons: one in the <code>Save As</code> window which merely sets a pathname and another in the main window.  The .mhm file isn't written until you click the second <code>Save</code> button.</div>
</li>
<li class="level2"><div class="li"> Under the <code>Files</code> tab, select the <code>Export</code> sub-tab.</div>
</li>
<li class="level2"><div class="li"> Select <code>Blender exchange (mhx)</code> as the export format.</div>
</li>
<li class="level2"><div class="li"> Export to a file.  Again, there's a <code>Save</code> button in the Save As window which merely sets a pathname.  The .mhx file isn't written until you click the <code>Export</code> button in the main window.</div>
</li>
<li class="level2"><div class="li"> You may now close the MakeHuman application.</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Convert the .mhx file to a .blend file:</div>
<ul>
<li class="level2"><div class="li"> Launch the Blender application and delete the initial cube.</div>
</li>
<li class="level2"><div class="li"> From the <code>Info</code> editor's toolbar, select <code>File</code> &gt; <code>Import</code> &gt; <code>MakeHuman(.mhx)…</code></div>
</li>
<li class="level2"><div class="li"> In the <code>File Browser</code>, select your .mhx file and click the <code>Import MHX</code> button.</div>
</li>
<li class="level2"><div class="li"> After the import completes, you can view and edit the model using a <code>3D View</code> editor.</div>
</li>
<li class="level2"><div class="li"> From the <code>Info</code> editor's toolbar, select <code>File</code> &gt; <code>Save As…</code></div>
</li>
<li class="level2"><div class="li"> Select a pathname in the assets/Models folder of your JME3 project.</div>
</li>
<li class="level2"><div class="li"> Clicking the <code>Save As Blender File</code> button in the <code>File Browser</code> writes the file.</div>
</li>
<li class="level2"><div class="li"> You may now close the Blender application.</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Convert the .blend file to a .j3o file:</div>
<ul>
<li class="level2"><div class="li"> Launch the jMonkeyEngine3 IDE.</div>
</li>
<li class="level2"><div class="li"> Open your JME3 project.</div>
</li>
<li class="level2"><div class="li"> Under the <code>Project Assets</code> node of your project, open the <code>Models</code> folder.</div>
</li>
<li class="level2"><div class="li"> Right-click on your .blend file and select <code>Convert to j3o binary</code></div>
</li>
</ul>
</li>
</ol>

</div>
