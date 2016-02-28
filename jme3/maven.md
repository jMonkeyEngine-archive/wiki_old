---
title: jME3 with Maven
---
<h1 class="sectionedit1" id="jme3_with_maven">jME3 with Maven</h1>
<div class="level1">

<p>
You can use jME3 with maven compatible build systems, the official maven repository for jME3 is at
<a href="http://updates.jmonkeyengine.org/maven/" class="urlextern" title="http://updates.jmonkeyengine.org/maven/" rel="nofollow">http://updates.jmonkeyengine.org/maven/</a>
</p>

<p>
The group id for all jME3 libraries is com.jme3, the following artifacts are currently available (version 3.0.10):
</p>
<ul>
<li class="level1"><div class="li"> jme3-core - Core libraries needed for all jME3 projects</div>
</li>
<li class="level1"><div class="li"> jme3-effects - Effects libraries for water and other post filters</div>
</li>
<li class="level1"><div class="li"> jme3-networking - jME3 networking libraries (aka spidermonkey)</div>
</li>
<li class="level1"><div class="li"> jme3-plugins - Loader plugins for OgreXML and jME-XML</div>
</li>
<li class="level1"><div class="li"> jme3-jogg - Loader for jogg audio files</div>
</li>
<li class="level1"><div class="li"> jme3-terrain - Terrain generation <abbr title="Application Programming Interface">API</abbr></div>
</li>
<li class="level1"><div class="li"> jme3-blender - Blender file loader, only works on desktop renderers</div>
</li>
<li class="level1"><div class="li"> jme3-jbullet - Physics support using jbullet (desktop only) <strong>Only jme3-jbullet OR jme3-bullet can be used</strong></div>
</li>
<li class="level1"><div class="li"> jme3-bullet - Physics support using native bullet, needs jme3-bullet-natives or jme3-bullet-natives-android (alpha)</div>
</li>
<li class="level1"><div class="li"> jme3-bullet-natives - Native libraries needed for bullet (not jbullet) on desktop (alpha)</div>
</li>
<li class="level1"><div class="li"> jme3-bullet-natives-android - Native libraries needed for bullet (not jbullet) on android (alpha)</div>
</li>
<li class="level1"><div class="li"> jme3-niftygui - NiftyGUI support for jME3</div>
</li>
<li class="level1"><div class="li"> jme3-desktop - Parts of the jME3 <abbr title="Application Programming Interface">API</abbr> that are only compatible with desktop renderers, needed for image loading on desktop</div>
</li>
<li class="level1"><div class="li"> jme3-lwjgl - Desktop renderer for jME3</div>
</li>
<li class="level1"><div class="li"> jme3-android - Android renderer for jME3</div>
</li>
<li class="level1"><div class="li"> jme3-ios - iOS renderer for jME3</div>
</li>
</ul>

<p>
For a basic desktop application to work you need to import at least
</p>
<ul>
<li class="level1"><div class="li"> jme3-core</div>
</li>
<li class="level1"><div class="li"> jme3-desktop</div>
</li>
<li class="level1"><div class="li"> jme3-lwjgl</div>
</li>
</ul>

<p>
For a basic android application to work you need to import at least
</p>
<ul>
<li class="level1"><div class="li"> jme3-core</div>
</li>
<li class="level1"><div class="li"> jme3-android</div>
</li>
</ul>

</div>
<!-- EDIT1 SECTION "jME3 with Maven" [1-1641] -->
<h2 class="sectionedit2" id="gradle">Gradle</h2>
<div class="level2">

<p>
If you happen to be using Gradle, you'll first need to add the repository, perhaps so it looks like this:
</p>
<pre class="code">repositories {
    mavenCentral()
    maven {
        url 'http://updates.jmonkeyengine.org/maven'
    }
}</pre>

<p>
Next you'll need to add dependencies on all the JARs – here's what it looks like for all desktop-related JARs, selecting the latest patch version:
</p>
<pre class="code">dependencies {
    compile 'com.jme3:jme3-core:3.0.+'
    compile 'com.jme3:jme3-effects:3.0.+'
    compile 'com.jme3:jme3-networking:3.0.+'
    compile 'com.jme3:jme3-plugins:3.0.+'
    compile 'com.jme3:jme3-jogg:3.0.+'
    compile 'com.jme3:jme3-terrain:3.0.+'
    compile 'com.jme3:jme3-blender:3.0.+'
    compile 'com.jme3:jme3-jbullet:3.0.+'
    compile 'com.jme3:jme3-niftygui:3.0.+'
    compile 'com.jme3:jme3-desktop:3.0.+'
    compile 'com.jme3:jme3-lwjgl:3.0.+'
}</pre>

<p>
If you'd rather factor out the “3.0” bit, you can also do this:
</p>
<pre class="code">def jmonkeyengine_version = '3.0'

dependencies {
    compile "com.jme3:jme3-core:$jmonkeyengine_version.+"
    compile "com.jme3:jme3-effects:$jmonkeyengine_version.+"
    compile "com.jme3:jme3-networking:$jmonkeyengine_version.+"
    compile "com.jme3:jme3-plugins:$jmonkeyengine_version.+"
    compile "com.jme3:jme3-jogg:$jmonkeyengine_version.+"
    compile "com.jme3:jme3-terrain:$jmonkeyengine_version.+"
    compile "com.jme3:jme3-blender:$jmonkeyengine_version.+"
    compile "com.jme3:jme3-jbullet:$jmonkeyengine_version.+"
    compile "com.jme3:jme3-niftygui:$jmonkeyengine_version.+"
    compile "com.jme3:jme3-desktop:$jmonkeyengine_version.+"
    compile "com.jme3:jme3-lwjgl:$jmonkeyengine_version.+"
}</pre>

</div>
<!-- EDIT2 SECTION "Gradle" [1642-] -->
