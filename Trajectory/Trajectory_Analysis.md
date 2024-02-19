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

These trajectory files can be visualized using a software such as ChimeraX with the appropriate initial configuration file (`step3_input.gro` for surface-free and `step5_input.gro` for surface).