---
title: jMonkeyEngine SDK: Code Editor and Palette
---
<h1 class="sectionedit1" id="jmonkeyengine_sdkcode_editor_and_palette">jMonkeyEngine SDK: Code Editor and Palette</h1>
<div class="level1">

<p>
The Source Code Editor is the central part of the jMonkeyEngine SDK. This documentation shows you how to make the most of the jMonkeyEngine SDK's assistive features.
</p>

<p>
Note: Since the jMonkeyEngine SDK is based on the NetBeans Platform framework, you can learn about certain jMonkeyEngine SDK features by reading the corresponding NetBeans IDE tutorials (in the “see also links”). 
</p>

</div>
<!-- EDIT1 SECTION "jMonkeyEngine SDK: Code Editor and Palette" [1-440] -->
<h2 class="sectionedit2" id="code_completion_and_code_generation">Code Completion and Code Generation</h2>
<div class="level2">

<p>
While typing Java code in the source code editor, you will see popups that help you to write more quickly by completing keywords, and generating code snippets. Additionally, they will let you see the javadoc for the classes you are working with.
</p>

<p>
<a href="/resources/sdk-netbeans_code_completion.png" class="media" title="sdk:netbeans_code_completion.png"><img src="/resources/sdk-netbeans_code_completion.png" class="mediaright" alt="" /></a>
</p>

<p>
<strong>Code Completion</strong>
</p>
<ul>
<li class="level1"><div class="li"> Complete keyword / method / variable: <strong>Ctrl-Space</strong> <br />
Alternatively you can also use <strong>Ctrl-\</strong>.</div>
<ul>
<li class="level2"><div class="li"> Customize Code Completion options: Tools &gt; Options &gt; Editor &gt; Code Completion </div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Show expected parameters of this method in a tooltip: <strong>Ctrl-P</strong> </div>
</li>
<li class="level1"><div class="li"> Complete any string (even non-Java) that has been used before: <strong>(Shift-)Ctrl-K</strong></div>
</li>
</ul>

<p>
<strong>Code Generation</strong>
</p>
<ul>
<li class="level1"><div class="li"> Auto-fix import statements: <strong>Ctrl-Shift-I</strong></div>
</li>
<li class="level1"><div class="li"> Auto-generate getters/setters, try/catch, equals/hashCode: <strong>Alt-Insert</strong></div>
<ul>
<li class="level2"><div class="li"> Customize code completion: Choose Tools &gt; Options &gt; Editor &gt; Code Completion</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Auto-generate common code snippets such as loops, declarations, println, by typing the <strong>template name + TabKey</strong> </div>
<ul>
<li class="level2"><div class="li"> Customize code templates: Choose Tools &gt; Options &gt; Editor &gt; Code Templates</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Rename, move, or introduce methods, fields, and variables, without breaking the project: <strong>Refactoring menu</strong></div>
</li>
</ul>

</div>
<!-- EDIT2 SECTION "Code Completion and Code Generation" [441-1686] -->
<h2 class="sectionedit3" id="semantic_and_syntactic_coloring">Semantic and Syntactic Coloring</h2>
<div class="level2">

<p>
<a href="/resources/sdk-jmonkeyplatform-docu-5.png" class="media" title="sdk:jmonkeyplatform-docu-5.png"><img src="/resources/sdk-jmonkeyplatform-docu-5.png" class="mediaright" alt="" width="421" height="298" /></a>
</p>

<p>
The text color in the editor gives you important hints how the compiler will interpret what you typed, even before you compiled it.
</p>

<p>
Examples:
</p>
<ul>
<li class="level1"><div class="li"> Java keywords are <strong>blue</strong>, variables and fields are <strong>green</strong>, parameters are <strong>orange</strong>. </div>
</li>
<li class="level1"><div class="li"> <del>Strikethrough</del> means deprecated method or field. </div>
</li>
<li class="level1"><div class="li"> <em class="u">Gray underline</em> means unused variable or method.</div>
</li>
<li class="level1"><div class="li"> Place the caret in a method or variable and all its ocurrences are marked <strong>tan</strong>.</div>
</li>
<li class="level1"><div class="li"> Place the caret in a method's return type to highlight all exit points</div>
</li>
<li class="level1"><div class="li"> and many more…</div>
</li>
</ul>

<p>
To customize Colors and indentation:
</p>
<ul>
<li class="level1"><div class="li"> Tools &gt; Options &gt; Editor &gt; Formatting.</div>
</li>
<li class="level1"><div class="li"> Tools &gt; Options &gt; Fonts and Colors.</div>
</li>
</ul>

</div>
<!-- EDIT3 SECTION "Semantic and Syntactic Coloring" [1687-2443] -->
<h2 class="sectionedit4" id="editor_hints_and_quick_fixes_aka_lightbulbs">Editor Hints and Quick Fixes (a.k.a. Lightbulbs)</h2>
<div class="level2">

<p>
Editor hints and quick fixes show as lightbulbs along the left edge of the editor. They point out warnings and errors, and often propose useful solutions! 
</p>
<ul>
<li class="level1"><div class="li"> Execute a quick fix: Place the caret in the line next to the lightbulb and press <strong>Alt-Enter</strong> (or click the lightbulb)</div>
<ul>
<li class="level2"><div class="li"> Customize hints: Choose Tools &gt; Options &gt; Editor &gt; Hints.</div>
</li>
</ul>
</li>
</ul>

</div>
<!-- EDIT4 SECTION "Editor Hints and Quick Fixes (a.k.a. Lightbulbs)" [2444-2851] -->
<h2 class="sectionedit5" id="javadoc">Javadoc</h2>
<div class="level2">
<ul>
<li class="level1"><div class="li"> Place the caret above a method or a class that has no Javadoc, type <code class="code html4strict">/**</code> and press Enter: The editor generates skeleton code for a Javadoc comment. </div>
</li>
<li class="level1"><div class="li"> Right-click the project in the Projects window and choose Generate Javadoc.</div>
</li>
<li class="level1"><div class="li"> Right-click a file and choose Tools &gt; Analyze Javadoc</div>
</li>
</ul>

<p>
To display a javadoc popup in the editor, place the caret in a line and press <strong>Ctrl-Space</strong> (Alternatively use <strong>Ctrl-\</strong>).
</p>
<ul>
<li class="level1"><div class="li"> If the javadoc popup doesn't work, make certain that</div>
<ul>
<li class="level2"><div class="li"> You have the Java JDK documentation installed and set up: Tools &gt; Java Platforms </div>
</li>
<li class="level2"><div class="li"> You downloaded and set up javadoc for third-party libraries: Project properties &gt; Libraries &gt; Edit</div>
</li>
</ul>
</li>
</ul>

</div>
<!-- EDIT5 SECTION "Javadoc" [2852-3553] -->
<h2 class="sectionedit6" id="navigating_the_jme3_source">Navigating the jME3 Source</h2>
<div class="level2">

<p>
When the JavaDoc does not deliver enough information, you can have a look at the source of every method or object of jME3 that you use. Just right-click the variable or method, select “Navigate &gt; Go to source..” and an editor will open showing you the source file of jME3.
</p>

</div>
<!-- EDIT6 SECTION "Navigating the jME3 Source" [3554-3867] -->
<h2 class="sectionedit7" id="palette">Palette</h2>
<div class="level2">

<p>
<a href="/resources/sdk-jmonkeyplatform-docu-4.png" class="media" title="sdk:jmonkeyplatform-docu-4.png"><img src="/resources/sdk-jmonkeyplatform-docu-4.png" class="mediaright" alt="" width="421" height="298" /></a>
</p>

<p>
Choose Windows &gt; Palette to open the context-sensitive Palette. The jMonkeyEngine SDK provides you with jme3 code snippets here that you can drag and drop into your source files.
</p>
<ul>
<li class="level1"><div class="li"> Examples: Node and Model creation code snippets.</div>
</li>
</ul>

<p>
Tip: Choose Tools &gt; Add to Palette… from the menu to add your own code snippets to the Palette. (not available yet in beta build)
</p>

</div>
<!-- EDIT7 SECTION "Palette" [3868-4301] -->
<h2 class="sectionedit8" id="keyboard_shortcuts">Keyboard Shortcuts</h2>
<div class="level2">

<p>
Keyboard Shortcuts save you time when when you need to repeat common actions such as Build&amp;Run or navigation to files.
</p>
<ul>
<li class="level1"><div class="li"> Go to File: <strong>Alt-Shift-O</strong></div>
</li>
<li class="level1"><div class="li"> Go to Type: <strong>Ctrl-O</strong></div>
</li>
<li class="level1"><div class="li"> Open in Projects / Files / Favorites window: <strong>Ctrl-Shift-1 / 2 / 3</strong></div>
</li>
<li class="level1"><div class="li"> Build&amp;Run the main class of the Project: <strong>F6</strong> </div>
</li>
<li class="level1"><div class="li"> Run the open file: <strong>Shift-F6</strong> </div>
</li>
<li class="level1"><div class="li"> Switch to Editor / Projects / Files / Navigator: <strong>Ctrl-0 / 1 / 3 / 7</strong></div>
</li>
<li class="level1"><div class="li"> Indent code: <strong>Ctrl-Shift-F</strong></div>
</li>
</ul>

<p>
By default, jMonkeyEngine uses the same <a href="http://netbeans.org/project_downloads/www/shortcuts-6.5.pdf" class="urlextern" title="http://netbeans.org/project_downloads/www/shortcuts-6.5.pdf" rel="nofollow">Editor Shortcuts</a> as the NetBeans IDE, but you can also switch to an Eclipse Keymap, or create your own set.
</p>
<ul>
<li class="level1"><div class="li"> Customize keyboard shortcuts: Tools &gt; Options &gt; Keymap</div>
</li>
</ul>

</div>
<!-- EDIT8 SECTION "Keyboard Shortcuts" [4302-5059] -->
<h2 class="sectionedit9" id="tips_and_tricks">Tips and Tricks</h2>
<div class="level2">
<ul>
<li class="level1"><div class="li"> To browse the physical file structure of your project, use the Files window: <strong>Ctrl-2</strong></div>
</li>
<li class="level1"><div class="li"> To open a file that is not part of a Java project, add it to the Favorites window: <strong>Ctrl-3</strong></div>
</li>
<li class="level1"><div class="li"> If you cannot find a particular menu item or option panel, use the IDE Search box in the top right! <strong>Ctrl-i</strong></div>
</li>
<li class="level1"><div class="li"> If a code block, class, or javadoc is quite long and you don't want to scroll over it, click the <strong>+/-</strong> signs to collapse (fold) the code block temporarily.</div>
</li>
<li class="level1"><div class="li"> Press <strong>F1</strong> for Help</div>
</li>
</ul>
<hr />

<p>
See also
</p>
<ul>
<li class="level1"><div class="li"> <a href="http://netbeans.org/kb/docs/java/editor-codereference.html" class="urlextern" title="http://netbeans.org/kb/docs/java/editor-codereference.html" rel="nofollow">Code Assistance</a></div>
</li>
</ul>
<div class="tags"><span>
	<a href="/tag/documentation.html" class="wikilink1" title="tag:documentation" rel="tag">documentation</a>,
	<a href="/tag/sdk.html" class="wikilink1" title="tag:sdk" rel="tag">sdk</a>,
	<a href="/tag/editor.html" class="wikilink1" title="tag:editor" rel="tag">editor</a>
</span></div>

</div>
<!-- EDIT9 SECTION "Tips and Tricks" [5060-] -->
