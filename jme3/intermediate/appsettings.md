---
title: jME3 Application Display Settings
---
<h1 class="sectionedit1" id="jme3_application_display_settings">jME3 Application Display Settings</h1>
<div class="level1">

<p>
Every class that extends jme3.app.SimpleApplication has properties that can be configured by customizing a <code>com.jme3.system.AppSettings</code> object. 
</p>

<p>
</p><p></p><div class="noteimportant">Configure application settings in <code>main()</code>, before you call <code>app.start()</code> on the application object. If you change display settings during runtime, for example in <code>simpleInitApp()</code>, you must call <code>app.restart()</code> to make them take effect.
</div>


<p>
<strong>Note:</strong> Other runtime settings are covered in <a href="/jme3/intermediate/simpleapplication.html" class="wikilink1" title="jme3:intermediate:simpleapplication">SimpleApplication</a>.
</p>

</div>
<!-- EDIT1 SECTION "jME3 Application Display Settings" [1-558] -->
<h2 class="sectionedit2" id="code_samples">Code Samples</h2>
<div class="level2">

<p>
Specify settings for a game (here called <code>MyGame</code>, or whatever you called your SimpleApplication instance) in the <code>main()</code> method before the game starts:
</p>
<pre class="code java"><span class="kw1">public</span> <span class="kw1">static</span> <span class="kw4">void</span> main<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a><span class="br0">[</span><span class="br0">]</span> args<span class="br0">)</span> <span class="br0">{</span>
  AppSettings settings <span class="sy0">=</span> <span class="kw1">new</span> AppSettings<span class="br0">(</span><span class="kw2">true</span><span class="br0">)</span><span class="sy0">;</span>
  settings.<span class="me1">setResolution</span><span class="br0">(</span><span class="nu0">640</span>,<span class="nu0">480</span><span class="br0">)</span><span class="sy0">;</span>
  <span class="co1">// ... other properties, see below</span>
  MyGame app <span class="sy0">=</span> <span class="kw1">new</span> MyGame<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span> 
  app.<span class="me1">setSettings</span><span class="br0">(</span>settings<span class="br0">)</span><span class="sy0">;</span>
  app.<span class="me1">start</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
<span class="br0">}</span></pre>

<p>
Set the boolean in the AppSettings contructor to true if you want to keep the default settings for values that you do not specify. Set this parameter to false if you want the application to load user settings from previous launches. In either case you can still customize individual settings.
</p>

<p>
This example toggles the settings to fullscreen while the game is already running. Then it restarts the game context (not the whole game) which applies the changed settings.
</p>
<pre class="code java"><span class="kw1">public</span> <span class="kw4">void</span> toggleToFullscreen<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
  <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+graphicsdevice"><span class="kw3">GraphicsDevice</span></a> device <span class="sy0">=</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+graphicsenvironment"><span class="kw3">GraphicsEnvironment</span></a>.<span class="me1">getLocalGraphicsEnvironment</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">getDefaultScreenDevice</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
  DisplayMode<span class="br0">[</span><span class="br0">]</span> modes <span class="sy0">=</span> device.<span class="me1">getDisplayModes</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
  <span class="kw4">int</span> i<span class="sy0">=</span><span class="nu0">0</span><span class="sy0">;</span> <span class="co1">// note: there are usually several, let's pick the first</span>
  settings.<span class="me1">setResolution</span><span class="br0">(</span>modes<span class="br0">[</span>i<span class="br0">]</span>.<span class="me1">getWidth</span><span class="br0">(</span><span class="br0">)</span>,modes<span class="br0">[</span>i<span class="br0">]</span>.<span class="me1">getHeight</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
  settings.<span class="me1">setFrequency</span><span class="br0">(</span>modes<span class="br0">[</span>i<span class="br0">]</span>.<span class="me1">getRefreshRate</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
  settings.<span class="me1">setBitsPerPixel</span><span class="br0">(</span>modes<span class="br0">[</span>i<span class="br0">]</span>.<span class="me1">getBitDepth</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
  settings.<span class="me1">setFullscreen</span><span class="br0">(</span>device.<span class="me1">isFullScreenSupported</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
  app.<span class="me1">setSettings</span><span class="br0">(</span>settings<span class="br0">)</span><span class="sy0">;</span>
  app.<span class="me1">restart</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// restart the context to apply changes</span>
<span class="br0">}</span></pre>

</div>
<!-- EDIT2 SECTION "Code Samples" [559-2062] -->
<h2 class="sectionedit3" id="properties">Properties</h2>
<div class="level2">
<div class="table sectionedit4"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0">Settings Property (Video)</th><th class="col1">Description</th><th class="col2">Default</th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0">setRenderer(AppSettings.LWJGL_OPENGL1) <br />
setRenderer(AppSettings.LWJGL_OPENGL2) <br />
setRenderer(AppSettings.LWJGL_OPENGL3)</td><td class="col1">Switch Video Renderer to OpenGL 1.1, OpenGL 2, or OpenGL 3.3. If your graphic card does not support all OpenGL2 features (<code>UnsupportedOperationException: GLSL and OpenGL2 is required for the LWJGL renderer</code>), then you can force your SimpleApplication to use OpenGL1 compatibility. (Then you still can't use special OpenGL2 features, but at least the error goes away and you can continue with the rest.) </td><td class="col2"> OpenGL 2 </td>
	</tr>
	<tr class="row2">
		<td class="col0">setBitsPerPixel(32)</td><td class="col1">Set the color depth. <br />
1 bpp = black and white, 2 bpp = gray, <br />
4 bpp = 16 colors, 8 bpp = 256 colors, 24 or 32 bpp = “truecolor”.</td><td class="col2">24</td>
	</tr>
	<tr class="row3">
		<td class="col0">setFramerate(60)</td><td class="col1">How often per second the engine should try to refresh the frame. For the release, usually 60 fps. Can be lower (30) if you need to free up the CPU for other applications. No use setting it to a higher value than the screen frequency! If the framerate goes below 30 fps, viewers start to notice choppiness or flickering.</td><td class="col2">-1 (unlimited)</td>
	</tr>
	<tr class="row4">
		<td class="col0">setFullscreen(true)</td><td class="col1">Set this to true to make the game window fill the whole screen; you need to provide a key that calls app.stop() to exit the fullscreen view gracefully (default: escape). <br />
Set this to false to play the game in a normal window of its own.</td><td class="col2">False (windowed)</td>
	</tr>
	<tr class="row5">
		<td class="col0">setHeight(480), setWidth(640) <br />
setResolution(640,480)</td><td class="col1">Two equivalent ways of setting the display resolution.</td><td class="col2">640×480 pixels</td>
	</tr>
	<tr class="row6">
		<td class="col0">setSamples(4)</td><td class="col1">Set multisampling to 0 to switch antialiasing off (harder edges, faster.) <br />
Set multisampling to 2 or 4 to activate antialising (softer edges, may be slower.) <br />
Depending on your graphic card, you may be able to set multisampling to higher values such as 8, 16, or 32 samples.</td><td class="col2">0</td>
	</tr>
	<tr class="row7">
		<td class="col0">setVSync(true) <br />
setFrequency(60)</td><td class="col1">Set vertical syncing to true to time the frame buffer to coincide with the refresh frequency of the screen. VSync prevents ugly page tearing artefacts, but is a bit slower; recommened for release build. <br />
Set VSync to false to deactivate vertical syncing (faster, but possible page tearing artifacts); can remain deactivated during development or for slower PCs.</td><td class="col2">false <br />
60 fps</td>
	</tr>
	<tr class="row8">
		<td class="col0">setStencilBits(8)</td><td class="col1">Set the number of stencil bits. <br />
This value is only relevant when the stencil buffer is being used. Specify 8 to indicate an 8-bit stencil buffer, specify 0 to disable the stencil buffer.</td><td class="col2">0 (disabled)</td>
	</tr>
	<tr class="row9">
		<td class="col0">setDepthBits(16)</td><td class="col1">Sets the number of depth bits to use. <br />
 The number of depth bits specifies the precision of the depth buffer. To increase precision, specify 32 bits. To decrease precision, specify 16 bits. On some platforms 24 bits might not be supported, in that case, specify 16 bits. </td><td class="col2">24</td>
	</tr>
</table></div>
<!-- EDIT4 TABLE [2087-4827] --><div class="table sectionedit5"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0">Settings Property (Input)</th><th class="col1">Description</th><th class="col2">Default</th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0">setUseInput(false)</td><td class="col1">Respond to user input by mouse and keyboard. Can be deactivated for use cases where you only display a 3D scene on the canvas without any interaction.</td><td class="col2">true</td>
	</tr>
	<tr class="row2">
		<td class="col0">setUseJoysticks(true)</td><td class="col1">Activate optional joystick support</td><td class="col2">false</td>
	</tr>
	<tr class="row3">
		<td class="col0">setEmulateMouse(true)</td><td class="col1">Enable or disable mouse emulation for touchscreen-based devices. Setting this to true converts taps on the touchscreen to clicks, and finger swiping gestures over the touchscreen into mouse axis events.</td><td class="col2">false</td>
	</tr>
	<tr class="row4">
		<td class="col0">setEmulateMouseFlipAxis(true,true)</td><td class="col1">Flips the X or Y (or both) axes for the emulated mouse. Set the first parameter to true to flip the x axis, and the second to flip the y axis.</td><td class="col2">false,false</td>
	</tr>
</table></div>
<!-- EDIT5 TABLE [4829-5543] --><div class="table sectionedit6"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0">Settings Property (Audio)</th><th class="col1">Description</th><th class="col2">Default</th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0">setAudioRenderer(AppSettings.LWJGL_OPENAL)</td><td class="col1">Switch Audio Renderer. Currently there is only one option. </td><td class="col2">OpenAL</td>
	</tr>
	<tr class="row2">
		<td class="col0">setStereo3D(true)</td><td class="col1">Enable 3D stereo. This feature requires hardware support from the GPU driver. See <a href="http://en.wikipedia.org/wiki/Quad_buffering" class="urlextern" title="http://en.wikipedia.org/wiki/Quad_buffering" rel="nofollow">Quad Buffering</a>. Currently, your everday user's hardware does not support this, so you can ignore it for now.</td><td class="col2">false</td>
	</tr>
</table></div>
<!-- EDIT6 TABLE [5545-5969] --><div class="table sectionedit7"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0">Settings Property (Branding)</th><th class="col1">Description</th><th class="col2">Default</th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0">setTitle(“My Game”)</td><td class="col1">This string will be visible in the titlebar, unless the window is fullscreen.</td><td class="col2">“jMonkey Engine 3.0”</td>
	</tr>
	<tr class="row2">
		<td class="col0">setIcons(new BufferedImage[]{ <br />
ImageIO.read(new File(“”)), …});</td><td class="col1">This specifies the little application icon in the titlebar of the application (unused in MacOS?). You should specify the icon in various sizes (256,128,32,16) to look good on various operating systems. Note: This is not the application icon on the desktop.</td><td class="col2">null</td>
	</tr>
	<tr class="row3">
		<td class="col0">setSettingsDialogImage(“Interface/mysplashscreen.png”)</td><td class="col1">A custom splashscreen image in the <code>assets/Interface</code> directory which is displayed when the settings dialog is shown.</td><td class="col2">“/com/jme3/app/Monkey.png”</td>
	</tr>
</table></div>
<!-- EDIT7 TABLE [5971-6678] -->
<p>
</p><p></p><div class="notetip">You can use <code>app.setShowSettings(true);</code> and <code>setSettingsDialogImage(“Interface/mysplashscreen.png”)</code> to present the user with jme3's default display settings dialog when starting the game. Use <code>app.setShowSettings(false);</code> to hide the default settings screen. Set this boolean before calling <code>app.start()</code> on the SimpleApplication.
</div>


</div>
<!-- EDIT3 SECTION "Properties" [2063-7038] -->
<h2 class="sectionedit8" id="toggling_and_activating_settings">Toggling and Activating Settings</h2>
<div class="level2">
<div class="table sectionedit9"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0">SimpleApplication method</th><th class="col1">Description</th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0">app.setShowSettings(boolean)</td><td class="col1">Activate or deactivate the default settings screen before start()ing the game. If you let users use this screen, you do not need to modify the settings object. Note: Most developers implement their own custom settings screen, but the default one is useful during the alpha stages.</td>
	</tr>
	<tr class="row2">
		<td class="col0">app.setSettings(settings)</td><td class="col1">After you have modified the properties on the settings object, you apply it to your application. Note that the settings are not automatically reloaded while the game is running.</td>
	</tr>
	<tr class="row3">
		<td class="col0">app.start()</td><td class="col1">Every game calls start() in the beginning to initialize the game and apply the settings. Modify and set your settings before calling start().</td>
	</tr>
	<tr class="row4">
		<td class="col0">app.restart()</td><td class="col1">Restart()ing a running game restarts the game context and applies the updated settings object. (This does not restart or reinitialize the whole game.)</td>
	</tr>
</table></div>
<!-- EDIT9 TABLE [7085-7966] -->
</div>
<!-- EDIT8 SECTION "Toggling and Activating Settings" [7039-7967] -->
<h2 class="sectionedit10" id="saving_and_loading_settings">Saving and Loading Settings</h2>
<div class="level2">

<p>
An AppSettings object also supports the following methods to save your settings under a unique key (in this example “com.foo.MyCoolGame3”):
</p>
<ul>
<li class="level1"><div class="li"> Use <code>settings.save(“com.foo.MyCoolGame3”)</code> to save your settings via standard java.io serialization.</div>
</li>
<li class="level1"><div class="li"> Use <code>settings.load(“com.foo.MyCoolGame3”)</code> to load your settings.</div>
</li>
<li class="level1"><div class="li"> Use <code>settings2.copyFrom(settings)</code> to copy a settings object.</div>
</li>
</ul>

<p>
Usage: 
</p>

<p>
Provide the unique name of your jME3 application as the String argument. For example <code>com.foo.MyCoolGame3</code>.
</p>
<pre class="code java">    <span class="kw1">try</span> <span class="br0">{</span> settings.<span class="me1">save</span><span class="br0">(</span><span class="st0">"com.foo.MyCoolGame3"</span><span class="br0">)</span><span class="sy0">;</span> <span class="br0">}</span> 
    <span class="kw1">catch</span> <span class="br0">(</span>BackingStoreException ex<span class="br0">)</span> <span class="br0">{</span> <span class="co3">/** could not save settings */</span> <span class="br0">}</span></pre>
<ul>
<li class="level1"><div class="li"> On Windows, the preferences are saved under the following registry key: <br />
<code>HKEY_CURRENT_USER\Software\JavaSoft\Prefs\com\foo\MyCoolGame3</code></div>
</li>
<li class="level1"><div class="li"> On Linux, the preferences are saved in an XML file under: <br />
<code>$HOME/.java/.userPrefs/com/foo/MyCoolGame3</code></div>
</li>
<li class="level1"><div class="li"> On Mac <abbr title="Operating System">OS</abbr> X, the preferences are saved as XML file under: <br />
<code>$HOME/Library/Preferences/com.foo.MyCoolGame3.plist</code></div>
</li>
</ul>

</div>
<!-- EDIT10 SECTION "Saving and Loading Settings" [7968-] -->
