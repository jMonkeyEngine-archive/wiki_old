---
title: Atom's GUI
---
<h2 class="sectionedit1" id="atom_s_gui">Atom's GUI</h2>
<div class="level2">

<p>
In Atom framework, I choose NiftyGUI because its much more features, expandable, have active developing status, and good friendly supports. 
</p>

<p>
AtomGUI is the base of AtomEditor component (of Atom framework), which in turn provide easy editing support for game objects, configs and such, just like Swing does with Java's bean and Models, but in 3D with hardware accelarated.
</p>

</div>
<!-- EDIT1 SECTION "Atom's GUI" [1-394] -->
<h3 class="sectionedit2" id="additions">Additions</h3>
<div class="level3">

<p>
My additions for NiftyGUI:
</p>
<ul>
<li class="level1"><div class="li"> Lightweight MVC</div>
</li>
<li class="level2"><div class="li"> Template framework</div>
</li>
<li class="level2"><div class="li"> a Groovy builder</div>
</li>
<li class="level2"><div class="li"> a <abbr title="Cascading Style Sheets">CSS</abbr> (Cascaded Style Sheet) implementation (for NiftyGUI), even a LESS</div>
</li>
<li class="level2"><div class="li"> a simplier Localization framework</div>
</li>
<li class="level2"><div class="li"> GQuery stand for “JQuery in Groovy”</div>
</li>
<li class="level2"><div class="li"> a lot of Groovy  scripting and functional sugar for NiftyGUI</div>
</li>
</ul>

</div>
<!-- EDIT2 SECTION "Additions" [395-739] -->
<h3 class="sectionedit3" id="ideas">Ideas</h3>
<div class="level3">

</div>

<h4 id="javascript_and_web_world_ideas">JavaScript and Web world Ideas</h4>
<div class="level4">

<p>
It's worthy to note that I come from the Web world, and I use JavaScript everyday beside of Java. That's why I always want “good” things in JavaScript world show up in game dev world.
</p>

<p>
Things such like Template, <abbr title="Cascading Style Sheets">CSS</abbr>, GQuery, … corporate tightly with JME3 systems but with a lot of additional gun and gears. Make Nifty and JME3 a real powerful monkey as it should!
</p>

</div>
<!-- EDIT3 SECTION "Ideas" [740-1158] -->
<h3 class="sectionedit4" id="template_and_css">Template and CSS</h3>
<div class="level3">

<p>
Every Web framework come with a Template framework, facade and styles make the Web world colorful and attractive but <abbr title="HyperText Markup Language">HTML</abbr> and <abbr title="Cascading Style Sheets">CSS</abbr> is a blow-up standard!!! 
</p>

<p>
What we trying to do here is to make is compact and usable but with posibility to enhance and extend.
There are some “good” template framework in the Java and JavaScript world:
- Mustache
- StringBuilder
- Veclocity
</p>

<p>
Also worth to take a look is : LESS (the scriptable <abbr title="Cascading Style Sheets">CSS</abbr>)
</p>

<p>
I see much powerful can be gained if we open this direction with the combination of : JME3 + Nifty + Groovy. That's why I experiment all this stuffs.
</p>

</div>
<!-- EDIT4 SECTION "Template and CSS" [1159-1765] -->
<h3 class="sectionedit5" id="gquery">GQuery</h3>
<div class="level3">

<p>
GQuery stand for “JQuery like in Groovy”. 
</p>

<p>
JQuery is a famous framework in the JavaScript and Web world. GQuery try to provide some of its features, immtimate its syntax and sugars, leverage by Groovy:
</p>
<ul>
<li class="level1"><div class="li"> Query, select a Node Tree (like <abbr title="HyperText Markup Language">HTML</abbr>, Nifty elements,…) with a minimal Path syntax , same as XPath</div>
</li>
<li class="level1"><div class="li"> Hooks to Node's (components, elements..) events with Eventbus</div>
</li>
</ul>

</div>
<!-- EDIT5 SECTION "GQuery" [1766-] -->
