---
title: Soccer AI
---
<h2 class="sectionedit1" id="soccer_ai">Soccer AI</h2>
<div class="level2">

<p>
</p><p></p><div class="notewarning">This is a very loooong story… 
</div>
Sport and Physical, Human AI are very active parts of AI nowaday. It involve a lot of subjects… That's why is also quite hard to bring into game.


<p>
Two category:
</p>
<ol>
<li class="level1"><div class="li"> Invidual AI:</div>
<ol>
<li class="level2"><div class="li"> Human as Agent in a Team in a sport Game.</div>
</li>
<li class="level2"><div class="li"> Human behaviour in a sport Game.</div>
<ol>
<li class="level3"><div class="li"> Movement behaviour</div>
</li>
<li class="level3"><div class="li"> Brain</div>
</li>
<li class="level3"><div class="li"> Physical (tesion, …) </div>
</li>
<li class="level3"><div class="li"> Balance and locomotion</div>
</li>
</ol>
</li>
</ol>
</li>
<li class="level1"><div class="li"> Group AI:</div>
<ol>
<li class="level2"><div class="li"> Stragegy </div>
</li>
<li class="level2"><div class="li"> Plan (Goal , situation base..)</div>
</li>
<li class="level2"><div class="li"> Some thing else…</div>
</li>
</ol>
</li>
</ol>

</div>

<h4 id="initial_approach">Initial approach</h4>
<div class="level4">

<p>
As for EuroKick, my <strong>initial approach</strong> is the most basic form:
</p>
<ol>
<li class="level1"><div class="li"> State machine for invidual AI</div>
</li>
<li class="level1"><div class="li"> Hard code decision tree and some support techniques for group AI</div>
</li>
</ol>

<p>
For futher reading about this naive approach, almost adapt from the SportAI chapter of the famous “Programming Game AI by example” book, you can find it here: <a href="http://www.ai-junkie.com/books/toc_pgaibe.html" class="urlextern" title="http://www.ai-junkie.com/books/toc_pgaibe.html" rel="nofollow">http://www.ai-junkie.com/books/toc_pgaibe.html</a>
</p>

<p>
The book come with C++ source code, and fortunately someone port it to Java: <a href="http://www.sallyx.org/sally/en/game-ai/" class="urlextern" title="http://www.sallyx.org/sally/en/game-ai/" rel="nofollow">http://www.sallyx.org/sally/en/game-ai/</a> , of source I use the source code but I port it to Groovy and change a lot in the structure to fit with out JME3 architecture, 3D, animations…etc Why Groovy? For operation overiding, scripting and such…
</p>

<p>
For this approach, the invidual AI represent as a moving point and some simplest action, it normally is quite enough for a management game (and also for the tutorial) but for a football controlling game like ProEvolution soccer or Fifa it's lack a lot of supports.
</p>

</div>

<h4 id="next-gen_approaches">Next-gen approaches</h4>
<div class="level4">

<p>
In my second attempt recently, I'd like to improve both invidual level and group level envolve fuzzy, emotional, goalbase and training. 
</p>

<p>
Also in the process of making AtomAI, envolving more advance AI techniques like AI programming language and some “new born” - “academic” like POSH, Pogamut … <a href="/doku.php/jme3:advanced:atom_framework:atomai" class="wikilink2" title="jme3:advanced:atom_framework:atomai" rel="nofollow">Read AtomAI</a>, I want to make a push to this project by envolving this “new born” techs.
</p>

<p>
Football player in the field can consider a physical-emotional creature know how to:
</p>
<ol>
<li class="level1"><div class="li"> move (run,jump,balance..) </div>
</li>
<li class="level1"><div class="li"> play with the ball masterfully (kick, lead, pass..) </div>
</li>
<li class="level1"><div class="li"> have own personalities and charateristic.. </div>
</li>
</ol>

<p>
compare to a single steering point (in the old approach)!
</p>

<p>
The players and all other characters:
 - interact, comunicate with teammates, refree, activities on the field
 - have overal stragegy, tactic, formation which can be change on the fly, train via training course .. etc..
</p>

<p>
Other than that, football players, coachs - they have nagotiation skills and can chat! If you watch Soccer Manager game evolutions closely, you can find the charater get smarter and smarter every year when they negotiate about the transactions, rercuitment … They have memories, can also express their ideas, emotions, and words …
</p>

<p>
That make the game much more challanging, interesting and enjoyable! Of course the underlying techs change and enable a whole new level of intelligent game agents, the same we want to see in our game!
</p>

<p>
But for a game development process, at some point you have to decide how much efforts are considered enough for your game and stop there! It's a game anyway, not a freaking science simmulation. Let's named what we have:
</p>

</div>

<h4 id="physical_-_emotional_human_ai">Physical - Emotional Human AI</h4>
<div class="level4">

<p>
This mainly required by Match gameplay.
Human brain and emotions is very difficult to simmulate. These are what AtomAI brings:
</p>
<ol>
<li class="level1"><div class="li"> Emotions ( fuzzy, memories, ..)</div>
</li>
<li class="level1"><div class="li"> Physical ( balance, physic aware, IK..)</div>
</li>
<li class="level1"><div class="li"> Talkative agent ( chatbot, memories, nature language processing …)</div>
</li>
<li class="level1"><div class="li"> Learnable - Trainable ( machine learning, skill improving with althelist simmulation models …)</div>
</li>
</ol>

</div>

<h4 id="group_ai">Group AI</h4>
<div class="level4">

<p>
This mainly required by Coaching gameplay.
A group of invidual agents obey, rely on some global/overal stragegy or direction, in which forming a coach in real life.
</p>

<p>
Of course coaching appreared as in-match and our-match plans. Which we will consider to simmulate in different ways in our design.
</p>

</div>

<h4 id="data">Data</h4>
<div class="level4">

<p>
The data for this game can be huge to make some techniques work well:
</p>
<ol>
<li class="level1"><div class="li"> Datas of gameplay: Football players and clubs infomations (attributes, tranactions, trainings, 3d models, characteristics …) to use in gameplay, simmulate economic models.. <a href="/doku.php/jme3:atomixtuts:kickgame:data" class="wikilink2" title="jme3:atomixtuts:kickgame:data" rel="nofollow">Read more in Data section</a></div>
</li>
<li class="level1"><div class="li"> Datas for AI: human physical-emotions simmulation, language recoginizing, processing, training materials…</div>
</li>
</ol>

<p>
I still want to sketch a framework and open it for community driven like other opensource: Then the required data can be procedured in network, webs of computers and devs…That's my point!
</p>

</div>
