---
title: 
---
<p>
This page is to make your own multiplayer game, mainly by using a template and understanding how it works.
</p>

<p>
The template for a multiplayer project can be found here:
<a href="http://hub.jmonkeyengine.org/forum/topic/multiplayer-game-template/" class="urlextern" title="http://hub.jmonkeyengine.org/forum/topic/multiplayer-game-template/" rel="nofollow">http://hub.jmonkeyengine.org/forum/topic/multiplayer-game-template/</a>
</p>

<p>
Additional information e.g. links to jars can be found here:
<a href="http://hub.jmonkeyengine.org/forum/topic/need-help-need-jar-files-for-a-project/#post-292081" class="urlextern" title="http://hub.jmonkeyengine.org/forum/topic/need-help-need-jar-files-for-a-project/#post-292081" rel="nofollow">http://hub.jmonkeyengine.org/forum/topic/need-help-need-jar-files-for-a-project/#post-292081</a>
</p>

<p>
Class diagram (template only):
<a href="http://puu.sh/a4azI/8c37cd8cf4.png" class="urlextern" title="http://puu.sh/a4azI/8c37cd8cf4.png" rel="nofollow">http://puu.sh/a4azI/8c37cd8cf4.png</a>
</p>

<p>
A lot of work has to be done, but the best thing to start with, is summing up the classes, with  the variables and explaining what the use is of those.
</p>

<p>
Classes (by package):
</p>

<p>
NetworkRpg:
</p>
<ol>
<li class="level1"><div class="li"> GameClient (Interface)</div>
</li>
<li class="level1"><div class="li"> GameConstants</div>
</li>
<li class="level1"><div class="li"> GameGuiController</div>
</li>
<li class="level1"><div class="li"> Main</div>
</li>
</ol>
<pre class="code">  private AppSettings settings;  sets the resolution
  private boolean isFullScreen = false;  obvious: fullscreen</pre>
<ol>
<li class="level1"><div class="li"> MenuInputMapping (No variables)</div>
</li>
<li class="level1"><div class="li"> RemoteGameClient</div>
</li>
<li class="level1"><div class="li"> ServerMain</div>
</li>
<li class="level1"><div class="li"> ThirdPersonCamera</div>
</li>
<li class="level1"><div class="li"> TimeProvider (Interface)</div>
</li>
</ol>

<p>
NetworkRpg.AppStates:
</p>
<ol>
<li class="level1"><div class="li"> BaseAppState</div>
</li>
<li class="level1"><div class="li"> ConnectionState</div>
</li>
<li class="level1"><div class="li"> EntityDataState</div>
</li>
<li class="level1"><div class="li"> ErrorState</div>
</li>
<li class="level1"><div class="li"> GamePlayState</div>
</li>
<li class="level1"><div class="li"> MainMenuState</div>
</li>
<li class="level1"><div class="li"> ModelState</div>
</li>
<li class="level1"><div class="li"> WorldState</div>
</li>
</ol>

<p>
NetworkRpg.Components:
</p>
<ol>
<li class="level1"><div class="li"> ModelType</div>
</li>
<li class="level1"><div class="li"> Position</div>
</li>
<li class="level1"><div class="li"> walkDirection (No variables)</div>
</li>
</ol>

<p>
NetworkRpg.Factories:
</p>
<ol>
<li class="level1"><div class="li"> EntityFactories</div>
</li>
<li class="level1"><div class="li"> GameModelFactory</div>
</li>
<li class="level1"><div class="li"> ModelFactory</div>
</li>
</ol>

<p>
NetworkRpgt.Handlers:
</p>
<ol>
<li class="level1"><div class="li"> GameMessageHandler</div>
</li>
</ol>

<p>
NetworkRpg.Networking:
</p>
<ol>
<li class="level1"><div class="li"> Util</div>
</li>
</ol>
<pre class="code">  public static final int tcpPort = 1337;   portnumber used for tcp connections
  public static final int udpPort = 1337;   portnumber used for udp connections (http://www.diffen.com/difference/TCP_vs_UDP)
  public static final String GAME_NAME ="Network RPG"; name of the game
  public static final int PROTOCOL_VERSION = 1; version of the udp/tcp protocol being used</pre>

<p>
NetworkRpg.Networking.Msg:
</p>
<ol>
<li class="level1"><div class="li"> ChatMessage</div>
</li>
<li class="level1"><div class="li"> CommandSet</div>
</li>
<li class="level1"><div class="li"> GameTimeMessage</div>
</li>
<li class="level1"><div class="li"> PlayerInfoMessage</div>
</li>
<li class="level1"><div class="li"> ViewDirection</div>
</li>
</ol>

<p>
NetworkRpg.Objects:
</p>
<ol>
<li class="level1"><div class="li"> Avatar</div>
</li>
</ol>
<pre class="code">  public Spatial avatarSpatial;      holds information about the character
  private Node avatarNode;     a node which contains the modelnode  
  private Node model;          a node which contains your character (the green thing on the map)    
  public BetterCharacterControl avatarControl;  this is used to set the gravity
  private SimpleApplication App;  we need this to get the rootnode
  private BulletAppState bulletAppState; allows using bullet physics in an Application. 
  private Node rootNode;   the node which gets all the nodes (add to this one, and it'll be visible)
  private AnimChannel animChannel; used to change the current anitmation
  private AnimControl animControl;   this is needed to create an animchannel
  private BitmapText label;     label where we add a the textnode to
  private Node textNode;           name above the head of the player
  private String idleAnim = "IdleBase";   name of the animation (not 100% sure)
  private String walkAnim = "RunBase";
  private String attackAnim = "SliceHorizontal";
  private String jumpAnim = "JumpLoop"; 
  private BitmapFont guiFont;    the font
  private String playerName;     name above the avatar</pre>

<p>
NetworkRpg.Services:
</p>
<ol>
<li class="level1"><div class="li"> EntityDataService</div>
</li>
<li class="level1"><div class="li"> GameSystems</div>
</li>
<li class="level1"><div class="li"> MovementService</div>
</li>
<li class="level1"><div class="li"> Service (Interface)</div>
</li>
</ol>

<p>
This is a total of 35 classes.
</p>
