---
title: jMonkeyEngine 教程 & 文档
---
<h1 class="sectionedit1" id="jmonkeyengine_教程_文档">jMonkeyEngine 教程 &amp; 文档</h1>
<div class="level1">

</div>
<!-- EDIT1 SECTION "jMonkeyEngine 教程 & 文档" [1-45] -->
<h2 class="sectionedit2" id="初级教程">初级教程</h2>
<div class="level2">

<p>
初级教程将介绍一些常见的游戏开发实例，并解释一些基本概念。在正式学习前，请确认自己是否了解<a href="/jme3/terminology.html" class="wikilink1" title="jme3:terminology">3D游戏开发的一些基本概念</a>，例如<a href="/jme3/the_scene_graph.html" class="wikilink1" title="jme3:the_scene_graph">场景图</a>。如果你不太了解的话，建议先学习“<a href="/jme3/math_for_dummies.html" class="wikilink1" title="jme3:math_for_dummies">3D数学基础知识</a>”以及“<a href="/jme3/scenegraph_for_dummies.html" class="wikilink1" title="jme3:scenegraph_for_dummies">3D场景图的基本概念</a>”。
</p>

<p>
<a href="https://github.com/jMonkeyEngine/jmonkeyengine/tree/master/jme3-examples/src/main/java/jme3test" class="urlextern" title="https://github.com/jMonkeyEngine/jmonkeyengine/tree/master/jme3-examples/src/main/java/jme3test" rel="nofollow">所有示例代码</a>均已包含在jMonkeyEngine SDK中（yan：通过github搜索jMonkeyEngine也能找到源码），你只需要在创建工程时选择<code>JmeTests</code>模板，即可查阅这些代码。如果你要自己开发游戏的话，建议在创建工程时选择<code>BasicGame</code>模板。
</p>

<p>
建议读者在学习的过程中把所有的示例代码都编写运行一遍，并且尝试着去修改这些代码，有助于加深对本教程的理解。
</p>

<p>
</p><p></p><div class="noteimportant"> <strong> 使用<a href="/sdk.html" class="wikilink1" title="sdk">jMonkeyEngine SDK</a>开发项目时，按F1键可以搜索并浏览本wiki的一份副本，帮助文档的内容与你所使用的SDK版本同步。本wiki随<a href="https://github.com/jMonkeyEngine/jmonkeyengine" class="urlextern" title="https://github.com/jMonkeyEngine/jmonkeyengine" rel="nofollow">jME3最新版本</a>同步更新。</strong> 
</div>


<p>
<a href="/resources/jme3-beginner-beginner-physics.png" class="media" title="jme3:beginner:beginner-physics.png"><img src="/resources/jme3-beginner-beginner-physics.png" class="mediaright" alt="" width="360" height="291" /></a>
</p>
<ol>
<li class="level1"><div class="li"> <a href="/jme3/beginner/hello_simpleapplication_zh.html" class="wikilink1" title="jme3:beginner:hello_simpleapplication_zh">第一个JME3程序</a> – 实现一个简单的程序</div>
</li>
<li class="level2"><div class="li"> <a href="/jme3/beginner/hello_node_zh.html" class="wikilink1" title="jme3:beginner:hello_node_zh">节点(Node)</a> – 在场景图中改变几何体和节点属性</div>
</li>
<li class="level2"><div class="li"> <a href="/doku.php/jme3:beginner:hello_asset_zh" class="wikilink2" title="jme3:beginner:hello_asset_zh" rel="nofollow">资源(Assets)</a> – 加载三维模型、场景和其他的资源</div>
</li>
<li class="level2"><div class="li"> <a href="/doku.php/jme3:beginner:hello_main_event_loop_zh" class="wikilink2" title="jme3:beginner:hello_main_event_loop_zh" rel="nofollow">事件循环(Loop)</a> – 在事件循环中实现事件控制功能</div>
</li>
<li class="level2"><div class="li"> <a href="/doku.php/jme3:beginner:hello_input_system_zh" class="wikilink2" title="jme3:beginner:hello_input_system_zh" rel="nofollow">输入(Input)</a> – 对于键盘和鼠标的输入作出响应</div>
</li>
<li class="level2"><div class="li"> <a href="/doku.php/jme3:beginner:hello_material_zh" class="wikilink2" title="jme3:beginner:hello_material_zh" rel="nofollow">材质(Material)</a> – 设置材质、纹理、透明度</div>
</li>
<li class="level2"><div class="li"> <a href="/doku.php/jme3:beginner:hello_animation_zh" class="wikilink2" title="jme3:beginner:hello_animation_zh" rel="nofollow">动画(Animation)</a> – 控制动画模型</div>
</li>
<li class="level2"><div class="li"> <a href="/doku.php/jme3:beginner:hello_picking_zh" class="wikilink2" title="jme3:beginner:hello_picking_zh" rel="nofollow">拣选(Picking)</a> – 射击、压下按钮、选择、捡起选项</div>
</li>
<li class="level2"><div class="li"> <a href="/doku.php/jme3:beginner:hello_collision_zh" class="wikilink2" title="jme3:beginner:hello_collision_zh" rel="nofollow">碰撞(Collision)</a> – 建造墙壁和固体地板</div>
</li>
<li class="level2"><div class="li"> <a href="/doku.php/jme3:beginner:hello_terrain_zh" class="wikilink2" title="jme3:beginner:hello_terrain_zh" rel="nofollow">地形(Terrain)</a> – 使用贴图创建小山的风景</div>
</li>
<li class="level2"><div class="li"> <a href="/doku.php/jme3:beginner:hello_audio_zh" class="wikilink2" title="jme3:beginner:hello_audio_zh" rel="nofollow">音效(Audio)</a> – 按照位置和事件来实现三维音效</div>
</li>
<li class="level2"><div class="li"> <a href="/doku.php/jme3:beginner:hello_effects_zh" class="wikilink2" title="jme3:beginner:hello_effects_zh" rel="nofollow">特效(Effects)</a> – 创建粒子特效，比如：火焰、爆炸、魔法</div>
</li>
<li class="level2"><div class="li"> <a href="/doku.php/jme3:beginner:hello_physics_zh" class="wikilink2" title="jme3:beginner:hello_physics_zh" rel="nofollow">物理(Physics)</a> – 撞球和坠落的砖头</div>
</li>
<li class="level2"><div class="li"> <a href="/doku.php/jme3:beginner:hello_vector_zh" class="wikilink2" title="jme3:beginner:hello_vector_zh" rel="nofollow">向量(Vector)</a> – 可视化向量与向量操作</div>
</li>
<li class="level2"><div class="li"> <a href="/doku.php/jme3:beginner:hello_chase_camera_zh" class="wikilink2" title="jme3:beginner:hello_chase_camera_zh" rel="nofollow">摄像机(Camera)</a> – aka的第三人称摄像机示例代码</div>
</li>
</ol>

<p>
See also: <a href="/sdk/sample_code.html" class="wikilink1" title="sdk:sample_code">运行示例代码遇到了问题吗</a>?
</p>

<p>
For more help getting started, check out this tuts+ guide on “<a href="http://gamedevelopment.tutsplus.com/articles/how-to-learn-jmonkeyengine-3--gamedev-10479" class="urlextern" title="http://gamedevelopment.tutsplus.com/articles/how-to-learn-jmonkeyengine-3--gamedev-10479" rel="nofollow"> How to learn jMonkeyEngine 3</a>”.
</p>

</div>
<!-- EDIT2 SECTION "初级教程" [46-3119] -->
<h2 class="sectionedit3" id="中级教程">中级教程</h2>
<div class="level2">

<p>
学初级教程后，你已经了解了所有的基本概念，是时候把它们综合起来了。下面这些文章可以帮助你理解如何在实践开发中综合应用这些知识。
</p>

<p>
<strong>jMonkeyEngine3 概念</strong>
</p>
<ul>
<li class="level1"><div class="li"> <a href="/jme3/intermediate/best_practices.html" class="wikilink1" title="jme3:intermediate:best_practices">最佳实践</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/intermediate/simpleapplication.html" class="wikilink1" title="jme3:intermediate:simpleapplication">深入SimpleApplication类</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/intermediate/appsettings.html" class="wikilink1" title="jme3:intermediate:appsettings">jME3显示配置</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/intermediate/file_types.html" class="wikilink1" title="jme3:intermediate:file_types">文件类型</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/intermediate/optimization.html" class="wikilink1" title="jme3:intermediate:optimization">优化</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/faq.html" class="wikilink1" title="jme3:faq">常见问题解答(FAQ)</a></div>
</li>
</ul>

<p>
<strong>数学概念</strong>
</p>
<ul>
<li class="level1"><div class="li"> <a href="/jme3/math_for_dummies.html" class="wikilink1" title="jme3:math_for_dummies">jME3数学基础</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/intermediate/math.html" class="wikilink1" title="jme3:intermediate:math">Short 3D math "cheat sheet"</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/math.html" class="wikilink1" title="jme3:math">jME3数学概述</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/math_video_tutorials.html" class="wikilink1" title="jme3:math_video_tutorials">视频: jME3数学系列教程</a></div>
</li>
</ul>

<p>
<strong>3D图形学概念</strong>
</p>
<ul>
<li class="level1"><div class="li"> <a href="/jme3/intermediate/multi-media_asset_pipeline.html" class="wikilink1" title="jme3:intermediate:multi-media_asset_pipeline">多媒体资源管道</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/scenegraph_for_dummies.html" class="wikilink1" title="jme3:scenegraph_for_dummies">3D场景图的基本概念</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/terminology.html" class="wikilink1" title="jme3:terminology">3D图形学术语</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/intermediate/how_to_use_materials.html" class="wikilink1" title="jme3:intermediate:how_to_use_materials">如何使用材质</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/intermediate/transparency_sorting.html" class="wikilink1" title="jme3:intermediate:transparency_sorting">透明度排序</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/external/blender.html" class="wikilink1" title="jme3:external:blender">使用Blender创建兼容jME3的模型</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/external/3dsmax.html" class="wikilink1" title="jme3:external:3dsmax">使用3dsmax创建兼容jME3的模型</a></div>
</li>
</ul>

<p>
<strong>游戏教程</strong>
</p>
<ul>
<li class="level1"><div class="li"> <a href="http://gamedevelopment.tutsplus.com/series/cross-platform-vector-shooter-jmonkeyengine--gamedev-13757" class="urlextern" title="http://gamedevelopment.tutsplus.com/series/cross-platform-vector-shooter-jmonkeyengine--gamedev-13757" rel="nofollow">Neon Vector Shooter tutorial on Tuts+</a></div>
</li>
</ul>

<p>
<strong>视频实例教程</strong>
- 注意：以下视频中使用了jME 3.1 alpha 版的一些特性
</p>
<ul>
<li class="level1"><div class="li"> <a href="http://www.youtube.com/watch?v=-OzRZscLlHY" class="urlextern" title="http://www.youtube.com/watch?v=-OzRZscLlHY" rel="nofollow">Video: jMonkeyEngine SDK Use Case Demo 1 (Quixote)</a></div>
</li>
<li class="level1"><div class="li"> <a href="http://www.youtube.com/watch?v=6-YWxD3JByE" class="urlextern" title="http://www.youtube.com/watch?v=6-YWxD3JByE" rel="nofollow">Video: jMonkeyEngine SDK Use Case Demo 2 (Models and Materials)</a></div>
</li>
</ul>

<p>
Learn from sample code in <a href="https://github.com/jMonkeyEngine/jmonkeyengine/tree/master/jme3-examples/src/main/java/jme3test" class="urlextern" title="https://github.com/jMonkeyEngine/jmonkeyengine/tree/master/jme3-examples/src/main/java/jme3test" rel="nofollow">src/main/java/jme3test</a> (also available in the sdk by File &gt; New Project &gt; JME3 Tests) and the example games provided by the community!
</p>

</div>
<!-- EDIT3 SECTION "中级教程" [3120-5124] -->
<h2 class="sectionedit4" id="进阶教程">进阶教程</h2>
<div class="level2">

<p>
现在你已经学会了所有的概念，是时候学习jMonkeyEngine的全部内容了！深入到API中去了解所有的选项，包括那些不太常用的高级方法。但是不要过度延长自己，开发游戏需要时间和奉献精神，一步一个脚印，战士！ :)
</p>

<p>
<strong>控制游戏逻辑</strong>
</p>
<ul>
<li class="level1"><div class="li"> <a href="/jme3/advanced/update_loop.html" class="wikilink1" title="jme3:advanced:update_loop">主循环</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/advanced/application_states.html" class="wikilink1" title="jme3:advanced:application_states">AppStates</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/advanced/custom_controls.html" class="wikilink1" title="jme3:advanced:custom_controls">自定义Control</a></div>
<ul>
<li class="level2"><div class="li"> <a href="http://www.youtube.com/watch?v=MNDiZ9YHIpM" class="urlextern" title="http://www.youtube.com/watch?v=MNDiZ9YHIpM" rel="nofollow">Video: How to control any scene node</a></div>
</li>
<li class="level2"><div class="li"> <a href="http://www.youtube.com/watch?v=-OzRZscLlHY" class="urlextern" title="http://www.youtube.com/watch?v=-OzRZscLlHY" rel="nofollow">Video: How to remote control a character in a scene</a></div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> <a href="/jme3/advanced/multithreading.html" class="wikilink1" title="jme3:advanced:multithreading">多线程</a></div>
</li>
</ul>

<p>
<strong>管理3D场景图中的对象</strong>
</p>
<ul>
<li class="level1"><div class="li"> <a href="/jme3/advanced/traverse_scenegraph.html" class="wikilink1" title="jme3:advanced:traverse_scenegraph">遍历场景图</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/advanced/spatial.html" class="wikilink1" title="jme3:advanced:spatial">Spatial: Node与Geometry的对比</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/advanced/mesh.html" class="wikilink1" title="jme3:advanced:mesh">网格</a></div>
<ul>
<li class="level2"><div class="li"> <a href="/jme3/advanced/shape.html" class="wikilink1" title="jme3:advanced:shape">形状</a></div>
</li>
<li class="level2"><div class="li"> <a href="/jme3/advanced/3d_models.html" class="wikilink1" title="jme3:advanced:3d_models">3D模型</a></div>
</li>
<li class="level2"><div class="li"> <a href="/jme3/advanced/custom_meshes.html" class="wikilink1" title="jme3:advanced:custom_meshes">自定义网格</a></div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> <a href="/jme3/advanced/asset_manager.html" class="wikilink1" title="jme3:advanced:asset_manager">资源管理器</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/advanced/save_and_load.html" class="wikilink1" title="jme3:advanced:save_and_load">读写节点数据(.J3O文件)</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/advanced/collision_and_intersection.html" class="wikilink1" title="jme3:advanced:collision_and_intersection">碰撞与交点</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/advanced/level_of_detail.html" class="wikilink1" title="jme3:advanced:level_of_detail">层次细节(LOD)</a></div>
</li>
</ul>

<p>
<strong>动画和场景</strong>
</p>
<ul>
<li class="level1"><div class="li"> <a href="/jme3/advanced/animation.html" class="wikilink1" title="jme3:advanced:animation">Animation</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/advanced/cinematics.html" class="wikilink1" title="jme3:advanced:cinematics">Cinematics (cutscenes, fake destruction physics)</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/advanced/motionpath.html" class="wikilink1" title="jme3:advanced:motionpath">MotionPaths and waypoints</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/external/blender.html" class="wikilink1" title="jme3:external:blender">Creating jME3 compatible 3D models in Blender</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/advanced/makehuman_blender_ogrexml_toolchain.html" class="wikilink1" title="jme3:advanced:makehuman_blender_ogrexml_toolchain">MakeHuman Blender OgreXML toolchain for creating and importing animated human characters</a></div>
</li>
<li class="level1"><div class="li"> <a href="/sdk/blender.html" class="wikilink1" title="sdk:blender">Converting Blender Models to JME3 (.J3o files)</a></div>
<ul>
<li class="level2"><div class="li"> <a href="https://www.youtube.com/watch?v=QiLCs4AKh28" class="urlextern" title="https://www.youtube.com/watch?v=QiLCs4AKh28" rel="nofollow">Video: Import animated models from Blender 2.6 to JME3</a></div>
</li>
<li class="level2"><div class="li"> <a href="http://www.youtube.com/watch?v=NdjC9sCRV0s" class="urlextern" title="http://www.youtube.com/watch?v=NdjC9sCRV0s" rel="nofollow">Video: Creating and Exporting OgreXML Animations from Blender 2.61 to JME3</a></div>
</li>
<li class="level2"><div class="li"> <a href="https://docs.google.com/fileview?id=0B9hhZie2D-fENDBlZDU5MzgtNzlkYi00YmQzLTliNTQtNzZhYTJhYjEzNWNk&amp;hl=en" class="urlextern" title="https://docs.google.com/fileview?id=0B9hhZie2D-fENDBlZDU5MzgtNzlkYi00YmQzLTliNTQtNzZhYTJhYjEzNWNk&amp;hl=en" rel="nofollow">Scene Workflow:</a></div>
</li>
</ul>
</li>
</ul>

<p>
Create jme3 compatible racing tracks in blender
* <a href="http://www.youtube.com/watch?v=3481ueuDJwQ&amp;feature=youtu.be" class="urlextern" title="http://www.youtube.com/watch?v=3481ueuDJwQ&amp;feature=youtu.be" rel="nofollow">Video: Create jme3 compatible models in blender</a>
</p>

<p>
Exporting OgreXML scenes from Blender to JME3
</p>
<ul>
<li class="level1"><div class="li"> <a href="https://docs.google.com/leaf?id=0B9hhZie2D-fEYmRkMTYwN2YtMzQ0My00NTM4LThhOTYtZTk1MTRlYTNjYTc3&amp;hl=en" class="urlextern" title="https://docs.google.com/leaf?id=0B9hhZie2D-fEYmRkMTYwN2YtMzQ0My00NTM4LThhOTYtZTk1MTRlYTNjYTc3&amp;hl=en" rel="nofollow">Animation Workflow: Create Animated UV-Mapped OgreXML Models in Blender, and use them in JME3</a></div>
</li>
<li class="level2"><div class="li"> <a href="http://www.youtube.com/watch?v=IDHMWsu_PqA" class="urlextern" title="http://www.youtube.com/watch?v=IDHMWsu_PqA" rel="nofollow">Video: Creating Worlds with Instances in Blender</a></div>
</li>
<li class="level2"><div class="li"> <a href="/jme3/advanced/ogrecompatibility.html" class="wikilink1" title="jme3:advanced:ogrecompatibility">OgreCompatibility</a></div>
</li>
</ul>

<p>
<strong>材质、光影</strong>
</p>
<ul>
<li class="level1"><div class="li"> <a href="/jme3/intermediate/how_to_use_materials.html" class="wikilink1" title="jme3:intermediate:how_to_use_materials">How to Use Materials</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/advanced/j3m_material_files.html" class="wikilink1" title="jme3:advanced:j3m_material_files">Creating .j3m Materials</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/advanced/material_definitions.html" class="wikilink1" title="jme3:advanced:material_definitions">How to Use Material Definitions (.j3md)</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/advanced/materials_overview.html" class="wikilink1" title="jme3:advanced:materials_overview">All Material Definition Properties</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/advanced/anisotropic_filtering.html" class="wikilink1" title="jme3:advanced:anisotropic_filtering">Anisotropic Filtering for Textures</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/advanced/light_and_shadow.html" class="wikilink1" title="jme3:advanced:light_and_shadow">Light and Shadow</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/advanced/jme3_shaders.html" class="wikilink1" title="jme3:advanced:jme3_shaders">About JME3 and Shaders</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/advanced/jme3_shadernodes.html" class="wikilink1" title="jme3:advanced:jme3_shadernodes">Shader Node System</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/advanced/jme3_srgbpipeline.html" class="wikilink1" title="jme3:advanced:jme3_srgbpipeline">Gamma correction or sRGB pipeline</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/shader_video_tutorials.html" class="wikilink1" title="jme3:shader_video_tutorials">Videos: jME3 introduction to shaders video tutorial series</a></div>
</li>
<li class="level1"><div class="li"> <a href="http://www.youtube.com/watch?v=IuEMUFwdheE" class="urlextern" title="http://www.youtube.com/watch?v=IuEMUFwdheE" rel="nofollow">Video: jME3 Material with Alpha Channel</a></div>
</li>
</ul>

<p>
<strong>物理集成</strong>
</p>
<ul>
<li class="level1"><div class="li"> <a href="/jme3/advanced/physics.html" class="wikilink1" title="jme3:advanced:physics">Physics: Gravity, Collisions, Forces</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/advanced/bullet_multithreading.html" class="wikilink1" title="jme3:advanced:bullet_multithreading">Multi-Threaded Physics</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/advanced/physics_listeners.html" class="wikilink1" title="jme3:advanced:physics_listeners">Physics Listeners and Collision Detection</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/advanced/hinges_and_joints.html" class="wikilink1" title="jme3:advanced:hinges_and_joints">Hinges and Joints</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/advanced/walking_character.html" class="wikilink1" title="jme3:advanced:walking_character">Walking Character</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/advanced/ragdoll.html" class="wikilink1" title="jme3:advanced:ragdoll">Ragdoll</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/advanced/vehicles.html" class="wikilink1" title="jme3:advanced:vehicles">Vehicles</a></div>
</li>
<li class="level1"><div class="li"> <a href="/doku.php/jme3:advanced:ray_and_sweep_tests" class="wikilink2" title="jme3:advanced:ray_and_sweep_tests" rel="nofollow">Physics Rays and Sweep Tests</a></div>
</li>
<li class="level1"><div class="li"> <a href="http://www.youtube.com/watch?v=yS9a9o4WzL8" class="urlextern" title="http://www.youtube.com/watch?v=yS9a9o4WzL8" rel="nofollow">Video: Mesh Tool &amp; Physics Editor</a></div>
</li>
</ul>

<p>
<strong>音频和视频</strong>
</p>
<ul>
<li class="level1"><div class="li"> <a href="/jme3/advanced/audio.html" class="wikilink1" title="jme3:advanced:audio">Audio: Playing Sounds</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/advanced/audio_environment_presets.html" class="wikilink1" title="jme3:advanced:audio_environment_presets">Audio Environment Presets</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/advanced/video.html" class="wikilink1" title="jme3:advanced:video">Video: Playing Clips</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/advanced/screenshots.html" class="wikilink1" title="jme3:advanced:screenshots">Capture Screenshots</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/advanced/capture_audio_video_to_a_file.html" class="wikilink1" title="jme3:advanced:capture_audio_video_to_a_file">Capture Audio/Video to a File</a></div>
</li>
</ul>

<p>
<strong>后置处理过滤器与特效</strong>
</p>
<ul>
<li class="level1"><div class="li"> <a href="/jme3/advanced/effects_overview.html" class="wikilink1" title="jme3:advanced:effects_overview">Effects and Filters Overview</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/advanced/bloom_and_glow.html" class="wikilink1" title="jme3:advanced:bloom_and_glow">Bloom and Glow</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/advanced/particle_emitters.html" class="wikilink1" title="jme3:advanced:particle_emitters">Particle Emitters</a></div>
</li>
</ul>

<p>
<strong>地形</strong>
</p>
<ul>
<li class="level1"><div class="li"> <a href="/jme3/advanced/sky.html" class="wikilink1" title="jme3:advanced:sky">Sky</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/advanced/terrain.html" class="wikilink1" title="jme3:advanced:terrain">Terrain (TerraMonkey)</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/advanced/endless_terraingrid.html" class="wikilink1" title="jme3:advanced:endless_terraingrid">Endless Terrain (TerrainGrid)</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/advanced/terrain_collision.html" class="wikilink1" title="jme3:advanced:terrain_collision">Terrain Collision</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/contributions/cubes.html" class="wikilink1" title="jme3:contributions:cubes">Cubes - A Block World Framework</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/advanced/water.html" class="wikilink1" title="jme3:advanced:water">Simple Water</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/advanced/post-processor_water.html" class="wikilink1" title="jme3:advanced:post-processor_water">Post-Processor Water (SeaMonkey)</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/contributions/vegetationsystem.html" class="wikilink1" title="jme3:contributions:vegetationsystem">Vegetation System</a></div>
</li>
</ul>

<p>
<strong>人工智能(AI)</strong>
</p>
<ul>
<li class="level1"><div class="li"> <a href="/jme3/advanced/recast.html" class="wikilink1" title="jme3:advanced:recast">Recast Navigation</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/advanced/building_recast.html" class="wikilink1" title="jme3:advanced:building_recast">Updating and building Recast Native Bindings</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/advanced/monkey_brains.html" class="wikilink1" title="jme3:advanced:monkey_brains">Monkey Brains</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/advanced/steer_behaviours.html" class="wikilink1" title="jme3:advanced:steer_behaviours">Steer Behaviours</a></div>
</li>
</ul>

<p>
<strong>多人联网游戏</strong>
</p>
<ul>
<li class="level1"><div class="li"> <a href="/jme3/advanced/networking.html" class="wikilink1" title="jme3:advanced:networking">Multiplayer Networking (SpiderMonkey)</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/advanced/headless_server.html" class="wikilink1" title="jme3:advanced:headless_server">Headless Server</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/advanced/monkey_zone.html" class="wikilink1" title="jme3:advanced:monkey_zone">Monkey Zone: Multi-Player Demo Code</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/advanced/open_game_finder.html" class="wikilink1" title="jme3:advanced:open_game_finder">Open Game Finder</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/advanced/networking_video_tutorials.html" class="wikilink1" title="jme3:advanced:networking_video_tutorials">Videos: jME3 networking video tutorial series</a> </div>
</li>
</ul>

<p>
<strong>实体系统</strong>
</p>
<ul>
<li class="level1"><div class="li"> <a href="/jme3/contributions/entitysystem.html" class="wikilink1" title="jme3:contributions:entitysystem"> The Zay-ES Entity System</a></div>
</li>
</ul>

<p>
<strong>摄像机</strong>
</p>
<ul>
<li class="level1"><div class="li"> <a href="/jme3/advanced/camera.html" class="wikilink1" title="jme3:advanced:camera">Camera</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/advanced/making_the_camera_follow_a_character.html" class="wikilink1" title="jme3:advanced:making_the_camera_follow_a_character">Making the Camera Follow a Character</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/advanced/remote-controlling_the_camera.html" class="wikilink1" title="jme3:advanced:remote-controlling_the_camera">Remote-Controlling the Camera</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/advanced/multiple_camera_views.html" class="wikilink1" title="jme3:advanced:multiple_camera_views">Multiple Camera Views</a> </div>
</li>
</ul>

<p>
<strong>用户交互</strong>
</p>
<ul>
<li class="level1"><div class="li"> <a href="/jme3/advanced/input_handling.html" class="wikilink1" title="jme3:advanced:input_handling">Input Handling</a></div>
<ul>
<li class="level2"><div class="li"> <a href="https://github.com/jMonkeyEngine-Contributions/Lemur/wiki/Modules" class="urlextern" title="https://github.com/jMonkeyEngine-Contributions/Lemur/wiki/Modules" rel="nofollow">Lemur Scene Graph Tools</a></div>
<ul>
<li class="level3"><div class="li"> <a href="http://hub.jmonkeyengine.org/t/lemur-gems-1-inputmapper-based-camera-movement/28703" class="urlextern" title="http://hub.jmonkeyengine.org/t/lemur-gems-1-inputmapper-based-camera-movement/28703" rel="nofollow">Lemur Gems #1 - Input mapper based camera movement. </a></div>
</li>
<li class="level3"><div class="li"> <a href="http://hub.jmonkeyengine.org/t/lemur-gems-2-inputmapper-delegates/28710" class="urlextern" title="http://hub.jmonkeyengine.org/t/lemur-gems-2-inputmapper-delegates/28710" rel="nofollow">Lemur Gems #2 - Input mapper delegates</a></div>
</li>
<li class="level3"><div class="li"> <a href="http://hub.jmonkeyengine.org/t/lemur-gems-3-scene-picking/28713" class="urlextern" title="http://hub.jmonkeyengine.org/t/lemur-gems-3-scene-picking/28713" rel="nofollow">Lemur Gems #3 - Scene picking</a></div>
</li>
</ul>
</li>
</ul>
</li>
<li class="level1"><div class="li"> <a href="/jme3/advanced/combo_moves.html" class="wikilink1" title="jme3:advanced:combo_moves">Combo Moves</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/advanced/mouse_picking.html" class="wikilink1" title="jme3:advanced:mouse_picking">Mouse Picking: Click to Select</a></div>
</li>
</ul>

<p>
<strong>图形用户界面(<abbr title="Graphical User Interface">GUI</abbr>)</strong>
</p>
<ul>
<li class="level1"><div class="li"> <a href="https://github.com/jMonkeyEngine-Contributions/Lemur" class="urlextern" title="https://github.com/jMonkeyEngine-Contributions/Lemur" rel="nofollow">Lemur - a native jME3 GUI library with scene graph tools</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/contributions/tonegodgui.html" class="wikilink1" title="jme3:contributions:tonegodgui">tonegodGUI - a native jME3 GUI library</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/advanced/nifty_gui.html" class="wikilink1" title="jme3:advanced:nifty_gui">Nifty GUI - JME3 Integration Tutorial</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/advanced/nifty_gui_best_practices.html" class="wikilink1" title="jme3:advanced:nifty_gui_best_practices">Nifty GUI - Best Practices</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/advanced/nifty_gui_scenarios.html" class="wikilink1" title="jme3:advanced:nifty_gui_scenarios">Nifty GUI Scenarios (Load Screen etc)</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/advanced/hud.html" class="wikilink1" title="jme3:advanced:hud">Head-Up Display (HUD)</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/advanced/localization.html" class="wikilink1" title="jme3:advanced:localization">Localization</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/advanced/swing_canvas.html" class="wikilink1" title="jme3:advanced:swing_canvas">Swing Canvas</a></div>
</li>
</ul>

<p>
<strong>自定义渲染</strong>
</p>
<ul>
<li class="level1"><div class="li"> <a href="/doku.php/jme3:advanced:jme3_forwardrendering" class="wikilink2" title="jme3:advanced:jme3_forwardrendering" rel="nofollow">Forward Rendering process</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/advanced/jme3_renderbuckets.html" class="wikilink1" title="jme3:advanced:jme3_renderbuckets">Render Buckets</a></div>
</li>
</ul>

<p>
<strong>自定义工具</strong>
</p>
<ul>
<li class="level1"><div class="li"> <a href="/jme3/tools/navigation.html" class="wikilink1" title="jme3:tools:navigation">Mercator Projection Tool (Marine Navigation)</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/tools/charts.html" class="wikilink1" title="jme3:tools:charts">Visualizing Maps in JME3 (Marine Charts)</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/advanced/atom_framework.html" class="wikilink1" title="jme3:advanced:atom_framework">Atom framework. Mash-up of other plugins</a></div>
</li>
</ul>

<p>
<strong>日志与调试</strong>
</p>
<ul>
<li class="level1"><div class="li"> <a href="/jme3/advanced/logging.html" class="wikilink1" title="jme3:advanced:logging">Logging</a></div>
</li>
<li class="level1"><div class="li"> <a href="/sdk/log_files.html" class="wikilink1" title="sdk:log_files">Log Files</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/advanced/read_graphic_card_capabilites.html" class="wikilink1" title="jme3:advanced:read_graphic_card_capabilites">Read Graphic Card Capabilites</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/advanced/debugging.html" class="wikilink1" title="jme3:advanced:debugging">Debugging with Wireframes</a></div>
</li>
</ul>

<p>
<strong>Android项目开发</strong>
</p>
<ul>
<li class="level1"><div class="li"> <a href="/jme3/advanced/android.html" class="wikilink1" title="jme3:advanced:android">Android Project Cheat Sheet</a></div>
</li>
</ul>

<p>
<strong>项目部署</strong>
</p>
<ul>
<li class="level1"><div class="li"> <a href="/jme3/android.html" class="wikilink1" title="jme3:android">Android</a></div>
</li>
<li class="level1"><div class="li"> <a href="/sdk/application_deployment.html" class="wikilink1" title="sdk:application_deployment">Application Deployment (using jMonkeyEngine SDK)</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/webstart.html" class="wikilink1" title="jme3:webstart">WebStart Deployment (without jMonkeyEngine SDK)</a></div>
</li>
</ul>

<p>
<strong>脚本</strong>
</p>
<ul>
<li class="level1"><div class="li"> <a href="/jme3/scripting.html" class="wikilink1" title="jme3:scripting"> Groovy 脚本语言</a></div>
</li>
</ul>

<p>
<strong>虚拟现实&amp;模拟器</strong>
</p>
<ul>
<li class="level1"><div class="li"> <a href="/jme3/virtualreality.html" class="wikilink1" title="jme3:virtualreality"> Virtual Reality. OpenCV &amp; JavaCV</a></div>
</li>
</ul>

<p>
<strong>jMonkey User Contributions</strong>
</p>
<ul>
<li class="level1"><div class="li"> <a href="/jme3/contributions.html" class="wikilink1" title="jme3:contributions"> Contributions - User made utilities to add functionality to the engine.</a></div>
</li>
</ul>

<p>
<strong>Sample Projects</strong>
</p>
<ul>
<li class="level1"><div class="li"> <a href="/sdk/sample_code.html" class="wikilink1" title="sdk:sample_code">JmeTests</a> – The “official” sample project JmeTests.</div>
</li>
<li class="level1"><div class="li"> <a href="http://code.google.com/p/jmonkeyengine/source/browse/BookSamples/#BookSamples%2Fsrc" class="urlextern" title="http://code.google.com/p/jmonkeyengine/source/browse/BookSamples/#BookSamples%2Fsrc" rel="nofollow">BookSamples</a> – Some more jME3 code samples</div>
</li>
</ul>

<p>
These code examples are not supported by the core team and we cannot guarantee their correctness:
</p>
<ul>
<li class="level1"><div class="li"> <a href="/jme3/user_examples_project.html" class="wikilink1" title="jme3:user_examples_project">User Examples Project</a> – The jME3 users examples project.</div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/shaderblow_project.html" class="wikilink1" title="jme3:shaderblow_project">ShaderBlow Project</a> – The jME3 users shaders project.</div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/rise_of_mutants_project.html" class="wikilink1" title="jme3:rise_of_mutants_project">Rise of Mutants Project</a> – Rise of Mutants Project by BigBoots Team.</div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/atomixtuts.html" class="wikilink1" title="jme3:atomixtuts">atomixtuts</a> – Atomix Tutorial Series</div>
</li>
<li class="level1"><div class="li"> <a href="http://code.google.com/p/street-rally-3d/source/browse/#svn%2Ftrunk%2Fsrc%2Fsr3d" class="urlextern" title="http://code.google.com/p/street-rally-3d/source/browse/#svn%2Ftrunk%2Fsrc%2Fsr3d" rel="nofollow">Street rally 3d source code</a> – A racing game programmed by rhymez.</div>
</li>
</ul>

</div>
<!-- EDIT4 SECTION "进阶教程" [5125-14058] -->
<h2 class="sectionedit5" id="sdk_documentation">SDK Documentation</h2>
<div class="level2">

<p>
<a href="/resources/sdk-jmonkeyplatform-docu-2.png" class="media" title="sdk:jmonkeyplatform-docu-2.png"><img src="/resources/sdk-jmonkeyplatform-docu-2.png" class="mediaright" alt="" width="420" height="300" /></a>
</p>

<p>
The <a href="/sdk.html" class="wikilink1" title="sdk">jMonkeyEngine SDK</a> is our recommended game development environment.
</p>
<ul>
<li class="level1"><div class="li"> <a href="/sdk/comic.html" class="wikilink1" title="sdk:comic">jMonkeyEngine SDK - the Comic</a></div>
</li>
<li class="level1"><div class="li"> <a href="/sdk.html" class="wikilink1" title="sdk">SDK Documentation (All editors, plugins, etc)</a></div>
</li>
</ul>

<p>
Here are some videos of how the jMonkeyEngine SDK makes your development team's life easier:
</p>
<ul>
<li class="level1"><div class="li"> <a href="http://www.youtube.com/watch?v=nL7woH40i5c" class="urlextern" title="http://www.youtube.com/watch?v=nL7woH40i5c" rel="nofollow">Video: Importing Models</a></div>
</li>
<li class="level1"><div class="li"> <a href="http://www.youtube.com/watch?v=ntPAmtsQ6eM" class="urlextern" title="http://www.youtube.com/watch?v=ntPAmtsQ6eM" rel="nofollow">Video: Scene Composing</a></div>
</li>
<li class="level1"><div class="li"> <a href="http://www.youtube.com/watch?v=DUmgAjiNzhY" class="urlextern" title="http://www.youtube.com/watch?v=DUmgAjiNzhY" rel="nofollow">Video: Dragging&amp;Dropping Nodes</a></div>
</li>
<li class="level1"><div class="li"> <a href="http://www.youtube.com/watch?v=Feu3-mrpolc" class="urlextern" title="http://www.youtube.com/watch?v=Feu3-mrpolc" rel="nofollow">Video: Working with Materials</a></div>
</li>
<li class="level1"><div class="li"> <a href="http://www.youtube.com/watch?v=oZnssg8TBWQ" class="urlextern" title="http://www.youtube.com/watch?v=oZnssg8TBWQ" rel="nofollow">Video: WebStart Deployment</a></div>
</li>
<li class="level1"><div class="li"> <a href="http://www.youtube.com/watch?v=MNDiZ9YHIpM" class="urlextern" title="http://www.youtube.com/watch?v=MNDiZ9YHIpM" rel="nofollow">Video: Custom Controls</a></div>
</li>
<li class="level1"><div class="li"> Read the <a href="/sdk.html" class="wikilink1" title="sdk">SDK documentation</a> for details.</div>
</li>
</ul>

</div>
<!-- EDIT5 SECTION "SDK Documentation" [14059-14936] -->
<h2 class="sectionedit6" id="下载和安装jme3">下载和安装JME3</h2>
<div class="level2">
<ul>
<li class="level1"><div class="li"> <a href="/bsd_license.html" class="wikilink1" title="bsd_license">Use jMonkeyEngine 3 for free under the BSD License</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/requirements.html" class="wikilink1" title="jme3:requirements">Software and hardware requirements</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/features.html" class="wikilink1" title="jme3:features">All Supported Features</a></div>
</li>
<li class="level1"><div class="li"> <a href="http://jmonkeyengine.org/wiki/doku.php#Installation" class="urlextern" title="http://jmonkeyengine.org/wiki/doku.php#Installation" rel="nofollow">Download jMonkeyEngine 3 SDK</a></div>
</li>
</ul>

</div>
<!-- EDIT6 SECTION "下载和安装JME3" [14937-15236] -->
<h2 class="sectionedit7" id="feedback">Feedback</h2>
<div class="level2">

<p>
jME3 is in development; if a tutorial doesn't work as expected, try using the latest daily build. If that doesn't “fix it” then:
</p>
<ul>
<li class="level1"><div class="li"> <a href="http://code.google.com/p/jmonkeyengine/issues/list?can=2&amp;q=label:Component-Docs" class="urlextern" title="http://code.google.com/p/jmonkeyengine/issues/list?can=2&amp;q=label:Component-Docs" rel="nofollow">Report a Documentation Task</a></div>
</li>
<li class="level1"><div class="li"> <a href="http://jmonkeyengine.org/wiki/doku.php/report_bugs" class="urlextern" title="http://jmonkeyengine.org/wiki/doku.php/report_bugs" rel="nofollow">Report a Bug</a></div>
</li>
<li class="level1"><div class="li"> <a href="http://jmonkeyengine.org/forums" class="urlextern" title="http://jmonkeyengine.org/forums" rel="nofollow">Ask (and Answer!) Questions on the Forum</a></div>
</li>
</ul>
<div class="tags"><span>
	<a href="/tag/documentation.html" class="wikilink1" title="tag:documentation" rel="tag">documentation</a>,
	<a href="/tag/intro.html" class="wikilink1" title="tag:intro" rel="tag">intro</a>,
	<a href="/tag/intermediate.html" class="wikilink1" title="tag:intermediate" rel="tag">intermediate</a>,
	<a href="/tag/about.html" class="wikilink1" title="tag:about" rel="tag">about</a>
</span></div>

</div>
<!-- EDIT7 SECTION "Feedback" [15237-] -->
