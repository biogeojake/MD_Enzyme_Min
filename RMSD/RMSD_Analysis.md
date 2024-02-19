## Calculating RMSD for a Single System

The root-mean-square-deviation (RMSD) of the enzyme backbone from the predicted ColabFold structure was calculated using the `gmx rms` function in GROMACS. The trajectory was manipulated to perform a best fit of the backbone to the reference structure present within the initial topology file.

For surface-free simulations, the trajectory was manipulated as such:

```{bash}
gmx_mpi trjconv -s step4.0_minimization.tpr -f traj_100ns_noPBC.xtc -o traj_100ns_align.xtc -fit rot+trans
# (Select 4-Backbone for LSQ and 4-Backbone for output)

gmx_mpi convert-tpr -s step4.0_minimization.tpr -o align.tpr
# (Select 4-Backbone)
```

For surface simulations, the trajectory was manipulated as such:

```{bash}
gmx_mpi trjconv -s step6.0_minimization.tpr -f traj_100ns_noPBC.xtc -o traj_100ns_align.xtc -fit rot+trans
# (Select 4-Backbone for LSQ and 4-Backbone for output)

gmx_mpi convert-tpr -s step6.0_minimization.tpr -o align.tpr
# (Select 4-Backbone)
```

To calculate RMSD,

```{bash}
gmx_mpi rms -s align.tpr -f traj_100ns_align.xtc -o rmsd_100ns_BB.xvg -tu ns
# (Select 4-Backbone for LSQ and 4-Backbone for output)
```

## 
