---
title: Wiki Tasks
---
<h1 class="sectionedit1" id="wiki_tasks">Wiki Tasks</h1>
<div class="level1">

<p>
This page lists all tasks in the wiki.
</p>

</div>
<!-- EDIT1 SECTION "Wiki Tasks" [1-65] -->
<h2 class="sectionedit2" id="jme3_doku_tasks">jME3 Doku Tasks</h2>
<div class="level2">

<p>
<a href="/lib/exe/fetch.php/tasks_jme3_noform" class="media mediafile mf_ wikilink2" title="tasks_jme3_noform">tasks_jme3_noform</a>
</p>

</div>
<!-- EDIT2 SECTION "jME3 Doku Tasks" [66-117] -->
<h2 class="sectionedit3" id="sdk_doku_tasks">SDK Doku Tasks</h2>
<div class="level2">

<p>
<a href="/lib/exe/fetch.php/tasks_sdk_noform" class="media mediafile mf_ wikilink2" title="tasks_sdk_noform">tasks_sdk_noform</a>
</p>

</div>

<h4 id="creating_tasks">Creating Tasks</h4>
<div class="level4">

<p>
Place <code>~~TASK~~</code> on any page to mark it as a task. The title (first heading) is considered to be the summary of the task, the contents its description. Use Alt-N on mac to create a ~ character.
</p>

</div>

<h4 id="full_usage_description">Full usage description</h4>
<div class="level4">
<pre class="code">~~TASK:[user]?[due date][priority]~~</pre>
<div class="table sectionedit4"><table class="inline">
	<tr class="row0">
		<th class="col0"> [user] </th><td class="col1"> person responsible for this task – either user or full name </td><td class="col2"> optional; default is unassigned </td>
	</tr>
	<tr class="row1">
		<th class="col0"> [due date] </th><td class="col1"> date the task should be completed in YYYY-MM-DD form; if only year or year and month are given, the last day is assumed </td><td class="col2"> optional; default is without due date </td>
	</tr>
	<tr class="row2">
		<th class="col0"> [priority] </th><td class="col1"> low, medium <code>!</code>, high <code>!!</code> or critical <code>!!!</code> expressed with 0 to 3 exclamation marks </td><td class="col2"> optional; default is low priority </td>
	</tr>
</table></div>
<!-- EDIT4 TABLE [464-900] -->
<p>
If a task is unassigned, any registered user of the wiki can accept it. Once a task is taken, the user to whom it is assigned to can change the status of the task to one of these values:
</p>
<ul>
<li class="level1"><div class="li"> rejected – task is not worthwhile or not accepted by user</div>
</li>
<li class="level1"><div class="li"> new – reassign task so somebody else can take it</div>
</li>
<li class="level1"><div class="li"> accepted – user took over task but did not yet start the work</div>
</li>
<li class="level1"><div class="li"> started – work on task started</div>
</li>
<li class="level1"><div class="li"> done – work on task completed</div>
</li>
</ul>

<p>
If the task is done, other users can verify whether it's really done. If yes, the status can be set to verified.
</p>

<p>
The priority is reflected by the intensity of the orange shade of the task box.
</p>

<p>
Next to the title of the task box is an icon. It links to download an .ics file for the task. That can be imported by almost any calendar application that understands the VTODO component of the iCalendar standard.
</p>

</div>
<!-- EDIT3 SECTION "SDK Doku Tasks" [118-] -->
