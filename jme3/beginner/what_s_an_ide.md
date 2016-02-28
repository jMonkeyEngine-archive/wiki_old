---
title: What's an IDE?
---
<h1 class="sectionedit1" id="what_s_an_ide">What's an IDE?</h1>
<div class="level1">
<ul>
<li class="level1"><div class="li"> IDE stands for Integrated Development Environment. It's a software tool for developers.</div>
</li>
<li class="level1"><div class="li"> NetBeans IDE, Eclipse, IntelliJ are examples of development environments (=IDEs) for developers who are writing Java applications. </div>
</li>
<li class="level1"><div class="li"> Java is a programming language.</div>
<ul>
<li class="level2"><div class="li"> “Java Beans” is just a funny way of naming a certain type of data object that you can write in Java. <br />
(Java = coffee… coffee beans, get it? No, developers aren’t very funny.) <br />
<em>Java Beans have nothing to do with this topic or NetBeans!</em></div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> jMonkeyEngine is a game engine written in Java. You use it by putting a JAR library on the class path, and calling its <abbr title="Application Programming Interface">API</abbr> from your Java code. </div>
</li>
<li class="level1"><div class="li"> The jMonkeyEngine <a href="/sdk.html" class="wikilink1" title="sdk">SDK</a> (Software Development Kit) is a customized NetBeans IDE that has special tools that help you develop 3D Java games.</div>
</li>
</ul>

<p>
</p><p></p><div class="noteimportant">The writing of the game (the actual game development) is still up to you, the person using these tools. There is an expectation that you, the person using these tools, already know how to program in Java. 
</div>


<p>
<a href="/resources/sdk-jme3-jmonkeyplatform.png" class="media" title="sdk:jme3-jmonkeyplatform.png"><img src="/resources/sdk-jme3-jmonkeyplatform.png" class="mediacenter" alt="" width="640" height="400" /></a>
</p>

</div>
<!-- EDIT1 SECTION "What's an IDE?" [1-1119] -->
<h2 class="sectionedit2" id="the_pasta_world_without_ides">The Past: A World Without IDEs</h2>
<div class="level2">

<p>
Let's say you have no IDE. The typical stuff that you need for game development is:
</p>
<ol>
<li class="level1"><div class="li"> Install the Java SDK (“JDK 6”) from Sun/Oracle. </div>
<ul>
<li class="level2"><div class="li"> The JDK includes essential development tools, such as the Java compiler (<code>javac</code>) and Java runtime (<code>java</code>).</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Install the jMonkeyEngine JAR libraries.</div>
<ul>
<li class="level2"><div class="li"> These libraries include the special classes that you need for game development.</div>
</li>
<li class="level2"><div class="li"> As with all Java applications, you put JAR libraries on the classpath. (<code>java -cp “bla.jar;foo.jar” myapp</code>…)</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Get a text editor to write .java and .xml files.</div>
</li>
<li class="level1"><div class="li"> Get a 3D model editor to preview 3D models and arrange them in scenes.</div>
</li>
<li class="level1"><div class="li"> Create Java project: </div>
<ol>
<li class="level2"><div class="li"> create directories for Java packages, </div>
</li>
<li class="level2"><div class="li"> create more directories for textures and sound files and 3D models, </div>
</li>
<li class="level2"><div class="li"> write an Ant build script, </div>
</li>
<li class="level2"><div class="li"> move JAR files around and check the classpath…</div>
</li>
</ol>
</li>
<li class="level1"><div class="li"> Write code:</div>
<ol>
<li class="level2"><div class="li"> write code in text editor, </div>
</li>
<li class="level2"><div class="li"> look up javadoc in the web browser, </div>
</li>
<li class="level2"><div class="li"> compile and then run code in the terminal, </div>
</li>
<li class="level2"><div class="li"> when you get error output in the terminal, go find the file and line back in text editor… </div>
</li>
</ol>
</li>
<li class="level1"><div class="li"> Repeat.</div>
</li>
</ol>

<p>
Basically, you switch back and forth between terminal, 3D model editor, web browser, and text editor a lot. You have to repeat lots of manual fine-tuning for every new file and project. 
</p>

<p>
Some people got annoyed by these maintenance tasks, and that's why they invented the IDE.
</p>

</div>
<!-- EDIT2 SECTION "The Past: A World Without IDEs" [1120-2566] -->
<h2 class="sectionedit3" id="the_presentthe_world_with_ides">The Present: The world with IDEs</h2>
<div class="level2">

<p>
An IDE is a source code editor that developers use to write applications and manage projects. It replaces the text editor – and all the switching between browser and terminal and text editors.
The essential word here is <strong>integrated</strong>: An IDE integrates all development tools (listed above) in one window.
</p>
<ul>
<li class="level1"><div class="li"> There are New Project and New File menu items that create directories and packages. It creates a professional Ant script. It manages the classpath for you. These formerly manual tasks are always the same for you – now they are automated in the “Project window”.</div>
</li>
<li class="level1"><div class="li"> The “Editor window” lets you edit Java and XML files. (more details below)</div>
</li>
<li class="level1"><div class="li"> You can drag and drop commonly used code snippets from a “Palette window” into your Java files.</div>
</li>
<li class="level1"><div class="li"> A “Navigator window” gives you a quick overview of long Java classes, and lets you jump to methods and fields.</div>
</li>
<li class="level1"><div class="li"> The Build button starts the JDK6 compiler (<code>ant</code> and <code>javac</code>), the Clean button runs <code>ant clean</code>, the Run button runs the application (<code>ant run</code> and <code>java</code>) – all these tasks are now once-click actions in a toolbar or context menu.</div>
</li>
<li class="level1"><div class="li"> After building and running, the IDE opens the “Application window”. This window is what end-users of your applications will see. Here you can test your gameplay.</div>
</li>
</ul>

<p>
<strong>The Editor</strong> is the heart of the IDE, and it has tons of great additional capabilties:
</p>
<ul>
<li class="level1"><div class="li"> The IDE tries to compile in the background what you write in the Editor. If you made a horrible, but obvious, mistake (forgot semicolon, mixed up data types, made a typo in a method call…) it tells you so immediately through warning colors and icons. This is called syntactic and semantic code highlighting. </div>
<ul>
<li class="level2"><div class="li"> You still get Terminal output for errors and warnings (in the “Output window” inside the IDE), but this way you erradicate tiny typos and compiletime errors immediately, and you can focus on serious runtime errors in the Output window.</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> The number of commands in the Java <abbr title="Application Programming Interface">API</abbr> is limited. So while you type a method or class name, there is only a limited number of things it can be. If you temporarily forgot what a method was called, the Editor pops up a list of options (plus javadoc comments), and you can simply select it.</div>
</li>
<li class="level1"><div class="li"> Similarly, every class and method only has a limited number of arguments. Again, the IDE pops up a list of expected arguments, so you don't need to search for them in the javadoc.</div>
</li>
</ul>

</div>
<!-- EDIT3 SECTION "The Present: The world with IDEs" [2567-5020] -->
<h2 class="sectionedit4" id="your_futurea_world_with_jmonkeyengine_sdk">Your Future: A World With jMonkeyEngine SDK</h2>
<div class="level2">

<p>
The jMonkeyEngine SDK is the same as NetBeans IDE, plus
</p>
<ul>
<li class="level1"><div class="li"> The New Project Wizards automatically adds the jMonkeyEngine libraries on the classpath and creates a build script.</div>
</li>
<li class="level1"><div class="li"> The javadoc popup dispalys Standard Java and jMonkeyEngine APIs in the editor.</div>
</li>
<li class="level1"><div class="li"> The Palette contains special code snippets from the jMonkeyEngine <abbr title="Application Programming Interface">API</abbr> for loading and saving 3D objects, input handling, nodes, lights, materials, rotation constants, etc.</div>
</li>
<li class="level1"><div class="li"> The Projects, SceneComposer, and SceneExplorer windows let you convert, preview, and arrange 3D models before you load them in your Java code.</div>
</li>
<li class="level1"><div class="li"> And more…</div>
</li>
</ul>

<p>
<a href="/resources/sdk-jmonkeyplatform-docu-1.png" class="media" title="sdk:jmonkeyplatform-docu-1.png"><img src="/resources/sdk-jmonkeyplatform-docu-1.png" class="mediacenter" alt="" /></a>
</p>

<p>
You see how such a unique IDE can speed up your development process drastically, it's worth giving it a try!
</p>
<ul>
<li class="level1"><div class="li"> <a href="http://www.youtube.com/watch?v=cTErYjsJ_Yk" class="urlextern" title="http://www.youtube.com/watch?v=cTErYjsJ_Yk" rel="nofollow">Video: jMonkeyEngine3 - Intro</a></div>
</li>
<li class="level1"><div class="li"> <a href="/sdk/comic.html" class="wikilink1" title="sdk:comic">jMonkeyEngine SDK - the Comic</a></div>
</li>
</ul>

</div>
<!-- EDIT4 SECTION "Your Future: A World With jMonkeyEngine SDK" [5021-] -->
