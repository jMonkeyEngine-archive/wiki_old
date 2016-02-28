---
title: jMonkeyEngine SDK: Debugging, Profiling, Testing
---
<h1 class="sectionedit1" id="jmonkeyengine_sdkdebugging_profiling_testing">jMonkeyEngine SDK: Debugging, Profiling, Testing</h1>
<div class="level1">

<p>
Debugging, testing and profiling are important parts of the development cycle. This documentation shows you how to make the most of the jMonkeyEngine SDK's assistive features.
</p>

<p>
</p><p></p><div class="notetip">Since the jMonkeyEngine SDK is based on the NetBeans IDE and the NetBeans Platform, you can learn about certain jMonkeyEngine SDK features by reading the corresponding NetBeans IDE tutorials (in the “see also links”).
</div>


</div>
<!-- EDIT1 SECTION "jMonkeyEngine SDK: Debugging, Profiling, Testing" [1-478] -->
<h2 class="sectionedit2" id="testing">Testing</h2>
<div class="level2">

<p>
The jMonkeyEngine SDK supports the JUnit testing framework. It is a good practice to write tests (assertions) for each of your classes. Each test makes certain this “unit” (e.g. method) meets its design and behaves as intended. Run your tests after each major change and you immediately see if you broke something.
</p>

</div>

<h4 id="creating_tests">Creating Tests</h4>
<div class="level4">
<ol>
<li class="level1"><div class="li"> Right-click a Java file in the Projects window and choose Tools &gt; Create JUnit Tests.</div>
</li>
<li class="level1"><div class="li"> Click OK. The jMonkeyEngine SDK creates a JUnit test skeleton in the Test Package directory.</div>
</li>
<li class="level1"><div class="li"> The body of each generated test method is provided solely as a guide. In their place, you need to write your actual test cases!</div>
</li>
<li class="level1"><div class="li"> You can use tests such as <code>assertTrue(), assertFalse(), assertEquals()</code>, or <code>assert()</code>.</div>
<ul>
<li class="level2"><div class="li"> The following example assertions test an addition method: <code>assert( add(1, 1) == 2); assertTrue( add(7,-5) == add(-5,7) )…</code></div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> “Ideally”, you write a test case for every method (100% coverage).</div>
</li>
</ol>

<p>
<strong>Tip:</strong> Use the Navigate menu to jump from a test to its tested class, and back!
</p>

</div>

<h4 id="running_tests">Running Tests</h4>
<div class="level4">
<ol>
<li class="level1"><div class="li"> Run one or all tests:</div>
<ul>
<li class="level2"><div class="li"> Right-click the class in the Projects window and Choose Test File, or </div>
</li>
<li class="level2"><div class="li"> Right-click the project and select Test to run all tests.</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Check the Test window to see successful tests (green) and failures (red). </div>
</li>
<li class="level1"><div class="li"> If a test fails that has succeeded before, you know that your latest changes broke something!</div>
</li>
</ol>

<p>
Using unit tests regularly allows you to detect side-effects on classes that you thought were unaffected by a code change. 
</p>

<p>
See also:
</p>
<ul>
<li class="level1"><div class="li"> <a href="http://netbeans.org/kb/docs/java/junit-intro.html" class="urlextern" title="http://netbeans.org/kb/docs/java/junit-intro.html" rel="nofollow">Writing JUnit Tests</a></div>
</li>
<li class="level1"><div class="li"> <a href="http://www.junit.org" class="urlextern" title="http://www.junit.org" rel="nofollow">http://www.junit.org</a></div>
</li>
<li class="level1"><div class="li"> <a href="http://download.oracle.com/javase/1.4.2/docs/guide/lang/assert.html" class="urlextern" title="http://download.oracle.com/javase/1.4.2/docs/guide/lang/assert.html" rel="nofollow">Java Assertions</a></div>
</li>
</ul>

</div>
<!-- EDIT2 SECTION "Testing" [479-2245] -->
<h2 class="sectionedit3" id="debugging">Debugging</h2>
<div class="level2">

<p>
In the jMonkeyEngine SDK, you have access to a debugger to examine your application for errors such as deadlocks and NullPointerExeptions. You can set breakpoints, watch variables, and execute your code line-by-line to identify the source of a problem. 
</p>
<ol>
<li class="level1"><div class="li"> First, you set breakpoints and/or watches before the problematic lines of code where you suspect the bug.</div>
<ul>
<li class="level2"><div class="li"> If you want to watch a variable's value: Right-click on a variable and select New Watch from the context menu.</div>
</li>
<li class="level2"><div class="li"> If you want to step through the execution line by line: Right-click on a line and choose Toggle Line Breakpoint; a pink box appears as a mark.</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Choose “Debug &gt; Debug Main Project” to start a debugger session for the whole project. Or, right-click a file and select Debug File to debug only one file. </div>
</li>
<li class="level1"><div class="li"> The application starts running normally. If you have set a breakpoint, the execution stops in this line. Debugger windows open and print debugger output. </div>
</li>
<li class="level1"><div class="li"> You can do many things now to track down a bug:</div>
<ul>
<li class="level2"><div class="li"> Inspect the values of local variables.</div>
</li>
<li class="level2"><div class="li"> Use the Step buttons in the top to step into, out of, and over expressions while you watch the execution.</div>
</li>
<li class="level2"><div class="li"> Navigate through your application's call stack. Right-click on threads to suspend or resume them.</div>
</li>
<li class="level2"><div class="li"> Choose Debug &gt; Evaluate Expression from the menu to evaluate an expression. </div>
</li>
<li class="level2"><div class="li"> Move the mouse pointer over a variable to inspect its value in a tooltip.</div>
</li>
<li class="level2"><div class="li"> Inspect the classes loaded on the heap and the percentage and number of object instances. Right-click a class in the Loaded Classes window and choose Show in Instances view (JDK 6 only). </div>
</li>
<li class="level2"><div class="li"> And more…</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> To stop debugging, choose Debug &gt; End Debugger Session from the menu.</div>
</li>
</ol>

</div>
<!-- EDIT3 SECTION "Debugging" [2246-3982] -->
<h2 class="sectionedit4" id="profiling">Profiling</h2>
<div class="level2">

<p>
The profiler tool is used to monitor thread states, CPU performance, and memory usage of your jme3 application. It helps you detect memory leaks and bottlenecks in your game while it's running.
</p>

</div>

<h4 id="installing_the_profiler">Installing the Profiler</h4>
<div class="level4">

<p>
If you do not see a Profiler menu in the jMonkeyEngine SDK, you need to download the Profiler plugin first.
</p>
<ol>
<li class="level1"><div class="li"> Open the Tools &gt; Plugins menu, and got to the “Available plugins” tab </div>
</li>
<li class="level1"><div class="li"> Find the “Java Profiler” plugin (“Java SE” category) and check the Install box.</div>
</li>
<li class="level1"><div class="li"> Click the install button and follow the instructions.</div>
</li>
<li class="level1"><div class="li"> When you start the profiler for the first time, you are prompted to run a calibration once. Click OK in the “Profiler integration” dialog to complete the installation process.</div>
</li>
</ol>

</div>

<h4 id="monitoring_and_analyzing">Monitoring and Analyzing</h4>
<div class="level4">
<ol>
<li class="level1"><div class="li"> Choose Profile Project from the Profile menu. </div>
</li>
<li class="level1"><div class="li"> Select one of three tasks:</div>
<ul>
<li class="level2"><div class="li"> <strong>Monitor Application</strong> – Collect high-level information about properties of the target JVM, including thread activity and memory allocations.</div>
</li>
<li class="level2"><div class="li"> <strong>Analyze CPU Performance</strong> – Collect detailed data on application performance, including the time to execute methods and the number of times the method is invoked.</div>
</li>
<li class="level2"><div class="li"> <strong>Analyze Memory Usage</strong> – Collect detailed data on object allocation and garbage collection.</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Click Run. Your application starts and runs normally. </div>
</li>
<li class="level1"><div class="li"> Use the Profiling window to track and collect live profiling results while you application is running.</div>
</li>
</ol>

</div>

<h4 id="comparing_snapshots">Comparing Snapshots</h4>
<div class="level4">

<p>
Click the Take Snapshot button to capture the profiling data for later!
</p>
<ul>
<li class="level1"><div class="li"> You can store and view snapshots in the Profiling window. </div>
</li>
<li class="level1"><div class="li"> Choose Compare Snapshots from the profiler window to compare two selected snapshots</div>
</li>
</ul>

</div>

<h4 id="using_profiling_points">Using Profiling Points</h4>
<div class="level4">

<p>
Profiling points are similar to debugger breakpoints: You place them directly in the source code and they can trigger profiling behaviour when hit.
</p>
<ul>
<li class="level1"><div class="li"> Open a class in the browser, right-click in a line, and select Profiling &gt; Insert Profiling Point to add a profiling point here.</div>
</li>
<li class="level1"><div class="li"> Use Profiling points if you need a trigger to reset profiling results, take a snapshot or heap dump, record the timestamp or execution time of a code fragment, stop and start a load generator script (requires the load generator plugin).</div>
</li>
<li class="level1"><div class="li"> Open the Profiling Points window to view, modify and delete the Profiling Points in your projects. </div>
</li>
</ul>

<p>
See also:
</p>
<ul>
<li class="level1"><div class="li"> <a href="http://netbeans.org/kb/docs/java/profiler-intro.html" class="urlextern" title="http://netbeans.org/kb/docs/java/profiler-intro.html" rel="nofollow">Introduction to Profiling Java Applications (netbeans.org)</a></div>
</li>
<li class="level1"><div class="li"> <a href="http://netbeans.org/kb/docs/java/profiler-profilingpoints.html" class="urlextern" title="http://netbeans.org/kb/docs/java/profiler-profilingpoints.html" rel="nofollow">Using Profiling Points (netbeans.org)</a></div>
</li>
</ul>
<div class="tags"><span>
	<a href="/tag/documentation.html" class="wikilink1" title="tag:documentation" rel="tag">documentation</a>,
	<a href="/tag/sdk.html" class="wikilink1" title="tag:sdk" rel="tag">sdk</a>,
	<a href="/tag/tool.html" class="wikilink1" title="tag:tool" rel="tag">tool</a>
</span></div>

</div>
<!-- EDIT4 SECTION "Profiling" [3983-] -->
