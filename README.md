The provided files are intended to be used as inputs to the LINES model to
identify degrees of freedom in a molecular coordinate in the form of a
reaction coordinate such that sampling across energy barriers is accelerated.

==============================================================
Each of the following files contain important information for running simulations:

charmm36-jul2021.ff => Forcefield used to capture atomic interations of the protein system.
toppar => Non-standard forcefield parameters provided by CHARMM-GUI.
topol.top => Topology of interactions for the system.
md_config_start.gro => Initial structure file for TIM3-P26 system.
md_config_start.cpt => Initial checkpoint file for TIM3-P26 system that contains the velocities of the atoms.
md.mdp => Molecular dynamics parameters inputted in GROMACS software.
MCs_list.dat => List of the molecular coordinates defined with PLUMED nomenclature used by LINES.
biasing_potential.dat => Biasing potential used to enhance sampling in MD simulations.

============================================================

To run a simulation, GROMACS and PLUMED software must be installed and added to current PATH variable in bash environment.
Additionally, GROMACS must be patched with PLUMED during installation. An example of running a biased MD simulation could be
performed as follows:

gmx grompp -f md.mdp -c md_config_start.gro -t md_config_start.cpt -p topol.top -o trajectory.tpr

gmx mdrun -f trajectory.tpr -plumed biasing_potential.dat

==================================================================
The PLUMED biasing potential file will automatically save the biasing potential and each molecular coordinate
such that the MCs can be used to train the normalizing flow model and identify a reaction coordinate.

