---
title: Next Generation Particles - Reference
---
<h1 class="sectionedit1" id="next_generation_particles_-_reference">Next Generation Particles - Reference</h1>
<div class="level1">

<p>
The Parameters for a ParticleController are:
</p>
<div class="table sectionedit2"><table class="inline">
	<tr class="row0">
		<td class="col0"> name </td><td class="col1"> The name to use for the geometry in the scene graph </td>
	</tr>
	<tr class="row1">
		<td class="col0"> mesh </td><td class="col1"> The mesh to use (Usually either PointMesh or QuadMesh) </td>
	</tr>
	<tr class="row2">
		<td class="col0"> maxParticles </td><td class="col1"> The maximum number of particles to allow active at any one time </td>
	</tr>
	<tr class="row3">
		<td class="col0"> lifeMin </td><td class="col1"> The minimum amount of time (in seconds) for which each particle lives </td>
	</tr>
	<tr class="row4">
		<td class="col0"> lifeMax </td><td class="col1"> The maximum amount of time (in seconds) for which each particle lives </td>
	</tr>
	<tr class="row5">
		<td class="col0"> source </td><td class="col1"> The source from which the particles are spawned </td>
	</tr>
	<tr class="row6">
		<td class="col0"> emissionController </td><td class="col1"> The frequency and timing with which particles are spawned. If null then no particles are automatically spawned and they must be triggered manually using emitNextParticle() or emitAllParticles() </td>
	</tr>
	<tr class="row7">
		<td class="col0"> influencers </td><td class="col1"> Zero or more ParticleInfluencers, each of which changes the behaviour of the particles. </td>
	</tr>
</table></div>
<!-- EDIT2 TABLE [99-864] -->
<p>
All of the following classes have defined Interfaces or Abstract Classes to allow custom implementations and behaviour to easily be plugged into the system.
</p>

<p>
Javadoc for the system can be found at <a href="http://www.zero-separation.com/particles/javadoc" class="urlextern" title="http://www.zero-separation.com/particles/javadoc" rel="nofollow">http://www.zero-separation.com/particles/javadoc</a>
</p>

</div>
<!-- EDIT1 SECTION "Next Generation Particles - Reference" [1-1116] -->
<h2 class="sectionedit3" id="mesh">Mesh</h2>
<div class="level2">

<p>
The Mesh options are:
</p>
<div class="table sectionedit4"><table class="inline">
	<tr class="row0">
		<td class="col0"> PointMesh </td><td class="col1"> Fastest and most efficient, but also most limited </td>
	</tr>
	<tr class="row1">
		<td class="col0"> QuadMesh </td><td class="col1"> Much more flexible than point mesh, all particles are represented as 2-dimensional quads </td>
	</tr>
	<tr class="row2">
		<td class="col0"> TemplateMesh </td><td class="col1"> Allows particles to be full 3d objects, with the mesh for each particle being generated from one of any number of template meshes. This allows fully 3d particles and takes in texture co-ordinates and even (if required) vertex colours and normals from the original mesh converting them as required. </td>
	</tr>
</table></div>
<!-- EDIT4 TABLE [1157-1643] -->
</div>
<!-- EDIT3 SECTION "Mesh" [1117-1644] -->
<h2 class="sectionedit5" id="source">Source</h2>
<div class="level2">

<p>
The Source options are:
</p>
<div class="table sectionedit6"><table class="inline">
	<tr class="row0">
		<td class="col0"> PointSource </td><td class="col1"> Generates all particles from a specific point with a random velocity. The point itself is a spatial so can be attached to the scene graph and will move with it. </td>
	</tr>
	<tr class="row1">
		<td class="col0"> MeshSource </td><td class="col1"> Generates all particles from a randomly selected point on the given mesh. A random triangle is selected and then the particle emitter from a random point within that triangle along the triangle's normal vector. </td>
	</tr>
	<tr class="row2">
		<td class="col0"> WeightedMeshSource </td><td class="col1"> Provides the same functionality as MeshSource but weights triangles based on their relative size, larger triangles will tend to emit more particles. This provides a more even spread but uses more resources and needs to be kept updated if the mesh changes. </td>
	</tr>
	<tr class="row3">
		<td class="col0"> ParticleParticleSource </td><td class="col1"> Emits particles from another ParticleController. The particle is emitted from a randomly selected active particle and the new particle starts with identical velocity, rotation, etc as the particle it is being emitted from. </td>
	</tr>
</table></div>
<!-- EDIT6 TABLE [1689-2628] -->
</div>
<!-- EDIT5 SECTION "Source" [1645-2629] -->
<h2 class="sectionedit7" id="emissioncontrollers">EmissionControllers</h2>
<div class="level2">
<div class="table sectionedit8"><table class="inline">
	<tr class="row0">
		<td class="col0"> NULL </td><td class="col1"> The NULL EmissionController does not automatically emit any particles, they must be emitted externally by a call to the ParticleController emitNextParticle() or emitAllParticles(). Note that if the ParticleController is not in use for an extended period of time it is recommended that to save resources you pause it by either disabling the controller or removing the Geometry from the scene graph. </td>
	</tr>
	<tr class="row1">
		<td class="col0"> RegularEmission </td><td class="col1"> This EmissionController just emits particles at regular intervals, it will emit multiple particles in one frame if more than one interval has passed since the previous frame. </td>
	</tr>
</table></div>
<!-- EDIT8 TABLE [2663-3268] -->
</div>
<!-- EDIT7 SECTION "EmissionControllers" [2630-3269] -->
<h2 class="sectionedit9" id="influencers">Influencers</h2>
<div class="level2">
<div class="table sectionedit10"><table class="inline">
	<tr class="row0">
		<td class="col0"> ColorInfluencer </td><td class="col1"> Modify the particle's color over time </td>
	</tr>
	<tr class="row1">
		<td class="col0"> GravityInfluencer </td><td class="col1"> Apply steady acceleration in a specified direction over time </td>
	</tr>
	<tr class="row2">
		<td class="col0"> MultiColorInfluencer </td><td class="col1"> Modify the particle's color through multiple colors over time </td>
	</tr>
	<tr class="row3">
		<td class="col0"> PreferredDestinationInfluencer </td><td class="col1"> Move the particle towards a specified point </td>
	</tr>
	<tr class="row4">
		<td class="col0"> PreferredDirectionInfluencer </td><td class="col1"> Rotate the particles velocity towards the given direction over time </td>
	</tr>
	<tr class="row5">
		<td class="col0"> RandomImpulseInfluencer </td><td class="col1"> Apply a random impulse to the particle either at initialization or every frame </td>
	</tr>
	<tr class="row6">
		<td class="col0"> RandomSpriteInfluencer </td><td class="col1"> Select a random sprite for the particle from those available when it is initialized </td>
	</tr>
	<tr class="row7">
		<td class="col0"> RotationInfluencer </td><td class="col1"> Rotate the particle by picking an initial rotational velocity at random and then maintaining it </td>
	</tr>
	<tr class="row8">
		<td class="col0"> SizeInfluencer </td><td class="col1"> Modify the particle's size over time </td>
	</tr>
	<tr class="row9">
		<td class="col0"> SpatialDestinationInfluencer </td><td class="col1"> Move the particle towards a given spatial, it will attempt to reach the current location of the spatial by the end of the particle's life cycle. </td>
	</tr>
	<tr class="row10">
		<td class="col0"> SpeedInfluencer </td><td class="col1"> Modify the particle's speed over time </td>
	</tr>
	<tr class="row11">
		<td class="col0"> SpriteAnimationInfluencer </td><td class="col1"> Animate the particle through the available sprites over time </td>
	</tr>
</table></div>
<!-- EDIT10 TABLE [3295-4446] -->
</div>
<!-- EDIT9 SECTION "Influencers" [3270-] -->
