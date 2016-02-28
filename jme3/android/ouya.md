---
title: This is just notes at the moment
---
<h1 class="sectionedit1" id="this_is_just_notes_at_the_moment">This is just notes at the moment</h1>
<div class="level1">

<p>
Noting down Ouya stuff, will be turned into a proper doc later.
</p>

<p>
Installing Ouya drivers etc: 
<a href="https://devs.ouya.tv/developers/docs/setup" class="urlextern" title="https://devs.ouya.tv/developers/docs/setup" rel="nofollow">https://devs.ouya.tv/developers/docs/setup</a>
</p>

<p>
Note that you need to connect the USB to the micro USB port, not the full sized one!
</p>

<p>
Be aware that because the driver is unsigned it can be a real pain for windows to find it. You need to really persist until you get an android ADB Interface or similar. Windows tends to try and install it as an MTP USB Device instead - which will allow you to transfer files but not actually debug or run anything!
</p>

<p>
ADB Interface didn't work, had to use USB Composite. Google gives conflicting advice on this though so no idea if different people will find different. Key thing is to make sure the Ouya appears in adb devices.
</p>

<p>
Some helpful advice: <a href="http://ouyaforum.com/showthread.php?1425-Tutorial-Jmonkey-and-OUYA" class="urlextern" title="http://ouyaforum.com/showthread.php?1425-Tutorial-Jmonkey-and-OUYA" rel="nofollow">http://ouyaforum.com/showthread.php?1425-Tutorial-Jmonkey-and-OUYA</a>
</p>

<p>
Need to download Ouya Dev Kit (ODK) from <a href="https://devs.ouya.tv/developers/odk" class="urlextern" title="https://devs.ouya.tv/developers/odk" rel="nofollow">https://devs.ouya.tv/developers/odk</a>
</p>

<p>
Add the libraries from the download into the project.
</p>

</div>
