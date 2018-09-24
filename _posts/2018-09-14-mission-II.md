---
layout: post-left
title: "AdamsSat"
date: 2018-09-14 00:00:00
permalink: /missions/adamssat.html
category: missions adams attitude-control optimal-control convex-optimization optimal-spacecraft-attitude-motion
icon: fa-sync
---
<section class="wrapper style2 container">
	<header> <h2> Mission Objectives </h2> </header>
	<p> Named after the second tallest mountain in our state, our second mission will develop an advanced guidance, navigation and control (GNC) subsystem capable of reorienting the spacecraft while satisfying key constraints. This mission will also provide earth-imaging capability, with stringent pointing requirements allowing us to image specified regions of the earth. <br/><br/>
	Using convex optimization, time-optimal control torques are computed that guarantee the sun does not leave the field of view of on-board sun sensors, while ensuring on-board cameras are not subject to direct sunlight. </p>
</section>
<!-- One -->
<section class="wrapper style4">		
	<header><h2> Guidance Navigation and Control </h2></header>
			<p> The primary payload of AdamsSat is an experimental GNC system capable of reorienting the spacecraft while guaranteeing hard pointing constraints and in a time-optimal fashion.</p>			
	<div class="row">
		<div class="4u">
		<!-- Sidebar -->
			<div class="sidebar">
				<section>
					<header>
					<h3>Attitude Constraints</h3>
					</header>
					<p>The GNC system guarantees that attitude maneuvers can be accomplished with the sun in the field of view of a sun-sensor, while not in the field of view of our on-board camera. </p>
<!-- 					<footer>
					<ul class="buttons">
						<li><a href="#" class="button small">Learn More</a></li>
					</ul>
					</footer> -->
				</section>
				<section>
				<a href="#" class="image featured"><img src="/images/pic01.jpg" alt="" /></a>
					<header>
					<h3>Optimal Control and Convex Optimization</h3>
					</header>
					<p>We combine elements of optimal control theory and convex optimization to compute actuator commands that will satisfy mission-level constraints. These are implemented in the on-board flight software.</p>
				</section>
			</div>
		</div>
		<div class="8u skel-cell-important">								
		<!-- Content -->
			<div class="content">
				<section>
					<a href="#" class="imagenb featured"><img src="/images/tikz_cubesat_1.jpg" alt="" /></a>
						<header>
						<h3>Constrained Attitude Control</h3>
						</header>
						<p>Use this section to give some details on our implementation, problem statements, etc. Figure out how to put latex equations in here.</p>
						<p>Make sure to provide references and links to the works. </p>
				</section>
			</div>
		</div>
	</div>			
	<div class="row">
		<div class="4u">						
			<section>
				<center>
					<header>
						<h3>Software Implementation</h3>
					</header>
					<p>See the open source GNC code based in Matlab/Simulink.</p>
					<footer>
						<ul class="buttons">
						<li><a href="https://github.com/tpreynolds/uw_cubesat_adcs" class="button small special">Visit GitHub</a></li>
						</ul>
					</footer>
				</center>	
			</section>					
		</div>
		<div class="4u">						
			<section>
				<center>
					<header>
						<h3>System Validation</h3>
					</header>
					<p>Read about our experimental GNC system validation</p>
					<footer>
						<ul class="buttons">
							<li><a href="#" class="button small special">See the Process</a></li>
						</ul>
					</footer>
				</center>
			</section>				
		</div>
		<div class="4u">						
			<section>
				<center>
					<header>
						<h3>Publications</h3>
					</header>
						<p>See our publications to read more on this topic.</p>
					<footer>
						<ul class="buttons">
							<li><a href="/publications.html" class="button small special">Read More</a></li>
						</ul>
					</footer>
				</center>
			</section>						
		</div>
	</div>		
</section>
<!-- Other Subsystems -->
<section class="wrapper style4 container">
	<header> <h2> Power System </h2> </header>
	<p> Placeholder for description of power system </p>
</section>

<section class="wrapper style4 container">
	<header> <h2> Communication System </h2> </header>
	<p> Placeholder for description of communication system </p>
</section>

<section class="wrapper style4 container">
	<header> <h2> Structural and Thermal System </h2> </header>
	<p> Placeholder for description of structure/thermal system </p>
</section>

<section id="cta">			
	<header>
		<h2><strong> Project Partners </strong></h2>
		<p>Put logos of folks that partnered with us on this specific project.</p>
	</header>	
</section>	


