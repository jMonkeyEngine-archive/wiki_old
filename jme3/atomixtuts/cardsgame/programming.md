---
title: CardGame - Programming
---
<h2 class="sectionedit1" id="cardgame_-_programming">CardGame - Programming</h2>
<div class="level2">

</div>
<!-- EDIT1 SECTION "CardGame - Programming" [1-33] -->
<h3 class="sectionedit2" id="introduction">Introduction</h3>
<div class="level3">

<p>
This is the section descibled the detail process of Programming the card game in Java, Groovy
</p>

<p>
Almost the tasks are trivial and suite for beginers and newbies to JME3. 
</p>

<p>
FYI, some part require knowledge:
</p>
<ol>
<li class="level1"><div class="li"> advanced Java concept such as multi-threading, serialize … Groovy such as Closure</div>
</li>
<li class="level1"><div class="li"> JME3 like …AppState, picking… </div>
</li>
<li class="level1"><div class="li"> or knowledge of Atom framework </div>
</li>
</ol>

<p>
which you should read before start here. The links help you can revise your knowledges:
</p>

<p>
<a href="/jme3.html" class="wikilink1" title="jme3"> JME3 Advanced</a>
<a href="/jme3/scripting.html" class="wikilink1" title="jme3:scripting"> JME3 Scripting</a>
<a href="/jme3/advanced/atom_framework.html" class="wikilink1" title="jme3:advanced:atom_framework"> AtomFramework </a>
</p>

</div>
<!-- EDIT2 SECTION "Introduction" [34-623] -->
<h3 class="sectionedit3" id="short_list">Short list</h3>
<div class="level3">

<p>
Checklist of what we going to implementation in this tutorial:
</p>
<ul>
<li class="level1"><div class="li"> GameStage and Gameplay</div>
<ul>
<li class="level2"><div class="li"> Card gameplay elements (Game, Turn, Phase,..)</div>
</li>
<li class="level2"><div class="li"> GameWorld</div>
</li>
<li class="level2"><div class="li"> Select/Picking</div>
</li>
<li class="level2"><div class="li"> Start/pause</div>
</li>
<li class="level2"><div class="li"> Save/load game states</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Entities</div>
<ul>
<li class="level2"><div class="li"> Card</div>
</li>
<li class="level2"><div class="li"> More</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> States</div>
<ul>
<li class="level2"><div class="li"> Menu</div>
</li>
<li class="level2"><div class="li"> InGame</div>
</li>
<li class="level2"><div class="li"> Loading</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Managers</div>
<ul>
<li class="level2"><div class="li"> StageManager</div>
</li>
<li class="level2"><div class="li"> GUIManager</div>
</li>
<li class="level2"><div class="li"> GamePlayManager</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Controls</div>
<ul>
<li class="level2"><div class="li"> SelectControl</div>
</li>
<li class="level2"><div class="li"> CardEntityControl</div>
</li>
</ul>
</li>
</ul>

</div>
<!-- EDIT3 SECTION "Short list" [624-1079] -->
<h3 class="sectionedit4" id="gamestage_and_gameplay">GameStage and GamePlay</h3>
<div class="level3">

<p>
Here is where you clean up your game design, and write down a few most obvious Classes that build up the game.
</p>

<p>
<strong>CardGame</strong> : obvious
</p>

<p>
<strong>Card</strong> : represent a Card in the game
</p>

<p>
<strong>CardPlayer</strong> extends <strong>Player</strong>: a Player in Atom framework have basic ID, name, character…, already have built-in mechanism to go online -multiplayers if need!
</p>

<p>
<strong>CardTable</strong> extends <strong>GameLevel</strong>: represent the Table where two opponent sit and duel. Of course we can have different levels (in different Modes) like when Player traveling around and play in the future!
</p>

<p>
<strong>CardMatch</strong> : a Match can be held between two CardPlayer opponents
</p>

<p>
<strong>Turn</strong> : a Turn represent a Turn in this card game. Has index number and a point to a Player take that Turn. a Turn has 6 TurnPhase (s)
</p>

<p>
<strong>TurnPhase</strong> : DrawPhase, MainPhase, MainPhase2… contains a bunch of CardAction
</p>

<p>
<strong>CardAction</strong> : obvious. action taken of Player, like : add one more card in his hand and summon etc…
</p>

<p>
see the full implementation in the source code. Detailed explanation below!
</p>

</div>
<!-- EDIT4 SECTION "GameStage and GamePlay" [1080-2138] -->
<h3 class="sectionedit5" id="entities">Entities</h3>
<div class="level3">

</div>

<h4 id="card">Card</h4>
<div class="level4">

<p>
Consider the a Card as a most basic Entity.
[ Warning: Don't mistake I'm going to use any kind of Composing Entity System here! ].
</p>

<p>
An Card Entity should contains infomations relate to a real card in a card game, it also has a representation, which is a 3D Model in JME scenegraph. That’s why Card class extends SpatialEntity.
</p>
<pre class="code">  SpatialEntity This is the handy parent class for classes in Atom framework which also holding Entity data, and has a Spatial as representation. Atom use a built-in two-way connection between the Entity – Spatial, a mechanism which helps you do almost anything you want with SpatialEntity (select-picking,enable/disable…ect)</pre>

<p>
Information relate to the orginal Magic card game:
</p>
<pre class="code java"><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> cardId<span class="sy0">=</span>”<span class="st0">"
String name = “”
String picture = “”
 
int attack = -1
int defend = -1
String cardType = “”
 
String attribute = “”</span></pre>

<p>
[…full in the source code.The meanings are obvious.] 
</p>

<p>
If you declare like this in Groovy, that mean each of these fields are a Property, which have basic generated Setter/Getter by Groovy compiler. We need one more attribute:
Card orgCard
</p>

<p>
This hold a link to the orginal Card in the CardLibrary, which keeps information of every card avaiable in this game. We will implement this class later. Card.groovy
</p>
<pre class="code java"><span class="kw1">package</span> <span class="co2">magiccard.gameplay</span>
 
<span class="kw1">import</span> <span class="co2">com.jme3.scene.Spatial</span>
<span class="kw1">import</span> <span class="co2">sg.atom.entity.SpatialEntity</span>
<span class="co3">/**
*
* @author cuong.nguyenmanh2
*/</span>
<span class="kw1">public</span> <span class="kw1">class</span> Card  <span class="kw1">extends</span> SpatialEntity<span class="br0">{</span>
    <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> cardId<span class="sy0">=</span>”<span class="st0">"
    String name = “”
    String picture = “”
 
    int attack = -1
    int defend = -1
    String cardType = “”
 
    String attribute = “”
    String cardSubType = “”
    int level = -1
 
    String summonRule = “”
    String effect = “”
    String desc = “”
    String longDesc = “”
    String character = “”
    String flipScript=”"</span>
    <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> effectScript<span class="sy0">=</span>”<span class="st0">"
    String rarity=”"</span>
    Card orgCard
 
    <span class="kw1">public</span> Card<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> name<span class="br0">)</span><span class="br0">{</span>
        <span class="kw1">super</span><span class="br0">(</span>name,name<span class="br0">)</span>
        <span class="kw1">this</span>.<span class="me1">name</span> <span class="sy0">=</span> name
    <span class="br0">}</span>
 
    <span class="kw1">public</span> Card<span class="br0">(</span>Card orgCard<span class="br0">)</span><span class="br0">{</span>
        <span class="kw1">super</span><span class="br0">(</span>orgCard.<span class="me1">name</span>,orgCard.<span class="me1">name</span><span class="br0">)</span>
        <span class="kw1">this</span>.<span class="me1">orgCard</span> <span class="sy0">=</span> orgCard
        <span class="kw1">this</span>.<span class="me1">cardId</span> <span class="sy0">=</span> orgCard.<span class="me1">cardId</span>
        <span class="kw1">this</span>.<span class="me1">name</span> <span class="sy0">=</span> orgCard.<span class="me1">name</span>
        <span class="kw1">this</span>.<span class="me1">picture</span> <span class="sy0">=</span> orgCard.<span class="me1">picture</span>
        <span class="kw1">this</span>.<span class="me1">attack</span> <span class="sy0">=</span> orgCard.<span class="me1">attack</span>
        <span class="kw1">this</span>.<span class="me1">defend</span> <span class="sy0">=</span> orgCard.<span class="me1">defend</span>
        <span class="kw1">this</span>.<span class="me1">cardType</span> <span class="sy0">=</span> orgCard.<span class="me1">cardType</span>
        <span class="kw1">this</span>.<span class="me1">level</span> <span class="sy0">=</span> orgCard.<span class="me1">level</span>
        <span class="kw1">this</span>.<span class="me1">desc</span> <span class="sy0">=</span> orgCard.<span class="me1">desc</span>
        <span class="kw1">this</span>.<span class="me1">longDesc</span> <span class="sy0">=</span> orgCard.<span class="me1">longDesc</span>
    <span class="br0">}</span>
<span class="br0">}</span></pre>

</div>

<h4 id="show_the_card">Show the card</h4>
<div class="level4">

<p>
According to the Atom framework, the representation part of a Card should be provided by a EntityFactory. In this implementation, I just ask the GameLevel – The CardTable, to made it up, cause it’s really simple.
</p>

<p>
Now consider a Card spatial built from a flatten 3d box and 2 sides: front &amp; back with approriate textures title FrontTexture and BackTexture. In YugiGame, BackTexture are the same for all the Card, remember that we already set it in the SceneEditor! Now our job is to load the Card model and change the FrontTexture to the path in card.picture.
</p>

<p>
This is a part of the CardTable class which create and “attach” the Card spatial to the levelNode, add two more controls for movement handle and select handle. Simple isn’t it?
</p>
<pre class="code java">    <span class="kw1">public</span> <span class="kw4">void</span> createCardOrg<span class="br0">(</span><span class="br0">)</span><span class="br0">{</span>
        cardOrg <span class="sy0">=</span> <span class="br0">(</span><span class="br0">(</span>Node<span class="br0">)</span> <span class="br0">(</span><span class="br0">(</span>Node<span class="br0">)</span> assetManager.<span class="me1">loadModel</span><span class="br0">(</span>“Models<span class="sy0">/</span>Cards<span class="sy0">/</span>Template<span class="sy0">/</span>card1.<span class="me1">j3o</span>”<span class="br0">)</span><span class="br0">)</span>.<span class="me1">getChild</span><span class="br0">(</span>“Card”<span class="br0">)</span><span class="br0">)</span>.<span class="me1">getChild</span><span class="br0">(</span>“Cube1″<span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
    Geometry createCard<span class="br0">(</span>Card card<span class="br0">)</span> <span class="br0">{</span>
        <span class="co1">// extract the card info</span>
        <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> path <span class="sy0">=</span> card.<span class="me1">picture</span>
 
        <span class="co1">// create the geometry</span>
        Geometry newCard <span class="sy0">=</span> <span class="br0">(</span>Geometry<span class="br0">)</span> cardOrg.<span class="me1">clone</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
        Material cloneMat <span class="sy0">=</span> newCard.<span class="me1">getMaterial</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">clone</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
        cloneMat.<span class="me1">setTexture</span><span class="br0">(</span>“ColorMap2″, assetManager.<span class="me1">loadTexture</span><span class="br0">(</span>path<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
        newCard.<span class="me1">setMaterial</span><span class="br0">(</span>cloneMat<span class="br0">)</span><span class="sy0">;</span>
        <span class="co1">//cloneMat.setBoolean(“MixGlow”,true);</span>
        levelNode.<span class="me1">attachChild</span><span class="br0">(</span>newCard<span class="br0">)</span><span class="sy0">;</span>
        card.<span class="me1">spatial</span> <span class="sy0">=</span> newCard<span class="sy0">;</span>
        newCard.<span class="me1">setLocalScale</span><span class="br0">(</span><span class="sy0">-</span>0.4f,<span class="sy0">-</span>0.4f,0.4f<span class="br0">)</span>
        <span class="co1">// attach the control</span>
        newCard.<span class="me1">addControl</span><span class="br0">(</span><span class="kw1">new</span> CardSpatialControl<span class="br0">(</span>worldManager,card<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
        newCard.<span class="me1">addControl</span><span class="br0">(</span><span class="kw1">new</span> CardSelectControl<span class="br0">(</span>worldManager,gamePlayManager<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="kw1">return</span> newCard<span class="sy0">;</span>
    <span class="br0">}</span></pre>

</div>

<h4 id="card_movement">Card movement</h4>
<div class="level4">
<pre class="code">  For this kind of game, I just want to introduce most basic movement form, Steering movements with brace, veclocity..etc will be introduced in next tuts. </pre>

<p>
By basic movement forms, I want to talk about: 
</p>
<pre class="code">– MOVETO: Move smoothly in a straight line from one point to another. 
– ROTTO: Rotate smoothly by Quaternion from one angle to another. 
– GIGGLE : Shaking, for example prepare to explode! </pre>

<p>
These 3 basic movement types are already enough to compose quite fascinated effects if you know how to. See by your self in the video in the first post! The most normal and obvious way to put movements into a Spatial in JME3 is to make an Control, name it CardSpatialControl. 
</p>
<pre class="code java"><span class="kw1">package</span> <span class="co2">magiccard.gameplay</span>
 
<span class="kw1">import</span> <span class="co2">com.jme3.scene.control.AbstractControl</span>
<span class="kw1">import</span> <span class="co2">com.jme3.math.Vector3f</span>
<span class="kw1">import</span> <span class="co2">com.jme3.math.FastMath</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">sg.atom.entity.SpatialEntityControl</span>
<span class="kw1">import</span> <span class="co2">sg.atom.stage.SelectManager</span>
<span class="kw1">import</span> <span class="co2">sg.atom.stage.WorldManager</span>
<span class="kw1">import</span> <span class="co2">com.jme3.math.Quaternion</span>
<span class="co3">/**
 *
 * @author hungcuong
 */</span>
<span class="kw1">public</span> <span class="kw1">class</span> CardSpatialControl <span class="kw1">extends</span> SpatialEntityControl<span class="br0">{</span>
 
    <span class="kw4">boolean</span> stopMove <span class="sy0">=</span> <span class="kw2">false</span><span class="sy0">;</span>
    <span class="kw4">boolean</span> stopRot <span class="sy0">=</span> <span class="kw2">false</span><span class="sy0">;</span>
    <span class="kw4">boolean</span> gigle <span class="sy0">=</span> <span class="kw2">false</span><span class="sy0">;</span>
    Vector3f targetPos<span class="sy0">;</span>
    Vector3f oldPos<span class="sy0">;</span>
    Quaternion oldRot<span class="sy0">;</span>
    Quaternion targetRot<span class="sy0">;</span>
    <span class="kw4">float</span> timeRot <span class="sy0">=</span> <span class="nu0">0</span><span class="sy0">;</span>
    <span class="kw4">float</span> speedRot <span class="sy0">=</span> 0.3f<span class="sy0">;</span>
    <span class="kw4">float</span> speedPos <span class="sy0">=</span> 0.04f<span class="sy0">;</span>
 
    <span class="kw1">public</span> CardSpatialControl<span class="br0">(</span>WorldManager worldManager, Card card<span class="br0">)</span> <span class="br0">{</span>
        <span class="kw1">super</span><span class="br0">(</span>worldManager, card<span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    <span class="kw4">void</span> pos<span class="br0">(</span>Vector3f targetPos<span class="br0">)</span><span class="br0">{</span>
        <span class="kw1">this</span>.<span class="me1">targetPos</span> <span class="sy0">=</span> targetPos.<span class="me1">clone</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;;</span>
        <span class="kw1">this</span>.<span class="me1">oldPos</span> <span class="sy0">=</span> spatial.<span class="me1">getLocalTranslation</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">clone</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
        stopMove <span class="sy0">=</span> <span class="kw2">false</span><span class="sy0">;</span>
    <span class="br0">}</span>
    <span class="kw4">void</span> rot<span class="br0">(</span>Quaternion targetRot<span class="br0">)</span><span class="br0">{</span>
        <span class="kw1">this</span>.<span class="me1">targetRot</span> <span class="sy0">=</span> targetRot.<span class="me1">clone</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="kw1">this</span>.<span class="me1">oldRot</span> <span class="sy0">=</span> spatial.<span class="me1">getLocalRotation</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">clone</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
        timeRot <span class="sy0">=</span> <span class="nu0">0</span><span class="sy0">;</span>
        stopRot <span class="sy0">=</span> <span class="kw2">false</span><span class="sy0">;</span>
    <span class="br0">}</span> 
 
    <span class="kw1">public</span> <span class="kw4">void</span> controlUpdate<span class="br0">(</span><span class="kw4">float</span> tpf<span class="br0">)</span><span class="br0">{</span>
        updatePos<span class="br0">(</span>tpf<span class="br0">)</span><span class="sy0">;</span>
        updateRot<span class="br0">(</span>tpf<span class="br0">)</span><span class="sy0">;</span>
        <span class="kw1">if</span> <span class="br0">(</span>gigle<span class="br0">)</span><span class="br0">{</span>
            updateGiggle<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="br0">}</span>
    <span class="br0">}</span>
    <span class="kw4">void</span> updatePos<span class="br0">(</span><span class="kw4">float</span> tpf<span class="br0">)</span><span class="br0">{</span>
        <span class="kw1">if</span> <span class="br0">(</span>targetPos<span class="sy0">!=</span><span class="kw2">null</span><span class="br0">)</span><span class="br0">{</span>
            Vector3f newPos<span class="sy0">;</span>
            Vector3f currentPos <span class="sy0">=</span> spatial.<span class="me1">getLocalTranslation</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
            <span class="kw4">float</span> dis <span class="sy0">=</span> currentPos.<span class="me1">distance</span><span class="br0">(</span>targetPos<span class="br0">)</span>
            <span class="kw1">if</span> <span class="br0">(</span><span class="sy0">!</span>stopMove<span class="br0">)</span><span class="br0">{</span>
                <span class="kw1">if</span> <span class="br0">(</span> dis<span class="sy0">&gt;</span> speedPos<span class="br0">)</span><span class="br0">{</span>
                    Vector3f force <span class="sy0">=</span> targetPos.<span class="me1">subtract</span><span class="br0">(</span>currentPos<span class="br0">)</span>.<span class="me1">normalize</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">mult</span><span class="br0">(</span>speedPos<span class="br0">)</span>
                    newPos <span class="sy0">=</span> currentPos.<span class="me1">add</span><span class="br0">(</span>force<span class="br0">)</span>
                <span class="br0">}</span> <span class="kw1">else</span> <span class="br0">{</span>
                    newPos <span class="sy0">=</span> targetPos.<span class="me1">clone</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
                    stopMove <span class="sy0">=</span> <span class="kw2">true</span><span class="sy0">;</span>
 
                <span class="br0">}</span>
                spatial.<span class="me1">setLocalTranslation</span><span class="br0">(</span>newPos<span class="br0">)</span>
            <span class="br0">}</span>
 
        <span class="br0">}</span>
    <span class="br0">}</span>
 
    <span class="kw4">void</span> updateRot<span class="br0">(</span><span class="kw4">float</span> tpf<span class="br0">)</span><span class="br0">{</span>
        <span class="kw1">if</span> <span class="br0">(</span>targetRot<span class="sy0">!=</span>null<span class="sy0">&amp;&amp;</span>oldRot<span class="sy0">!=</span><span class="kw2">null</span><span class="br0">)</span><span class="br0">{</span>
            <span class="kw1">if</span> <span class="br0">(</span><span class="sy0">!</span>stopRot<span class="br0">)</span><span class="br0">{</span>
                Quaternion newRot <span class="sy0">=</span> <span class="kw1">new</span> Quaternion<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
                <span class="kw1">if</span> <span class="br0">(</span> timeRot <span class="sy0">&lt;</span>speedRot<span class="br0">)</span><span class="br0">{</span>
                    newRot.<span class="me1">slerp</span><span class="br0">(</span>oldRot,targetRot,<span class="br0">(</span><span class="kw4">float</span><span class="br0">)</span><span class="br0">(</span>timeRot<span class="sy0">/</span>speedRot<span class="br0">)</span><span class="br0">)</span>
                    timeRot <span class="sy0">+=</span> tpf<span class="sy0">;</span>
                <span class="br0">}</span> <span class="kw1">else</span> <span class="br0">{</span>
                    stopRot <span class="sy0">=</span> <span class="kw2">true</span><span class="sy0">;</span>
                    newRot.<span class="me1">set</span><span class="br0">(</span>targetRot<span class="br0">)</span>
                <span class="br0">}</span>
                spatial.<span class="me1">setLocalRotation</span><span class="br0">(</span>newRot<span class="br0">)</span><span class="sy0">;</span>
            <span class="br0">}</span>
        <span class="br0">}</span>
    <span class="br0">}</span>
 
    <span class="kw4">void</span> updateGiggle<span class="br0">(</span><span class="br0">)</span><span class="br0">{</span>
        <span class="kw4">float</span> x <span class="sy0">=</span><span class="br0">(</span>0.5f<span class="sy0">-</span>FastMath.<span class="me1">nextRandomFloat</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span> <span class="sy0">*</span> 0.005f<span class="sy0">;</span>
        <span class="kw4">float</span> y <span class="sy0">=</span><span class="br0">(</span>0.5f<span class="sy0">-</span>FastMath.<span class="me1">nextRandomFloat</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span> <span class="sy0">*</span> 0.005f<span class="sy0">;</span>
        <span class="kw4">float</span> z <span class="sy0">=</span><span class="nu0">0</span><span class="sy0">;</span>
        Vector3f oldPos<span class="sy0">=</span>spatial.<span class="me1">getLocalTranslation</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">clone</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
        spatial.<span class="me1">setLocalTranslation</span><span class="br0">(</span>oldPos.<span class="me1">add</span><span class="br0">(</span>x,y,z<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
<span class="br0">}</span></pre>

</div>

<h4 id="more">More</h4>
<div class="level4">

</div>
<!-- EDIT5 SECTION "Entities" [2139-9828] -->
<h3 class="sectionedit6" id="world">World</h3>
<div class="level3">

<p>
First consider the Table a GameLevel. In that specific enviroment, cards are showed, moved rotated…etc..
</p>

<p>
<strong>Explanation:</strong>
The CardTable take care of 3 things: 
</p>
<pre class="code">  
  (1| Creating:</pre>
<ol>
<li class="level1"><div class="li"> Its self from a 16×16 Quad and the Texture</div>
</li>
<li class="level4"><div class="li"> The Cards from the OrgCard model with appropriate picture</div>
</li>
<li class="level4"><div class="li"> The effects</div>
</li>
<li class="level4"><div class="li"> The 3D models</div>
</li>
</ol>
<pre class="code">  (2| Destroying things in delayed fashion:</pre>
<ol>
<li class="level1"><div class="li"> Explode the Card (cool effect!)</div>
</li>
</ol>
<pre class="code">  (3| Calculate the postions,directions of all action triggered by GamePlay. Arrange and reArrange the cards in hands, in Deck. handPos,gravePos,groundPos, deckPos…etc</pre>

<p>
We need the world to calculate postions the card place and for the translating: the target position of which the card will head to. Remember that we made a Table texture from a 4×4 Grid. Now use that and do simple math ;O :
</p>

<p>
This part
</p>
<ul>
<li class="level1"><div class="li"> load the level </div>
</li>
<li class="level1"><div class="li"> create a deck</div>
</li>
<li class="level1"><div class="li"> load card models with texture (cover) and attach a CardControl to handle the Movement and highlight</div>
</li>
</ul>
<pre class="code java"><span class="kw1">package</span> <span class="co2">magiccard.gameplay</span>
 
<span class="kw1">import</span> <span class="co2">com.jme3.asset.AssetManager</span>
<span class="kw1">import</span> <span class="co2">com.jme3.material.Material</span>
<span class="kw1">import</span> <span class="co2">com.jme3.math.ColorRGBA</span>
<span class="kw1">import</span> <span class="co2">com.jme3.math.Vector3f</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.Node</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.Geometry</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.Spatial</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.shape.Box</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.shape.Quad</span>
<span class="kw1">import</span> <span class="co2">sg.atom.gameplay.GameLevel</span>
<span class="kw1">import</span> <span class="co2">sg.atom.stage.GamePlayManager</span>
<span class="kw1">import</span> <span class="co2">sg.atom.stage.WorldManager</span>
 
<span class="kw1">import</span> <span class="co2">com.jme3.material.RenderState</span>
<span class="kw1">import</span> <span class="co2">com.jme3.renderer.queue.RenderQueue</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.shape.Sphere</span>
<span class="kw1">import</span> <span class="co2">com.jme3.math.Quaternion</span>
<span class="kw1">import</span> <span class="co2">com.jme3.math.FastMath</span>
<span class="kw1">import</span> <span class="co2">magiccard.stage.CardSelectControl</span>
<span class="kw1">import</span> <span class="co2">sg.atom.fx.particle.ParticleFactory</span>
<span class="kw1">import</span> <span class="co2">sg.atom.fx.particle.ExplosionNodeControl</span>
<span class="kw1">import</span> <span class="co2">com.jme3.light.PointLight</span>
<span class="kw1">import</span> <span class="co2">com.jme3.effect.ParticleEmitter</span>
 
<span class="kw1">class</span> CardTable <span class="kw1">extends</span> GameLevel<span class="br0">{</span>
 
<span class="kw1">private</span> Spatial cardOrg<span class="sy0">;</span>
AssetManager assetManager
 
<span class="co1">// Layout to position cards and table</span>
Vector3f center <span class="sy0">=</span> <span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">3</span>,<span class="nu0">0</span>,<span class="sy0">-</span><span class="nu0">5</span><span class="br0">)</span><span class="sy0">;</span>
<span class="kw4">float</span> handLength<span class="sy0">=</span> 2.5f
<span class="kw4">float</span> spaceBetweenCard <span class="sy0">=</span> 0.5f
<span class="kw4">float</span> peakPos<span class="sy0">=</span> 0.2f
<span class="kw4">float</span> boardSizeX <span class="sy0">=</span> <span class="nu0">16</span><span class="sy0">;</span>
<span class="kw4">float</span> boardSizeY<span class="sy0">=</span> <span class="nu0">16</span><span class="sy0">;</span>
 
Vector3f scaledCardSize <span class="sy0">=</span> <span class="kw1">new</span> Vector3f<span class="br0">(</span>1.9f,2.7f,0.02f<span class="br0">)</span><span class="sy0">;</span>
Vector3f gridGapSize <span class="sy0">=</span> <span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">1</span>,<span class="nu0">1</span>,<span class="nu0">1</span><span class="br0">)</span><span class="sy0">;</span>
<span class="kw1">public</span> <span class="kw1">static</span> faceUpQuat <span class="sy0">=</span> <span class="kw1">new</span> Quaternion<span class="br0">(</span><span class="br0">)</span>.<span class="me1">fromAngles</span><span class="br0">(</span>0f,FastMath.<span class="me1">PI</span>,0f<span class="br0">)</span><span class="sy0">;</span>
<span class="kw1">public</span> <span class="kw1">static</span> faceDownQuat <span class="sy0">=</span> <span class="kw1">new</span> Quaternion<span class="br0">(</span><span class="br0">)</span>.<span class="me1">fromAngles</span><span class="br0">(</span><span class="sy0">-</span>FastMath.<span class="me1">PI</span>,<span class="sy0">-</span>FastMath.<span class="me1">PI</span>,0f<span class="br0">)</span><span class="sy0">;</span>
<a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+list"><span class="kw3">List</span></a> actions <span class="sy0">=</span><span class="br0">[</span><span class="br0">]</span>
 
<span class="kw1">public</span> CardTable<span class="br0">(</span>GamePlayManager gameplay,WorldManager world,<a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> name,<a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> path<span class="br0">)</span><span class="br0">{</span>
<span class="kw1">super</span><span class="br0">(</span>gameplay,world,name,path<span class="br0">)</span>
assetManager <span class="sy0">=</span> world.<span class="me1">assetManager</span>
<span class="br0">}</span>
 
Quaternion getCardRot<span class="br0">(</span><span class="kw4">boolean</span> faceUp<span class="br0">)</span><span class="br0">{</span>
<span class="kw1">if</span> <span class="br0">(</span>faceUp<span class="br0">)</span><span class="br0">{</span>
<span class="kw1">return</span> faceUpQuat.<span class="me1">clone</span><span class="br0">(</span><span class="br0">)</span>
<span class="br0">}</span> <span class="kw1">else</span> <span class="br0">{</span>
<span class="kw1">return</span> faceDownQuat.<span class="me1">clone</span><span class="br0">(</span><span class="br0">)</span>
<span class="br0">}</span>
<span class="br0">}</span>
 
<span class="coMULTI">/*
* Load level, override the method in GameLevel class
*/</span>
<span class="kw1">public</span> <span class="kw4">void</span> loadLevel<span class="br0">(</span><span class="br0">)</span><span class="br0">{</span>
<span class="kw1">super</span>.<span class="me1">loadLevel</span><span class="br0">(</span><span class="br0">)</span>
createCardOrg<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
createCardBoard<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
createEffects<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
<span class="br0">}</span>
 
<span class="coMULTI">/*
* Short for new Vector3f
*/</span>
Vector3f vec3<span class="br0">(</span><span class="kw4">float</span> x,<span class="kw4">float</span> y,<span class="kw4">float</span> z<span class="br0">)</span><span class="br0">{</span>
<span class="kw1">return</span> <span class="kw1">new</span> Vector3f<span class="br0">(</span>x,y,z<span class="br0">)</span><span class="sy0">;</span>
<span class="br0">}</span>
 
<span class="coMULTI">/*
* Create the Card board model
*/</span>
<span class="kw1">public</span> <span class="kw4">void</span> createCardBoard<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
<span class="co1">//levelNode = new Node(“LevelNode”);</span>
 
Quad cardBoardShape <span class="sy0">=</span> <span class="kw1">new</span> Quad<span class="br0">(</span>boardSizeX,boardSizeY<span class="br0">)</span><span class="sy0">;</span>
Geometry cardBoard <span class="sy0">=</span> <span class="kw1">new</span> Geometry<span class="br0">(</span>“CardBoardGeo”, cardBoardShape<span class="br0">)</span><span class="sy0">;</span>
 
Material mat <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>assetManager, “MatDefs<span class="sy0">/</span>ColoredTextured.<span class="me1">j3md</span>”<span class="br0">)</span><span class="sy0">;</span>
mat.<span class="me1">setTexture</span><span class="br0">(</span>“ColorMap”, assetManager.<span class="me1">loadTexture</span><span class="br0">(</span>“Textures<span class="sy0">/</span>CardBoard<span class="sy0">/</span>DiffuseTex.<span class="me1">png</span>”<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
mat.<span class="me1">setColor</span><span class="br0">(</span>“<a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+color"><span class="kw3">Color</span></a>”, <span class="kw1">new</span> ColorRGBA<span class="br0">(</span><span class="nu0">1</span>, <span class="nu0">1</span>, <span class="nu0">1</span>, 0.9f<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
mat.<span class="me1">getAdditionalRenderState</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">setBlendMode</span><span class="br0">(</span>RenderState.<span class="me1">BlendMode</span>.<span class="me1">Alpha</span><span class="br0">)</span><span class="sy0">;</span>
cardBoard.<span class="me1">setMaterial</span><span class="br0">(</span>mat<span class="br0">)</span><span class="sy0">;</span>
cardBoard.<span class="me1">setLocalTranslation</span><span class="br0">(</span>center.<span class="me1">add</span><span class="br0">(</span><span class="br0">(</span><span class="kw4">float</span><span class="br0">)</span><span class="br0">(</span><span class="sy0">-</span>boardSizeX<span class="sy0">/</span><span class="nu0">2</span><span class="br0">)</span>,<span class="br0">(</span><span class="kw4">float</span><span class="br0">)</span><span class="br0">(</span><span class="sy0">-</span>boardSizeY<span class="sy0">/</span><span class="nu0">2</span><span class="br0">)</span>,0f<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
cardBoard.<span class="me1">setQueueBucket</span><span class="br0">(</span>RenderQueue.<span class="me1">Bucket</span>.<span class="me1">Transparent</span><span class="br0">)</span><span class="sy0">;</span>
 
levelNode.<span class="me1">attachChild</span><span class="br0">(</span>cardBoard<span class="br0">)</span><span class="sy0">;</span>
<span class="br0">}</span>
<span class="coMULTI">/*
* For debuging positions
*/</span>
<span class="kw1">public</span> <span class="kw4">void</span> createSphere<span class="br0">(</span><span class="kw4">float</span> size,ColorRGBA color,Vector3f pos<span class="br0">)</span><span class="br0">{</span>
Sphere sh<span class="sy0">=</span><span class="kw1">new</span> Sphere<span class="br0">(</span><span class="nu0">8</span>,<span class="nu0">8</span>,size<span class="br0">)</span>
Geometry sGeo <span class="sy0">=</span> <span class="kw1">new</span> Geometry<span class="br0">(</span>“S”,sh<span class="br0">)</span>
Material mat <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>assetManager, “Common<span class="sy0">/</span>MatDefs<span class="sy0">/</span>Misc<span class="sy0">/</span>Unshaded.<span class="me1">j3md</span>”<span class="br0">)</span><span class="sy0">;</span>
sGeo.<span class="me1">material</span> <span class="sy0">=</span> mat
mat.<span class="me1">setColor</span><span class="br0">(</span>“<a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+color"><span class="kw3">Color</span></a>”,color<span class="br0">)</span>
sGeo.<span class="me1">localTranslation</span> <span class="sy0">=</span> pos
levelNode.<span class="me1">attachChild</span><span class="br0">(</span>sGeo<span class="br0">)</span>
<span class="br0">}</span>
<span class="coMULTI">/*
* Create the orginal Card model
*/</span>
<span class="kw1">public</span> <span class="kw4">void</span> createCardOrg<span class="br0">(</span><span class="br0">)</span><span class="br0">{</span>
cardOrg <span class="sy0">=</span> <span class="br0">(</span><span class="br0">(</span>Node<span class="br0">)</span> <span class="br0">(</span><span class="br0">(</span>Node<span class="br0">)</span> assetManager.<span class="me1">loadModel</span><span class="br0">(</span>“Models<span class="sy0">/</span>Cards<span class="sy0">/</span>Template<span class="sy0">/</span>card1.<span class="me1">j3o</span>”<span class="br0">)</span><span class="br0">)</span>.<span class="me1">getChild</span><span class="br0">(</span>“Card”<span class="br0">)</span><span class="br0">)</span>.<span class="me1">getChild</span><span class="br0">(</span>“Cube1″<span class="br0">)</span><span class="sy0">;</span>
<span class="br0">}</span>
 
<span class="kw1">public</span> <span class="kw4">void</span> createDeck<span class="br0">(</span>CardPlayer player<span class="br0">)</span> <span class="br0">{</span>
<span class="co1">// create Cards for player</span>
 
player.<span class="me1">currentDeck</span>.<span class="me1">cardList</span>.<span class="me1">eachWithIndex</span><span class="br0">{</span>card,i<span class="sy0">-&gt;</span>
<span class="co1">//fromDeckToHand(player)</span>
def newCard <span class="sy0">=</span> createCard<span class="br0">(</span>card<span class="br0">)</span>
<span class="br0">}</span>
arrangeDeck<span class="br0">(</span>player<span class="br0">)</span>
<span class="br0">}</span>
 
<span class="kw1">public</span> <span class="kw4">void</span> createHand<span class="br0">(</span>CardPlayer player<span class="br0">)</span><span class="br0">{</span>
player.<span class="me1">hand</span>.<span class="me1">eachWithIndex</span><span class="br0">{</span>card,i<span class="sy0">-&gt;</span>
<span class="co1">//fromDeckToHand(player)</span>
def newCard <span class="sy0">=</span> createCard<span class="br0">(</span>card<span class="br0">)</span>
<span class="br0">}</span>
arrangeHand<span class="br0">(</span>player<span class="br0">)</span>
<span class="br0">}</span>
 
Geometry createCard<span class="br0">(</span>Card card<span class="br0">)</span> <span class="br0">{</span>
<span class="co1">// extract the card info</span>
<a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> path <span class="sy0">=</span> card.<span class="me1">picture</span>
 
<span class="co1">// create the geometry</span>
Geometry newCard <span class="sy0">=</span> <span class="br0">(</span>Geometry<span class="br0">)</span> cardOrg.<span class="me1">clone</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
Material cloneMat <span class="sy0">=</span> newCard.<span class="me1">getMaterial</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">clone</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
cloneMat.<span class="me1">setTexture</span><span class="br0">(</span>“ColorMap2″, assetManager.<span class="me1">loadTexture</span><span class="br0">(</span>path<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
newCard.<span class="me1">setMaterial</span><span class="br0">(</span>cloneMat<span class="br0">)</span><span class="sy0">;</span>
<span class="co1">//cloneMat.setBoolean(“MixGlow”,true);</span>
levelNode.<span class="me1">attachChild</span><span class="br0">(</span>newCard<span class="br0">)</span><span class="sy0">;</span>
card.<span class="me1">spatial</span> <span class="sy0">=</span> newCard<span class="sy0">;</span>
newCard.<span class="me1">setLocalScale</span><span class="br0">(</span><span class="sy0">-</span>0.4f,<span class="sy0">-</span>0.4f,0.4f<span class="br0">)</span>
<span class="co1">// attach the control</span>
newCard.<span class="me1">addControl</span><span class="br0">(</span><span class="kw1">new</span> CardSpatialControl<span class="br0">(</span>worldManager,card<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
newCard.<span class="me1">addControl</span><span class="br0">(</span><span class="kw1">new</span> CardSelectControl<span class="br0">(</span>worldManager,gamePlayManager<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
<span class="kw1">return</span> newCard<span class="sy0">;</span>
<span class="br0">}</span>
 
CardSpatialControl getCardControl<span class="br0">(</span>Spatial spatial<span class="br0">)</span><span class="br0">{</span>
<span class="kw1">return</span> spatial.<span class="me1">getControl</span><span class="br0">(</span>CardSpatialControl.<span class="kw1">class</span><span class="br0">)</span>
<span class="br0">}</span></pre>

<p>
These pieces help to find the exact location of card in each situation:
</p>
<ul>
<li class="level1"><div class="li"> ArrangeDeck</div>
</li>
<li class="level1"><div class="li"> ArrangHand</div>
</li>
<li class="level1"><div class="li"> CenterHandPos</div>
</li>
<li class="level1"><div class="li"> DeckPos</div>
</li>
<li class="level1"><div class="li"> GravePos</div>
</li>
<li class="level1"><div class="li"> GroundPos</div>
</li>
<li class="level1"><div class="li"> MagicPos</div>
</li>
</ul>
<pre class="code java"><span class="kw1">public</span> <span class="kw4">void</span> arrangeDeck<span class="br0">(</span>CardPlayer player<span class="br0">)</span><span class="br0">{</span>
<span class="kw4">int</span> numOfCards <span class="sy0">=</span> player.<span class="me1">currentDeck</span>.<span class="me1">cardList</span>.<span class="me1">size</span><span class="br0">(</span><span class="br0">)</span>
 
Vector3f centerDeck <span class="sy0">=</span> getCenterHandPos<span class="br0">(</span>player<span class="br0">)</span><span class="sy0">;</span>
Vector3f gap <span class="sy0">=</span> vec3<span class="br0">(</span>0.4f,<span class="nu0">0</span>,0.02f<span class="br0">)</span><span class="sy0">;</span>
Vector3f handSize <span class="sy0">=</span> vec3<span class="br0">(</span><span class="nu0">0</span>,<span class="nu0">0</span>,0.5f<span class="br0">)</span><span class="sy0">;</span>
 
gap <span class="sy0">=</span> handSize.<span class="me1">divide</span><span class="br0">(</span>vec3<span class="br0">(</span><span class="nu0">1</span>,<span class="nu0">1</span>,<span class="br0">(</span><span class="kw4">float</span><span class="br0">)</span> numOfCards<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
player.<span class="me1">currentDeck</span>.<span class="me1">cardList</span>.<span class="me1">eachWithIndex</span><span class="br0">{</span>card,i<span class="sy0">-&gt;</span>
<span class="co1">//fromDeckToHand(player)</span>
def newCard <span class="sy0">=</span> card.<span class="me1">spatial</span>
 
<span class="co1">//Quaternion rotPIY =new Quaternion().fromAngleAxis(FastMath.PI,Vector3f.UNIT_Y);</span>
<span class="co1">//Quaternion rotPIZ =new Quaternion().fromAngleAxis(FastMath.PI,Vector3f.UNIT_Z);</span>
<span class="co1">//Quaternion rotXYZ =new Quaternion().fromAngles(0f,FastMath.PI,0f)</span>
<span class="co1">//newCard.setLocalRotation(rotXYZ)</span>
 
Vector3f cardPos <span class="sy0">=</span> gap.<span class="me1">mult</span><span class="br0">(</span>vec3<span class="br0">(</span><span class="br0">(</span><span class="kw4">float</span><span class="br0">)</span>i,1f,<span class="br0">(</span><span class="kw4">float</span><span class="br0">)</span>i<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
Vector3f deckPos<span class="sy0">;</span>
<span class="kw1">if</span> <span class="br0">(</span>isCurrentPlayer<span class="br0">(</span>player<span class="br0">)</span><span class="br0">)</span><span class="br0">{</span>
deckPos <span class="sy0">=</span>vec3<span class="br0">(</span>9f,<span class="sy0">-</span><span class="nu0">6.5</span>,<span class="sy0">-</span><span class="nu0">5</span><span class="br0">)</span>
<span class="br0">}</span> <span class="kw1">else</span> <span class="br0">{</span>
deckPos <span class="sy0">=</span>vec3<span class="br0">(</span><span class="sy0">-</span>3f,<span class="nu0">6.5</span>,<span class="sy0">-</span><span class="nu0">5</span><span class="br0">)</span>
<span class="br0">}</span>
newCard.<span class="me1">setLocalTranslation</span><span class="br0">(</span>deckPos.<span class="me1">add</span><span class="br0">(</span>cardPos<span class="br0">)</span><span class="br0">)</span>
<span class="br0">}</span>
<span class="br0">}</span>
<span class="kw1">public</span> <span class="kw4">void</span> arrangeHand<span class="br0">(</span>CardPlayer player<span class="br0">)</span><span class="br0">{</span>
<span class="kw4">int</span> numOfCards <span class="sy0">=</span> player.<span class="me1">hand</span>.<span class="me1">size</span><span class="br0">(</span><span class="br0">)</span>
 
Vector3f centerHand <span class="sy0">=</span> getCenterHandPos<span class="br0">(</span>player<span class="br0">)</span><span class="sy0">;</span>
Vector3f gap <span class="sy0">=</span> vec3<span class="br0">(</span>0.4f,0f,0.02f<span class="br0">)</span><span class="sy0">;</span>
<span class="kw4">float</span> squareSize<span class="sy0">=</span> boardSizeX<span class="sy0">-</span>6f
Vector3f handSize <span class="sy0">=</span> vec3<span class="br0">(</span>squareSize,0f,0.02f<span class="br0">)</span><span class="sy0">;</span>
 
gap <span class="sy0">=</span> handSize.<span class="me1">divide</span><span class="br0">(</span>vec3<span class="br0">(</span><span class="br0">(</span><span class="kw4">float</span><span class="br0">)</span> numOfCards,<span class="nu0">1</span>,<span class="nu0">1</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
<span class="kw4">boolean</span> faceUp <span class="sy0">=</span> isCurrentPlayer<span class="br0">(</span>player<span class="br0">)</span><span class="sy0">;</span>
player.<span class="me1">hand</span>.<span class="me1">eachWithIndex</span><span class="br0">{</span>card,i<span class="sy0">-&gt;</span>
<span class="co1">//fromDeckToHand(player)</span>
def newCard <span class="sy0">=</span> card.<span class="me1">spatial</span>
 
Quaternion rotPIY <span class="sy0">=</span><span class="kw1">new</span> Quaternion<span class="br0">(</span><span class="br0">)</span>.<span class="me1">fromAngleAxis</span><span class="br0">(</span>FastMath.<span class="me1">PI</span>,Vector3f.<span class="me1">UNIT_Y</span><span class="br0">)</span><span class="sy0">;</span>
Quaternion rotPIZ <span class="sy0">=</span><span class="kw1">new</span> Quaternion<span class="br0">(</span><span class="br0">)</span>.<span class="me1">fromAngleAxis</span><span class="br0">(</span>FastMath.<span class="me1">PI</span>,Vector3f.<span class="me1">UNIT_Z</span><span class="br0">)</span><span class="sy0">;</span>
Quaternion rotXYZ <span class="sy0">=</span>getCardRot<span class="br0">(</span>faceUp <span class="sy0">||</span> gamePlayManager.<span class="me1">debugMode</span><span class="br0">)</span>
<span class="co1">//newCard.setLocalRotation(rotXYZ)</span>
 
Vector3f cardPos <span class="sy0">=</span> gap.<span class="me1">mult</span><span class="br0">(</span>vec3<span class="br0">(</span><span class="br0">(</span><span class="kw4">float</span><span class="br0">)</span>i,1f,<span class="br0">(</span><span class="kw4">float</span><span class="br0">)</span>i<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
Vector3f handPos <span class="sy0">=</span> centerHand.<span class="me1">add</span><span class="br0">(</span>0f,0f,0f<span class="br0">)</span><span class="sy0">;</span>
<span class="co1">//newCard.setLocalTranslation(handPos.add(cardPos));</span>
CardSpatialControl cc<span class="sy0">=</span>getCardControl<span class="br0">(</span>card.<span class="me1">spatial</span><span class="br0">)</span>
cc.<span class="me1">pos</span><span class="br0">(</span>handPos.<span class="me1">add</span><span class="br0">(</span>cardPos<span class="br0">)</span><span class="br0">)</span>
 
cc.<span class="me1">rot</span><span class="br0">(</span>rotXYZ<span class="br0">)</span>
 
<span class="br0">}</span>
 
<span class="br0">}</span>
 
<span class="kw4">void</span> putToGrave<span class="br0">(</span><span class="br0">)</span><span class="br0">{</span>
 
<span class="br0">}</span>
<span class="kw4">boolean</span> isCurrentPlayer<span class="br0">(</span>CardPlayer player<span class="br0">)</span><span class="br0">{</span>
<span class="kw1">return</span> gamePlayManager.<span class="me1">isCurrentPlayer</span><span class="br0">(</span>player<span class="br0">)</span>
<span class="br0">}</span>
 
Vector3f getCenterHandPos<span class="br0">(</span>CardPlayer player<span class="br0">)</span><span class="br0">{</span>
Vector3f centerHandPos<span class="sy0">;</span>
<span class="kw4">float</span> halfSizeY <span class="sy0">=</span> <span class="br0">(</span><span class="kw4">float</span><span class="br0">)</span><span class="br0">(</span><span class="br0">(</span>boardSizeY – 0.3f<span class="br0">)</span><span class="sy0">/</span>2f<span class="br0">)</span><span class="sy0">;</span>
<span class="kw1">if</span> <span class="br0">(</span>isCurrentPlayer<span class="br0">(</span>player<span class="br0">)</span><span class="br0">)</span><span class="br0">{</span>
centerHandPos <span class="sy0">=</span> center.<span class="me1">add</span><span class="br0">(</span>0f,<span class="sy0">-</span>halfSizeY,0.5f<span class="br0">)</span>
<span class="br0">}</span> <span class="kw1">else</span> <span class="br0">{</span>
centerHandPos <span class="sy0">=</span> center.<span class="me1">add</span><span class="br0">(</span>0f,halfSizeY,0.5f<span class="br0">)</span>
<span class="br0">}</span>
<span class="kw1">return</span> centerHandPos<span class="sy0">;</span>
<span class="br0">}</span>
 
Vector3f handPos<span class="br0">(</span>CardPlayer player,<span class="kw4">int</span> index,<span class="kw4">boolean</span> peak<span class="br0">)</span><span class="br0">{</span>
Vector3f centerHandPos <span class="sy0">=</span> getCenterHandPos<span class="br0">(</span>player<span class="br0">)</span>
 
<span class="kw4">int</span> numHandCards <span class="sy0">=</span>player.<span class="me1">hand</span>.<span class="me1">size</span><span class="br0">(</span><span class="br0">)</span>
<span class="kw4">float</span> indexf<span class="sy0">=</span><span class="nu0">0</span>
 
<span class="kw1">if</span> <span class="br0">(</span>index <span class="sy0">==</span> <span class="sy0">-</span><span class="nu0">1</span><span class="br0">)</span><span class="br0">{</span>
numHandCards <span class="sy0">++</span>
indexf <span class="sy0">=</span> numHandCards
<span class="br0">}</span> <span class="kw1">else</span> <span class="kw1">if</span> <span class="br0">(</span>index <span class="sy0">==</span> <span class="sy0">-</span><span class="nu0">2</span><span class="br0">)</span><span class="br0">{</span>
indexf <span class="sy0">=</span> numHandCards <span class="sy0">+</span> <span class="nu0">2</span>
<span class="br0">}</span> <span class="kw1">else</span> <span class="kw1">if</span> <span class="br0">(</span>index <span class="sy0">==</span> <span class="sy0">-</span><span class="nu0">3</span><span class="br0">)</span><span class="br0">{</span>
indexf <span class="sy0">=</span> numHandCards
numHandCards <span class="sy0">=</span> <span class="nu0">5</span>
<span class="br0">}</span>
horizontalPos <span class="sy0">=</span> handLength <span class="sy0">*</span> indexf <span class="sy0">+</span> numHandCards
 
Vector3f nextCardPos <span class="sy0">=</span> vec3<span class="br0">(</span><span class="nu0">0</span>,horizontalPos,<span class="nu0">0</span><span class="br0">)</span>.<span class="me1">add</span><span class="br0">(</span>centerHandPos<span class="br0">)</span>
 
<span class="kw1">if</span> <span class="br0">(</span>peak<span class="br0">)</span><span class="br0">{</span>
nextCardPos.<span class="me1">add</span><span class="br0">(</span>vec3<span class="br0">(</span><span class="nu0">0</span>,peakPos,<span class="nu0">0</span><span class="br0">)</span><span class="br0">)</span>
<span class="br0">}</span>
<span class="kw1">return</span> nextCardPos<span class="sy0">;</span>
<span class="br0">}</span>
 
Vector3f deckPos<span class="br0">(</span>CardPlayer player<span class="br0">)</span><span class="br0">{</span>
<span class="kw1">if</span> <span class="br0">(</span>isCurrentPlayer<span class="br0">(</span>player<span class="br0">)</span><span class="br0">)</span><span class="br0">{</span>
<span class="kw1">return</span> vec3<span class="br0">(</span><span class="nu0">1</span>,<span class="nu0">1</span>,<span class="nu0">1</span><span class="br0">)</span>
<span class="br0">}</span> <span class="kw1">else</span> <span class="br0">{</span>
<span class="kw1">return</span> vec3<span class="br0">(</span><span class="nu0">1</span>,<span class="nu0">4</span>,<span class="nu0">1</span><span class="br0">)</span>
<span class="br0">}</span>
<span class="br0">}</span>
Vector3f gravePos<span class="br0">(</span>CardPlayer player<span class="br0">)</span><span class="br0">{</span>
<span class="kw1">if</span> <span class="br0">(</span>isCurrentPlayer<span class="br0">(</span>player<span class="br0">)</span><span class="br0">)</span><span class="br0">{</span>
<span class="kw1">return</span> vec3<span class="br0">(</span><span class="nu0">1</span>,<span class="nu0">1</span>,<span class="nu0">1</span><span class="br0">)</span>
<span class="br0">}</span> <span class="kw1">else</span> <span class="br0">{</span>
<span class="kw1">return</span> vec3<span class="br0">(</span><span class="nu0">1</span>,<span class="nu0">4</span>,<span class="nu0">1</span><span class="br0">)</span>
<span class="br0">}</span>
<span class="br0">}</span>
Vector3f groundPos<span class="br0">(</span>CardPlayer player,<span class="kw4">int</span> index<span class="br0">)</span><span class="br0">{</span>
<span class="kw1">if</span> <span class="br0">(</span>isCurrentPlayer<span class="br0">(</span>player<span class="br0">)</span><span class="br0">)</span><span class="br0">{</span>
<span class="kw1">return</span> vec3<span class="br0">(</span><span class="sy0">-</span>0.8f,<span class="sy0">-</span>1.7f,<span class="sy0">-</span><span class="nu0">5</span><span class="br0">)</span>.<span class="me1">add</span><span class="br0">(</span>scaledCardSize.<span class="me1">mult</span><span class="br0">(</span>vec3<span class="br0">(</span><span class="br0">(</span><span class="kw4">float</span><span class="br0">)</span>index,0f,0f<span class="br0">)</span><span class="br0">)</span><span class="br0">)</span>
<span class="br0">}</span> <span class="kw1">else</span> <span class="br0">{</span>
<span class="kw1">return</span> vec3<span class="br0">(</span><span class="sy0">-</span>0.8f,1.7f,<span class="sy0">-</span><span class="nu0">5</span><span class="br0">)</span>.<span class="me1">add</span><span class="br0">(</span>scaledCardSize.<span class="me1">mult</span><span class="br0">(</span>vec3<span class="br0">(</span><span class="br0">(</span><span class="kw4">float</span><span class="br0">)</span>index,0f,0f<span class="br0">)</span><span class="br0">)</span><span class="br0">)</span>
<span class="br0">}</span>
<span class="br0">}</span>
Vector3f magicPos<span class="br0">(</span>CardPlayer player,<span class="kw4">int</span> index<span class="br0">)</span><span class="br0">{</span>
<span class="kw1">if</span> <span class="br0">(</span>isCurrentPlayer<span class="br0">(</span>player<span class="br0">)</span><span class="br0">)</span><span class="br0">{</span>
<span class="kw1">return</span> vec3<span class="br0">(</span><span class="sy0">-</span>0.8f,<span class="sy0">-</span>4.5f,<span class="sy0">-</span><span class="nu0">5</span><span class="br0">)</span>.<span class="me1">add</span><span class="br0">(</span>scaledCardSize.<span class="me1">mult</span><span class="br0">(</span>vec3<span class="br0">(</span><span class="br0">(</span><span class="kw4">float</span><span class="br0">)</span>index,0f,0f<span class="br0">)</span><span class="br0">)</span><span class="br0">)</span>
<span class="br0">}</span> <span class="kw1">else</span> <span class="br0">{</span>
<span class="kw1">return</span> vec3<span class="br0">(</span><span class="sy0">-</span>0.8f,4.5f,<span class="sy0">-</span><span class="nu0">5</span><span class="br0">)</span>.<span class="me1">add</span><span class="br0">(</span>scaledCardSize.<span class="me1">mult</span><span class="br0">(</span>vec3<span class="br0">(</span><span class="br0">(</span><span class="kw4">float</span><span class="br0">)</span>index,0f,0f<span class="br0">)</span><span class="br0">)</span><span class="br0">)</span>
<span class="br0">}</span>
<span class="br0">}</span>
<span class="kw4">void</span> fromDeckToHand<span class="br0">(</span>CardPlayer player,Card card<span class="br0">)</span><span class="br0">{</span>
Vector3f nextCardPos<span class="sy0">=</span>handPos<span class="br0">(</span>player,<span class="sy0">-</span><span class="nu0">3</span>,<span class="kw2">false</span><span class="br0">)</span>
CardSpatialControl cc<span class="sy0">=</span>getCardControl<span class="br0">(</span>card.<span class="me1">spatial</span><span class="br0">)</span>
cc.<span class="me1">pos</span><span class="br0">(</span>nextCardPos<span class="br0">)</span>
<span class="co1">//cc.faceUp()</span>
<span class="co1">//cc.moveTo(nextCardPos,3)</span>
<span class="br0">}</span>
<span class="kw4">void</span> fromHandToMagic<span class="br0">(</span>CardPlayer player,Card card<span class="br0">)</span><span class="br0">{</span>
Vector3f nextCardPos<span class="sy0">=</span>magicPos<span class="br0">(</span>player,player.<span class="me1">magic</span>.<span class="me1">size</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span>
CardSpatialControl cc<span class="sy0">=</span>getCardControl<span class="br0">(</span>card.<span class="me1">spatial</span><span class="br0">)</span>
cc.<span class="me1">pos</span><span class="br0">(</span>nextCardPos<span class="br0">)</span>
cc.<span class="me1">rot</span><span class="br0">(</span>getCardRot<span class="br0">(</span><span class="kw2">false</span><span class="br0">)</span><span class="br0">)</span>
 
<span class="br0">}</span>
 
<span class="kw4">void</span> fromHandToGround<span class="br0">(</span>CardPlayer player,Card card<span class="br0">)</span><span class="br0">{</span>
Vector3f nextCardPos<span class="sy0">=</span>groundPos<span class="br0">(</span>player,player.<span class="me1">ground</span>.<span class="me1">size</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span>
CardSpatialControl cc<span class="sy0">=</span>getCardControl<span class="br0">(</span>card.<span class="me1">spatial</span><span class="br0">)</span>
cc.<span class="me1">pos</span><span class="br0">(</span>nextCardPos<span class="br0">)</span>
 
<span class="br0">}</span>
<span class="kw1">public</span> Vector3f getCamPos<span class="br0">(</span><span class="br0">)</span><span class="br0">{</span>
<span class="kw1">return</span> center.<span class="me1">add</span><span class="br0">(</span>0f,<span class="sy0">-</span>8f,20f<span class="br0">)</span>
<span class="br0">}</span></pre>

<p>
This is the update hook of the Level. We update it by clean up and execute delayed actions!!!
</p>
<pre class="code java"><span class="kw1">public</span> <span class="kw4">void</span> simpleUpdate<span class="br0">(</span><span class="kw4">float</span> tpf<span class="br0">)</span><span class="br0">{</span>
<span class="co1">// see if anything queued</span>
<span class="kw1">for</span> <span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+iterator"><span class="kw3">Iterator</span></a> it<span class="sy0">=</span>actions.<span class="me1">iterator</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span> it.<span class="me1">hasNext</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span> <span class="br0">)</span> <span class="br0">{</span>
def action <span class="sy0">=</span> it.<span class="me1">next</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
<span class="kw1">if</span> <span class="br0">(</span><span class="br0">(</span>action.<span class="me1">time</span> <span class="sy0">-=</span> tpf<span class="br0">)</span> <span class="sy0">&lt;</span><span class="nu0">0</span><span class="br0">)</span> <span class="br0">{</span>
action.<span class="kw1">do</span><span class="br0">(</span><span class="br0">)</span>
it.<span class="me1">remove</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
<span class="br0">}</span> <span class="kw1">else</span> <span class="br0">{</span>
<span class="co1">// do nothing but wait</span>
<span class="br0">}</span>
<span class="br0">}</span>
<span class="br0">}</span></pre>

<p>
Make a cool explosion effect by calling the Atom's ParticleFactory, play it when a card destroyed
</p>
<pre class="code java"><span class="kw4">void</span> destroy<span class="br0">(</span>CardPlayer player,Card card<span class="br0">)</span><span class="br0">{</span>
addExplosion<span class="br0">(</span>card.<span class="me1">spatial</span>.<span class="me1">localTranslation</span><span class="br0">)</span>
CardSpatialControl cc<span class="sy0">=</span>getCardControl<span class="br0">(</span>card.<span class="me1">spatial</span><span class="br0">)</span>
cc.<span class="me1">gigle</span> <span class="sy0">=</span> <span class="kw2">true</span><span class="sy0">;</span>
actions<span class="sy0">&lt;&lt;</span><span class="br0">[</span>
time<span class="sy0">:</span>1f,
<span class="kw1">do</span><span class="sy0">:</span><span class="br0">{</span>
card.<span class="me1">spatial</span>.<span class="me1">removeFromParent</span><span class="br0">(</span><span class="br0">)</span>
<span class="br0">}</span>
<span class="br0">]</span>
<span class="br0">}</span>
 
Node explosionPrefab<span class="sy0">;</span>
<span class="kw4">void</span> addExplosion<span class="br0">(</span>Vector3f pos<span class="br0">)</span><span class="br0">{</span>
def explosion <span class="sy0">=</span> explosionPrefab.<span class="me1">clone</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
explosion.<span class="me1">localTranslation</span> <span class="sy0">=</span>pos.<span class="me1">clone</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
<span class="coMULTI">/*
levelNode.attachChild(flame);
levelNode.attachChild(rain);
levelNode.attachChild(spark);
*/</span>
levelNode.<span class="me1">attachChild</span><span class="br0">(</span>explosion<span class="br0">)</span><span class="sy0">;</span>
<span class="br0">}</span>
 
<span class="kw4">void</span> createEffects<span class="br0">(</span><span class="br0">)</span><span class="br0">{</span>
ParticleFactory pf <span class="sy0">=</span> <span class="kw1">new</span> ParticleFactory<span class="br0">(</span>assetManager<span class="br0">)</span><span class="sy0">;</span>
<span class="coMULTI">/*
ParticleEmitter flame = pf.createFlame();
flame.setLocalTranslation(new Vector3f(6f,4f,-5f));
 
ParticleEmitter rain = pf.createRain(“”);
rain.setLocalTranslation(new Vector3f(0,0,-5f));
 
ParticleEmitter spark = pf.createSpark();
spark.setLocalTranslation(new Vector3f(0,0,-5f));
*/</span>
explosionPrefab <span class="sy0">=</span> pf.<span class="me1">createExplosionNode</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
explosionPrefab.<span class="me1">getControl</span><span class="br0">(</span>ExplosionNodeControl.<span class="kw1">class</span><span class="br0">)</span>.<span class="me1">setMaxTime</span><span class="br0">(</span>2f<span class="br0">)</span>
<span class="br0">}</span></pre>

<p>
Load the card character 3d model for a specific card
</p>
<pre class="code java"><span class="kw1">public</span> <span class="kw4">void</span> loadCharacters<span class="br0">(</span><span class="br0">)</span><span class="br0">{</span>
 
Quaternion rot<span class="sy0">=</span> <span class="kw1">new</span> Quaternion<span class="br0">(</span><span class="br0">)</span>.<span class="me1">fromAngleAxis</span><span class="br0">(</span>FastMath.<span class="me1">HALF_PI</span>,Vector3f.<span class="me1">UNIT_X</span><span class="br0">)</span>
<span class="coMULTI">/*
Spatial demon = assetManager.loadModel(“Models/Demons/BlueEyeWhiteDragon/BlueEyes.j3o”);
demon.scale(0.04f);
demon.setLocalRotation(rot);
levelNode.attachChild(demon);
*/</span>
Spatial witch <span class="sy0">=</span> assetManager.<span class="me1">loadModel</span><span class="br0">(</span>“Models<span class="sy0">/</span>Demons<span class="sy0">/</span>Magicians<span class="sy0">/</span>White<span class="sy0">/</span>WhiteFemaleMagician.<span class="me1">j3o</span>”<span class="br0">)</span><span class="sy0">;</span>
witch.<span class="me1">scale</span><span class="br0">(</span>0.5f<span class="br0">)</span><span class="sy0">;</span>
witch.<span class="me1">setLocalTranslation</span><span class="br0">(</span><span class="kw1">new</span> Vector3f<span class="br0">(</span>3f,4f,<span class="sy0">-</span>5f<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
witch.<span class="me1">setLocalRotation</span><span class="br0">(</span>rot<span class="br0">)</span><span class="sy0">;</span>
levelNode.<span class="me1">attachChild</span><span class="br0">(</span>witch<span class="br0">)</span><span class="sy0">;</span>
 
Spatial samurai <span class="sy0">=</span> assetManager.<span class="me1">loadModel</span><span class="br0">(</span>“Models<span class="sy0">/</span>Demons<span class="sy0">/</span>Warior<span class="sy0">/</span>SamuraiWarior.<span class="me1">j3o</span>”<span class="br0">)</span><span class="sy0">;</span>
samurai.<span class="me1">setLocalTranslation</span><span class="br0">(</span><span class="kw1">new</span> Vector3f<span class="br0">(</span>6f,4f,<span class="sy0">-</span>5f<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
samurai.<span class="me1">scale</span><span class="br0">(</span>0.5f<span class="br0">)</span><span class="sy0">;</span>
samurai.<span class="me1">setLocalRotation</span><span class="br0">(</span>rot<span class="br0">)</span><span class="sy0">;</span>
levelNode.<span class="me1">attachChild</span><span class="br0">(</span>samurai<span class="br0">)</span><span class="sy0">;</span>
 
<span class="co3">/** A white, spot light source. */</span>
PointLight lamp <span class="sy0">=</span> <span class="kw1">new</span> PointLight<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
lamp.<span class="me1">setPosition</span><span class="br0">(</span>getCamPos<span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
lamp.<span class="me1">setColor</span><span class="br0">(</span>ColorRGBA.<span class="me1">White</span><span class="br0">)</span><span class="sy0">;</span>
levelNode.<span class="me1">addLight</span><span class="br0">(</span>lamp<span class="br0">)</span><span class="sy0">;</span>
<span class="br0">}</span>
<span class="br0">}</span></pre>

</div>
<!-- EDIT6 SECTION "World" [9829-21945] -->
<h3 class="sectionedit7" id="select">Select</h3>
<div class="level3">

<p>
For a card game, select is a very important game mechanic, in fact, you are nearly ask to select/choose somethings almost everytime. In Atom, I introduce a generic way to hook your select function into your code game mechanic. 
This section is quite advance for who don’t familiar with groovy but keep your self cheerful cause you going to enjoy Groovy as much as I do! 
</p>

<p>
Short: 
</p>

<p>
Detailed: 
</p>

<p>
For this card game, we will implement a few things in this designed mechanic:
</p>

</div>

<h4 id="select_function">Select function:</h4>
<div class="level4">
<pre class="code java"> </pre>

</div>

<h4 id="select_condition">Select condition:</h4>
<div class="level4">
<pre class="code java"> </pre>

</div>

<h4 id="select_control">Select Control:</h4>
<div class="level4">
<pre class="code java"><span class="kw1">package</span> <span class="co2">magiccard.stage</span><span class="sy0">;</span>
 
<span class="kw1">import</span> <span class="co2">com.jme3.math.Vector3f</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.Geometry</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.Spatial</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">sg.atom.stage.WorldManager</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">sg.atom.stage.select.SpatialSelectControl</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">magiccard.gameplay.CardGamePlay</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">magiccard.gameplay.Card</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">magiccard.gameplay.CardSpatialControl</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">sg.atom.stage.select.EntitySelectCondition</span><span class="sy0">;</span>
 
<span class="co3">/**
*
* @author cuong.nguyenmanh2
*/</span>
<span class="kw1">public</span> <span class="kw1">class</span> CardSelectControl <span class="kw1">extends</span> SpatialSelectControl <span class="br0">{</span>
 
<span class="kw1">private</span> Vector3f bigScale<span class="sy0">;</span>
<span class="kw1">private</span> Vector3f orginalScale<span class="sy0">;</span>
<span class="kw1">private</span> Vector3f orginalPos<span class="sy0">;</span>
<span class="kw1">private</span> Vector3f peakPos<span class="sy0">;</span>
<span class="kw1">private</span> <span class="kw4">boolean</span> skipOutHover<span class="sy0">;</span>
<span class="kw1">private</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> currentFunction<span class="sy0">;</span>
<span class="kw1">private</span> CardGamePlay gameplay<span class="sy0">;</span>
<span class="kw1">private</span> Card card<span class="sy0">;</span>
<span class="kw1">private</span> <span class="kw4">boolean</span> isBigger <span class="sy0">=</span> <span class="kw2">false</span><span class="sy0">;</span>
<span class="kw1">private</span> <span class="kw4">boolean</span> isPeak <span class="sy0">=</span> <span class="kw2">false</span><span class="sy0">;</span>
<span class="kw1">private</span> <span class="kw4">boolean</span> isHighlight <span class="sy0">=</span> <span class="kw2">false</span><span class="sy0">;</span>
 
<span class="kw1">public</span> CardSelectControl<span class="br0">(</span>WorldManager worldManager, CardGamePlay gameplay<span class="br0">)</span> <span class="br0">{</span>
currentFunction <span class="sy0">=</span> “Normal”<span class="sy0">;</span>
<span class="kw1">this</span>.<span class="me1">gameplay</span> <span class="sy0">=</span> gameplay<span class="sy0">;</span>
<span class="br0">}</span>
 
@Override
<span class="kw1">public</span> <span class="kw4">void</span> setSpatial<span class="br0">(</span>Spatial spatial<span class="br0">)</span> <span class="br0">{</span>
<span class="kw1">super</span>.<span class="me1">setSpatial</span><span class="br0">(</span>spatial<span class="br0">)</span><span class="sy0">;</span>
<span class="kw1">this</span>.<span class="me1">card</span> <span class="sy0">=</span> <span class="br0">(</span>Card<span class="br0">)</span> spatial.<span class="me1">getControl</span><span class="br0">(</span>CardSpatialControl.<span class="kw1">class</span><span class="br0">)</span>.<span class="me1">getEntity</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
orginalScale <span class="sy0">=</span> spatial.<span class="me1">getLocalScale</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">clone</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
bigScale <span class="sy0">=</span> orginalScale.<span class="me1">mult</span><span class="br0">(</span>1.2f<span class="br0">)</span><span class="sy0">;</span>
orginalPos <span class="sy0">=</span> spatial.<span class="me1">getLocalTranslation</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">clone</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
<span class="br0">}</span>
 
@Override
<span class="kw1">protected</span> <span class="kw4">void</span> doSelected<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
<span class="kw1">super</span>.<span class="me1">doSelected</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
<span class="co1">//orginalScale = spatial.getLocalScale();</span>
<span class="co1">//orginalPos = spatial.getLocalTranslation().clone();</span>
<span class="co1">//peakPos = orginalPos.add(new Vector3f(0f, 0.4f, 0f));</span>
<span class="co1">//spatial.setLocalTranslation(peakPos);</span>
<span class="co1">//spatial.setLocalScale(bigScale);</span>
<span class="br0">}</span>
 
@Override
<span class="kw1">protected</span> <span class="kw4">void</span> doDeselected<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
<span class="kw1">super</span>.<span class="me1">doDeselected</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
<span class="co1">//spatial.setLocalScale(orginalScale);</span>
<span class="co1">//spatial.setLocalTranslation(orginalPos.clone());</span>
 
<span class="br0">}</span>
 
@Override
<span class="kw1">protected</span> <span class="kw4">void</span> doHovered<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
<span class="kw1">if</span> <span class="br0">(</span><span class="kw1">this</span>.<span class="me1">isHoverable</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
<span class="kw1">super</span>.<span class="me1">doHovered</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
<span class="co1">//orginalScale = spatial.getLocalScale();</span>
EntitySelectCondition inHand <span class="sy0">=</span> <span class="br0">(</span>EntitySelectCondition<span class="br0">)</span> gameplay.<span class="me1">cardSelectRules</span>.<span class="me1">get</span><span class="br0">(</span>“inHand”<span class="br0">)</span><span class="sy0">;</span>
EntitySelectCondition inGround <span class="sy0">=</span> <span class="br0">(</span>EntitySelectCondition<span class="br0">)</span> gameplay.<span class="me1">cardSelectRules</span>.<span class="me1">get</span><span class="br0">(</span>“inGround”<span class="br0">)</span><span class="sy0">;</span>
<span class="kw1">if</span> <span class="br0">(</span>inHand.<span class="me1">isSelected</span><span class="br0">(</span>card<span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
peak<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
bigger<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
highlight<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
<span class="br0">}</span> <span class="kw1">else</span> <span class="kw1">if</span> <span class="br0">(</span>inGround.<span class="me1">isSelected</span><span class="br0">(</span>card<span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
<span class="co1">// The card is the ground</span>
highlight<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
<span class="br0">}</span>
<span class="br0">}</span>
<span class="br0">}</span>
 
@Override
<span class="kw1">protected</span> <span class="kw4">void</span> doOutHovered<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
<span class="kw1">if</span> <span class="br0">(</span><span class="kw1">this</span>.<span class="me1">isHoverable</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
<span class="kw1">if</span> <span class="br0">(</span><span class="sy0">!</span><span class="kw1">this</span>.<span class="me1">skipOutHover</span><span class="br0">)</span> <span class="br0">{</span>
<span class="kw1">super</span>.<span class="me1">doOutHovered</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
 
noPeak<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
smaller<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
noHighlight<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
 
<span class="br0">}</span>
<span class="br0">}</span>
<span class="br0">}</span>
 
<span class="kw1">public</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> getCurrentFunction<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
<span class="kw1">return</span> currentFunction<span class="sy0">;</span>
<span class="br0">}</span>
 
<span class="kw1">public</span> <span class="kw4">void</span> setCurrentFunction<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> currentFunction<span class="br0">)</span> <span class="br0">{</span>
<span class="kw1">this</span>.<span class="me1">currentFunction</span> <span class="sy0">=</span> currentFunction<span class="sy0">;</span>
<span class="br0">}</span>
 
<span class="kw1">public</span> <span class="kw4">void</span> setSkipOutHover<span class="br0">(</span><span class="kw4">boolean</span> skipOutHover<span class="br0">)</span> <span class="br0">{</span>
<span class="kw1">this</span>.<span class="me1">skipOutHover</span> <span class="sy0">=</span> skipOutHover<span class="sy0">;</span>
<span class="br0">}</span>
 
<span class="kw1">public</span> <span class="kw4">boolean</span> isSkipOutHover<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
<span class="kw1">return</span> skipOutHover<span class="sy0">;</span>
<span class="br0">}</span>
 
<span class="kw4">void</span> bigger<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
<span class="kw1">if</span> <span class="br0">(</span><span class="sy0">!</span>isBigger<span class="br0">)</span> <span class="br0">{</span>
spatial.<span class="me1">setLocalScale</span><span class="br0">(</span>bigScale<span class="br0">)</span><span class="sy0">;</span>
isBigger <span class="sy0">=</span> <span class="kw2">true</span><span class="sy0">;</span>
<span class="br0">}</span>
<span class="br0">}</span>
 
<span class="kw4">void</span> peak<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
<span class="kw1">if</span> <span class="br0">(</span><span class="sy0">!</span>isPeak<span class="br0">)</span> <span class="br0">{</span>
orginalPos <span class="sy0">=</span> spatial.<span class="me1">getLocalTranslation</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">clone</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
peakPos <span class="sy0">=</span> orginalPos.<span class="me1">add</span><span class="br0">(</span><span class="kw1">new</span> Vector3f<span class="br0">(</span>0f, 0.2f, 0.2f<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
spatial.<span class="me1">setLocalTranslation</span><span class="br0">(</span>peakPos<span class="br0">)</span><span class="sy0">;</span>
isPeak <span class="sy0">=</span> <span class="kw2">true</span><span class="sy0">;</span>
<span class="br0">}</span>
<span class="br0">}</span>
 
<span class="kw4">void</span> noPeak<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
<span class="kw1">if</span> <span class="br0">(</span>isPeak<span class="br0">)</span> <span class="br0">{</span>
spatial.<span class="me1">setLocalTranslation</span><span class="br0">(</span>orginalPos.<span class="me1">clone</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
isPeak <span class="sy0">=</span> <span class="kw2">false</span><span class="sy0">;</span>
<span class="br0">}</span>
<span class="br0">}</span>
 
<span class="kw4">void</span> smaller<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
<span class="kw1">if</span> <span class="br0">(</span>isBigger<span class="br0">)</span> <span class="br0">{</span>
spatial.<span class="me1">setLocalScale</span><span class="br0">(</span>orginalScale<span class="br0">)</span><span class="sy0">;</span>
isBigger <span class="sy0">=</span> <span class="kw2">false</span><span class="sy0">;</span>
<span class="br0">}</span>
<span class="br0">}</span>
 
<span class="kw4">void</span> highlight<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
<span class="kw1">if</span> <span class="br0">(</span><span class="sy0">!</span>isHighlight<span class="br0">)</span> <span class="br0">{</span>
<span class="br0">(</span><span class="br0">(</span>Geometry<span class="br0">)</span> spatial<span class="br0">)</span>.<span class="me1">getMaterial</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">setBoolean</span><span class="br0">(</span>“MixGlow”, <span class="kw2">true</span><span class="br0">)</span><span class="sy0">;</span>
isHighlight <span class="sy0">=</span> <span class="kw2">true</span><span class="sy0">;</span>
<span class="br0">}</span>
<span class="br0">}</span>
 
<span class="kw4">void</span> noHighlight<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
<span class="kw1">if</span> <span class="br0">(</span>isHighlight<span class="br0">)</span> <span class="br0">{</span>
<span class="br0">(</span><span class="br0">(</span>Geometry<span class="br0">)</span> spatial<span class="br0">)</span>.<span class="me1">getMaterial</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">setBoolean</span><span class="br0">(</span>“MixGlow”, <span class="kw2">false</span><span class="br0">)</span><span class="sy0">;</span>
isHighlight <span class="sy0">=</span> <span class="kw2">false</span><span class="sy0">;</span>
<span class="br0">}</span>
<span class="br0">}</span>
<span class="br0">}</span></pre>

</div>

<h4 id="cached_conditions_rules">Cached conditions – Rules:</h4>
<div class="level4">

<p>
We use a Groovy Map cardSelectRules to save all rule in form of Closure that determine if a Card is selected or not. More about rules in the scripting part <a href="/jme3/atomixtuts/cardsgame/scripting.html" class="wikilink1" title="jme3:atomixtuts:cardsgame:scripting">scripting</a>
</p>

<p>
…part of CardGamePlay.groovy
</p>
<pre class="code java"><span class="kw1">public</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+map"><span class="kw3">Map</span></a> cardSelectRules<span class="sy0">=</span><span class="br0">[</span><span class="sy0">:</span><span class="br0">]</span><span class="sy0">;</span>
<span class="kw4">void</span> createSelectConditions<span class="br0">(</span><span class="br0">)</span><span class="br0">{</span>
<span class="co1">// RULE : The card is in hand</span>
def inHandRule <span class="sy0">=</span><span class="br0">{</span>card<span class="sy0">-&gt;</span>
 
CardPlayer player <span class="sy0">=</span> whichPlayerCard<span class="br0">(</span>card<span class="br0">)</span>
<span class="kw1">if</span> <span class="br0">(</span>player.<span class="me1">getHand</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">contains</span><span class="br0">(</span>card<span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
<span class="kw1">return</span> <span class="kw2">true</span><span class="sy0">;</span>
<span class="br0">}</span>
<span class="kw1">return</span> <span class="kw2">false</span><span class="sy0">;</span>
<span class="br0">}</span>
cardSelectRules<span class="br0">[</span><span class="st0">"inHand"</span><span class="br0">]</span> <span class="sy0">=</span><span class="kw1">new</span> ClosureSelectCondition<span class="br0">(</span>inHandRule<span class="br0">)</span><span class="sy0">;</span>
 
<span class="co1">// RULE : The card is in hand of the current player – who play this device!</span>
def inHandCurrentRule <span class="sy0">=</span><span class="br0">{</span>card<span class="sy0">-&gt;</span>
<span class="kw1">if</span> <span class="br0">(</span>isCurrentPlayer<span class="br0">(</span>whichPlayerCard<span class="br0">(</span>card<span class="br0">)</span><span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
CardPlayer player <span class="sy0">=</span> getCurrentPlayer<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
<span class="kw1">if</span> <span class="br0">(</span>player.<span class="me1">getHand</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">contains</span><span class="br0">(</span>card<span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
<span class="kw1">return</span> <span class="kw2">true</span><span class="sy0">;</span>
<span class="br0">}</span>
<span class="br0">}</span>
<span class="kw1">return</span> <span class="kw2">false</span><span class="sy0">;</span>
<span class="br0">}</span>
cardSelectRules<span class="br0">[</span><span class="st0">"inHandCurrent"</span><span class="br0">]</span> <span class="sy0">=</span><span class="kw1">new</span> ClosureSelectCondition<span class="br0">(</span>inHandCurrentRule<span class="br0">)</span><span class="sy0">;</span>
 
<span class="co1">// RULE : The card is in hand of the current turn player – who has this turn!</span>
def inHandTurnRule <span class="sy0">=</span><span class="br0">{</span>card<span class="sy0">-&gt;</span>
<span class="kw1">if</span> <span class="br0">(</span>isCurrentPlayer<span class="br0">(</span>whichPlayerCard<span class="br0">(</span>card<span class="br0">)</span><span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
CardPlayer player <span class="sy0">=</span> getCurrentPlayer<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
<span class="kw1">if</span> <span class="br0">(</span>player.<span class="me1">getHand</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">contains</span><span class="br0">(</span>card<span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
<span class="kw1">return</span> <span class="kw2">true</span><span class="sy0">;</span>
<span class="br0">}</span>
<span class="br0">}</span>
<span class="kw1">return</span> <span class="kw2">false</span><span class="sy0">;</span>
<span class="br0">}</span>
cardSelectRules<span class="br0">[</span><span class="st0">"inHandTurn"</span><span class="br0">]</span> <span class="sy0">=</span><span class="kw1">new</span> ClosureSelectCondition<span class="br0">(</span>inHandTurnRule<span class="br0">)</span><span class="sy0">;</span>
<span class="co1">// RULE: The card is in ground</span>
def inGroundRule <span class="sy0">=</span><span class="br0">{</span>card<span class="sy0">-&gt;</span>
 
CardPlayer player <span class="sy0">=</span> whichPlayerCard<span class="br0">(</span>card<span class="br0">)</span><span class="sy0">;</span>
<span class="kw1">if</span> <span class="br0">(</span>player.<span class="me1">ground</span>.<span class="me1">contains</span><span class="br0">(</span>card<span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
<span class="kw1">return</span> <span class="kw2">true</span><span class="sy0">;</span>
<span class="br0">}</span>
<span class="kw1">return</span> <span class="kw2">false</span><span class="sy0">;</span>
<span class="br0">}</span>
cardSelectRules<span class="br0">[</span><span class="st0">"inGround"</span><span class="br0">]</span> <span class="sy0">=</span><span class="kw1">new</span> ClosureSelectCondition<span class="br0">(</span>inGroundRule<span class="br0">)</span><span class="sy0">;</span>
<span class="co1">// RULE: Card in player Main phase</span>
def mainPhaseCards <span class="sy0">=</span> <span class="br0">{</span>card<span class="sy0">-&gt;</span>
<span class="kw1">if</span> <span class="br0">(</span>isCurrentPlayer<span class="br0">(</span>whichPlayerCard<span class="br0">(</span>card<span class="br0">)</span><span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
CardPlayer player <span class="sy0">=</span> getCurrentPlayer<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
<span class="kw1">if</span> <span class="br0">(</span>player.<span class="me1">hand</span>.<span class="me1">contains</span><span class="br0">(</span>card<span class="br0">)</span><span class="sy0">||</span>player.<span class="me1">ground</span>.<span class="me1">contains</span><span class="br0">(</span>card<span class="br0">)</span><span class="sy0">||</span>player.<span class="me1">magic</span>.<span class="me1">contains</span><span class="br0">(</span>card<span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
<span class="co1">//println(“Condition true”);</span>
<span class="kw1">return</span> <span class="kw2">true</span><span class="sy0">;</span>
<span class="br0">}</span>
<span class="br0">}</span>
<span class="kw1">return</span> <span class="kw2">false</span><span class="sy0">;</span>
<span class="br0">}</span>
cardSelectRules<span class="br0">[</span><span class="st0">"mainPhaseCards"</span><span class="br0">]</span> <span class="sy0">=</span><span class="kw1">new</span> ClosureSelectCondition<span class="br0">(</span>mainPhaseCards<span class="br0">)</span><span class="sy0">;</span>
<span class="co1">// RULE: Can not select any thing</span>
def noneSelect <span class="sy0">=</span> <span class="br0">{</span>card<span class="sy0">-&gt;</span>
<span class="kw1">return</span> <span class="kw2">false</span><span class="sy0">;</span>
<span class="br0">}</span>
cardSelectRules<span class="br0">[</span><span class="st0">"noneSelect"</span><span class="br0">]</span> <span class="sy0">=</span><span class="kw1">new</span> ClosureSelectCondition<span class="br0">(</span>noneSelect<span class="br0">)</span><span class="sy0">;</span>
 
<span class="br0">}</span></pre>

</div>
<!-- EDIT7 SECTION "Select" [21946-27999] -->
<h3 class="sectionedit8" id="states">States</h3>
<div class="level3">

</div>

<h4 id="mainmenustate">MainMenuState</h4>
<div class="level4">

</div>

<h4 id="ingamestate">InGameState</h4>
<div class="level4">

</div>

<h4 id="loadingstate">LoadingState</h4>
<div class="level4">

</div>
<!-- EDIT8 SECTION "States" [28000-28074] -->
<h3 class="sectionedit9" id="managers">Managers</h3>
<div class="level3">

</div>
<!-- EDIT9 SECTION "Managers" [28075-28092] -->
<h3 class="sectionedit10" id="controls">Controls</h3>
<div class="level3">

</div>
<!-- EDIT10 SECTION "Controls" [28093-28110] -->
<h3 class="sectionedit11" id="cardlibrary">CardLibrary</h3>
<div class="level3">

</div>
<!-- EDIT11 SECTION "CardLibrary" [28111-] -->
