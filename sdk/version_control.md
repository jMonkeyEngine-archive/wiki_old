---
title: jMonkeyEngine SDK: Version Control
---
<h1 class="sectionedit1" id="jmonkeyengine_sdkversion_control">jMonkeyEngine SDK: Version Control</h1>
<div class="level1">

<p>
Whether you work in a development team or alone: File versioning is a handy method to keep your code consistent, compare files line-by-line, and even roll back unwanted changes. This documentation shows you how to make the most of the SDK's integrated version control features for Subversion, Mercurial, and Git.
</p>

<p>
For every team member, the file versioning workflow is as follows:
</p>
<ol>
<li class="level1"><div class="li"> Once: Download a working copy of the project from the repository (“checkout”).</div>
</li>
<li class="level1"><div class="li"> Regularly: Upload your own changes to the repository (“commit”).</div>
</li>
<li class="level1"><div class="li"> Regularly: Download updates by others from the repository (“update”).     </div>
</li>
</ol>

<p>
Note: Since the jMonkeyEngine SDK is based on the NetBeans Platform framework, you can learn about certain jMonkeyEngine SDK features by reading the corresponding NetBeans IDE tutorials (in the “see also links”). 
</p>

</div>
<!-- EDIT1 SECTION "jMonkeyEngine SDK: Version Control" [1-878] -->
<h2 class="sectionedit2" id="version_control_systems">Version Control Systems</h2>
<div class="level2">

<p>
The jMonkeyEngine SDK supports various Version Control Systems such as Subversion, Mercurial, and Git. No matter which of them you use, they all share a common user interface.
</p>

<p>
You can use file versioning alone or in a team. The advantages are that you can keep track of changes (who did it, when, and why), you can compare versions line-by-line, you can revert changes to files and lines, merge multiple changes to one file, and you can even undelete files.
</p>

</div>
<!-- EDIT2 SECTION "Version Control Systems" [879-1375] -->
<h2 class="sectionedit3" id="creating_a_repository_upload">Creating a Repository (Upload)</h2>
<div class="level2">

<p>
Requirements:
</p>
<ul>
<li class="level1"><div class="li"> You must have a project that you want to version. </div>
</li>
<li class="level1"><div class="li"> You must have version control software installed (Subversion, Mercurial, or Git) and have initialized a repository.</div>
<ul>
<li class="level2"><div class="li"> Tip: For Subversion, for example, the init command looks like this example: <code>svnadmin create /home/joe/jMonkeyProjects/MyGame</code></div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> The computer where the repository is to be hosted must be available in your team's network, or you will only be able to use your repo locally.</div>
<ul>
<li class="level2"><div class="li"> Tip: Hosts such as SourceForge, GoogleCode, dev.java.net offer free version control services for open-source projects.</div>
</li>
</ul>
</li>
</ul>

<p>
Now you create a repository to store your project's files. 
</p>
<ol>
<li class="level1"><div class="li"> In the jMonkeyEngine SDK, right-click the project in the Projects window and choose Versioning &gt; Import Into Subversion Repository (or initialize Mercurial Project, etc, respectively). </div>
<ul>
<li class="level2"><div class="li"> Tip: If you haven't evaluated yet which system to choose, start with Subversion for now.</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Go through the wizard and fill in the fields to set up the repository.</div>
</li>
</ol>

</div>
<!-- EDIT3 SECTION "Creating a Repository (Upload)" [1376-2439] -->
<h2 class="sectionedit4" id="checking_out_a_repository_download">Checking Out a Repository (Download)</h2>
<div class="level2">

<p>
You and your team mates check out (download) the repository to their individual workstations. 
</p>
<ol>
<li class="level1"><div class="li"> Go to the Team menu and choose Subversion &gt; Checkout (or Git or Mercurial respectively)</div>
</li>
<li class="level1"><div class="li"> Fill in your repo data into the wizard and click Finish.</div>
<ul>
<li class="level2"><div class="li"> A typical repository <abbr title="Uniform Resource Locator">URL</abbr> looks like this example: <code><a href="http://jmonkeyengine.googlecode.com/svn/trunk/engine" class="urlextern" title="http://jmonkeyengine.googlecode.com/svn/trunk/engine" rel="nofollow">http://jmonkeyengine.googlecode.com/svn/trunk/engine</a></code></div>
</li>
<li class="level2"><div class="li"> If you want to be able to submit changes, you must have a username and password to this repository. Otherwise leave these fields blank.</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> The repository is downloaded and stored in the location you chose. </div>
</li>
<li class="level1"><div class="li"> Use the File &gt; Open Project menu to open the checkout as project and start working. </div>
<ul>
<li class="level2"><div class="li"> If the checkout is not recognized you need to choose File &gt; New Project from Existing Sources</div>
</li>
</ul>
</li>
</ol>

<p>
Of course you can also check out existing repositories and access code from other open-source projects (e.g. SourceForge, GoogleCode, dev.java.net). 
</p>

</div>
<!-- EDIT4 SECTION "Checking Out a Repository (Download)" [2440-3407] -->
<h2 class="sectionedit5" id="updating_and_committing_changes_send_and_receive">Updating and Committing Changes (Send and Receive)</h2>
<div class="level2">

<p>
Receiving the latest changes from the team's repository is referred to as <code>updating</code>. Sending your changes to the team's repository is refered to as <code>commiting</code>.
</p>
<ol>
<li class="level1"><div class="li"> Before making changes, right-click the project and select Subversion &gt; Update to make sure you have the latest revision.</div>
<ul>
<li class="level2"><div class="li"> Get in the habit of updating regularly, always before you edit a version controlled file. It will spare you much grief.</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> After making changes to the project, make certain your change did not break anything.</div>
<ol>
<li class="level2"><div class="li"> Update, build, run, test.</div>
</li>
<li class="level2"><div class="li"> Look at the red/green/blue marks in the editor to review what you have deleted/added/changed. Click the marks to review all differences in a file.</div>
</li>
<li class="level2"><div class="li"> Choose Subversion &gt; Show Changes to see all files that were recently changed – by you and other team members. </div>
</li>
<li class="level2"><div class="li"> <em>Update again</em> in case your team mates made changes while you were reviewing.</div>
</li>
</ol>
</li>
<li class="level1"><div class="li"> If there are no conflicts and you want to commit your changes, choose Subversion &gt; Commit from the menu.</div>
</li>
<li class="level1"><div class="li"> Write a commit message describing what you changed. </div>
<ul>
<li class="level2"><div class="li"> Remember, you are writing “a message to your future self”. Never write redundant stuff like “I changed something”.</div>
</li>
</ul>
</li>
</ol>

</div>
<!-- EDIT5 SECTION "Updating and Committing Changes (Send and Receive)" [3408-4656] -->
<h2 class="sectionedit6" id="comparing_and_reverting_changes">Comparing and Reverting Changes</h2>
<div class="level2">
<ul>
<li class="level1"><div class="li"> If you and another committer edited the same line, there is a conflict, and the jMonkeyEngine SDK will show an error message. </div>
<ul>
<li class="level2"><div class="li"> Right-click a file Choose Subversion &gt; Resolve Conflict</div>
<ol>
<li class="level3"><div class="li"> Compare the conflicting versions. Press the buttons to accept or reject each change individually. </div>
</li>
<li class="level3"><div class="li"> After the resolver shows green, save the resolution.</div>
</li>
<li class="level3"><div class="li"> Build and test the resolution, update, and commit.</div>
</li>
</ol>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Right-click a file and choose Subversion &gt; Search History.</div>
<ul>
<li class="level2"><div class="li"> You can inspect a file's history and see who changed what, why, and when. </div>
</li>
<li class="level2"><div class="li"> You can roll back a file to a historic version if necessary.</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> In general, you can choose Subversion &gt; Diff for any file to see two versions of a file next to each other.</div>
</li>
</ul>

</div>
<!-- EDIT6 SECTION "Comparing and Reverting Changes" [4657-5448] -->
<h2 class="sectionedit7" id="no_version_control_local_history">No Version Control? Local History!</h2>
<div class="level2">

<p>
If you do not use any version control, you can still track changes in projects to a certain degree.
</p>
<ul>
<li class="level1"><div class="li"> Right-click a file or directory and choose Local History to show or revert changes, or undelete files.</div>
</li>
<li class="level1"><div class="li"> You can also select any two files in the Project window and choose Tools &gt; Diff to compare them.</div>
</li>
<li class="level1"><div class="li"> Local History only works for files edited in jMonkeyEngine SDK Projects (It does not work for other files, e.g. in the Favorites window.)</div>
</li>
</ul>

<p>
See also:
</p>
<ul>
<li class="level1"><div class="li"> <a href="http://netbeans.org/kb/docs/ide/subversion.html" class="urlextern" title="http://netbeans.org/kb/docs/ide/subversion.html" rel="nofollow">Source Code Management with Subversion</a></div>
</li>
</ul>
<div class="tags"><span>
	<a href="/tag/documentation.html" class="wikilink1" title="tag:documentation" rel="tag">documentation</a>,
	<a href="/tag/sdk.html" class="wikilink1" title="tag:sdk" rel="tag">sdk</a>,
	<a href="/tag/editor.html" class="wikilink1" title="tag:editor" rel="tag">editor</a>,
	<a href="/tag/tool.html" class="wikilink1" title="tag:tool" rel="tag">tool</a>
</span></div>

</div>
<!-- EDIT7 SECTION "No Version Control? Local History!" [5449-] -->
