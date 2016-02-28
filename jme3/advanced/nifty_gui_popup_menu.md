---
title: Nifty GUI: Create a PopUp Menu
---
<h1 class="sectionedit1" id="nifty_guicreate_a_popup_menu">Nifty GUI: Create a PopUp Menu</h1>
<div class="level1">

<p>
Even though you create and populate the popup menu in Java, you still need a “placeholder” in your XML file.
The popup element needs to be placed <em>outside</em> of any screen!
</p>
<pre class="code xml"><span class="sc3"><span class="re1">&lt;useControls</span> <span class="re0">filename</span>=<span class="st0">"nifty-default-controls.xml"</span><span class="re2">/&gt;</span></span>
...
<span class="sc3"><span class="re1">&lt;popup</span> <span class="re0">id</span>=<span class="st0">"niftyPopupMenu"</span> <span class="re0">childLayout</span>=<span class="st0">"absolute-inside"</span></span>
<span class="sc3">       <span class="re0">controller</span>=<span class="st0">"ControllerOfYourChoice"</span> <span class="re0">width</span>=<span class="st0">"10%"</span><span class="re2">&gt;</span></span>
  <span class="sc3"><span class="re1">&lt;interact</span> <span class="re0">onClick</span>=<span class="st0">"closePopup()"</span> <span class="re0">onSecondaryClick</span>=<span class="st0">"closePopup()"</span> <span class="re0">onTertiaryClick</span>=<span class="st0">"closePopup()"</span> <span class="re2">/&gt;</span></span>
  <span class="sc3"><span class="re1">&lt;control</span> <span class="re0">id</span>=<span class="st0">"#menu"</span> <span class="re0">name</span>=<span class="st0">"niftyMenu"</span> <span class="re2">/&gt;</span></span>
<span class="sc3"><span class="re1">&lt;/popup<span class="re2">&gt;</span></span></span>
...</pre>

<p>
A brief explanation of some the attributes above:
</p>
<ul>
<li class="level1"><div class="li"> The popup id is used within your Java code so that nifty knows which popup placeholder to create.</div>
</li>
<li class="level1"><div class="li"> The Controller tells Nifty which Java class handles MenuItemActivatedEvent.</div>
</li>
<li class="level1"><div class="li"> The on(Secondary/Tertiary)Click tells Nifty to close the popup if the user clicks anywhere except on the menu items (in this example; you have to define the closePopup()-method yourself, in the screen controller)</div>
</li>
<li class="level1"><div class="li"> The control id is used by the Java class to define a control type (i.e. Menu)</div>
</li>
</ul>

<p>
The Java code within your defined ScreenController implementation:
</p>
<pre class="code java"><span class="kw1">private</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+element"><span class="kw3">Element</span></a> popup<span class="sy0">;</span>
...
<span class="kw1">public</span> <span class="kw4">void</span> createMyPopupMenu<span class="br0">(</span><span class="br0">)</span><span class="br0">{</span>
  popup <span class="sy0">=</span> nifty.<span class="me1">createPopup</span><span class="br0">(</span><span class="st0">"niftyPopupMenu"</span><span class="br0">)</span><span class="sy0">;</span>
  <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+menu"><span class="kw3">Menu</span></a> myMenu <span class="sy0">=</span> popup.<span class="me1">findNiftyControl</span><span class="br0">(</span><span class="st0">"#menu"</span>, <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+menu"><span class="kw3">Menu</span></a>.<span class="kw1">class</span><span class="br0">)</span><span class="sy0">;</span>
  myMenu.<span class="me1">setWidth</span><span class="br0">(</span><span class="kw1">new</span> SizeValue<span class="br0">(</span><span class="st0">"100px"</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// must be set</span>
  myMenu.<span class="me1">addMenuItem</span><span class="br0">(</span><span class="st0">"Click me!"</span>, <span class="st0">"menuItemIcon.png"</span>, 
    <span class="kw1">new</span> menuItem<span class="br0">(</span><span class="st0">"menuItemid"</span>, <span class="st0">"blah blah"</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// menuItem is a custom class</span>
  nifty.<span class="me1">subscribe</span><span class="br0">(</span>
    nifty.<span class="me1">getCurrentScreen</span><span class="br0">(</span><span class="br0">)</span>, 
    myMenu.<span class="me1">getId</span><span class="br0">(</span><span class="br0">)</span>, 
    MenuItemActivatedEvent.<span class="kw1">class</span>, 
    <span class="kw1">new</span> MenuItemActivatedEventSubscriber<span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
<span class="br0">}</span>
 
<span class="kw1">public</span> <span class="kw4">void</span> showMenu<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span> <span class="co1">// the method to trigger the menu</span>
  <span class="co1">// If this is a menu that is going to be used many times, then</span>
  <span class="co1">// call this in your constructor rather than here   </span>
  createMyPopupMenu<span class="br0">(</span><span class="br0">)</span> 
  <span class="co1">// call the popup to screen of your choice:</span>
  nifty.<span class="me1">showPopup</span><span class="br0">(</span>nifty.<span class="me1">getCurrentScreen</span><span class="br0">(</span><span class="br0">)</span>, popup.<span class="me1">getId</span><span class="br0">(</span><span class="br0">)</span>, <span class="kw2">null</span><span class="br0">)</span><span class="sy0">;</span> 
<span class="br0">}</span>
 
<span class="kw1">private</span> <span class="kw1">class</span> menuItem <span class="br0">{</span>
  <span class="kw1">public</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> id<span class="sy0">;</span>
  <span class="kw1">public</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> name<span class="sy0">;</span>
  <span class="kw1">public</span> menuItem<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> id, <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> name<span class="br0">)</span><span class="br0">{</span>
    <span class="kw1">this</span>.<span class="me1">id</span><span class="sy0">=</span> id<span class="sy0">;</span>
    <span class="kw1">this</span>.<span class="me1">name</span> <span class="sy0">=</span> name<span class="sy0">;</span>
  <span class="br0">}</span>
<span class="br0">}</span></pre>
<ul>
<li class="level1"><div class="li"> The createMyPopupMenu() method creates the menu with set width so that you can populate it.</div>
</li>
<li class="level1"><div class="li"> The showMenu() method is called by something to trigger the menu (i.e. could be a Key or some other method).</div>
</li>
<li class="level1"><div class="li"> Note: if you want to be able to access the popup via your id, use createPopupWithId(id, id) instead.</div>
</li>
</ul>

<p>
To handle menu item events (i.e. calling a method when you click on a menu item), you register (subscribe) a EventTopicSubscriber&lt;MenuItemActivatedEvent&gt; class implementation to a nifty screen and element.
</p>
<pre class="code java">  <span class="kw1">private</span> <span class="kw1">class</span> MenuItemActivatedEventSubscriber 
    <span class="kw1">implements</span> EventTopicSubscriber<span class="sy0">&lt;</span>MenuItemActivatedEvent<span class="sy0">&gt;</span> <span class="br0">{</span>
 
    @Override
    <span class="kw1">public</span> <span class="kw4">void</span> onEvent<span class="br0">(</span><span class="kw1">final</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> id, <span class="kw1">final</span> MenuItemActivatedEvent event<span class="br0">)</span> <span class="br0">{</span>
    	menuItem item <span class="sy0">=</span> <span class="br0">(</span>menuItem<span class="br0">)</span> event.<span class="me1">getItem</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
       <span class="kw1">if</span> <span class="br0">(</span><span class="st0">"menuItemid"</span>.<span class="me1">equals</span><span class="br0">(</span>item.<span class="me1">id</span><span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
		<span class="co1">//do something !!!</span>
       <span class="br0">}</span>
    <span class="br0">}</span>
  <span class="br0">}</span><span class="sy0">;</span></pre>

</div>
