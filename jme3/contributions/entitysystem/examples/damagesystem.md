---
title: Damage Systems Example
---
<h1 class="sectionedit1" id="damage_systems_example">Damage Systems Example</h1>
<div class="level1">

<p>
As written in the Entity System Advanced article, there should only be one class which changes one special Component.
This makes the code easy to debug and prevents component changes from being skipped.
</p>

</div>
<!-- EDIT1 SECTION "Damage Systems Example" [1-241] -->
<h2 class="sectionedit2" id="the_components">The Components</h2>
<div class="level2">

</div>
<!-- EDIT2 SECTION "The Components" [242-267] -->
<h3 class="sectionedit3" id="the_healthcomponent">The HealthComponent</h3>
<div class="level3">
<pre class="code java"><span class="kw1">public</span> <span class="kw1">class</span> HealthComponent <span class="kw1">extends</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+component"><span class="kw3">Component</span></a> <span class="br0">{</span>
 
    <span class="kw1">public</span> <span class="kw4">float</span> health<span class="sy0">;</span>
 
    <span class="kw1">public</span> HealthComponent<span class="br0">(</span><span class="kw4">float</span> health<span class="br0">)</span>
    <span class="br0">{</span>
        <span class="kw1">this</span>.<span class="me1">health</span> <span class="sy0">=</span> health<span class="sy0">;</span>
    <span class="br0">}</span>
 
    <span class="kw1">public</span> <span class="kw4">float</span> getHealth<span class="br0">(</span><span class="br0">)</span>
    <span class="br0">{</span>
        <span class="kw1">return</span> health<span class="sy0">;</span>
    <span class="br0">}</span>
 
<span class="br0">}</span></pre>

</div>
<!-- EDIT3 SECTION "The HealthComponent" [268-559] -->
<h3 class="sectionedit4" id="the_damagecomponent">The DamageComponent</h3>
<div class="level3">
<pre class="code java">    <span class="kw1">private</span> <span class="kw4">float</span> damage<span class="sy0">;</span>
    <span class="kw1">private</span> EntityId target<span class="sy0">;</span>
 
    <span class="kw1">public</span> DamageComponent<span class="br0">(</span>EntityId target, <span class="kw4">float</span> damage<span class="br0">)</span>
    <span class="br0">{</span>
        <span class="kw1">this</span>.<span class="me1">damage</span><span class="sy0">=</span>damage<span class="sy0">;</span>
        <span class="kw1">this</span>.<span class="me1">target</span><span class="sy0">=</span>target<span class="sy0">;</span>
    <span class="br0">}</span>
 
    <span class="kw1">public</span> <span class="kw4">float</span> getDamage<span class="br0">(</span><span class="br0">)</span>
    <span class="br0">{</span>
        <span class="kw1">return</span> damage<span class="sy0">;</span>
    <span class="br0">}</span>
 
    <span class="kw1">public</span> EntityId getTarget<span class="br0">(</span><span class="br0">)</span>
    <span class="br0">{</span>
        <span class="kw1">return</span> target<span class="sy0">;</span>
    <span class="br0">}</span></pre>

</div>
<!-- EDIT4 SECTION "The DamageComponent" [560-935] -->
<h2 class="sectionedit5" id="the_appstate">The AppState</h2>
<div class="level2">
<pre class="code java"><span class="kw1">public</span> <span class="kw1">class</span> DamageAppState <span class="kw1">extends</span> AbstractAppState <span class="br0">{</span>
 
    EntitySet damageSet<span class="sy0">;</span>
    EntitySet healthSet<span class="sy0">;</span>
 
   <span class="kw1">public</span> <span class="kw4">void</span> initialize<span class="br0">(</span>AppStateManager stateManager, Application app<span class="br0">)</span> <span class="br0">{</span>
        EntitySystem entitySystem <span class="sy0">=</span> <span class="br0">(</span><span class="br0">(</span>Main<span class="br0">)</span>app<span class="br0">)</span>.<span class="me1">getEntitySystem</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
        damageSet <span class="sy0">=</span> entitySystem.<span class="me1">getEntitySet</span><span class="br0">(</span>DamageComponent.<span class="kw1">class</span><span class="br0">)</span><span class="sy0">;</span>
        healthSet <span class="sy0">=</span> entitySystem.<span class="me1">getEntitySet</span><span class="br0">(</span>HealthComponent.<span class="kw1">class</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
   @Override
   <span class="kw1">public</span> <span class="kw4">void</span> update<span class="br0">(</span><span class="kw4">float</span> tpf<span class="br0">)</span> <span class="br0">{</span>
 
       Map<span class="sy0">&lt;</span>EntityId,Float<span class="sy0">&gt;</span> damageSummary <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+hashmap"><span class="kw3">HashMap</span></a><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
 
       damageSet.<span class="me1">applyChanges</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
       healthSet.<span class="me1">applyChanges</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
 
       Iterator<span class="sy0">&lt;</span>Entity<span class="sy0">&gt;</span> iterator <span class="sy0">=</span> damageSet.<span class="me1">getIterator</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
       <span class="kw1">while</span><span class="br0">(</span>iterator.<span class="me1">hasNext</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span>
       <span class="br0">{</span>
           <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+entity"><span class="kw3">Entity</span></a> entity <span class="sy0">=</span> iterator.<span class="me1">next</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
           DamageComponent dc <span class="sy0">=</span> entity.<span class="me1">getComponent</span><span class="br0">(</span>DamageComponent.<span class="kw1">class</span><span class="br0">)</span><span class="sy0">;</span>
 
           <span class="kw4">float</span> f <span class="sy0">=</span> <span class="nu0">0</span><span class="sy0">;</span>
           <span class="kw1">if</span><span class="br0">(</span>damageSummary.<span class="me1">containsKey</span><span class="br0">(</span>dc.<span class="me1">getTarget</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="br0">)</span>
           <span class="br0">{</span>
               f <span class="sy0">=</span> damageSummary.<span class="me1">get</span><span class="br0">(</span>dc.<span class="me1">getTarget</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
           <span class="br0">}</span>
 
           f <span class="sy0">+=</span> dc.<span class="me1">getDamage</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
           damageSummary.<span class="me1">put</span><span class="br0">(</span>dc.<span class="me1">getTarget</span><span class="br0">(</span><span class="br0">)</span>,f<span class="br0">)</span><span class="sy0">;</span>
 
           entity.<span class="me1">destroy</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
       <span class="br0">}</span>
 
       Iterator<span class="sy0">&lt;</span>EntityId<span class="sy0">&gt;</span> keyIterator <span class="sy0">=</span> damageSummary.<span class="me1">keySet</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">iterator</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
       <span class="kw1">while</span><span class="br0">(</span>keyIterator.<span class="me1">hasNext</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span>
       <span class="br0">{</span>
           EntityId entityId <span class="sy0">=</span> keyIterator.<span class="me1">next</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
           <span class="kw4">float</span> damage <span class="sy0">=</span> damageSummary.<span class="me1">get</span><span class="br0">(</span>entityId<span class="br0">)</span><span class="sy0">;</span>
 
           <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+entity"><span class="kw3">Entity</span></a> entity <span class="sy0">=</span> healthSet.<span class="me1">getEntity</span><span class="br0">(</span>entityId<span class="br0">)</span><span class="sy0">;</span>
           <span class="kw1">if</span><span class="br0">(</span>entity <span class="sy0">!=</span> <span class="kw2">null</span><span class="br0">)</span>
           <span class="br0">{</span>
               HealthComponent hc <span class="sy0">=</span> entity.<span class="me1">getComponent</span><span class="br0">(</span>HealthComponent.<span class="kw1">class</span><span class="br0">)</span><span class="sy0">;</span>
               <span class="kw4">float</span> newLife <span class="sy0">=</span> hc.<span class="me1">getHealth</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">-</span>damage<span class="sy0">;</span>
 
               <span class="kw1">if</span><span class="br0">(</span>newLife <span class="sy0">&lt;</span> <span class="nu0">0</span><span class="br0">)</span>
               <span class="br0">{</span>
                   entity.<span class="me1">removeComponent</span><span class="br0">(</span>HealthComponent.<span class="kw1">class</span><span class="br0">)</span><span class="sy0">;</span>
               <span class="br0">}</span><span class="kw1">else</span><span class="br0">{</span>
                   entity.<span class="me1">setComponent</span><span class="br0">(</span><span class="kw1">new</span> HealthComponent<span class="br0">(</span>newLife<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
               <span class="br0">}</span>
           <span class="br0">}</span>
       <span class="br0">}</span>
   <span class="br0">}</span>
 
<span class="br0">}</span></pre>

</div>
<!-- EDIT5 SECTION "The AppState" [936-2875] -->
<h2 class="sectionedit6" id="usage">Usage</h2>
<div class="level2">
<pre class="code java"><span class="co1">//Create a new Entity System</span>
entitySystem <span class="sy0">=</span> <span class="kw1">new</span> EntitySystem<span class="br0">(</span><span class="kw1">new</span> MapEntityData<span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
 
<span class="co1">//Add the DamageAppState to the Application</span>
stateManager.<span class="me1">attach</span><span class="br0">(</span><span class="kw1">new</span> DamageAppState<span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
 
<span class="co1">//Create a new Entity with 100 HP</span>
EntityId healthEntity <span class="sy0">=</span> entitySystem.<span class="me1">newEntity</span><span class="br0">(</span><span class="kw1">new</span> HealthComponent<span class="br0">(</span><span class="nu0">100</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
 
<span class="co1">//Create a new Damage Entity who deals 5 damage to the health entity</span>
entitySystem.<span class="me1">newEntity</span><span class="br0">(</span><span class="kw1">new</span> DamageComponent<span class="br0">(</span>healthEntity,<span class="nu0">5</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span></pre>

</div>
<!-- EDIT6 SECTION "Usage" [2876-] -->
