# Dynamics-Of-A-Monocylinder-Engine-In-Salome-Meca
Simulating dynamics of a monocylinder engine is a tedious task if no multi-node cluster is at hand. It's well known, that even engine manufacturers and engine engineering companies tend to avoid this task and rather simulate static cases via applying substitution forces for the body forces of the crank train. However, if, nevertheless dynamics is indeed simulated, there is dedicated highly optimized FEA software for this. But what can you do, if you do not have 100k $ at hand for such a license? This repository tries to show that design and simulation is absolutely possible with only free and open-source software. The first images show the parts we want to simulate. The whole design was done in FreeCAD 1.0 over the course of a few hours. It features a reasonably real piston with diameter 100mm, which was designed with an old (mid 2000s) formula one piston in mind (it is a bit higher though :-) ). Stroke is 100mm, the dummy crankshaft does not feature any counterbalance weights:

view 1           |  view 2
:-------------------------:|:-------------------------:
![Bildschirmfoto vom 2024-12-03 20-52-12](https://github.com/user-attachments/assets/8eb5331b-c6bb-43aa-9c61-4c46dd7e4776) | ![Bildschirmfoto vom 2024-12-03 20-52-42](https://github.com/user-attachments/assets/05dd2957-b8a2-4613-913a-5ce4a6c5dff0)

For simplification, some features are not included: Piston ring slots, valve pockets, connecting rod bolts (+ necessary features on the rod), cylinder liner. For the simulation, the crank is turned 80° to put it in a positon 10° after TDC. As is visible in the attached command file, a maximum pressure or 120bar is applied to the piston surface in a 'smoother' profile. Two full rotations are simulated, because the total time needed is not known before the simulation, there is some leeway in the timestep list, just the final time must be given. If needed the simulation can be continued for a certain time by adding an additional stage and taking the already computed result as initial state (ETAT_INIT). We need ~13.1ms for one full rotation, this equates to about 4580rpm of the engine. There is no friction in all the bearings, nevertheless, the model absolutely allows for this. However, the calculation time may increase a lot. The materials are modeled with ELAS_FO and ECRO_LINE, a simple elasto linear plastic model. Surprisingly, the performance with this model is quite good. 
From the computed data, Von Mises stresses are computed in each frame of the simulation (every 0.2ms), a video of these results is included. The animation was done in Paraview completely, the video was concatenated with oggCat (contained in oggvideotools in Ubuntu-repos). Clearly, in the video we can see some bending of the piston pin during ignition, this is absolutly happening in high performance engines. High end piston designs even account for that. Don't forget to increase the speed of the video in VLC by pressing the '+' button.
Some technical stuff: this simulation took 52h on a not-so-up-to-date workstation, peak memory usage was ~110GB. Post processing the results and computing Von Mises stresses needed in excess of 300GB of memory. If you are doing HPC on a large machine in the Top500 list, this would take maybe 1-10 minutes, tops. 
Below a Von Mises still image at 1.6ms is shown, it corresponds to peak forces on the assembly: 

![vmis_1 6ms](https://github.com/user-attachments/assets/8a72fd17-6530-4889-bfa1-79b8c9238274)

You may conclude that the mesh resolution is not enough comparable to a static (or pseudo-static) analysis of such an assembly and perhaps you are right. But for studying dynamics this can be abolutely sufficient, even more so considering the hardware needs and the fact that only FOSS software was used. For example, we can easily extract basic data like velocity and acceleration on a point in the piston crown (top of piston):

![Bildschirmfoto vom 2024-12-10 12-50-45](https://github.com/user-attachments/assets/989ce17f-76ad-4311-97b3-a45dc54ca637)

As the assembly starts from zero velocity, we also find that in the point data. The following two cycles are almost perfect (a bit slanted) sines with only minor fluctuations. Let's take a look at the associated acceleration in the same point:

![Bildschirmfoto vom 2024-12-10 12-39-42](https://github.com/user-attachments/assets/fe399487-5174-433d-af7a-a694884aa5a9)
In the beginning, the acceleration is a bit shaky, but transients seem to tone down and give a nice curve over the two cycles (units are mm/s²).


emefff@gmx.at
