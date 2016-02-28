---
title: Taking Screenshots
---
<h1 class="sectionedit1" id="taking_screenshots">Taking Screenshots</h1>
<div class="level1">

<p>
The com.jme3.app.state.ScreenshotAppState enables your users to take screenshots of the running game.
</p>

<p>
You activate this feature as follows in your simpleInitApp() method:
</p>
<pre class="code java">ScreenshotAppState screenShotState <span class="sy0">=</span> <span class="kw1">new</span> ScreenshotAppState<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
<span class="kw1">this</span>.<span class="me1">stateManager</span>.<span class="me1">attach</span><span class="br0">(</span>screenShotState<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
The default screenshot key is KeyInput.KEY_SYSRQ, alos known as “System Request / Print Screen” key. On Mac keyboards, this key does not exist, so on Mac <abbr title="Operating System">OS</abbr> you take screenshots using Command+Shift+3 (fullscreen) or Command+Shift+4 (windowed: press space to select a window and then click).
</p>

<p>
The screenshot is saved to the user directory.
</p>

</div>
