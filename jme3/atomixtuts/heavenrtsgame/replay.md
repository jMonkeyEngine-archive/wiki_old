---
title: Replay (Save/Load) & Memento
---
<h2 class="sectionedit1" id="replay_save_load_memento">Replay (Save/Load) &amp; Memento</h2>
<div class="level2">

<p>
Read first:
</p>

<p>
<a href="http://sourcemaking.com/design_patterns/memento" class="urlextern" title="http://sourcemaking.com/design_patterns/memento" rel="nofollow">http://sourcemaking.com/design_patterns/memento</a>
</p>

<p>
<a href="http://www.gamasutra.com/view/feature/2029/developing_your_own_replay_system.php" class="urlextern" title="http://www.gamasutra.com/view/feature/2029/developing_your_own_replay_system.php" rel="nofollow">http://www.gamasutra.com/view/feature/2029/developing_your_own_replay_system.php</a>
</p>

<p>
This implement the Memento pattern which represent a view of neccessary imformations need (also call internal state) for later decision and observasion like in AI or replay.
</p>

<p>
For optimization purpose it's normally not a full view, it just save the differences compare to its previous state 
Also note that the context (Originator) in the Memento pattern here is the GamePlay. So any info from StageLevel or Network level, even physics… is unknown! 
</p>

<p>
In GamePlay level, available information is valids Input and Actions, etc..
</p>

<p>
In this RTS game, GameState contains the current Map object, Units object, the Player objects, the AI object and the time since the game started, in milliseconds…
</p>

<p>
This is the distinct difference between Atom's Replay version and others implementation.
</p>

</div>
