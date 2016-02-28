---
title: Head-Up Display (HUD)
---
<h1 class="sectionedit1" id="head-up_display_hud">Head-Up Display (HUD)</h1>
<div class="level1">

<p>
<a href="/resources/fetch.php" class="media" title="http://www.jmonkeyengine.com/wp-content/uploads/2010/10/grapplinghook.jpg"><img src="/resources/fetch.php" class="mediaright" title="www.jmonkeyengine.com_wp-content_uploads_2010_10_grapplinghook.jpg" alt="www.jmonkeyengine.com_wp-content_uploads_2010_10_grapplinghook.jpg" width="256" height="192" /></a>
</p>

<p>
A HUD (Head-Up Display) is part of a game's visual user interface. It's an overlay that displays additional information as (typically) 2-dimensional text or icons on the screen, on top of the 3D scene. Not all games have, or need a HUD. To avoid breaking the immersion and cluttering the screen, only use a HUD if it is the only way to convey certain information.
</p>

<p>
HUDs are used to supply players with essential information about the game state.
</p>
<ul>
<li class="level1"><div class="li"> Status: Score, minimap, points, stealth mode, …</div>
</li>
<li class="level1"><div class="li"> Resources: Ammunition, lives/health, time, …</div>
</li>
<li class="level1"><div class="li"> Vehicle instruments: Cockpit, speedometer, …</div>
</li>
<li class="level1"><div class="li"> Navigational aides: Crosshairs, mouse pointer or hand, …</div>
</li>
</ul>

<p>
You have multiple options how to create HUDs.
</p>
<div class="table sectionedit2"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0">Option</th><th class="col1">Pros</th><th class="col2">Cons</th>
	</tr>
	</thead>
	<tr class="row1">
		<th class="col0">Attach elements to default guiNode:</th><td class="col1">Easy to learn. jMonkeyEngine built-in <abbr title="Application Programming Interface">API</abbr> for attaching plain images and bitmap text.</td><td class="col2">Only basic features. <br />
You will have to write custom controls / buttons / effects if you need them.</td>
	</tr>
	<tr class="row2">
		<th class="col0">Use advanced <a href="/jme3/advanced/nifty_gui.html" class="wikilink1" title="jme3:advanced:nifty_gui">Nifty GUI</a> integration:</th><td class="col1">Full-featured interactive user interface. <br />
Includes buttons, effects, controls. <br />
Supports XML and Java layouts.</td><td class="col2">Steeper learning curve.</td>
	</tr>
	<tr class="row3">
		<th class="col0">Use user contributed <abbr title="Graphical User Interface">GUI</abbr> libraries such as <a href="/jme3/contributions/tonegodgui.html" class="wikilink1" title="jme3:contributions:tonegodgui">tonegodgui</a> or <a href="http://hub.jmonkeyengine.org/t/lemur-api-documentation/27209" class="urlextern" title="http://hub.jmonkeyengine.org/t/lemur-api-documentation/27209" rel="nofollow">Lemur</a>:</th><td class="col1">Both have many features that would be difficult to do with Nifty <br />
Includes buttons, effects, controls. <br />
New features are still being released </td><td class="col2">Are not necessarily guaranteed future updates, not as well documented</td>
	</tr>
</table></div>
<!-- EDIT2 TABLE [839-1635] -->
<p>
Using the <abbr title="Graphical User Interface">GUI</abbr> Node is the default approach in jme3 to create simple HUDs. If you just quickly want to display a line of text, or a simple icon on the screen, use the no-frills <abbr title="Graphical User Interface">GUI</abbr> Node, it's easier.
</p>

</div>
<!-- EDIT1 SECTION "Head-Up Display (HUD)" [1-1835] -->
<h2 class="sectionedit3" id="simple_hudgui_node">Simple HUD: GUI Node</h2>
<div class="level2">

<p>
You already know the <code>rootNode</code> that holds the 3-dimensional scene graph. jME3 also offers a 2-dimension (orthogonal) node, the <code>guiNode</code>. 
</p>

<p>
This is how you use the guiNode for HUDs:
</p>
<ul>
<li class="level1"><div class="li"> Create a <abbr title="Graphical User Interface">GUI</abbr> element: a BitmapText or Picture object.</div>
</li>
<li class="level1"><div class="li"> Attach the element to the guiNode. </div>
</li>
<li class="level1"><div class="li"> Place the element in the orthogonal render queue using <code>setQueueBucket(Bucket.Gui)</code>. </div>
</li>
</ul>

<p>
The BitmapTexts and Pictures appear as 2 dimensional element on the screen.
</p>

<p>
</p><p></p><div class="notetip">By default, the guiNode has some scene graph statistics attached. To clear the guiNode before you attach your own <abbr title="Graphical User Interface">GUI</abbr> elements, use the following methods: 

<pre class="code java">setDisplayStatView<span class="br0">(</span><span class="kw2">false</span><span class="br0">)</span><span class="sy0">;</span> setDisplayFps<span class="br0">(</span><span class="kw2">false</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>

</p></div>


</div>
<!-- EDIT3 SECTION "Simple HUD: GUI Node" [1836-2564] -->
<h3 class="sectionedit4" id="displaying_pictures_in_the_hud">Displaying Pictures in the HUD</h3>
<div class="level3">

<p>
A simple image can be displayed using <code>com.jme3.ui.Picture</code>.
</p>
<pre class="code java">Picture pic <span class="sy0">=</span> <span class="kw1">new</span> Picture<span class="br0">(</span><span class="st0">"HUD Picture"</span><span class="br0">)</span><span class="sy0">;</span>
pic.<span class="me1">setImage</span><span class="br0">(</span>assetManager, <span class="st0">"Textures/ColoredTex/Monkey.png"</span>, <span class="kw2">true</span><span class="br0">)</span><span class="sy0">;</span>
pic.<span class="me1">setWidth</span><span class="br0">(</span>settings.<span class="me1">getWidth</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">/</span><span class="nu0">2</span><span class="br0">)</span><span class="sy0">;</span>
pic.<span class="me1">setHeight</span><span class="br0">(</span>settings.<span class="me1">getHeight</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">/</span><span class="nu0">2</span><span class="br0">)</span><span class="sy0">;</span>
pic.<span class="me1">setPosition</span><span class="br0">(</span>settings.<span class="me1">getWidth</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">/</span><span class="nu0">4</span>, settings.<span class="me1">getHeight</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">/</span><span class="nu0">4</span><span class="br0">)</span><span class="sy0">;</span>
guiNode.<span class="me1">attachChild</span><span class="br0">(</span>pic<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
When you set the last boolean in setImage() to true, the alpha channel of your image is rendered transparent/translucent.
</p>

</div>
<!-- EDIT4 SECTION "Displaying Pictures in the HUD" [2565-3089] -->
<h3 class="sectionedit5" id="displaying_text_in_the_hud">Displaying Text in the HUD</h3>
<div class="level3">

<p>
You use <code>com.jme3.font.BitmapText</code> to display text on the screen. 
</p>
<pre class="code java">BitmapText hudText <span class="sy0">=</span> <span class="kw1">new</span> BitmapText<span class="br0">(</span>guiFont, <span class="kw2">false</span><span class="br0">)</span><span class="sy0">;</span>          
hudText.<span class="me1">setSize</span><span class="br0">(</span>guiFont.<span class="me1">getCharSet</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">getRenderedSize</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>      <span class="co1">// font size</span>
hudText.<span class="me1">setColor</span><span class="br0">(</span>ColorRGBA.<span class="me1">Blue</span><span class="br0">)</span><span class="sy0">;</span>                             <span class="co1">// font color</span>
hudText.<span class="me1">setText</span><span class="br0">(</span><span class="st0">"You can write any string here"</span><span class="br0">)</span><span class="sy0">;</span>             <span class="co1">// the text</span>
hudText.<span class="me1">setLocalTranslation</span><span class="br0">(</span><span class="nu0">300</span>, hudText.<span class="me1">getLineHeight</span><span class="br0">(</span><span class="br0">)</span>, <span class="nu0">0</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// position</span>
guiNode.<span class="me1">attachChild</span><span class="br0">(</span>hudText<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
The BitmapFont object <code>guiFont</code> is a default font provided by SimpleApplication. Copy you own fonts as .fnt plus .png files into the <code>assets/Interface/Fonts</code> directory and load them like this:
</p>
<pre class="code">BitmapFont myFont = assetManager.loadFont("Interface/Fonts/Console.fnt");
hudText = new BitmapText(myFont, false);</pre>

</div>
<!-- EDIT5 SECTION "Displaying Text in the HUD" [3090-3937] -->
<h3 class="sectionedit6" id="positioning_hud_elements">Positioning HUD Elements</h3>
<div class="level3">
<ul>
<li class="level1"><div class="li"> When positioning <abbr title="Graphical User Interface">GUI</abbr> text and images in 2D, the <strong>bottom left corner</strong> of the screen is <code>(0f,0f)</code>, and the <strong>top right corner</strong> is at <code>(settings.getWidth(),settings.getHeight())</code>.</div>
</li>
<li class="level1"><div class="li"> If you have several 2D elements in the <abbr title="Graphical User Interface">GUI</abbr> bucket that overlap, define their depth order by specifing a Z value. For example use <code>pic.move(x, y, -1)</code> to move the picture to the background, or <code>hudText.setLocalTranslation(x,y,1)</code> to move text to the foreground.</div>
</li>
<li class="level1"><div class="li"> Size and length values in the orthogonal render queue are treated like pixels. A 20*20-wu big quad is rendered 20 pixels wide.</div>
</li>
</ul>

</div>
<!-- EDIT6 SECTION "Positioning HUD Elements" [3938-4562] -->
<h3 class="sectionedit7" id="displaying_geometries_in_the_hud">Displaying Geometries in the HUD</h3>
<div class="level3">

<p>
It is technically possible to attach Quads and 3D Geometries to the HUD. They show up as flat, static <abbr title="Graphical User Interface">GUI</abbr> elements. The size unit for the guiNode is pixels, not world units. If you attach a Geometry that uses a lit Material, you must add a light to the guiNode. 
</p>

<p>
</p><p></p><div class="noteimportant">If you don't see an attached object in the <abbr title="Graphical User Interface">GUI</abbr>, check it's position and material (add a light to guiNode). Also verify whether it is not too tiny to be seen. For comparison: A 1 world-unit wide cube is only 1 pixel wide when attached to the guiNode! You may need to scale it bigger.
</div>


</div>
<!-- EDIT7 SECTION "Displaying Geometries in the HUD" [4563-5178] -->
<h3 class="sectionedit8" id="keeping_the_hud_up-to-date">Keeping the HUD Up-To-Date</h3>
<div class="level3">

<p>
Use the update loop to keep the content up-to-date.
</p>
<pre class="code java"><span class="kw1">public</span> <span class="kw4">void</span> simpleUpdate<span class="br0">(</span><span class="kw4">float</span> tpf<span class="br0">)</span> <span class="br0">{</span>
  ...
  <span class="me1">hudText</span>.<span class="me1">setText</span><span class="br0">(</span><span class="st0">"Score: "</span> <span class="sy0">+</span> score<span class="br0">)</span><span class="sy0">;</span>
  ...
  <span class="me1">picture</span>.<span class="me1">setImage</span><span class="br0">(</span>assetManager, <span class="st0">"Interface/statechange.png"</span>, <span class="kw2">true</span><span class="br0">)</span><span class="sy0">;</span>
  ...
<span class="br0">}</span></pre>

</div>
<!-- EDIT8 SECTION "Keeping the HUD Up-To-Date" [5179-5453] -->
<h2 class="sectionedit9" id="advanced_hudnifty_gui">Advanced HUD: Nifty GUI</h2>
<div class="level2">

<p>
The recommended approach to create HUDs is using <a href="/jme3/advanced/nifty_gui.html" class="wikilink1" title="jme3:advanced:nifty_gui">Nifty GUI</a>.
</p>
<ol>
<li class="level1"><div class="li"> Lay out the <abbr title="Graphical User Interface">GUI</abbr> in one or several Nifty XML or Java files. </div>
</li>
<li class="level1"><div class="li"> Write the controller classes in Java.</div>
</li>
<li class="level1"><div class="li"> Load the XML file with the controller object in your game's simpleInit() method.</div>
</li>
</ol>

<p>
The advantage of Nifty <abbr title="Graphical User Interface">GUI</abbr> is that it is well integrated into jME and the jMonkeyEngine SDK, and that it offers all the features that you expect from a professional modern user interface. 
</p>

<p>
For HUDs, you basically follow the same instructions as for creating a normal <a href="/jme3/advanced/nifty_gui.html" class="wikilink1" title="jme3:advanced:nifty_gui">Nifty GUI</a>, you just don't pause the game while the HUD is up.
</p>

</div>
<!-- EDIT9 SECTION "Advanced HUD: Nifty GUI" [5454-6097] -->
<h2 class="sectionedit10" id="see_also">See also</h2>
<div class="level2">
<ul>
<li class="level1"><div class="li"> <a href="/jme3/external/fonts.html" class="wikilink1" title="jme3:external:fonts">Fonts</a></div>
</li>
</ul>
<div class="tags"><span>
	<a href="/tag/gui.html" class="wikilink1" title="tag:gui" rel="tag">gui</a>,
	<a href="/tag/display.html" class="wikilink1" title="tag:display" rel="tag">display</a>,
	<a href="/tag/documentation.html" class="wikilink1" title="tag:documentation" rel="tag">documentation</a>,
	<a href="/tag/hud.html" class="wikilink1" title="tag:hud" rel="tag">hud</a>
</span></div>

</div>
<!-- EDIT10 SECTION "See also" [6098-] -->
