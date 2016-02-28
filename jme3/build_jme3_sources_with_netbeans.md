---
title: Setting up JME3 in Netbeans 6+
---
<h1 class="sectionedit1" id="setting_up_jme3_in_netbeans_6">Setting up JME3 in Netbeans 6+</h1>
<div class="level1">

<p>
You are welcome to try out the new jME3, and contribute patches and features! This document shows how to download, set up, build, and run the latest development version from the sources. These instructions work in NetBeans IDE 6 or better.
</p>

<p>
Note: In the following, always replace “~” with the path to your home directory.
</p>

</div>
<!-- EDIT1 SECTION "Setting up JME3 in Netbeans 6+" [1-369] -->
<h2 class="sectionedit2" id="downloading_the_sources">Downloading the Sources</h2>
<div class="level2">

<p>
Check out the sources from the repository. (The following NetBeans instructions are equivalent to executing <code>cd ~/NetBeansProjects; svn checkout <a href="http://jmonkeyengine.googlecode.com/svn/branches/3.0final/engine" class="urlextern" title="http://jmonkeyengine.googlecode.com/svn/branches/3.0final/engine" rel="nofollow">http://jmonkeyengine.googlecode.com/svn/branches/3.0final/engine</a> jme3</code> on the commandline.)
</p>
<ol>
<li class="level1"><div class="li"> In NetBeans go to Team &gt; Subversion &gt; Checkout</div>
<ol>
<li class="level2"><div class="li"> Repository <abbr title="Uniform Resource Locator">URL</abbr>: <code><a href="https://jmonkeyengine.googlecode.com/svn" class="urlextern" title="https://jmonkeyengine.googlecode.com/svn" rel="nofollow">https://jmonkeyengine.googlecode.com/svn</a></code></div>
</li>
<li class="level2"><div class="li"> You can leave user/pw blank for anonymous access. </div>
</li>
</ol>
</li>
<li class="level1"><div class="li"> Click Next</div>
<ol>
<li class="level2"><div class="li"> Repository Folders: <code>branches/3.0final/engine</code></div>
</li>
<li class="level2"><div class="li"> Enable the checkbox to Skip “engine” and only checkout its contents.</div>
</li>
<li class="level2"><div class="li"> Local Folder: <code>~/NetBeansProjects/jme3</code></div>
</li>
</ol>
</li>
<li class="level1"><div class="li"> Click Finish and wait.</div>
</li>
</ol>

<p>
The jme3 project opens in the Project window. It already includes a working ANT build script for building and running.
</p>

<p>
Look into the Libraries node and confirm that the project depends on the following libraries in the classpath:
</p>
<ul>
<li class="level1"><div class="li"> j-ogg-oggd.jar        </div>
</li>
<li class="level1"><div class="li"> j-ogg-vorbisd.jar       </div>
</li>
<li class="level1"><div class="li"> jbullet.jar	         </div>
</li>
<li class="level1"><div class="li"> stack-alloc.jar</div>
</li>
<li class="level1"><div class="li"> vecmath.jar     </div>
</li>
<li class="level1"><div class="li"> lwjgl.jar       </div>
</li>
<li class="level1"><div class="li"> jME3-lwjgl-natives.jar	</div>
</li>
<li class="level1"><div class="li"> jinput.jar	</div>
</li>
<li class="level1"><div class="li"> eventbus.jar</div>
</li>
<li class="level1"><div class="li"> nifty-default-controls.jar                              </div>
</li>
<li class="level1"><div class="li"> nifty-examples.jar                              </div>
</li>
<li class="level1"><div class="li"> nifty-style-black.jar                              </div>
</li>
<li class="level1"><div class="li"> nifty.jar</div>
</li>
<li class="level1"><div class="li"> jglfont-core.jar                              </div>
</li>
<li class="level1"><div class="li"> xmlpull-xpp3.jar</div>
</li>
<li class="level1"><div class="li"> android.jar</div>
</li>
<li class="level1"><div class="li"> jME3-bullet-natives.jar</div>
</li>
<li class="level1"><div class="li"> gluegen-rt.jar</div>
</li>
<li class="level1"><div class="li"> joal.jar</div>
</li>
<li class="level1"><div class="li"> jogl-all.jar</div>
</li>
<li class="level1"><div class="li"> jME3-natives-joal.jar</div>
</li>
<li class="level1"><div class="li"> jME3-openal-soft-natives-android.jar</div>
</li>
</ul>

<p>
For a detailed description of the separate jar files see <a href="/jme3/jme3_source_structure.html" class="wikilink1" title="jme3:jme3_source_structure">this list</a>.
</p>

</div>
<!-- EDIT2 SECTION "Downloading the Sources" [370-2029] -->
<h2 class="sectionedit3" id="build_the_project_and_run_a_sample_app">Build the Project and Run a Sample App</h2>
<div class="level2">
<ol>
<li class="level1"><div class="li"> Right-click the jme3 project node and “Clean and Build” the project.</div>
</li>
<li class="level1"><div class="li"> In the Projects window, open the <code>Test</code> folder which contains the sample apps.</div>
</li>
<li class="level1"><div class="li"> Every file with a Main class (for example <code>jme3test.model/TestHoverTank.java</code> or <code>jme3test.game/CubeField.java</code>) is an app.</div>
</li>
<li class="level1"><div class="li"> Right-click a sample app and choose “Run File” (Shift-F6).</div>
</li>
<li class="level1"><div class="li"> Generally in sample apps:</div>
<ol>
<li class="level2"><div class="li"> the mouse and the WASD keys control movement</div>
</li>
<li class="level2"><div class="li"> the Esc key exits the application</div>
</li>
</ol>
</li>
</ol>

</div>
<!-- EDIT3 SECTION "Build the Project and Run a Sample App" [2030-2555] -->
<h2 class="sectionedit4" id="optionaljavadoc_popups_and_source_navigation_in_netbeans">Optional: Javadoc Popups and Source Navigation in NetBeans</h2>
<div class="level2">

<p>
If you are working on the jme3 sources:
</p>
<ol>
<li class="level1"><div class="li"> In the Projects window, right-click the jme3 project and choose Generate Javadoc. Wait.</div>
</li>
<li class="level1"><div class="li"> Confirm in the Files window that the javadoc has been created in <code>~/NetBeansProjects/jme3/dist/javadoc</code></div>
</li>
<li class="level1"><div class="li"> In the editor, place the caret in a jme class and press ctrl-space to view javadoc.</div>
</li>
</ol>

<p>
If you are working on a game project that depends on jme3:
</p>
<ol>
<li class="level1"><div class="li"> First follow the previous tip. (In the future, we may offer jme javadoc as download instead.)</div>
</li>
<li class="level1"><div class="li"> In your game project, right-click the Libraries node and choose “Properties”.</div>
</li>
<li class="level1"><div class="li"> In the Library properties, select jme3.jar and click the Edit button.</div>
<ol>
<li class="level2"><div class="li"> For the Javadoc field, browse to <code>~/NetBeansProjects/jme3/dist/javadoc</code>. Check “as relative path” and click select.</div>
</li>
<li class="level2"><div class="li"> For the Sources field, browse to <code>~/NetBeansProjects/jme3/src</code>. Check “as relative path” and click select.</div>
</li>
<li class="level2"><div class="li"> Click OK.</div>
</li>
</ol>
</li>
<li class="level1"><div class="li"> In the editor, place the caret in a jme class and press ctrl-space to view javadoc. Ctrl-click any jme3 method to jump to its definition in the sources. </div>
</li>
</ol>

<p>
This tip works for any third-party JAR library that you use. (You may have to download the javadoc/sources from their home page separately).
</p>
<hr />

<p>
Sources used: <a href="http://code.google.com/p/jmonkeyengine/wiki/BuildJme3" class="urlextern" title="http://code.google.com/p/jmonkeyengine/wiki/BuildJme3" rel="nofollow">BuildJme3</a>, <a href="http://www.jmonkeyengine.com/forum/index.php?topic=13108.0" class="urlextern" title="http://www.jmonkeyengine.com/forum/index.php?topic=13108.0" rel="nofollow">NetBeans tutorial from forum</a>
</p>
<div class="tags"><span>
	<a href="/tag/documentation.html" class="wikilink1" title="tag:documentation" rel="tag">documentation</a>,
	<a href="/tag/install.html" class="wikilink1" title="tag:install" rel="tag">install</a>
</span></div>

</div>
<!-- EDIT4 SECTION "Optional: Javadoc Popups and Source Navigation in NetBeans" [2556-] -->
