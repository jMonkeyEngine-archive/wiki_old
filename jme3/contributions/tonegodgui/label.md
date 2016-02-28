---
title: Label Class
---
<h1 class="sectionedit1" id="label_class">Label Class</h1>
<div class="level1">

<p>
Though there was no real need for providing a Label class, as the Element class is a label (as well as everything else), one is provided for two reasons:
</p>
<ul>
<li class="level1"><div class="li"> 1. Provide the 3 common constructors</div>
</li>
<li class="level1"><div class="li"> 2. Use of styles to allow for global settings for all text using the Label class.</div>
</li>
</ul>

<p>
NOTE:
Style information can be overridden by any instance by using the Text/Font setters provided by the Element class
</p>
<hr />

</div>

<h5 id="alternatively_the_labelelement_class_can_be_used_to_create_a_label_if_deemed_more_convenient">Alternatively, the LabelElement class can be used to create a label, if deemed more convenient.</h5>
<div class="level5">

<p>
Here is an <strong><em class="u">example</em></strong> of how the Label class (or LabelElement class) can be used:
</p>

<p>
The following Gui class can be instantiated and called from the initialize() method of an appState [preferred], or the simpleInitApp() method of the app class itself [which extends SimpleApplication], like this:
</p>
<pre class="code">  @Override
  public void simpleInitApp() {
      gui = new Gui(this);
      guiNode.addControl(gui.getScreen());
      gui.setText1("Rotate to 0 degrees.");
      gui.setText2("Rotating clockwise.");
  }</pre>

<p>
Below is the code that creates the label(s):
</p>
<pre class="code java"><span class="kw1">public</span> <span class="kw1">class</span> Gui <span class="br0">{</span>
 
    <span class="kw1">private</span> Screen screen<span class="sy0">;</span>
    <span class="co1">//private LabelElement label1, label2;</span>
    <span class="kw1">private</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+label"><span class="kw3">Label</span></a> label1, label2<span class="sy0">;</span>
    <span class="kw1">private</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+panel"><span class="kw3">Panel</span></a> background<span class="sy0">;</span>
 
    <span class="kw1">public</span> Gui<span class="br0">(</span>App app<span class="br0">)</span><span class="br0">{</span>
        screen <span class="sy0">=</span> <span class="kw1">new</span> Screen<span class="br0">(</span>app<span class="br0">)</span><span class="sy0">;</span>
        <span class="kw4">float</span> width  <span class="sy0">=</span> 300f<span class="sy0">;</span>
        <span class="kw4">float</span> height <span class="sy0">=</span> 100f<span class="sy0">;</span>
 
        <span class="co1">//label1 = new LabelElement(</span>
        label1 <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+label"><span class="kw3">Label</span></a><span class="br0">(</span>
                screen,                           <span class="co1">// Screen</span>
                <span class="st0">"text1"</span>,                          <span class="co1">// ID</span>
                <span class="kw1">new</span> Vector2f<span class="br0">(</span>0f, height <span class="sy0">/</span> 10f<span class="br0">)</span>,   <span class="co1">// position</span>
                <span class="kw1">new</span> Vector2f<span class="br0">(</span>width, height <span class="sy0">/</span> <span class="nu0">2</span><span class="br0">)</span>,  <span class="co1">// size</span>
                <span class="kw1">new</span> Vector4f<span class="br0">(</span>0f, 0f, 0f, 0f<span class="br0">)</span>,     <span class="co1">// resize borders</span>
                <span class="kw2">null</span><span class="br0">)</span><span class="sy0">;</span>                            <span class="co1">// image</span>
 
        <span class="co1">//label2 = new LabelElement(</span>
        label2 <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+label"><span class="kw3">Label</span></a><span class="br0">(</span>
                screen,                             <span class="co1">// Screen</span>
                <span class="st0">"text2"</span>,                            <span class="co1">// ID</span>
                <span class="kw1">new</span> Vector2f<span class="br0">(</span>0f, height <span class="sy0">/</span> <span class="nu0">2</span> <span class="sy0">-</span> 10f<span class="br0">)</span>, <span class="co1">// position</span>
                <span class="kw1">new</span> Vector2f<span class="br0">(</span>width, height <span class="sy0">/</span> <span class="nu0">2</span><span class="br0">)</span>,    <span class="co1">// size</span>
                <span class="kw1">new</span> Vector4f<span class="br0">(</span>0f, 0f, 0f, 0f<span class="br0">)</span>,       <span class="co1">// resize borders</span>
                <span class="kw2">null</span><span class="br0">)</span><span class="sy0">;</span>                              <span class="co1">// image</span>
 
        background <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+panel"><span class="kw3">Panel</span></a><span class="br0">(</span>
                screen,                                       <span class="co1">// Screen</span>
                <span class="st0">"background"</span>,                                 <span class="co1">// ID</span>
                <span class="kw1">new</span> Vector2f<span class="br0">(</span>20f, 20f<span class="br0">)</span>,                       <span class="co1">// position</span>
                <span class="kw1">new</span> Vector2f<span class="br0">(</span>width, height<span class="br0">)</span>,                  <span class="co1">// size</span>
                <span class="kw1">new</span> Vector4f<span class="br0">(</span>10f, 10f, 10f, 10f<span class="br0">)</span>,             <span class="co1">// resize borders</span>
                <span class="st0">"tonegod/gui/style/def/Window/panel_x.png"</span><span class="br0">)</span><span class="sy0">;</span>  <span class="co1">// image</span>
 
 
<span class="co1">//        AssetManager assetManager = app.getAssetManager();</span>
<span class="co1">//        Material mat = new Material(assetManager, "Common/MatDefs/Misc/Unshaded.j3md");</span>
<span class="co1">//        mat.setColor("Color", ColorRGBA.Gray); </span>
<span class="co1">//        background.setMaterial(mat);</span>
 
        label1.<span class="me1">setText</span><span class="br0">(</span><span class="st0">"First Text"</span><span class="br0">)</span><span class="sy0">;</span>
        label1.<span class="me1">setFontColor</span><span class="br0">(</span>ColorRGBA.<span class="me1">White</span><span class="br0">)</span><span class="sy0">;</span>
        label1.<span class="me1">setTextAlign</span><span class="br0">(</span>BitmapFont.<span class="me1">Align</span>.<span class="me1">Center</span><span class="br0">)</span><span class="sy0">;</span>
 
        label2.<span class="me1">setText</span><span class="br0">(</span><span class="st0">"Second Text"</span><span class="br0">)</span><span class="sy0">;</span>
        label2.<span class="me1">setFontColor</span><span class="br0">(</span>ColorRGBA.<span class="me1">White</span><span class="br0">)</span><span class="sy0">;</span>
        label2.<span class="me1">setTextAlign</span><span class="br0">(</span>BitmapFont.<span class="me1">Align</span>.<span class="me1">Center</span><span class="br0">)</span><span class="sy0">;</span>
 
        background.<span class="me1">addChild</span><span class="br0">(</span>label1<span class="br0">)</span><span class="sy0">;</span>
        background.<span class="me1">addChild</span><span class="br0">(</span>label2<span class="br0">)</span><span class="sy0">;</span>
        screen.<span class="me1">addElement</span><span class="br0">(</span>background<span class="br0">)</span><span class="sy0">;</span>
 
    <span class="br0">}</span>
 
    <span class="kw1">public</span> Screen getScreen<span class="br0">(</span><span class="br0">)</span><span class="br0">{</span>
        <span class="kw1">return</span> screen<span class="sy0">;</span>
    <span class="br0">}</span>
 
    <span class="kw1">public</span> <span class="kw4">void</span> setText1<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> text1<span class="br0">)</span><span class="br0">{</span>
        label1.<span class="me1">setText</span><span class="br0">(</span>text1<span class="br0">)</span><span class="sy0">;</span>
        <span class="co1">//label1.show();</span>
    <span class="br0">}</span>
 
    <span class="kw1">public</span> <span class="kw4">void</span> setText2<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> text1<span class="br0">)</span><span class="br0">{</span>
        label2.<span class="me1">setText</span><span class="br0">(</span>text1<span class="br0">)</span><span class="sy0">;</span>
        <span class="co1">//label2.show();</span>
    <span class="br0">}</span>
<span class="br0">}</span></pre>

</div>

<h5 id="troubleshooting">Troubleshooting:</h5>
<div class="level5">

<p>
<strong>If your labels don't show up</strong>, make sure that the ID string for each of them is different.  For labels that have the same ID String, only the first one will show up.  Consequent ones will not be added to the parent, and … as far as I know … it doesn't throw an exception.  Having the same ID Strings between labels, or any other element, can come from copying and pasting constructors.  
</p>

<p>
… been there … done that …  <img src="/lib/images/smileys/icon_lol.gif" class="icon" alt="LOL" />.  
</p>

</div>
