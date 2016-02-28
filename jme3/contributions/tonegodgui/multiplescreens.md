---
title: Implementing Multiple Screens
---
<h3 class="sectionedit1" id="implementing_multiple_screens">Implementing Multiple Screens</h3>
<div class="level3">

<p>
So, before I explain how to do this, ask yourself a question:<br />

<br />

Why the F do I need Multiple Screens?!??<br />

<br />

This is JME!  That's what AppStates are for.<br />

<br />

Now… on with the example of how to implement multiple screens using AppStates.<br />

<br />

</p>
<pre class="code java"><span class="kw1">public</span> <span class="kw1">class</span> UserLogin <span class="kw1">extends</span> AbstractAppState <span class="br0">{</span>
    Main app<span class="sy0">;</span>
    Screen screen<span class="sy0">;</span>
 
    LoginBox loginWindow<span class="sy0">;</span>
 
    <span class="kw1">public</span> UserLogin<span class="br0">(</span>Main app, Screen screen<span class="br0">)</span> <span class="br0">{</span>
        <span class="kw1">this</span>.<span class="me1">app</span> <span class="sy0">=</span> app<span class="sy0">;</span>
        <span class="kw1">this</span>.<span class="me1">screen</span> <span class="sy0">=</span> screen<span class="sy0">;</span>
    <span class="br0">}</span>
 
    @Override
    <span class="kw1">public</span> <span class="kw4">void</span> initialize<span class="br0">(</span>AppStateManager stateManager, Application app<span class="br0">)</span> <span class="br0">{</span>
        <span class="kw1">super</span>.<span class="me1">initialize</span><span class="br0">(</span>stateManager, app<span class="br0">)</span><span class="sy0">;</span>
 
        initLoginWindow<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    <span class="kw1">public</span> <span class="kw4">void</span> initLoginWindow<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
        loginWindow <span class="sy0">=</span> <span class="kw1">new</span> LoginBox<span class="br0">(</span>screen, 
                <span class="st0">"loginWindow"</span>,
                <span class="kw1">new</span> Vector2f<span class="br0">(</span>screen.<span class="me1">getWidth</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">/</span><span class="nu0">2</span><span class="sy0">-</span><span class="nu0">175</span>,screen.<span class="me1">getHeight</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">/</span><span class="nu0">2</span><span class="sy0">-</span><span class="nu0">125</span><span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
            @Override
            <span class="kw1">public</span> <span class="kw4">void</span> onButtonLoginPressed<span class="br0">(</span>MouseButtonEvent evt, <span class="kw4">boolean</span> toggled<span class="br0">)</span> <span class="br0">{</span>
                <span class="co1">// Some call to the server to log the client in</span>
                finalizeUserLogin<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
            <span class="br0">}</span>
        <span class="br0">}</span><span class="sy0">;</span>
        screen.<span class="me1">addElement</span><span class="br0">(</span>loginWindow<span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    @Override
    <span class="kw1">public</span> <span class="kw4">void</span> cleanup<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
        <span class="kw1">super</span>.<span class="me1">cleanup</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
 
        screen.<span class="me1">removeElement</span><span class="br0">(</span>loginWindow<span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    <span class="kw1">public</span> <span class="kw4">void</span> finalizeUserLogin<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
        <span class="co1">// Some call to your app to unload this AppState and load the next AppState</span>
        app.<span class="me1">someMethodToSwitchAppStates</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
<span class="br0">}</span></pre>

<p>
And Ker-pow! You have a screen without a new Screen.<br />

<br />

If you want to be fancy about loading and unloading the contents of the screen, use the EffectManager and call the following when running the effects from the cleanup() method of the AppState.
</p>
<pre class="code java">effect.<span class="me1">setDestroyOnHide</span><span class="br0">(</span><span class="kw2">true</span><span class="br0">)</span><span class="sy0">;</span></pre>

</div>
