dnamalci
========

`dnamalci` is an R-package that provides functions to easily apply the
DNA methylation alcohol scores (DNAm-Alcs) generated in:

> Liu C, Marioni RE, Hedman ÅK, Pfeiffer L, Tsai P-C, Reynolds LM et al.
> A DNA methylation biomarker of alcohol consumption. Mol Psychiatry
> 2016. <doi:10.1038/mp.2016.192>.

Installation
------------

Only a few steps are needed to install `dnamalci` in R. Just run the
following commands:

    install.packages("devtools") # if the devtools package is not installed
    library(devtools)
    install_github("yousefi138/dnamalci")

Example use
-----------

### Load a DNA methylation beta matrix

First, load a matrix of DNA methylation beta values of your choosing.

`dnamalci` installs with a test dataset which is a subset of results
from:

> Tsaprouni LG, Yang T-P, Bell J, Dick KJ, Kanoni S, Nisbet J et al.
> Cigarette smoking reduces DNA methylation levels at multiple genomic
> loci but the effect is partially reversible upon cessation.
> Epigenetics 2014; 9: 1382–1396.

This dataset is publicly available at GEO accession number
[GSE50660](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE50660)
:

    library(dnamalci)
    betas <- dnamalci.load.test.data()

The only requirements of user supplied beta values for `dnamalci` are
that they:

-   be contained in a matrix-formatted object where rows are CpG sites
    and columns are samples
-   `rownames` must contain CpG site names

<!-- -->

    head(rownames(betas))

    > [1] "cg00045114" "cg00085438" "cg00232160" "cg00252472" "cg00567854"
    > [6] "cg00883689"

### View available DNAm-Alcs

List the 4 flavors of DNAm-Alcs derived in Liu et al. 2016 that are
available for implementation in `dnamalci`:

    dnamalci.models()

    > [1] "dnamalc.144cpg" "dnamalc.23cpg"  "dnamalc.5cpg"   "dnamalc.78cpg"

### Estimate the DNAm-Alc score from your target DNA methylation beta matrix

    dnam.alc <- dnamalci(betas)
    head(dnam.alc$score)

    > [1] -6.507850 -5.925996 -6.821262 -6.486209 -6.858420 -6.774091

By default `dnamalci()` estimates the 144 CpG model from Liu et all, but
all DNAm-Alcs can be estimated by specifying the `model` argument:

    dnamalc.5cpg <- dnamalci(betas, model = "dnamalc.5cpg")
