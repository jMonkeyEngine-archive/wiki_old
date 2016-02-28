---
title: Quick Start Guide:
---
<h3 class="sectionedit1" id="quick_start_guide">Quick Start Guide:</h3>
<div class="level3">

<p>
For anyone who just wants to jump right in and read as you go, here are the basics for getting a UI up and running in minutes.<br />

<br />

The first step is to create the screen control. This can be done one of two ways.<br />

<br />

1. Using the provided default style information:
</p>
<pre class="code java"><span class="co1">// this = any JME Application</span>
Screen screen <span class="sy0">=</span> <span class="kw1">new</span> Screen<span class="br0">(</span><span class="kw1">this</span><span class="br0">)</span><span class="sy0">;</span>
screen.<span class="me1">initialize</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
guiNode.<span class="me1">addControl</span><span class="br0">(</span>screen<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
2. Providing a path to another Style map.
</p>
<pre class="code java"><span class="co1">// this = any JME Application</span>
Screen screen <span class="sy0">=</span> <span class="kw1">new</span> Screen<span class="br0">(</span><span class="kw1">this</span>, “tonegod<span class="sy0">/</span>gui<span class="sy0">/</span>style<span class="sy0">/</span>def<span class="sy0">/</span>style_map.<span class="me1">xml</span>”<span class="br0">)</span><span class="sy0">;</span>
screen.<span class="me1">initialize</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
guiNode.<span class="me1">addControl</span><span class="br0">(</span>screen<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
<strong>NOTE:</strong><br />

style_map.xml consists of a list of xml documents containing varied styles for varied use. You can copy the default style map and replace one, many, all with project specific style (Covered later in this tutorial).<br />

<br />

Next, we add a control. Might as well start with something interesting as all control contructors follow the same format. Let go with a window and then we’ll add a button to it. Here are the three contrustor choices for creating the window:<br />

</p>
<pre class="code java"><span class="co3">/** Parameters:
  * Screen screen,
  * String UID,
  * Vector2f position
  */</span>
 
<a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+window"><span class="kw3">Window</span></a> win <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+window"><span class="kw3">Window</span></a><span class="br0">(</span>screen, “win”, <span class="kw1">new</span> Vector2f<span class="br0">(</span><span class="nu0">15</span>, <span class="nu0">15</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
screen.<span class="me1">addElement</span><span class="br0">(</span>win<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
And… boom! You have a fancy new resizable, movable window as part of you’re UI. Now, let’s take a look at the two additional constructors.<br />

<br />

The second adds a 4th parameter to specify the windows dimensions, like such:
</p>
<pre class="code java"><span class="co3">/** Additional Parameter:
  * Vector2f dimensions  */</span>
 
<a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+window"><span class="kw3">Window</span></a> win <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+window"><span class="kw3">Window</span></a><span class="br0">(</span>screen, “win”, <span class="kw1">new</span> Vector2f<span class="br0">(</span><span class="nu0">15</span>, <span class="nu0">15</span><span class="br0">)</span>,
    <span class="kw1">new</span> Vector2f<span class="br0">(</span><span class="nu0">400</span>, <span class="nu0">300</span><span class="br0">)</span>
<span class="br0">)</span><span class="sy0">;</span>
screen.<span class="me1">addElement</span><span class="br0">(</span>win<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
The third option adds 2 more parameters and looks like this:
</p>
<pre class="code java"><span class="co3">/** Additional Parameters:
  * Vector4f resizeBorders,
  * String defaultImg
  */</span>
 
<a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+window"><span class="kw3">Window</span></a> win <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+window"><span class="kw3">Window</span></a><span class="br0">(</span>screen, “win”, <span class="kw1">new</span> Vector2f<span class="br0">(</span><span class="nu0">15</span>, <span class="nu0">15</span><span class="br0">)</span>, <span class="kw1">new</span> Vector2f<span class="br0">(</span><span class="nu0">400</span>, <span class="nu0">300</span><span class="br0">)</span>,
    <span class="kw1">new</span> Vector4f<span class="br0">(</span><span class="nu0">14</span>,<span class="nu0">14</span>,<span class="nu0">14</span>,<span class="nu0">14</span><span class="br0">)</span>,
    “tonegod<span class="sy0">/</span>gui<span class="sy0">/</span>style<span class="sy0">/</span>def<span class="sy0">/</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+window"><span class="kw3">Window</span></a><span class="sy0">/</span>panel_x.<span class="me1">png</span>”
<span class="br0">)</span><span class="sy0">;</span>
screen.<span class="me1">addElement</span><span class="br0">(</span>win<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
Any parameters not specified are derived from the defaults specified in the Window style information.<br />

<br />

<strong>NOTE:</strong><br />

The occasional control extends this contructor format, adding an additional Orientation parameter or possibly a boolean flag for controls that provide multiple configurable layouts.<br />

<br />

So, now lets add a button to the window that will create more windows!<br />

<br />

The Button class is one of the only <abbr title="Graphical User Interface">GUI</abbr> control classes that implements JME’s Control interface. The Control only becomes active if setInterval is called because the Button requires the use of stillPressed events. This and much more will be cover in later documentation. Again, you ave the three options above for creating an instance of the button control.<br />

<br />

<strong>NOTE:</strong><br />

The button control (like many controls) is abstract and provides methods for handling user input. All events can be consumed by using evt.setConsumed(); First, lets setup a method to create new windows:
</p>
<pre class="code java"><span class="kw1">private</span> <span class="kw4">int</span> winCount <span class="sy0">=</span> <span class="nu0">0</span><span class="sy0">;</span>
 
<span class="kw1">public</span> <span class="kw1">final</span> <span class="kw4">void</span> createNewWindow<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> someWindowTitle<span class="br0">)</span> <span class="br0">{</span>
    <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+window"><span class="kw3">Window</span></a> nWin <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+window"><span class="kw3">Window</span></a><span class="br0">(</span>
        screen,
        “<a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+window"><span class="kw3">Window</span></a>” <span class="sy0">+</span> winCount,
        <span class="kw1">new</span> Vector2f<span class="br0">(</span> <span class="br0">(</span>screen.<span class="me1">getWidth</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">/</span><span class="nu0">2</span><span class="br0">)</span><span class="sy0">-</span><span class="nu0">175</span>, <span class="br0">(</span>screen.<span class="me1">getHeight</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">/</span><span class="nu0">2</span><span class="br0">)</span><span class="sy0">-</span><span class="nu0">100</span> <span class="br0">)</span>
    <span class="br0">)</span><span class="sy0">;</span>
    nWin.<span class="me1">setWindowTitle</span><span class="br0">(</span>someWindowTitle<span class="br0">)</span><span class="sy0">;</span>
    screen.<span class="me1">addElement</span><span class="br0">(</span>nWin<span class="br0">)</span><span class="sy0">;</span>
    winCount<span class="sy0">++;</span>
<span class="br0">}</span></pre>

<p>
Now lets add the button to allow users to create new window:
</p>
<pre class="code java"><span class="co3">/** Parameters:
  * Screen screen,
  * String UID,
  * Vector2f position
  */</span>
 
ButtonAdapter makeWindow <span class="sy0">=</span> <span class="kw1">new</span> ButtonAdapter<span class="br0">(</span> screen, “Btn1″, <span class="kw1">new</span> Vector2f<span class="br0">(</span><span class="nu0">15</span>, <span class="nu0">55</span><span class="br0">)</span> <span class="br0">)</span> <span class="br0">{</span>
    @Override
    <span class="kw1">public</span> <span class="kw4">void</span> onButtonMouseLeftUp<span class="br0">(</span>MouseButtonEvent evt, <span class="kw4">boolean</span> toggled<span class="br0">)</span> <span class="br0">{</span>
        createNewWindow<span class="br0">(</span>“<span class="kw1">New</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+window"><span class="kw3">Window</span></a> ” <span class="sy0">+</span> winCount<span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
<span class="br0">}</span><span class="sy0">;</span>
 
<span class="co1">// Add it to out initial window</span>
win.<span class="me1">addChild</span><span class="br0">(</span>makeWindow<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
<strong>NOTE:</strong><br />

For layout purposes, it is suggested that you add all child Elements toa control PRIOR to adding the control to the screen… so, ceate a window, add a button, add window to screen.<br />

<br />

<strong>A Bit More Info:</strong><br />

 All controls are based on the Element class which has access to all default behaviors. Behaviors can be enabled disabled on ANY control or primitive Element.
</p>

</div>
<!-- EDIT1 SECTION "Quick Start Guide:" [1-4288] -->
<h3 class="sectionedit2" id="a_few_of_the_common_behaviors">A Few of the Common Behaviors:</h3>
<div class="level3">
<pre class="code java"><span class="co1">// Makes control resizable from defined borders</span>
setIsResizable<span class="br0">(</span><span class="kw4">boolean</span><span class="br0">)</span><span class="sy0">;</span>
 
<span class="co1">// Makes the control movable</span>
setIsMovable<span class="br0">(</span><span class="kw4">boolean</span><span class="br0">)</span><span class="sy0">;</span>
 
<span class="co1">// Constrained to parent dimensions</span>
setLockToParentBounds<span class="br0">(</span><span class="kw4">boolean</span><span class="br0">)</span><span class="sy0">;</span>
 
<span class="co1">// On interaction effects direct parent instead of self</span>
setEffectParent<span class="br0">(</span><span class="kw4">boolean</span><span class="br0">)</span><span class="sy0">;</span>
 
<span class="co1">// On interaction effects absolute parent (screen lvl) instead of self</span>
setEffectAbsoluteParent<span class="br0">(</span><span class="kw4">boolean</span><span class="br0">)</span><span class="sy0">;</span>
 
<span class="co1">// allows the control to scale north/south from any encapsulating parent resize</span>
setScaleNS<span class="br0">(</span><span class="kw4">boolean</span><span class="br0">)</span><span class="sy0">;</span>
<span class="co1">// allows the control to scale east/west from any encapsulating parent resize</span>
setScaleEW<span class="br0">(</span><span class="kw4">boolean</span><span class="br0">)</span><span class="sy0">;</span>
 
setDockN<span class="br0">(</span><span class="kw4">boolean</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// also enables/disables dock south</span>
setDockS<span class="br0">(</span><span class="kw4">boolean</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// also enables/disables dock north</span>
setDockE<span class="br0">(</span><span class="kw4">boolean</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// also enables/disables dock west</span>
setDockW<span class="br0">(</span><span class="kw4">boolean</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// also enables/disables dock east</span>
 
setIgnoreMouse<span class="br0">(</span><span class="kw4">boolean</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
<strong>NOTE:</strong><br />

There are far more behaviors, however, these are the most critical when creating custom controls to ensure that nested Elements react as you would like when a parent Element is altered.<br />

</p>

</div>
<!-- EDIT2 SECTION "A Few of the Common Behaviors:" [4289-] -->
