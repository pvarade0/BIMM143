Class 12: Structural Bioinformatics 2
================

## Prep for docking

We want to produce a protein- only PDB file and a drug only PDB file.

``` r
library(bio3d)

#DOWNLOAD THE pdb File using get.pdb("1hsg"), but i already have it.
```

``` r
pdb <- read.pdb("1hsg.pdb")
protein <- atom.select(pdb, "protein", value= TRUE)
write.pdb(protein, file= "1hsg_protein.pdb")
```

and for ligand

``` r
ligand <- atom.select(pdb,"ligand", value=TRUE)
write.pdb(ligand, file="1hsg_ligand.pdb")
```

Put in the 1hsg\_protein.pdbqt/ligand file that we made in AutoDockTool

Processing our docking results

``` r
library(bio3d)
res <- read.pdb("all.pdbqt", multi=TRUE)
write.pdb(res, "results.pdb")
```
