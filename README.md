# Dynamics-Of-A-Monocylinder-Engine-In-Salome-Meca
Simulating dynamics of a monocylinder engine is a tedious task if no multi-node cluster is at hand. It's well known, that even engine manufacturers and engine engineering companies tend to avoid this task and rather simulate static cases via applying substitution forces for the body forces of the crank train. However, if, nevertheless dynamics is indeed simulated, there is dedicated highly optimized FEA software for this. But what can you do, if you do not have 100k $ at hand for such a license? This repository tries to show that design and simulation is possible with only free and open-source software. The first image shows the parts we want to simualte. The whole design was done in FreeCAD 1.0 over the course of a few hours. It features a reasonably real piston with diameter 100mm, which was designed with an old (mid 2000s) formula one piston in mind. Stroke is 100mm, the dummy crankshaft does not feature any counterbalance weights:

![Bildschirmfoto vom 2024-12-03 14-13-49](https://github.com/user-attachments/assets/c129836e-a63b-4ed8-b071-8631eb0e7c8a)


