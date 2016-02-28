---
title: How to Build the jNavigation Recast Bindings
---
<h1 class="sectionedit1" id="how_to_build_the_jnavigation_recast_bindings">How to Build the jNavigation Recast Bindings</h1>
<div class="level1">

<p>
jNavigation is Java jME port for Recast Navigation written in C++. The project has two parts:
</p>
<ol>
<li class="level1"><div class="li"> <a href="https://github.com/QuietOne/jNavigation-native" class="urlextern" title="https://github.com/QuietOne/jNavigation-native" rel="nofollow">jNavigationNative</a> contains Recast Navigation library and C++ wrapper for java</div>
</li>
<li class="level1"><div class="li"> <a href="https://github.com/QuietOne/jNavigation" class="urlextern" title="https://github.com/QuietOne/jNavigation" rel="nofollow">jNavigation</a> is Java project that uses jNavigationNative and is the project that the end user will use</div>
</li>
</ol>

<p>
If there is need for updating Recast Navigation from native side, there are two kinds of updating bindings:
</p>
<ol>
<li class="level1"><div class="li"> only updating methods as the Recast made more efficient or more precise</div>
</li>
<li class="level1"><div class="li"> adding new methods for Recast use</div>
</li>
</ol>

</div>
<!-- EDIT1 SECTION "How to Build the jNavigation Recast Bindings" [1-661] -->
<h2 class="sectionedit2" id="updating_methods">Updating methods</h2>
<div class="level2">

<p>
Only updating methods are easy. The requirements needed:
</p>
<ul>
<li class="level1"><div class="li"> C++ compiler</div>
</li>
</ul>

<p>
The jNavigationNative that has following folders and files (it has more, but these are the most important for now):
</p>
<ul>
<li class="level1"><div class="li"> Recast</div>
<ul>
<li class="level2"><div class="li"> Include</div>
</li>
<li class="level2"><div class="li"> Source</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> README.md</div>
</li>
<li class="level1"><div class="li"> Recast_wrap.cxx - Java - C++ wrapper</div>
</li>
</ul>

<p>
Updating the methods is only the matter of putting all headers from Recast Navigation to Include folder, source to Source folders, and then building the project.
</p>

<p>
As author of this project used the NetBeans 7.4 for building the project, the following instruction is included, if the building from terminal doesn't work.
</p>
<ol>
<li class="level1"><div class="li"> Setting <a href="https://netbeans.org/kb/docs/cnd/beginning-jni-linux.html" class="urlextern" title="https://netbeans.org/kb/docs/cnd/beginning-jni-linux.html" rel="nofollow"> parameters for NetBeans compiler</a></div>
</li>
<li class="level1"><div class="li"> Remove all headers from Header Files</div>
</li>
<li class="level1"><div class="li"> Remove all source files <strong>EXCEPT Recast_wrap.cxx</strong> from Source Files</div>
</li>
<li class="level1"><div class="li"> Right click on Header files, select <code>Add Existing Item…</code> or <code>Add Existing Items from Folders…</code> and select needed headers</div>
</li>
<li class="level1"><div class="li"> Right click on Source files, select <code>Add Existing Item…</code> or <code>Add Existing Items from Folders…</code> and select needed source files</div>
</li>
<li class="level1"><div class="li"> Build</div>
</li>
<li class="level1"><div class="li"> Add built project to jNavigation project</div>
</li>
<li class="level1"><div class="li"> Build jNavigation project</div>
</li>
</ol>

</div>
<!-- EDIT2 SECTION "Updating methods" [662-1878] -->
<h3 class="sectionedit3" id="adding_new_methods_from_native_side">Adding new methods from native side</h3>
<div class="level3">

<p>
This is more complicated process and it includes the all work done in NetBeans mentioned in previous section. After that, there are two ways to add new function:
</p>
<ul>
<li class="level1"><div class="li"> manually adding code to wrapper</div>
</li>
<li class="level1"><div class="li"> creating new wrapper with <a href="http://swig.org/" class="urlextern" title="http://swig.org/" rel="nofollow">SWIG</a></div>
</li>
</ul>

</div>

<h4 id="manually_adding_code_to_wrapper">Manually adding code to wrapper</h4>
<div class="level4">

<p>
Example of method in wrapper:
</p>
<pre class="code java">SWIGEXPORT jint JNICALL Java_com_jme3_ai_navigation_utils_RecastJNI_rcIntArray_1size<span class="br0">(</span>JNIEnv <span class="sy0">*</span>jenv, jclass jcls, jlong jarg1, jobject jarg1_<span class="br0">)</span> <span class="br0">{</span>
 ...
<span class="br0">}</span></pre>

<p>
The Recast_wrap.cxx uses SWIG wrapper so for declaring method in wrapper you must first use the keyword <code>SWIGEXPORT</code> then returning type (for more information on returning types see <a href="http://docs.oracle.com/javase/1.5.0/docs/guide/jni/spec/types.html" class="urlextern" title="http://docs.oracle.com/javase/1.5.0/docs/guide/jni/spec/types.html" rel="nofollow">link</a>), then again keyword <code>JNICALL</code> and then as the name of method <code>Java_com_jme3_ai_navigation_utils_RecastJNI_</code> + <code>name of class</code> + <code>name of method</code>, after that, there goes list of parameters needed for the function (for more information see <a href="http://docs.oracle.com/javase/7/docs/technotes/guides/jni/spec/functions.html" class="urlextern" title="http://docs.oracle.com/javase/7/docs/technotes/guides/jni/spec/functions.html" rel="nofollow">link</a>). In body of method write how the function should be used.
</p>

<p>
After adding method to wrapper, compile project and add it to jNavigation.
In jNavigation project in class <code>com.jme3.ai.navigation.utils.RecastJNI.java</code> add native method, and after that add in class from which you would like to use this method to call this native method. It seems a little bit more complicated than it should be, but this also for support for updating native side with SWIG.
</p>

</div>

<h4 id="creating_new_wrapper_with_swig">Creating new wrapper with SWIG</h4>
<div class="level4">

<p>
In some temporary folder add all headers. It shouldn't contain any subfolders.
</p>

<p>
The following script was used for generating wrapper:
</p>
<pre class="code">%module Recast
%include "carrays.i"
%array_class(double, DoubleArray);
%array_class(float, FloatArray);
%array_class(int, IntArray);
%array_class(unsigned char, UCharArray);
%array_class(unsigned short, UShortArray);
%array_class(unsigned int, UIntArray);
%array_class(long, LongArray);
%array_class(bool, BooleanArray)

%{
#include "DetourAlloc.h"
#include "DetourAssert.h"
#include "DetourCommon.h"
#include "DetourCrowd.h"
#include "DetourLocalBoundary.h"
#include "DetourMath.h"
#include "DetourNavMesh.h"
#include "DetourNavMeshBuilder.h"
#include "DetourNavMeshQuery.h"
#include "DetourNode.h"
#include "DetourObstacleAvoidance.h"
#include "DetourPathCorridor.h"
#include "DetourPathQueue.h"
#include "DetourProximityGrid.h"
#include "DetourStatus.h"
#include "DetourTileCache.h"
#include "DetourTileCacheBuilder.h"
#include "Recast.h"
#include "RecastAlloc.h"
#include "RecastAssert.h"
%}

/* Let's just grab the original header file here */
%include "DetourAlloc.h"
%include "DetourAssert.h"
%include "DetourCommon.h"
%include "DetourCrowd.h"
%include "DetourLocalBoundary.h"
%include "DetourMath.h"
%include "DetourNavMesh.h"
%include "DetourNavMeshBuilder.h"
%include "DetourNavMeshQuery.h"
%include "DetourNode.h"
%include "DetourObstacleAvoidance.h"
%include "DetourPathCorridor.h"
%include "DetourPathQueue.h"
%include "DetourProximityGrid.h"
%include "DetourStatus.h"
%include "DetourTileCache.h"
%include "DetourTileCacheBuilder.h"
%include "Recast.h"
%include "RecastAlloc.h"
%include "RecastAssert.h"

%pragma(java) jniclasscode=%{
  static {
    System.load("Recast");
  }
%}</pre>

<p>
If there are more headers at some moment, include them in both places.
</p>
<ol>
<li class="level1"><div class="li"> Save script as Recast.i into temp folder with rest of the headers</div>
</li>
<li class="level1"><div class="li"> Install SWIG if not already</div>
</li>
<li class="level1"><div class="li"> Open terminal and go to folder where the script is</div>
</li>
<li class="level1"><div class="li"> Execute command <code>swig -c++ -java Recast.i</code></div>
</li>
<li class="level1"><div class="li"> Now SWIG will generate Java classes and new Recast_wrap.cxx</div>
</li>
<li class="level1"><div class="li"> Recast_wrap.cxx put in jNavigationNative with new headers and source files, as previously mentioned</div>
</li>
<li class="level1"><div class="li"> Build that project</div>
</li>
<li class="level1"><div class="li"> For jNavigation side, put only new methods in RecastJNI, and use where they are being used. For that you can see in Java class that are build with SWIG.</div>
</li>
<li class="level1"><div class="li"> If method uses some explicit SWIG type, try to use some method for converting it into jME type, or similar. You can probably find something in package <code>com.jme3.ai.navigation.utils</code></div>
</li>
</ol>

</div>
<!-- EDIT3 SECTION "Adding new methods from native side" [1879-] -->
