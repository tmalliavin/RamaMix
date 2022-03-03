# RamaMix
A finite mixture model for determining populations of conformations from a Ramachandran probability map


RamaMix_example.tgz contains an example of calculation. 
This example of run select the conformations and determine the corresponding populations allowing to optimize
the discrepancy measure between observed and reconstructed probability Ramachandran maps.

The input files are:
a) predABP.tab: the observed Ramachandran likelihood maps predicted 
by TALOS-N (Shen and Bax, Methods Mol Biol 1260, 17 (2015)).
https://spin.niddk.nih.gov/bax/software/TALOS-N/

b) run_RamaMix: the script to run RamaMix.

c) in the directory selected_confs, the files *.pdb describing the
conformation pool from which RamaMix will extract the representative
conformations and their populations.

d) before running RamaMix, the user should generate the normal mode
analysis (NMA) in internal coordinates for all the considered pdb files.
The following set of commands should be used:

cd selected_confs
./run_imode.sh
cd ..

The script run_imode.sh generates, for each pdb file, a file .bin containing
the NMA Hessian matrix.

NMA is performed using the software IMOD, Normal Mode Analysis in Internal
Coordinates, which has to be installed independently from:
https://chaconlab.org/multiscale-simulations/imod.
IMOD was presented in the reference:
Lopéz-Blanco, Garzón, Chacón, Bioinformatics 27, 2843 (2011)

The output files of the RamaMix run are:
1) histograms: the histogram description of the observed probability map.

2) out_positions.dat, out_shapes.dat and out_weights.dat: the optimized
values for the positions, for the shapes and for the populations of conformations.
The positions correspond to the phi/psi backbone angles.
The shapes (kappa1/kappa2/rho) characterize the bivariate periodic sine model
(von Mises distribution) used to describe the support of the probability
Ramachandran maps as a torus. The description proposed by
Mardia, Hughes, Taylor, Canadian Journal of Statistics 36, 99 (2008)
were used here for the implementation.

3) run.log and iterate.dat: the variations of optimized log-likelihood and
of log-likelihood gradient along the RamaMix optimization.
