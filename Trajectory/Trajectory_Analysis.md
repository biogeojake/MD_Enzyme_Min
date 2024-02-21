## Concatenating Trajectories

After completing data production for the MD simulations, the individual trajectories will need to be concatenated using `gmx trjcat` to create a continuous trajectory.

For the surface-free simulations,

```{bash}
gmx_mpi trjcat -f step5_*.xtc -o traj_100ns.xtc -settime -tu ns
```

For the surface simulations,

```{bash}
gmx_mpi trjcat -f step7_*.trr -o traj_100ns.xtc -settime -tu ns
```

To clean up the trajectory to make sure the enzyme is centered in the simulation and does not cross the periodic boundary, `gmx trjconv` was utilized in multiple steps.

For surface-free simulations,

```{bash}
gmx_mpi trjconv -s step4.0_minimization.tpr -f traj_100ns.xtc -o traj_100ns_noPBC.xtc -pbc mol -center
# (Select 1-Protein and 0-System to re-center)

gmx_mpi trjconv -s step4.0_minimization.tpr -f traj_100ns_noPBC.xtc -o traj_100ns_atom.xtc -pbc atom
# (Select 0-System)
```

For surface simulations,

```{bash}
gmx_mpi trjconv -s step6.0_minimization.tpr -f traj_100ns.xtc -o traj_100ns_noPBC.xtc -pbc mol -center
# (Select 1-Protein and 0-System to re-center)

gmx_mpi trjconv -s step6.0_minimization.tpr -f traj_100ns_noPBC.xtc -o traj_100ns_atom.xtc -pbc atom
# (Select 0-System)
```

The `traj_100ns_noPBC.xtc` trajectory file was used for RMSD and Rg analysis. The `traj_100ns_atom.xtc` was used for trajectory visualization.

These trajectory files can be visualized using a software such as ChimeraX with the appropriate initial configuration file (`step3_input.gro` for surface-free and `step5_input.gro` for surface).
