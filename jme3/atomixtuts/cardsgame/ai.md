---
title: CardsGame: AI
---
<h2 class="sectionedit1" id="cardsgameai">CardsGame: AI</h2>
<div class="level2">

<p>
Now back to the basic, in a general card game, gameplay consist of fews ideas:
</p>
<ol>
<li class="level1"><div class="li"> Which card to choose</div>
</li>
<li class="level1"><div class="li"> Which state of that card to choose</div>
</li>
</ol>

<p>
In a magic card game, two opponents including AI should concern a few more and how to answer these question to defeat the other:
</p>
<ul>
<li class="level1"><div class="li"> Which magic card support/destroy which card</div>
</li>
<li class="level1"><div class="li"> How to get Best health point and best damage</div>
</li>
</ul>

</div>
<!-- EDIT1 SECTION "CardsGame: AI" [1-394] -->
<h2 class="sectionedit2" id="a_tattic_and_stragegies">A – Tattic and stragegies</h2>
<div class="level2">

<p>
Now I kind of don’t want to write much about AI in the first tutorial but let’s go, it wont take too long.
</p>

<p>
In this game, the AI should have appropriate stragegies from Phase to Phase, even though, we should have a global stragegy for each round. Here are “naive” stragegies of the magic card AI:
</p>

</div>
<!-- EDIT2 SECTION "A – Tattic and stragegies" [395-738] -->
<h3 class="sectionedit3" id="summon_cards_main_phase_1_2">Summon Cards (Main phase 1&amp;2):</h3>
<div class="level3">

<p>
In the MainPhase, if you can summon, that mean there is card for you to have a valid summon. Wisely choose one option:
</p>

</div>

<h4 id="stragegy_1_choose_the_biggest_attack_defend_card">- STRAGEGY 1) Choose the biggest attack/defend card.</h4>
<div class="level4">

<p>
When you don’t have enough appropriate tribute cards to summon a “many stars” Card
</p>
<ol>
<li class="level1"><div class="li"> Just summon the biggest attack\defend card you have.</div>
</li>
<li class="level1"><div class="li"> To decide to summon (attack||defend), check what cards are in the field at the moment and compare your cards to your opponent cards, if the result is :</div>
<ol>
<li class="level2"><div class="li"> “GoodToAttack” – choose Biggest Attack – Attack State</div>
</li>
<li class="level2"><div class="li"> “ShouldDefend” – choose Biggest Defend – Defend state</div>
</li>
</ol>
</li>
<li class="level1"><div class="li"> summon it, and to the next Phase</div>
</li>
</ol>

</div>

<h4 id="stragegy_2_choose_fews_smallest_card_to_tribute_and_summon_a_biggest_one">- STRAGEGY 2) Choose fews smallest card to tribute and summon a biggest one.</h4>
<div class="level4">

<p>
When you HAVE enough appropriate tribute cards to summon a “many stars” Card (always with big attack/defend points and have effects)
</p>
<ol>
<li class="level1"><div class="li"> Choose the “biggest” and “most many stars” card.</div>
</li>
<li class="level1"><div class="li"> Choose the “smallest” cards enough to tribute to summon this card.</div>
<ol>
<li class="level2"><div class="li"> If you can not even summon anything, have to Pass (by the rule).</div>
</li>
</ol>
</li>
<li class="level1"><div class="li"> Futher, if there is no card in your ground mark the Brain with “Dangerous situation” and Pass.</div>
</li>
</ol>

<p>
——
</p>

</div>
<!-- EDIT3 SECTION "Summon Cards (Main phase 1&2):" [739-1969] -->
<h3 class="sectionedit4" id="use_support_cards_every_action_phases">Use support Cards (every action phases):</h3>
<div class="level3">

<p>
In every action phase, except for DrawPhase and Endphase, you can use support card like MagicCard, TrapCard…etc. We can design a function to evaluate thoose card by how good is going to be when called in the game, but for the time being, we use such simplest tragagy:
</p>
<hr />

</div>

<h4 id="stragegy_3_use_all_the_support_cards_in_one_turn">STRAGEGY 3) Use all the support cards in one turn</h4>
<div class="level4">

<p>
That mean you are very hungry for the final win. It’s not always intelligent to do so in the POV of a professional duelist but hey… Ok. Now we want to pull all out support cards in one turn.
</p>
<hr />

</div>

<h4 id="stragegy_4_category_cards_in_the_game">STRAGEGY 4) Category cards in the game</h4>
<div class="level4">

<p>
You should devide the support card and its effect to type and handle it by type, that’s the naive way but appropriate for DecisionTree technique we used here.
</p>
<hr />

<p>
Q&amp;A
</p>
<ol>
<li class="level1"><div class="li"> Q: How many type of support card are there?</div>
</li>
<li class="level1"><div class="li"> A: Trap card can flip whenever opponent take action like summon or attack. Magic card can do almost every effect from increase healpoint to destroy everything, change the field</div>
</li>
</ol>
<ol>
<li class="level1"><div class="li"> Q: How many type this naive AI know how to use?</div>
</li>
<li class="level1"><div class="li"> A: Many type of support card and effect are there in the real game but the AI use a “DecisionTree” technique just use a few which you know exactly what it do. For more complicated intelligent, we have to use complicated AI model like Neutral network or Genetic Algorimth..:</div>
</li>
</ol>
<ul>
<li class="level1"><div class="li"> o) Support Point Card: Card that increase/decrease the demon cards point.</div>
</li>
<li class="level1"><div class="li"> o) Heal Card: Card that increase/decrease the opponents point directly.</div>
</li>
<li class="level1"><div class="li"> o) Special Summon Card: Card that can bring demon card to the field in special way.</div>
</li>
<li class="level1"><div class="li"> o) Destroy/Clean Card: Card that destroy demons or other support card</div>
</li>
<li class="level1"><div class="li"> o) State Constraint Card: Card that lock or unlock the Limit of the game, like noActtack, noDefend..</div>
</li>
</ul>

<p>
——
</p>

</div>

<h4 id="stragegy_5_bigger_biggest_smallest_smaller">STRAGEGY 5) Bigger biggest – Smallest smaller</h4>
<div class="level4">

<p>
- Q: Which Support Point Card support to which demon?
</p>

<p>
- A: You want to combine a biggest possible Card. So all biggest support card to the biggest demon. In oposite, you want to decrease all the demon of opponent on the field to the point that you can destroy it by attack or can not attack you anymore. So you just try to find the way to decrease those attack point to
</p>
<ul>
<li class="level1"><div class="li"> o) the smallest defend point of your defend demon if you have any defend demon</div>
</li>
<li class="level1"><div class="li"> o) or smallest attack point if you only have attack demon</div>
</li>
<li class="level1"><div class="li"> o) or 0 if you have no demon</div>
</li>
</ul>

<p>
We can have sotisphicated way to distribute thoose support point but just do it as simple as possible.
</p>
<hr />

</div>
<!-- EDIT4 SECTION "Use support Cards (every action phases):" [1970-4476] -->
<h3 class="sectionedit5" id="decide_what_to_do">Decide what to do:</h3>
<div class="level3">

</div>

<h4 id="stragegy_6_attack_who_and_how_decide_to_attack_or_defend">STRAGEGY 6) Attack who and how? Decide to attack or defend</h4>
<div class="level4">

<p>
Image you have a few demons in the field to attack your opponent.
</p>

</div>

<h5 id="step1_first_glance_calculation">Step1, first glance calculation:</h5>
<div class="level5">

<p>
There is 3 situation here:
</p>
<ol>
<li class="level1"><div class="li"> All your demon are better than your opponent’s current avaiable cards, so you will not lose any health point in the next turn, even if your opponent attack back. It’s called Dominance in game theory   </div>
</li>
<li class="level1"><div class="li"> In our game, this situation call “GoodToAttack”</div>
</li>
<li class="level1"><div class="li"> You have a few better and a few worse, you want to attack. – This situation call “Average” and need futher calulation.</div>
</li>
<li class="level1"><div class="li"> You can not attack at all, or lost points. So you should switch to defend. – This situation call “ShouldDefend”. (Not to mention: Affaid of trap card will flip when you take action?)</div>
</li>
<li class="level1"><div class="li"> In fact, 3 above situations can be calculated by dertemine “forecast” result health point of two opponents.</div>
</li>
</ol>

</div>

<h5 id="step2_further_calculation">Step2, further calculation:</h5>
<div class="level5">

<p>
Apply the attack of all your the demons to each of your opponent demons and calculate the result points of both, call it a case. Best case is you win directly, less good case is you cause damage a lot, worse case, you should not attack cause you lose or lost points, it’s a bad idea.
</p>

</div>

<h5 id="step3_apply">Step3, Apply:</h5>
<div class="level5">

<p>
After finish calculation, you apply the whole case in the current turn.
</p>
<hr />

</div>

<h4 id="stragegy_7_dangerous_prevent_attack_goodtoattack_prevent_deffend">STRAGEGY 7) Dangerous – Prevent attack | GoodToAttack – Prevent deffend</h4>
<div class="level4">

<p>
The state constraints are very powerful stragegy when you can use it.
If you in Dangerous situation, which your AI brain mark. You can prevent your opponent not to attack in a few rounds or forever. In opposite, you can prevent your opponent to take defend by the opposite constraint.
If you only have the magic card to constraint one card, use it with the biggest or smallest card possible so your benifit is maximum!
</p>

<p>
The usage of Heal Card ,Destroy/Clean Card,Special Summon are trivial and pretty obvious by combining the previous stragegy so I ommited this part! :p
</p>
<hr />

</div>
<!-- EDIT5 SECTION "Decide what to do:" [4477-6484] -->
<h2 class="sectionedit6" id="b-ai_techs">B-AI Techs</h2>
<div class="level2">

<p>
As the result of making a sotiphicated AI, AI common techniques are used in mixed form, specific with the native of languages and tied to the game or the game engine. 
</p>

<p>
But it's a good idea to clarify some parts of them to help you see the design more clearly and recoginize the pattern for your futher developing.
</p>

<p>
It's also worth to mention some patterns that already used in JME3 here and there: like State pattern, .
</p>

</div>
<!-- EDIT6 SECTION "B-AI Techs" [6485-6927] -->
<h3 class="sectionedit7" id="decision_behavior_tree">Decision/Behavior Tree</h3>
<div class="level3">

<p>
Decision/Behavior Tree
</p>

<p>
From wikipedia 
</p>

<p>
In this game, Decision/Behavior Tree is not metioned as a implementation of Data base Decision/Behavior Tree like common in AI playground, but a structure to define actions and behaviours, that's a tree. Whatever your tree building techniques is, the Tree than decide very separation situations in a nested form.
</p>

<p>
That's why Decision Tree is pretty straight forward for almost programming language (via built in branching controls, such as : switch or if/else ).
</p>

<p>
In this game, Decision Tree help in organize situations in each phases.
</p>

</div>
<!-- EDIT7 SECTION "Decision/Behavior Tree" [6928-7536] -->
<h3 class="sectionedit8" id="finite_state_machine">Finite State Machine</h3>
<div class="level3">

<p>
In this game, Finite State Machine help to implement simple Card Character AI.
</p>

</div>
<!-- EDIT8 SECTION "Finite State Machine" [7537-7645] -->
<h3 class="sectionedit9" id="minimax">MiniMax</h3>
<div class="level3">

<p>
In the previous section, we talked about “Forecast what will happen in a few next rounds”, if you know the result, you can definitely choose a most appropriate path. There is a related problem in the field of AI Tactic, called Minimax. The basic idea of minimax is .
</p>

<p>
From wikipedia 
</p>

<p>
In this game, MiniMaxing is a little bit different from what you see in a normal Board/Chess game for example. MiniMaxing here help to evaluate the DesisionTree in a short term (mean short in time and light in processing space..)
</p>

</div>
<!-- EDIT9 SECTION "MiniMax" [7646-8183] -->
<h3 class="sectionedit10" id="fuzzylogic">FuzzyLogic</h3>
<div class="level3">

<p>
FuzzyLogic  is 
</p>

<p>
<a href="http://en.wikipedia.org/wiki/Fuzzy_logic" class="urlextern" title="http://en.wikipedia.org/wiki/Fuzzy_logic" rel="nofollow">http://en.wikipedia.org/wiki/Fuzzy_logic</a>
</p>

<p>
In this game, FuzzyLogic is applied to extract the features and the situation from the game state and help decide what situation its it. Its upper layer is Case base (formed by more exact , accurate AI situation model)
</p>

</div>
<!-- EDIT10 SECTION "FuzzyLogic" [8184-8484] -->
<h3 class="sectionedit11" id="casebase">CaseBase</h3>
<div class="level3">

</div>
<!-- EDIT11 SECTION "CaseBase" [8485-8503] -->
<h2 class="sectionedit12" id="c-atomai_usages">C-AtomAI usages</h2>
<div class="level2">

</div>
<!-- EDIT12 SECTION "C-AtomAI usages" [8504-8531] -->
<h2 class="sectionedit13" id="d-implementation">D-Implementation</h2>
<div class="level2">

<p>
In above sections, we already declare a few rules which can have us to filter out which card are in hand, which card are in grave, ground, magic… etc. Later we will use them as ultilites in the AI.
</p>

<p>
The first try to implement the AI
</p>
<pre class="code java"><span class="kw1">package</span> <span class="co2">magiccard.gameplay.ai</span>
 
<span class="kw1">import</span> <span class="co2">magiccard.*</span>
<span class="kw1">import</span> <span class="co2">magiccard.gameplay.*</span>
<span class="kw1">import</span> <span class="co2">static</span> magiccard.<span class="me1">gameplay</span>.<span class="me1">TurnPhase</span>.<span class="me1">TurnPhaseType</span>.<span class="sy0">*</span>
<span class="co3">/**
 * This class is the AI for playing YugiOh Magic Card game.
 * The main technique used is DecisionTree &amp; NeutralNetwork to decide actions
 */</span>
<span class="kw1">public</span> <span class="kw1">class</span> CardPlayerAI <span class="br0">{</span>
    <span class="kw1">enum</span> AILevel <span class="br0">{</span>Starter,Normal,HardCore,Duelist,Best<span class="sy0">;</span>
        <span class="kw4">int</span> deep<span class="sy0">;</span>
    <span class="br0">}</span>
    AILevel level<span class="sy0">;</span>
    CardGamePlay gamePlay<span class="sy0">;</span>
    CardPlayer player<span class="sy0">;</span>
    <span class="kw1">enum</span> StragegySituation <span class="br0">{</span>GoodToAttack,ShouldDefend,Unknown,Dangeous<span class="br0">}</span>
    StragegySituation situation<span class="sy0">=</span> StragegySituation.<span class="me1">Unknown</span><span class="sy0">;</span>
    def memories <span class="sy0">=</span> <span class="br0">[</span><span class="sy0">:</span><span class="br0">]</span>
    <span class="co1">// The list of special card (id) that will have higher priority at any time</span>
    def listOfSpecialCards <span class="sy0">=</span> <span class="br0">[</span><span class="br0">]</span>
 
    <span class="co3">/**
     *AI sepecific params
     **/</span>
    <span class="kw4">int</span> maxTime <span class="sy0">=</span> <span class="nu0">5000</span>
    <span class="kw4">int</span> maxSteps <span class="sy0">=</span> <span class="nu0">500</span>
    <span class="kw4">int</span> maxBranch <span class="sy0">=</span> <span class="nu0">50</span>
    <span class="kw4">int</span> maxGuess <span class="sy0">=</span> <span class="nu0">5</span>
 
    <span class="kw4">int</span> randomness <span class="sy0">=</span> <span class="nu0">30</span>
 
    <span class="co1">// save delayed action</span>
    def actions
    <span class="kw1">public</span> CardPlayerAI<span class="br0">(</span>CardGamePlay gamePlay<span class="br0">)</span><span class="br0">{</span>
        <span class="kw1">this</span>.<span class="me1">gamePlay</span> <span class="sy0">=</span> gamePlay<span class="sy0">;</span>
        <span class="kw1">this</span>.<span class="me1">actions</span> <span class="sy0">=</span> <span class="br0">[</span><span class="br0">]</span>
    <span class="br0">}</span>
 
    <span class="kw1">public</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> toString<span class="br0">(</span><span class="br0">)</span><span class="br0">{</span>
        <span class="kw1">return</span> “AI level <span class="sy0">:</span> “<span class="sy0">+</span><span class="kw1">this</span>.<span class="me1">level</span>.<span class="me1">toString</span><span class="br0">(</span><span class="br0">)</span> <span class="sy0">+</span> ” status <span class="sy0">:</span>” <span class="sy0">+</span> <span class="kw1">this</span>.<span class="me1">situation</span>.<span class="me1">toString</span><span class="br0">(</span><span class="br0">)</span>
    <span class="br0">}</span>
    <span class="kw1">public</span> <span class="kw4">int</span> think<span class="br0">(</span><span class="br0">)</span><span class="br0">{</span>
        <span class="kw4">int</span> startTime <span class="sy0">=</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+system"><span class="kw3">System</span></a>.<span class="me1">currentTimeMillis</span><span class="br0">(</span><span class="br0">)</span>
        <span class="kw1">if</span> <span class="br0">(</span>gamePlay.<span class="me1">currentTurn</span>.<span class="me1">currentPhase</span>.<span class="me1">type</span> <span class="sy0">==</span> MainPhase<span class="br0">)</span><span class="br0">{</span>
            <span class="co1">// try to summon</span>
            <span class="kw1">if</span> <span class="br0">(</span><span class="sy0">!</span>gamePlay.<span class="me1">currentTurn</span>.<span class="me1">currentPhase</span>.<span class="me1">monsterSummoned</span><span class="br0">)</span><span class="br0">{</span>
                def summonableCards <span class="sy0">=</span> player.<span class="me1">hand</span>.<span class="me1">findAll</span><span class="br0">{</span>card<span class="sy0">-&gt;</span> canSummon<span class="br0">(</span>card<span class="br0">)</span><span class="sy0">==</span><span class="kw2">true</span><span class="br0">}</span><span class="sy0">;</span>
                <span class="kw1">if</span> <span class="br0">(</span><span class="sy0">!</span>summonableCards.<span class="me1">isEmpty</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="br0">{</span>
                    def bestCard <span class="sy0">=</span> summonableCards.<span class="me1">max</span><span class="br0">{</span>card<span class="sy0">-&gt;</span> card.<span class="me1">attack</span><span class="br0">}</span>
                    actions<span class="sy0">&lt;</span>
            delayedAct<span class="br0">(</span><span class="br0">)</span>
        <span class="br0">}</span>
 
        actions.<span class="me1">clear</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
    <span class="co1">//self action</span>
 
    <span class="kw4">void</span> summon<span class="br0">(</span>Card card<span class="br0">)</span><span class="br0">{</span>
        gamePlay.<span class="me1">notifyMoveCard</span><span class="br0">(</span>card,”enableHover”<span class="br0">)</span>
        gamePlay.<span class="me1">fromHandToGround</span><span class="br0">(</span>card<span class="br0">)</span><span class="sy0">;</span>
        gamePlay.<span class="me1">currentTurn</span>.<span class="me1">currentPhase</span>.<span class="me1">monsterSummoned</span> <span class="sy0">=</span> <span class="kw2">true</span><span class="sy0">;</span>
    <span class="br0">}</span>
    <span class="co3">/**
     * MINIMAX SUPPORT
     * See the game as the minimum forecastable loss problem and calculate the case
     * In fact, you can use minimax as a base heristic case and then extend
     */</span>
 
    <span class="co3">/**
     * CASE BASE SUPPORT
     * Not for a naive approach anymore.
     * In fact, you can build a heristic case and calculate the result in a few next round to see if the value you gain (win) or lost is sastified
     */</span>
    def tryCase<span class="br0">(</span><span class="kw1">Case</span> aCase<span class="br0">)</span><span class="br0">{</span>
        <span class="kw1">return</span> result<span class="sy0">;</span>
    <span class="br0">}</span>
    def askForSelect<span class="br0">(</span>type,inCardList,info,condition<span class="br0">)</span><span class="br0">{</span>
 
    <span class="br0">}</span>
    <span class="kw1">public</span> <span class="kw1">Case</span> findBestSummonCase<span class="br0">(</span><span class="br0">)</span><span class="br0">{</span>
 
    <span class="br0">}</span>
    <span class="kw1">public</span> <span class="kw1">Case</span> findBestMagicCase<span class="br0">(</span><span class="br0">)</span><span class="br0">{</span>
 
    <span class="br0">}</span>
    <span class="kw1">public</span> <span class="kw1">Case</span> findBestSupportCase<span class="br0">(</span><span class="br0">)</span><span class="br0">{</span>
 
    <span class="br0">}</span>
    <span class="kw1">public</span> <span class="kw1">Case</span> findBestOveralCase<span class="br0">(</span><span class="br0">)</span><span class="br0">{</span><span class="br0">}</span>
 
    <span class="co1">// self evaluation</span>
    <span class="kw1">public</span> <span class="kw4">float</span> evalGoodToAttack<span class="br0">(</span>Card card<span class="br0">)</span><span class="br0">{</span>
 
    <span class="br0">}</span>
    <span class="kw1">public</span> <span class="kw4">float</span> evalGoodToDefend<span class="br0">(</span>Card card<span class="br0">)</span><span class="br0">{</span>
 
    <span class="br0">}</span>
    <span class="coMULTI">/* This function evaluate the value of these two cards when the AI choose to support targetCard with the approriate supportCard*/</span>
    <span class="kw1">public</span> <span class="kw4">float</span> evalGoodToSupport<span class="br0">(</span>Card targetCard,Card supportCard<span class="br0">)</span><span class="br0">{</span>
 
    <span class="br0">}</span>
    <span class="coMULTI">/* This function evaluate the value of this card when they want to keep or discard it by purpose */</span>
    <span class="kw1">public</span> <span class="kw4">float</span> evalGoodOveral<span class="br0">(</span>Card card<span class="br0">)</span><span class="br0">{</span>
 
    <span class="br0">}</span>
    <span class="co1">// Rule</span>
    <span class="kw1">public</span> <span class="kw4">boolean</span> canSummon<span class="br0">(</span>Card aCard<span class="br0">)</span><span class="br0">{</span>
 
        <span class="co1">// enough tribute</span>
        <span class="kw4">int</span> stars <span class="sy0">=</span> aCard.<span class="me1">level</span>.<span class="me1">toInteger</span><span class="br0">(</span><span class="br0">)</span>
        <span class="kw4">boolean</span> enoughStar<span class="sy0">=</span><span class="kw2">false</span><span class="sy0">;</span>
        <span class="kw1">if</span> <span class="br0">(</span> stars <span class="sy0">&gt;</span> <span class="nu0">6</span><span class="br0">)</span><span class="br0">{</span>
            <span class="kw1">if</span> <span class="br0">(</span>stars – <span class="nu0">5</span> <span class="sy0">&gt;</span> player.<span class="me1">ground</span>.<span class="me1">size</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="br0">{</span>
                enoughStar <span class="sy0">=</span><span class="kw2">true</span>
            <span class="br0">}</span> <span class="kw1">else</span> <span class="br0">{</span>
                enoughStar <span class="sy0">=</span><span class="kw2">false</span>
            <span class="br0">}</span>
 
        <span class="br0">}</span> <span class="kw1">else</span> <span class="br0">{</span>
            enoughStar<span class="sy0">=</span><span class="kw2">true</span><span class="sy0">;</span>
        <span class="br0">}</span>
        <span class="co1">//(!aCard.summonCancel) &amp;&amp; &amp;&amp; sastifySummonCondition(aCard)</span>
        <span class="kw1">return</span> <span class="br0">(</span>enoughStar <span class="sy0">&amp;&amp;</span> aCard.<span class="me1">isMonsterCard</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
<span class="br0">}</span></pre>

<p>
And the way to call it … CardGamePlay 
</p>
<pre class="code java">            <span class="kw1">case</span> MainPhase<span class="sy0">:</span>
                <span class="kw1">if</span> <span class="br0">(</span><span class="sy0">!</span>currentTurn.<span class="me1">player</span>.<span class="me1">aiPlayer</span><span class="br0">)</span><span class="br0">{</span>
                    <span class="kw1">if</span> <span class="br0">(</span>isPlayerChangePhase<span class="br0">(</span>MainPhase<span class="br0">)</span><span class="br0">)</span><span class="br0">{</span>
                        nextPhase<span class="br0">(</span><span class="br0">)</span>
                    <span class="br0">}</span> <span class="kw1">else</span> <span class="br0">{</span>
                        humanSelectFunction<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
                    <span class="br0">}</span>
                <span class="br0">}</span> <span class="kw1">else</span> <span class="br0">{</span>
                    println<span class="br0">(</span>currentTurn.<span class="me1">player</span>.<span class="me1">ai</span><span class="br0">)</span><span class="sy0">;</span>
                    currentTurn.<span class="me1">player</span>.<span class="me1">ai</span>.<span class="me1">think</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
                    currentTurn.<span class="me1">player</span>.<span class="me1">ai</span>.<span class="me1">act</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
                <span class="br0">}</span></pre>

<p>
The fun things here are we delayed Action we want the AI and save to Actions list made from Closure. In the main loop, we wait till ai.act is called then execute all the delayed action. The power of Groovy once again shown! By this technique we can easily introduce paralel computing with an cool ulitities of Groovy named <a href="/doku.php/jme3:atomixtuts:cardsgame:gpars" class="wikilink2" title="jme3:atomixtuts:cardsgame:gpars" rel="nofollow">GPars</a>. But we don’t use it right now though ! 
</p>

<p>
:roll:
</p>

</div>
<!-- EDIT13 SECTION "D-Implementation" [8532-] -->
