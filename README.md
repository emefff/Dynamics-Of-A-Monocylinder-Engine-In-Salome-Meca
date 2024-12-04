# Dynamics-Of-A-Monocylinder-Engine-In-Salome-Meca
Simulating dynamics of a monocylinder engine is a tedious task if no multi-node cluster is at hand. It's well known, that even engine manufacturers and engine engineering companies tend to avoid this task and rather simulate static cases via applying substitution forces for the body forces of the crank train. However, if, nevertheless dynamics is indeed simulated, there is dedicated highly optimized FEA software for this. But what can you do, if you do not have 100k $ at hand for such a license? This repository tries to show that design and simulation is absolutely possible with only free and open-source software. The first image shows the parts we want to simulate. The whole design was done in FreeCAD 1.0 over the course of a few hours. It features a reasonably real piston with diameter 100mm, which was designed with an old (mid 2000s) formula one piston in mind. Stroke is 100mm, the dummy crankshaft does not feature any counterbalance weights:
view 1           |  view 2
:-------------------------:|:-------------------------:
![Bildschirmfoto vom 2024-12-03 20-52-12](https://github.com/user-attachments/assets/8eb5331b-c6bb-43aa-9c61-4c46dd7e4776) |   ![Bildschirmfoto vom 2024-12-03 20-52-42](https://github.com/user-attachments/assets/05dd2957-b8a2-4613-913a-5ce4a6c5dff0)
               

For simplification, some features are not included: Piston ring slots, valve pockets, connecting rod bolts (+ necessary features on the rod), cylinder liner. For the simulation, the crank is turned 80° to put it in a positon 10° after TDC. As is visible in the attached command file, a maximum pressure or 120bar is applied to the piston surface in a 'smoother' profile. One full rotation is simulated, because the full time needed is not known before the simulation, there is some leeway in the timestep list, just the final time must be given. If needed the simulation can be continued for a certain time by adding an additional stage and taking the already computed result as initial state (ETAT_INIT). We need ~25ms for one full rotation, this equates to about 2400rmp of the engine. There is no friction in all the bearings, nevertheless, the model absolutely allows for this. However, the calculation time may increase a lot. The materials are modeled with ELAS_FO and ECRO_LINE, a simple elasto linear plastic model. Surprisingly, the performance with this model is quite good. 
